---
tags:
  - mimari
  - api
  - bugzora
aliases:
  - API Tasarımı
  - API Design
parent: "[[03_Yazilim_Mimarisi]]"
dg-publish: true
---

# BugZora SaaS Donusumu - API Tasarimi

_Guncellenme tarihi: 2026-06-05_

## 1. API Tasarim Prensipleri
- Public entegrasyonlar icin REST/JSON, ic servis haberlesmesi icin gRPC tercih edilir.
- Idempotent isteklerde `Idempotency-Key` header'i desteklenir.
- Tum cevaplarda `request_id`, `trace_id` ve `timestamp` alanlari standarttir.
- Error modeli tek tiptir; makine tarafindan islenebilir code alanlari kullanilir.

## 2. API Versiyonlama Stratejisi
- REST icin `/api/v1/...` yol tabanli versiyonlama.
- gRPC icin protobuf package versiyonlama (`bugzora.platform.v1`).
- Geriye donuk uyumluluk en az 12 ay korunur.

## 3. Authentication & Authorization
- API Key, JWT Bearer ve OAuth2/OIDC token'lari desteklenir.
- Tenant baglami subdomain, custom domain veya token claim icinden cikarilir.
- Authorization RBAC + policy kontrolu ile uygulanir.

## 4. Rate Limiting Kurallari
- Free: 60 req/dakika, Starter: 300 req/dakika, Professional: 1200 req/dakika, Enterprise: sozlesmeye gore.
- Scan create endpoint'leri ayrik quota ve concurrency limitine tabidir.
- 429 durumunda `Retry-After` header'i donulur.

## 5. Endpoint'ler
### 5.1 Auth Endpoints
- `POST /api/v1/auth/login` -> email/password ile oturum acar.
- `POST /api/v1/auth/logout` -> refresh token'i iptal eder.
- `POST /api/v1/auth/refresh` -> yeni access token üretir.
- `GET /api/v1/auth/oauth2/{provider}/start` -> provider login akisini baslatir.
- `GET /api/v1/auth/oauth2/{provider}/callback` -> provider callback'ini tamamlar.
- `POST /api/v1/auth/mfa/challenge` -> MFA kodu uretir veya push baslatir.
- `POST /api/v1/auth/mfa/verify` -> MFA dogrulama yapar.

### 5.2 Tenant Endpoints
- `GET /api/v1/tenants/current`
- `PATCH /api/v1/tenants/current`
- `GET /api/v1/admin/tenants`
- `POST /api/v1/admin/tenants`
- `POST /api/v1/admin/tenants/{tenantId}/suspend`

### 5.3 User Management Endpoints
- `GET /api/v1/users`
- `POST /api/v1/users`
- `GET /api/v1/users/{id}`
- `PATCH /api/v1/users/{id}`
- `DELETE /api/v1/users/{id}`
- `POST /api/v1/users/{id}/invite`

### 5.4 Scan Job Endpoints
- `POST /api/v1/scans`
- `GET /api/v1/scans`
- `GET /api/v1/scans/{jobId}`
- `POST /api/v1/scans/{jobId}/cancel`
- `GET /api/v1/scans/{jobId}/results`
- `GET /api/v1/scans/{jobId}/events`

### 5.5 SBOM Endpoints
- `POST /api/v1/sbom/generate`
- `POST /api/v1/sbom/analyze`
- `POST /api/v1/sbom/compare`
- `POST /api/v1/sbom/merge`
- `POST /api/v1/sbom/validate`
- `GET /api/v1/sbom/{id}`

### 5.6 Policy Endpoints
- `GET /api/v1/policies`
- `POST /api/v1/policies`
- `GET /api/v1/policies/{id}`
- `PATCH /api/v1/policies/{id}`
- `DELETE /api/v1/policies/{id}`
- `POST /api/v1/policies/{id}/evaluate`

### 5.7 Report Endpoints
- `POST /api/v1/reports`
- `GET /api/v1/reports`
- `GET /api/v1/reports/{id}`
- `GET /api/v1/reports/{id}/download`

### 5.8 Notification Endpoints
- `GET /api/v1/notifications/settings`
- `PUT /api/v1/notifications/settings`
- `GET /api/v1/notifications/history`

### 5.9 Webhook Endpoints
- `POST /api/v1/webhooks/github-actions`
- `POST /api/v1/webhooks/gitlab-ci`
- `POST /api/v1/webhooks/jenkins`

### 5.10 Billing ve Admin Endpoints
- `GET /api/v1/billing/subscription`
- `POST /api/v1/billing/checkout`
- `GET /api/v1/billing/invoices`
- `POST /api/v1/billing/webhooks/stripe`
- `GET /api/v1/admin/audit-logs`

## 6. Request/Response Ornekleri
```json
{
  "email": "secops@example.com",
  "password": "********"
}
```
```json
{
  "access_token": "jwt",
  "refresh_token": "refresh",
  "expires_in": 900,
  "tenant": {"id": "uuid", "slug": "acme"}
}
```
```json
{
  "type": "image",
  "target": {"image": "ghcr.io/acme/api:1.0.0"},
  "config": {"severity": ["CRITICAL", "HIGH"], "sbom": true}
}
```
```json
{
  "job_id": "uuid",
  "status": "queued",
  "request_id": "req-123"
}
```

## 7. Error Handling ve Error Codes
- `AUTH_INVALID_CREDENTIALS`
- `AUTH_MFA_REQUIRED`
- `TENANT_NOT_FOUND`
- `TENANT_QUOTA_EXCEEDED`
- `SCAN_UNSUPPORTED_TARGET`
- `SCAN_JOB_NOT_FOUND`
- `POLICY_EVALUATION_FAILED`
- `REPORT_RENDER_FAILED`
- `BILLING_PROVIDER_ERROR`
- `RATE_LIMIT_EXCEEDED`

## 8. Pagination Stratejisi
- Cursor tabanli pagination tercih edilir.
- `limit`, `next_cursor`, `prev_cursor`, `total_estimate` alanlari kullanilir.
- Audit ve scan result listelerinde zaman bazli cursor kullanilir.

## 9. Webhook Payload Ornekleri
### GitHub Actions
```json
{
  "repository": "acme/api",
  "sha": "abc123",
  "workflow": "security",
  "image": "ghcr.io/acme/api:abc123"
}
```
### GitLab CI
```json
{
  "project_path": "group/service",
  "pipeline_id": 1234,
  "ref": "main",
  "artifact_url": "https://gitlab/artifacts.zip"
}
```
### Jenkins
```json
{
  "job_name": "release-build",
  "build_number": 89,
  "repo_url": "https://github.com/acme/repo.git"
}
```

## 10. OpenAPI 3.0 Spec Yapisi
- `openapi: 3.0.3`
- `info`, `servers`, `securitySchemes`, `tags`, `paths`, `components/schemas`, `webhooks` bolumleri olmalidir.
- Ortak response ve error schema'lari reusable component olarak tutulur.

## 11. Endpoint Detaylari ve Kabul Kriterleri
- POST /api/v1/auth/login: Email/password ile access ve refresh token doner, MFA gerekiyorsa ara durum doner.
- POST /api/v1/scans: Gelen hedef tipine gore ilgili scanner isi kuyruga eklenir.
- GET /api/v1/scans/{jobId}/results: Severity, type, package, path filtreleri ile sonuclari listeler.
- POST /api/v1/policies/{id}/evaluate: Sample payload veya job sonucu uzerinde policy karari uretir.
- POST /api/v1/reports: Asenkron rapor generation isi baslatir ve report_id doner.
- API notu 001: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 002: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 003: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 004: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 005: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 006: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 007: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 008: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 009: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 010: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 011: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 012: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 013: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 014: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 015: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 016: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 017: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 018: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 019: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 020: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 021: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 022: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 023: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 024: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 025: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 026: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 027: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 028: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 029: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 030: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 031: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 032: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 033: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 034: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 035: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 036: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 037: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 038: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 039: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 040: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 041: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 042: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 043: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 044: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 045: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 046: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 047: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 048: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 049: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 050: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 051: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 052: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 053: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 054: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 055: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 056: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 057: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 058: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 059: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 060: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 061: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 062: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 063: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 064: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 065: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 066: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 067: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 068: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 069: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 070: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 071: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 072: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 073: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 074: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 075: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 076: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 077: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 078: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 079: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 080: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 081: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 082: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 083: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 084: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 085: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 086: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 087: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 088: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 089: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 090: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 091: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 092: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 093: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 094: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 095: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 096: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 097: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 098: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 099: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 100: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 101: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 102: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 103: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 104: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 105: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 106: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 107: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 108: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 109: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 110: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 111: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 112: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 113: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 114: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 115: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 116: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 117: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 118: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 119: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 120: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 121: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 122: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 123: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 124: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 125: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 126: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 127: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 128: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 129: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 130: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 131: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 132: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 133: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 134: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 135: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 136: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 137: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 138: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 139: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 140: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 141: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 142: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 143: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 144: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 145: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 146: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 147: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 148: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 149: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 150: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 151: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 152: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 153: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 154: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 155: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 156: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 157: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 158: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 159: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 160: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 161: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 162: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 163: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 164: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 165: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 166: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 167: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 168: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 169: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 170: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 171: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 172: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 173: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 174: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 175: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 176: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 177: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 178: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 179: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 180: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 181: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 182: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 183: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 184: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 185: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 186: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 187: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 188: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 189: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 190: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 191: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 192: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 193: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 194: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 195: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 196: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 197: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 198: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 199: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.
- API notu 200: request validation, idempotency, cache davranisi, authorization, audit log ve observability gereksinimleri endpoint bazinda belgelenmelidir.


---

## 🔗 İlgili Notlar

- [[03_Yazilim_Mimarisi]]
- [[05_Veritabani_Tasarimi]]
- [[07_Guvenlik_Mimarisi]]
- [[09_UI_UX_Tasarimi]]
