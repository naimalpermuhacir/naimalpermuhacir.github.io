---
tags:
  - mimari
  - veritabani
  - bugzora
aliases:
  - Veritabanı Tasarımı
  - Database Design
parent: "[[03_Yazilim_Mimarisi]]"
dg-publish: true
---

# BugZora SaaS Donusumu - Veritabani Tasarimi

_Guncellenme tarihi: 2026-06-05_

## 1. Veritabani Stratejisi
- Ana islemsel veritabani PostgreSQL'dir.
- Redis, cache, rate limit, distributed lock ve gecici job durumu icin kullanilir.
- Elasticsearch, log analytics ve full-text arama ihtiyaclari icin kullanilir.
- Tablolarda tenant_id zorunlu olup row-level security ile izolasyon guclendirilir.
- Tum zaman alanlari timestamptz olarak saklanir.

## 2. SQL Schema
```sql
CREATE EXTENSION IF NOT EXISTS "pgcrypto";
CREATE EXTENSION IF NOT EXISTS "citext";

CREATE TYPE plan_type AS ENUM ('free', 'starter', 'professional', 'enterprise', 'onprem');
CREATE TYPE tenant_status AS ENUM ('trial', 'active', 'suspended', 'cancelled');
CREATE TYPE job_type AS ENUM ('image', 'filesystem', 'repository', 'sbom', 'policy_eval');
CREATE TYPE job_status AS ENUM ('queued', 'running', 'completed', 'failed', 'cancelled');
CREATE TYPE report_format AS ENUM ('json', 'pdf', 'cyclonedx', 'spdx', 'table');
CREATE TYPE notification_status AS ENUM ('pending', 'sent', 'failed', 'suppressed');
CREATE TYPE billing_status AS ENUM ('trialing', 'active', 'past_due', 'cancelled', 'incomplete');

CREATE TABLE tenants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug CITEXT NOT NULL UNIQUE,
  plan plan_type NOT NULL DEFAULT 'free',
  status tenant_status NOT NULL DEFAULT 'trial',
  settings JSONB NOT NULL DEFAULT '{}'::jsonb,
  quota_config JSONB NOT NULL DEFAULT '{}'::jsonb,
  data_region TEXT,
  owner_email CITEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  deleted_at TIMESTAMPTZ
);

CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  email CITEXT NOT NULL,
  password_hash TEXT,
  full_name TEXT,
  role TEXT NOT NULL,
  permissions JSONB NOT NULL DEFAULT '[]'::jsonb,
  mfa_enabled BOOLEAN NOT NULL DEFAULT FALSE,
  sso_subject TEXT,
  status TEXT NOT NULL DEFAULT 'active',
  last_login_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  UNIQUE (tenant_id, email)
);

CREATE TABLE api_keys (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  created_by UUID REFERENCES users(id),
  name TEXT NOT NULL,
  key_hash TEXT NOT NULL,
  scopes JSONB NOT NULL DEFAULT '[]'::jsonb,
  rate_limit INTEGER NOT NULL DEFAULT 1000,
  expires_at TIMESTAMPTZ,
  last_used_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE scan_jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  created_by UUID REFERENCES users(id),
  type job_type NOT NULL,
  status job_status NOT NULL DEFAULT 'queued',
  target JSONB NOT NULL,
  config JSONB NOT NULL DEFAULT '{}'::jsonb,
  source_ref TEXT,
  correlation_id UUID NOT NULL DEFAULT gen_random_uuid(),
  queued_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  started_at TIMESTAMPTZ,
  finished_at TIMESTAMPTZ,
  result_summary JSONB NOT NULL DEFAULT '{}'::jsonb,
  error_message TEXT,
  worker_metadata JSONB NOT NULL DEFAULT '{}'::jsonb
);

CREATE TABLE scan_results (
  id BIGSERIAL PRIMARY KEY,
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  job_id UUID NOT NULL REFERENCES scan_jobs(id) ON DELETE CASCADE,
  severity TEXT NOT NULL,
  finding_type TEXT NOT NULL,
  cve_id TEXT,
  package_name TEXT,
  installed_version TEXT,
  fixed_version TEXT,
  target_path TEXT,
  title TEXT NOT NULL,
  description TEXT,
  references JSONB NOT NULL DEFAULT '[]'::jsonb,
  cvss_score NUMERIC(4,2),
  exploit_maturity TEXT,
  license_name TEXT,
  secret_type TEXT,
  policy_decision TEXT,
  raw_payload JSONB NOT NULL DEFAULT '{}'::jsonb,
  first_seen_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE sbom_files (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  job_id UUID REFERENCES scan_jobs(id) ON DELETE SET NULL,
  format report_format NOT NULL,
  object_path TEXT NOT NULL,
  content_hash TEXT NOT NULL,
  metadata JSONB NOT NULL DEFAULT '{}'::jsonb,
  generated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  expires_at TIMESTAMPTZ
);

CREATE TABLE policies (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  name TEXT NOT NULL,
  description TEXT,
  rules JSONB NOT NULL,
  rego_bundle_path TEXT,
  enforcement_mode TEXT NOT NULL DEFAULT 'advisory',
  version INTEGER NOT NULL DEFAULT 1,
  is_default BOOLEAN NOT NULL DEFAULT FALSE,
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE reports (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  job_id UUID REFERENCES scan_jobs(id) ON DELETE SET NULL,
  format report_format NOT NULL,
  status TEXT NOT NULL DEFAULT 'queued',
  file_path TEXT,
  signed_url_expires_at TIMESTAMPTZ,
  request_payload JSONB NOT NULL DEFAULT '{}'::jsonb,
  generated_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE notifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  user_id UUID REFERENCES users(id),
  type TEXT NOT NULL,
  channel TEXT NOT NULL,
  destination TEXT NOT NULL,
  status notification_status NOT NULL DEFAULT 'pending',
  payload JSONB NOT NULL DEFAULT '{}'::jsonb,
  sent_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE audit_logs (
  id BIGSERIAL PRIMARY KEY,
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  user_id UUID REFERENCES users(id),
  action TEXT NOT NULL,
  resource TEXT NOT NULL,
  resource_id TEXT,
  details JSONB NOT NULL DEFAULT '{}'::jsonb,
  ip_address INET,
  user_agent TEXT,
  trace_id TEXT,
  occurred_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE subscriptions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  provider TEXT NOT NULL DEFAULT 'stripe',
  provider_customer_id TEXT,
  provider_subscription_id TEXT,
  plan_id TEXT NOT NULL,
  status billing_status NOT NULL,
  period_start TIMESTAMPTZ NOT NULL,
  period_end TIMESTAMPTZ NOT NULL,
  cancel_at_period_end BOOLEAN NOT NULL DEFAULT FALSE,
  trial_end TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE invoices (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  subscription_id UUID REFERENCES subscriptions(id),
  provider_invoice_id TEXT,
  amount_due BIGINT NOT NULL,
  amount_paid BIGINT NOT NULL DEFAULT 0,
  currency TEXT NOT NULL DEFAULT 'usd',
  status TEXT NOT NULL,
  invoice_pdf TEXT,
  due_date TIMESTAMPTZ,
  paid_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  invoice_id UUID REFERENCES invoices(id),
  provider_payment_intent_id TEXT,
  amount BIGINT NOT NULL,
  currency TEXT NOT NULL DEFAULT 'usd',
  status TEXT NOT NULL,
  failure_reason TEXT,
  processed_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE TABLE integrations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(id),
  type TEXT NOT NULL,
  provider TEXT NOT NULL,
  config JSONB NOT NULL DEFAULT '{}'::jsonb,
  secret_ref TEXT,
  status TEXT NOT NULL DEFAULT 'active',
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

## 3. Indeks Stratejisi
```sql
CREATE INDEX idx_users_tenant_email ON users(tenant_id, email);
CREATE INDEX idx_api_keys_tenant ON api_keys(tenant_id);
CREATE INDEX idx_scan_jobs_tenant_status ON scan_jobs(tenant_id, status, queued_at DESC);
CREATE INDEX idx_scan_jobs_type_status ON scan_jobs(type, status);
CREATE INDEX idx_scan_results_job ON scan_results(job_id);
CREATE INDEX idx_scan_results_tenant_severity ON scan_results(tenant_id, severity);
CREATE INDEX idx_scan_results_cve ON scan_results(cve_id) WHERE cve_id IS NOT NULL;
CREATE INDEX idx_sbom_files_tenant_format ON sbom_files(tenant_id, format, generated_at DESC);
CREATE INDEX idx_policies_tenant_name ON policies(tenant_id, name);
CREATE INDEX idx_reports_tenant_created ON reports(tenant_id, created_at DESC);
CREATE INDEX idx_notifications_tenant_status ON notifications(tenant_id, status, created_at DESC);
CREATE INDEX idx_audit_logs_tenant_occurred ON audit_logs(tenant_id, occurred_at DESC);
CREATE INDEX idx_subscriptions_tenant_status ON subscriptions(tenant_id, status);
CREATE INDEX idx_integrations_tenant_provider ON integrations(tenant_id, provider);
```

## 4. Partitioning Stratejisi
- scan_results tablosu aylik RANGE partition ile bolunur.
- Yuksek hacimli tenantlar icin sub-partition by hash(tenant_id) dusunulur.
- audit_logs icin de aylik partition ve retention policy uygulanir.
- Partition maintenance otomasyon ile yeni ay baslamadan olusturulur.

## 5. Migration Stratejisi
- Goose veya Atlas ile versioned migration kullanilir.
- Her migration geri alma (down) planina sahip olur; geri donulemeyen migrationlar icin not dusulur.
- Expand/contract modeli ile sifir kesinti hedeflenir.
- Uretimde DDL zamanlamasi trafik disi pencerelerde uygulanir.

## 6. Veri Arsivleme Politikasi
- scan_results detay kayitlari 12 ay sonra soguk depoya tasinabilir.
- audit_logs compliance gereksinimine gore 1-7 yil saklanir.
- rapor ve sbom artifact'leri plan bazli retention politikasina tabidir.
- GDPR uyumlu silme talepleri tenant ve user seviyesinde izlenir.

## 7. Tasarim Notlari
- Veri notu 001: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 002: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 003: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 004: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 005: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 006: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 007: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 008: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 009: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 010: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 011: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 012: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 013: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 014: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 015: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 016: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 017: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 018: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 019: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 020: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 021: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 022: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 023: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 024: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 025: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 026: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 027: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 028: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 029: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 030: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 031: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 032: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 033: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 034: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 035: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 036: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 037: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 038: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 039: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 040: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 041: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 042: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 043: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 044: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 045: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 046: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 047: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 048: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 049: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 050: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 051: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 052: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 053: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 054: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 055: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 056: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 057: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 058: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 059: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 060: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 061: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 062: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 063: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 064: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 065: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 066: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 067: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 068: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 069: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 070: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 071: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 072: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 073: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 074: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 075: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 076: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 077: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 078: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 079: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 080: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 081: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 082: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 083: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 084: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 085: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 086: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 087: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 088: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 089: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 090: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 091: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 092: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 093: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 094: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 095: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 096: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 097: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 098: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 099: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 100: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 101: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 102: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 103: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 104: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 105: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 106: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 107: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 108: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 109: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 110: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 111: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 112: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 113: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 114: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 115: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 116: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 117: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 118: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 119: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 120: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 121: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 122: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 123: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 124: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 125: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 126: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 127: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 128: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 129: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 130: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 131: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 132: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 133: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 134: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 135: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 136: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 137: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 138: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 139: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 140: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 141: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 142: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 143: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 144: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 145: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 146: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 147: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 148: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 149: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 150: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 151: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 152: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 153: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 154: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 155: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 156: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 157: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 158: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 159: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 160: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 161: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 162: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 163: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 164: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 165: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 166: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 167: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 168: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 169: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 170: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 171: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 172: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 173: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 174: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 175: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 176: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 177: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 178: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 179: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.
- Veri notu 180: kolon adi, veri tipi, nullability, index etkisi, partition davranisi ve retention karari migration dokumantasyonunda aciklanmalidir.


---

## 🔗 İlgili Notlar

- [[03_Yazilim_Mimarisi]]
- [[06_API_Tasarimi]]
- [[07_Guvenlik_Mimarisi]]
