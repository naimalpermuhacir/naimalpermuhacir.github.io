---
tags:
  - strateji
  - bugzora
aliases:
  - Proje Yönetimi
  - Project Management
parent: "[[00_BugZora_Hub]]"
dg-publish: true
---

# BugZora SaaS Donusumu - Proje Yonetimi

_Guncellenme tarihi: 2026-06-05_

## 1. Proje Kapsami ve Hedefler
- Kapsam, mevcut BugZora scanning servislerinin cok kiracili SaaS platforma donusturulmesini kapsar.
- Hedef; 32 haftada MVP yayinlamak, 48 haftada enterprise-ready baseline olusturmak, 64 haftada ticari olcekte operasyon kurmaktir.
- In-scope konular: auth, tenant management, billing, API gateway, report, notification, dashboard, audit log, deployment automation.
- Out-of-scope ilk faz: runtime agent, CSPM, SAST engine, SIEM korelasyon modulu.
- Basari kriteri: MVP sonunda en az 5 pilot musteriyle canli kullanim ve ucretli deneme baslangici.

## 2. Proje Ekibi Yapisi ve Roller
- **Product Owner**: Backlog onceliklendirme, deger odakli kararlar, musteri gorusmeleri ve sprint hedeflerinin onayi.
- **Program Manager**: Takvim, butce, risk, paydas koordinasyonu ve release governance.
- **Solution Architect**: Servis sinirlari, teknik kararlar, ADR yonetimi ve NFR sahipligi.
- **Backend Lead**: API, auth, orchestration, veri modeli ve kalite standardi sahipligi.
- **Frontend Lead**: Dashboard deneyimi, tasarim sistemi, accessibility ve performans.
- **DevSecOps Lead**: Kubernetes, IaC, CI/CD, secret management, gozlemlenebilirlik.
- **QA Lead**: Test stratejisi, regression kapsamı, acceptance testler ve kalite raporlama.
- **Security Architect**: Threat model, pentest planlama, compliance kontrol haritasi.
- **Data/Reporting Engineer**: Raporlama servisi, analitik katman ve log/search mimarisi.
- **Customer Success**: Pilot onboarding, feedback toplama, dokumantasyon ve egitim.

## 3. Metodoloji (Scrum/Kanban Hybrid)
- Ust seviye planlama, 2 haftalik sprint cadence ile Scrum mantiginda yonetilir.
- Uretim destek, bugfix ve operasyonel isler Kanban swimlane'lerinde ayrica takip edilir.
- Sprint planning, daily, review ve retrospective seremonileri sabit tutulur.
- Acil guvenlik aciklari expedited lane ile backlog disi yonetilir.
- Product discovery calismalari onceki sprintte grooming olarak yapilir.
- WIP limitleri ekip bazinda tanimlanir; context switching kontrol edilir.
- Teknik borc kapasitesi her sprintte en az %15 ayrilir.

## 4. Sprint Planlamasi (16 Sprint, 2'ser haftalik)
### Sprint 1 - Kesif ve temel mimari
- Sprint hedefi: Kesif ve temel mimari alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: ADR seti.
- Planlanan is: domain modeli.
- Planlanan is: hedef altyapi karari.
- Planlanan is: epic backlog.
- Beklenen deliverable: Architecture board onayi.
- Beklenen deliverable: pilot musteri gereksinim toplama.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 2 - Platform foundation
- Sprint hedefi: Platform foundation alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: repo standardizasyonu.
- Planlanan is: CI temel pipeline.
- Planlanan is: Docker build.
- Planlanan is: local compose.
- Beklenen deliverable: dev ortam olusur.
- Beklenen deliverable: kod kalite kapilari tanimlanir.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 3 - Auth servisi
- Sprint hedefi: Auth servisi alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: JWT.
- Planlanan is: refresh token.
- Planlanan is: RBAC iskeleti.
- Planlanan is: audit hook.
- Beklenen deliverable: login/logout calisir.
- Beklenen deliverable: multi-tenant claims tanimlanir.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 4 - Tenant management
- Sprint hedefi: Tenant management alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: tenant CRUD.
- Planlanan is: plan ayarlari.
- Planlanan is: quota modeli.
- Planlanan is: admin panel API.
- Beklenen deliverable: tenant lifecycle netlesir.
- Beklenen deliverable: default policy atanir.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 5 - API gateway ve rate limit
- Sprint hedefi: API gateway ve rate limit alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: gateway routing.
- Planlanan is: request ID.
- Planlanan is: rate limit.
- Planlanan is: observability.
- Beklenen deliverable: public API beta.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 6 - ImageScan entegrasyonu
- Sprint hedefi: ImageScan entegrasyonu alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: job create.
- Planlanan is: async worker.
- Planlanan is: result normalize.
- Planlanan is: status endpoint.
- Beklenen deliverable: image scan e2e.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 7 - RepoScan entegrasyonu
- Sprint hedefi: RepoScan entegrasyonu alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: repo credentials.
- Planlanan is: secret/license bulgulari.
- Planlanan is: webhook tetikleme.
- Planlanan is: risk scoring.
- Beklenen deliverable: repo scan beta.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 8 - FileScan entegrasyonu
- Sprint hedefi: FileScan entegrasyonu alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: upload/url ingestion.
- Planlanan is: filesystem tarama.
- Planlanan is: artifact store.
- Planlanan is: cache.
- Beklenen deliverable: file scan beta.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 9 - SBOM servisi
- Sprint hedefi: SBOM servisi alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: generate.
- Planlanan is: compare.
- Planlanan is: merge.
- Planlanan is: validate.
- Beklenen deliverable: CycloneDX/SPDX output.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 10 - Policy servisi
- Sprint hedefi: Policy servisi alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: OPA bundle.
- Planlanan is: evaluation API.
- Planlanan is: exceptions.
- Planlanan is: enforcement mode.
- Beklenen deliverable: policy gate calisir.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 11 - Reporting
- Sprint hedefi: Reporting alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: PDF/JSON rapor.
- Planlanan is: scheduled jobs.
- Planlanan is: template engine.
- Planlanan is: download audit.
- Beklenen deliverable: ilk executive rapor.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 12 - Notification
- Sprint hedefi: Notification alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: email.
- Planlanan is: Slack.
- Planlanan is: PagerDuty.
- Planlanan is: digest jobs.
- Beklenen deliverable: kritik bulgu alarmi.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 13 - Billing ve subscription
- Sprint hedefi: Billing ve subscription alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: plans.
- Planlanan is: Stripe webhook.
- Planlanan is: usage metering.
- Planlanan is: invoice sync.
- Beklenen deliverable: ucretli plan beta.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 14 - Dashboard UX
- Sprint hedefi: Dashboard UX alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: overview metrics.
- Planlanan is: tables.
- Planlanan is: filters.
- Planlanan is: multi-tenant settings.
- Beklenen deliverable: pilot customer review.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 15 - Hardening ve performance
- Sprint hedefi: Hardening ve performance alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: load test.
- Planlanan is: security test.
- Planlanan is: DR rehearsal.
- Planlanan is: cost tuning.
- Beklenen deliverable: release candidate.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

### Sprint 16 - Go-live hazirlik
- Sprint hedefi: Go-live hazirlik alaninda teslim edilebilir urun parcasi cikarmak.
- Planlanan is: runbook.
- Planlanan is: SLA/SLO.
- Planlanan is: support handoff.
- Planlanan is: launch checklist.
- Beklenen deliverable: production launch.
- Demo kapsaminda teknik cikti, kabul kriteri ve risk notu sunulur.
- Retrospective ciktisi backlog iyilestirmelerine yansitilir.

## 5. Milestone'lar ve Deliverable'lar
- M1: Program kickoff -> Charter, scope, team staffing, baseline budget
- M2: Architecture freeze v1 -> ADR seti, domain event contract'lari, deployment hedefleri
- M3: Security foundation complete -> Auth, RBAC, audit, tenant isolation
- M4: Scanner integrations beta -> ImageScan, RepoScan, FileScan e2e jobs
- M5: MVP functional complete -> SBOM, policy, reports, notifications
- M6: Commercial readiness -> Billing, plans, pricing hooks, legal docs
- M7: Operational readiness -> Monitoring, alerting, runbooks, DR rehearsal
- M8: GA release -> Prod launch, pilot conversion, post-launch success plan

## 6. Risk Yonetimi Matrisi
| ID | Risk | Etki | Olasilik | Skor | Aksiyon |
| --- | --- | --- | --- | --- | --- |
| R1 | Scanner performansi hedefi tutmuyor | Yuksek | Orta | Yuksek | cache + worker autoscale + benchmark |
| R2 | Tenant izolasyonu hatasi | Cok Yuksek | Dusuk | Yuksek | RLS testleri + guvenlik incelemesi |
| R3 | Billing webhook tutarsizligi | Orta | Orta | Orta | idempotency key + replay kontrolu |
| R4 | CVE feed upstream kesintisi | Yuksek | Orta | Yuksek | mirror + graceful degradation |
| R5 | Pilot musteri gereksinim kaymasi | Orta | Yuksek | Yuksek | change board + MoSCoW kapsam |
| R6 | Ekip kapasite kaybi | Yuksek | Orta | Yuksek | yedekleme planı + contractor havuzu |
| R7 | Compliance gereksinimi gecikmesi | Yuksek | Orta | Yuksek | erken gap analizi |
| R8 | Multi-cloud maliyet artisi | Orta | Orta | Orta | FinOps dashboard + rezervasyon stratejisi |

## 7. Iletisim Plani
- Gunluk standup: 15 dakika, ekip engelleri ve gunluk plan.
- Haftalik program sync: milestone, risk, butce ve dependency durumu.
- Iki haftalik sprint review: urun demosu, kabul, sonraki oncelikler.
- Iki haftalik retrospective: surec iyilestirme ve aksiyon sahipligi.
- Aylik steering committee: C-level ozet, risk, pazar geri bildirimi.
- Aylik architecture board: ADR, NFR, teknik borc ve kapasite kararları.
- Pilot musteri office hour: urun geri bildirimi, adoption ve destek durumu.

## 8. Change Management Sureci
- Degisiklik talebi, is gerekcesi, kapsam etkisi, maliyet ve zaman etkisi ile birlikte kaydedilir.
- Urun sahibi, mimar ve program manager degisikligi CAB gundemine alir.
- MVP kapsamindaki degisiklikler MoSCoW prensibine gore yeniden siniflandirilir.
- Guvenlik ve uyumluluk etkisi olan degisikliklerde Security Architect onayi zorunludur.
- Karar sonucu backlog, roadmap ve release note'lara yansitilir.

## 9. Definition of Done
- Kod merge edilmistir ve en az bir reviewer onayi vardir.
- Unit ve integration testleri gecmistir.
- Security scan, lint ve build quality gate'leri saglanmistir.
- Dokumantasyon, API contract ve changelog guncellenmistir.
- Monitoring, logging ve alerting hook'lari eklenmistir.
- Acceptance kriterleri product owner tarafindan kabul edilmistir.

## 10. Gantt Chart (Metin Formati)
- Hafta 01-04 | Kesif ve mimari | ####
- Hafta 05-08 | Platform foundation + auth | ####
- Hafta 09-12 | Tenant + gateway + quotas | ####
- Hafta 13-18 | Scanner entegrasyonlari | ######
- Hafta 19-22 | SBOM + policy + reporting | ####
- Hafta 23-26 | Notification + dashboard | ####
- Hafta 27-30 | Billing + enterprise readiness | ####
- Hafta 31-32 | Hardening + launch prep | ##

## 11. Butce Planlamasi
| Kalem | Yil 1 | Yil 2 | Yil 3 |
| --- | --- | --- | --- |
| Maaslar | $420,000 | $620,000 | $840,000 |
| Bulut ve tooling | $48,000 | $96,000 | $150,000 |
| Compliance ve hukuk | $22,000 | $35,000 | $48,000 |
| Pazarlama | $30,000 | $90,000 | $160,000 |
| Partner enablement | $5,000 | $18,000 | $35,000 |
| Toplam | $525,000 | $859,000 | $1,233,000 |

## 12. MVP Scope Tanimi
- MVP dahil: Email/password auth + JWT + refresh token.
- MVP dahil: Tenant, user ve role yonetimi.
- MVP dahil: Image/Repo/File scan create-status-result flow.
- MVP dahil: SBOM generate/compare/validate.
- MVP dahil: Policy evaluate + basic enforcement.
- MVP dahil: PDF/JSON rapor ve indirme.
- MVP dahil: Email/Slack bildirimleri.
- MVP dahil: Stripe tabanli temel billing.
- MVP dahil: Dashboard overview ve filterable result listeleri.
- MVP dahil: Kubernetes deployment + ArgoCD + basic DR.
- MVP disi: SAML SSO.
- MVP disi: MSP white-labeling.
- MVP disi: advanced analytics warehouse.
- MVP disi: regional data residency.
- MVP disi: runtime security agent.

## 13. Yonetim Tavsiyeleri
- Tavsiye 01: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 02: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 03: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 04: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 05: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 06: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 07: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 08: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 09: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 10: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 11: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 12: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 13: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 14: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 15: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 16: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 17: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 18: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 19: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 20: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 21: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 22: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 23: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 24: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 25: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 26: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 27: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 28: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 29: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 30: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 31: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 32: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 33: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 34: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 35: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 36: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 37: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 38: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 39: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 40: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 41: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 42: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 43: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 44: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 45: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 46: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 47: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 48: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 49: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 50: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 51: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 52: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 53: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 54: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 55: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 56: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 57: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 58: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 59: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.
- Tavsiye 60: backlog onceliklendirmesinde teknik risk ile ticari etki birlikte degerlendirilmeli; sahip, bitis tarihi ve bagimlilik net yazilmalidir.


---

## 🔗 İlgili Notlar

- [[01_Is_Analizi]]
- [[03_Yazilim_Mimarisi]]
- [[10_DevOps_CI_CD]]
- [[08_SaaS_Modeli_Fiyatlandirma]]
