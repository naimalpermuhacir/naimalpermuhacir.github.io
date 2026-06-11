---
tags:
  - mimari
  - bugzora
aliases:
  - Yazılım Mimarisi
  - Software Architecture
parent: "[[00_BugZora_Hub]]"
dg-publish: true
---

# BugZora SaaS Donusumu - Yazilim Mimarisi

_Guncellenme tarihi: 2026-06-05_

## 1. Architecture Decision Records (ADR)
- **ADR-001 - Microservice mimarisi secimi**: Farkli tarama domainlerinin bagimsiz olceklenmesi ve lisansli modullerin ayrismasi icin secildi.
- **ADR-002 - API Gateway zorunlulugu**: Kimlik dogrulama, rate limit, tenant context ve versiyonlama tek noktadan yonetilecek.
- **ADR-003 - REST + gRPC birlikte kullanimi**: Dis entegrasyonlarda REST, ic servis iletisiminde gRPC ile performans ve tip guvenligi saglanacak.
- **ADR-004 - Event-driven orchestration**: Uzun sureli scan isleri asenkron olaylarla yonetilecek; kullanici deneyimi bloklanmayacak.
- **ADR-005 - PostgreSQL ana veri kaynagi**: Transactional guvenilirlik, JSONB esnekligi ve RLS destegi nedeniyle secildi.
- **ADR-006 - Redis cache ve ephemeral state**: Job queue, rate limit ve kisa omurlu cache senaryolari icin uygun maliyetli cozum.
- **ADR-007 - Elasticsearch log/search katmani**: Audit ve scan arama deneyimini hizlandirmak icin secildi.
- **ADR-008 - OPA/Rego policy engine**: Politika-as-code, yeniden kullanilabilir bundle ve enterprise beklentileri nedeniyle secildi.
- **ADR-009 - Kafka once, RabbitMQ alternatif**: Yuksek hacimli event streaming ve replay ihtiyacinda Kafka tercih edilir; kucuk kurulumlarda RabbitMQ opsiyoneldir.
- **ADR-010 - Kubernetes uzerinde dagitim**: HA, autoscaling, GitOps ve multi-cloud hedefleri ile uyumludur.

## 2. Sistem Baglami Diyagrami (C4 - Context Level, Metin)
- Aktor: Son kullanici / Security Engineer -> Web UI ve Public API uzerinden platforma erisir.
- Aktor: CI/CD sistemi -> webhook veya API ile scan job baslatir ve sonuc alir.
- Aktor: Identity Provider -> OAuth2/OIDC/SAML ile kimlik federasyonu saglar.
- Aktor: Billing provider -> abonelik, odeme ve webhook olaylarini iletir.
- Aktor: Notification kanallari -> email, Slack, Teams, PagerDuty uzerinden alarm dagitimi yapar.
- Sistem: BugZora Platform -> tarama orkestrasyonu, raporlama, politika, billing ve gozlemlenebilirlik saglar.
- Harici sistem: Git providerlar -> repo metadata, webhook ve source access saglar.
- Harici sistem: Container registry -> image pull ve manifest metadata saglar.
- Harici sistem: SIEM/GRC -> audit log veya rapor export tuketir.

## 3. Container Diyagrami (C4 - Metin)
- **Web Dashboard**: Next.js tabanli kullanici arayuzu; dashboard, scan yonetimi, policy ve billing sayfalari.
- **API Gateway**: Dis istemci trafigini alir; auth, rate limit, routing ve response shaping yapar.
- **Auth Service**: JWT, refresh token, OAuth2/OIDC ve SSO oturum yonetimi.
- **Tenant Management Service**: Tenant lifecycle, quota, plan ve organization ayarlari.
- **Scan Orchestrator**: Scan islerini planlar, worker'lara dagitir, status ve idempotency saglar.
- **ImageScan Service**: Container image CVE/SBOM/policy taramalarini calistirir.
- **FileScan Service**: Filesystem tabanli secret, vulnerability ve artifact analizini yapar.
- **RepoScan Service**: Repository secret, license ve dependency analizlerini yapar.
- **SBOM Service**: Generate, compare, merge ve validate operasyonlarini saglar.
- **Policy Service**: OPA bundle yukleme, evaluation ve exception yonetimi.
- **Report Service**: PDF/JSON/CycloneDX/SPDX cikti ve scheduled report sureci.
- **Notification Service**: Email/chat/incident kanallarina bildirim yollar.
- **Billing Service**: Plan, subscription, invoice ve webhook yonetimi.
- **Audit Log Service**: Tum kritik olaylari immutable formatta kaydeder.
- **Dashboard/Metrics Service**: Aggregation, KPI ve widget verilerini hazirlar.
- **PostgreSQL**: Transactional veri ve metadata.
- **Redis**: Cache, rate limit, queue state, distributed lock.
- **Kafka**: Job event ve domain event omurgasi.
- **Elasticsearch**: Audit/search ve log analytics.

## 4. Component Diyagrami (Metin)
- API Gateway -> auth middleware, tenant resolver, request validation, router, response mapper, rate limiter.
- Auth Service -> user credential store, session store, token issuer, SSO adapters, MFA orchestrator.
- Scan Orchestrator -> job scheduler, adapter registry, event producer, callback handler, result normalizer.
- Report Service -> template registry, rendering engine, object storage adapter, download signer.
- Policy Service -> policy registry, bundle compiler, evaluator, exception manager.
- Billing Service -> plan catalog, usage meter, invoice projector, webhook consumer.
- Dashboard Service -> materialized view refresher, metrics query API, cached widgets.

## 5. Microservice Listesi ve Sorumluluklari
### API Gateway Service
- REST public API sunar.
- JWT/API key dogrular.
- tenant context inject eder.
- rate limit uygular.
- audit metadata uretir.
- version routing yapar.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Auth Service
- JWT + refresh token.
- password policy.
- OAuth2/OIDC/SAML adapterlari.
- MFA challenge.
- session revocation.
- token introspection.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Tenant Management Service
- tenant CRUD.
- plan ve quota.
- organization settings.
- domain mapping.
- member daveti.
- plan degisiklik sinyali.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### BugZora-ImageScan Service
- registry/image pull.
- CVE analizi.
- SBOM generation.
- policy gate.
- cache warmup.
- normalized result publish.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### BugZora-FileScan Service
- filesystem/artifact ingestion.
- secret detection.
- package inventory.
- vulnerability mapping.
- result persistence hook.
- quota accounting.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### BugZora-RepoScan Service
- git clone/fetch.
- secret/license/dependency scan.
- branch or PR context.
- webhook correlation.
- credential isolation.
- source cleanup.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### SBOM Service
- CycloneDX/SPDX olusturma.
- compare.
- merge.
- validate.
- analytics summary.
- artifact retention.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Policy Service
- OPA/Rego policy saklama.
- evaluation.
- exception workflow.
- policy bundle versioning.
- tenant policy inheritance.
- decision log.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Report Service
- report definition.
- scheduled generation.
- download token.
- branding.
- PDF rendering.
- export audit.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Notification Service
- email.
- Slack/Teams.
- PagerDuty.
- deduplication.
- retry.
- preference enforcement.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Billing Service
- subscription.
- usage metering.
- invoice and payment sync.
- trial lifecycle.
- quota sync.
- dunning.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Audit Log Service
- immutable event store.
- tamper-evident hash chain.
- retention.
- search.
- export.
- compliance filters.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.

### Dashboard/Metrics Service
- aggregated KPIs.
- severity trend.
- top risks.
- tenant health score.
- cache.
- timeseries export.
- Servis API contract'lari protobuf/OpenAPI ile surumlenir.


## 6. Servisler Arasi Iletisim
- Gateway -> core servisler: REST/JSON; dis istemci uyumlulugu icin.
- Core servisler arasi synchronous cagrilar: gRPC; tip guvenligi, dusuk latency ve codegen avantajlari icin.
- Uzun sureli scan ve rapor isleri: Kafka event'leri ile event-driven akista ilerler.
- Notification ve billing webhook islemleri: idempotent consumer modeli ile asenkron ele alinir.
- Audit log yazimlari fire-and-forget degil; kritik islemlerde garanti yazim veya outbox pattern kullanilir.

## 7. Data Flow Diyagramlari (Metin)
### Scan Job Flow
- Kullanici veya CI webhooku Gateway'e istek yollar.
- Gateway Auth ve Tenant dogrulama yapar.
- Scan Orchestrator job kaydi acar.
- Kafka'ya scan.requested eventi gider.
- Uygun scanner worker isi alir.
- Sonuclar normalize edilip DB'ye yazilir.
- Policy Service degerlendirir.
- Notification/Report tetiklenir.
- Dashboard aggregation guncellenir.
### Billing Flow
- Subscription olayi Billing Service'e gelir.
- Plan ve quota tenant kaydina yansir.
- Kullanim event'leri metering deposuna akar.
- Donem sonunda invoice olusturulur.
- Odeme sonucu webhook ile guncellenir.
### SSO Login Flow
- Kullanici IdP'ye yonlendirilir.
- Callback Auth Service'e gelir.
- Claims tenant ve rol bilgisine eslenir.
- JWT uretimi yapilir.
- Session audit log'a yazilir.

## 8. Technology Stack Kararlari ve Gerekceleri
- Go 1.22+: yuksek performans, kolay concurrency, statik binary dagitimi.
- Gin veya Echo: hafif, middleware ekosistemi guclu, API-first gelistirmeye uygun.
- PostgreSQL: transaction, JSONB, RLS, partitioning, extension destegi.
- Redis: cache, distributed lock, short-lived queue semantics.
- Kafka: event sourcing benzeri replay ve yuksek throughput.
- OPA/Rego: policy as code standardizasyonu.
- Elasticsearch: arama ve log analytics hizlandirma.
- Next.js: dashboard tarafinda SSR/ISR ve gelistirici verimliligi.
- Prometheus/Grafana: metrics gozlemlenebilirligi ve SLO yonetimi.

## 9. Scalability Stratejisi
- Stateless API servisleri yatay olceklenir; session durumu Redis/JWT ile disari alinmistir.
- Scanner worker havuzu kuyruk derinligi, CPU ve bellek metrikleri ile otomatik olceklenir.
- Report generation ayrik queue kullanir; kullaniciya hizli cevap verilir.
- Read-heavy dashboard sorgulari materialized view ve cache ile hizlandirilir.
- Tenant bazli noisy neighbor etkisini azaltmak icin concurrency quota uygulanir.

## 10. Fault Tolerance ve Resilience Pattern'leri
- Circuit Breaker: registry, email veya billing provider kesintilerinde uygulama zincirleme bozulmaz.
- Retry with backoff: transient network hatalarinda kullanilir; idempotent endpointlerle sinirlandirilir.
- Bulkhead: worker pool ve outbound connector bazinda kaynak ayrimi saglanir.
- Timeout + cancellation: her dis baglanti icin zorunlu context timeout kullanilir.
- Outbox pattern: DB ve event publish atomikligi garanti altina alinir.
- Dead letter queue: basarisiz eventler inceleme ve replay icin saklanir.

## 11. Caching Stratejisi (Redis)
- Token blacklist ve oturum iptal cache'i.
- Rate limiting sayaclari.
- Registry metadata ve package index cache'i.
- Dashboard widget cache'i.
- Policy bundle cache'i.
- SBOM compare sonuc cache'i.
- Idempotency key store.

## 12. Message Queue Tasarimi (Kafka/RabbitMQ)
- Topic: `scan.requested` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `scan.started` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `scan.completed` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `scan.failed` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `policy.evaluated` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `report.requested` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `report.ready` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `notification.requested` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `billing.usage_recorded` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `billing.subscription_changed` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Topic: `audit.security_event` -> key alanlari: tenant_id, job_id, correlation_id, occurred_at.
- Mimari not 01: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 02: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 03: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 04: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 05: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 06: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 07: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 08: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 09: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 10: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 11: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 12: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 13: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 14: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 15: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 16: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 17: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 18: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 19: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 20: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 21: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 22: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 23: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 24: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 25: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 26: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 27: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 28: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 29: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 30: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 31: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 32: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 33: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 34: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 35: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 36: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 37: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 38: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 39: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 40: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 41: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 42: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 43: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 44: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 45: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 46: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 47: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 48: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 49: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 50: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 51: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 52: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 53: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 54: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 55: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 56: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 57: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 58: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 59: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 60: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 61: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 62: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 63: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 64: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 65: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 66: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 67: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 68: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 69: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 70: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 71: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 72: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 73: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 74: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 75: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 76: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 77: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 78: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 79: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 80: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 81: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 82: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 83: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 84: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 85: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 86: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 87: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 88: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 89: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.
- Mimari not 90: her servis icin saglik metrikleri, capacity hedefleri, timeout degerleri ve ownership bilgisi ADR deposunda tutulmalidir.


---

## 🔗 İlgili Notlar

- [[04_Altyapi_Mimarisi]]
- [[05_Veritabani_Tasarimi]]
- [[06_API_Tasarimi]]
- [[07_Guvenlik_Mimarisi]]
- [[10_DevOps_CI_CD]]
