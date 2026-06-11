---
tags:
  - devops
  - altyapi
  - bugzora
aliases:
  - DevOps
  - CI/CD
parent: "[[04_Altyapi_Mimarisi]]"
dg-publish: true
---

# BugZora SaaS Donusumu - DevOps ve CI/CD

_Guncellenme tarihi: 2026-06-05_

## 1. GitOps Workflow
- Branch stratejisi: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`.
- `main` her zaman production'a deploy edilebilir durumda tutulur.
- Infrastructure ve uygulama manifestleri ayrik repo veya mono-repo icinde net klasor yapisi ile tutulur.

## 2. CI Pipeline Detayi (GitHub Actions)
- Adim 1: lint + unit test + race test.
- Adim 2: build ve artifact olusturma.
- Adim 3: BugZora ile self-scan.
- Adim 4: Docker multi-arch build ve push.
- Adim 5: SBOM generation ve artifact upload.
- Adim 6: Helm chart lint/package.

## 3. CD Pipeline Detayi (ArgoCD)
- Dev -> Staging -> Production promote zinciri.
- Canary deployment progressive traffic shift ile yapilir.
- Blue-Green sadece kritik API veya gateway release'lerinde kullanilir.
- Rollback, onceki saglikli image tag ve Helm revision ile hizli yapilir.

## 4. Environment Yonetimi
- `.env.example` sadece gelistirme referansi icin tutulur.
- Production secret'lari Vault/External Secrets ile inject edilir.
- ConfigMap ve Secret ayrimi net uygulanir.

## 5. Quality Gates
- Test coverage >= %80.
- Lint pass.
- Security scan clean veya onayli exception.
- Helm ve deployment manifest validation gecmeli.

## 6. Monitoring ve Alerting Kurulumu
- SLI: availability, latency, error rate, queue lag, scan success rate.
- Alert policy: P1/P2/P3 siniflari; gunduz/gece rota farki.

## 7. SLA Hedefleri
- Cloud platform icin %99.9 uptime hedefi.
- Kritik incident icin MTTR < 60 dakika hedeflenir.

## 8. Incident Management Sureci
- Tespit -> triage -> komuta yapisi -> iletişim -> geri kazanım -> postmortem.
- Public status page ve musteri bilgilendirme sablonlari hazir tutulur.

## 9. Runbook Ornekleri
- Queue backlog artisi.
- Registry auth hatasi.
- DB connection saturation.
- ArgoCD sync drift.

## 10. On-Premise Kurulum Scriptleri ve Helm Values
```yaml
global:
  domain: bugzora.example.local
  storageClass: fast-ssd
postgresql:
  enabled: false
externalDatabase:
  host: postgres.local
  sslmode: require
```

## 11. Musteri Icin Kurulum Rehberi
- Gereksinimler, namespace hazirligi, secret olusturma, helm install, smoke test ve upgrade notlari.

## 12. Operasyon Notlari
- DevOps notu 001: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 002: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 003: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 004: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 005: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 006: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 007: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 008: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 009: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 010: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 011: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 012: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 013: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 014: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 015: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 016: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 017: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 018: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 019: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 020: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 021: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 022: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 023: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 024: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 025: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 026: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 027: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 028: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 029: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 030: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 031: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 032: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 033: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 034: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 035: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 036: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 037: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 038: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 039: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 040: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 041: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 042: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 043: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 044: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 045: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 046: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 047: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 048: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 049: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 050: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 051: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 052: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 053: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 054: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 055: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 056: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 057: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 058: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 059: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 060: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 061: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 062: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 063: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 064: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 065: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 066: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 067: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 068: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 069: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 070: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 071: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 072: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 073: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 074: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 075: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 076: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 077: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 078: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 079: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 080: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 081: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 082: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 083: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 084: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 085: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 086: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 087: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 088: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 089: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 090: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 091: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 092: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 093: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 094: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 095: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 096: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 097: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 098: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 099: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 100: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 101: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 102: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 103: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 104: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 105: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 106: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 107: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 108: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 109: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 110: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 111: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 112: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 113: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 114: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 115: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 116: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 117: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 118: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 119: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 120: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 121: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 122: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 123: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 124: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 125: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 126: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 127: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 128: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 129: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 130: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 131: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 132: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 133: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 134: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 135: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 136: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 137: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 138: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 139: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 140: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 141: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 142: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 143: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 144: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 145: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 146: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 147: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 148: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 149: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 150: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 151: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 152: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 153: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 154: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 155: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 156: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 157: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 158: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 159: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 160: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 161: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 162: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 163: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 164: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 165: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 166: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 167: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 168: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 169: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 170: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 171: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 172: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 173: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 174: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 175: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 176: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 177: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 178: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 179: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 180: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 181: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 182: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 183: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 184: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 185: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 186: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 187: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 188: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 189: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 190: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 191: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 192: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 193: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 194: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 195: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 196: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 197: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 198: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 199: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 200: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 201: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 202: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 203: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 204: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 205: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 206: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 207: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 208: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 209: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 210: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 211: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 212: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 213: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 214: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 215: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 216: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 217: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 218: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 219: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 220: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 221: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 222: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 223: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 224: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 225: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 226: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 227: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 228: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 229: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 230: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 231: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 232: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 233: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 234: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 235: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 236: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 237: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 238: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 239: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 240: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 241: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 242: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 243: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 244: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 245: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 246: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 247: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 248: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 249: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- DevOps notu 250: pipeline step owner'i, artefact retention, rollback kuralı, change freeze ve cost gözlemi açık biçimde tanimlanmalidir.
- Operasyonel not 001: devops ci cd icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 002: devops ci cd icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.


---

## 🔗 İlgili Notlar

- [[04_Altyapi_Mimarisi]]
- [[03_Yazilim_Mimarisi]]
- [[07_Guvenlik_Mimarisi]]
- [[PROMPT_04_Kubernetes_Altyapisi]]
