---
tags:
  - strateji
  - fiyatlandirma
  - bugzora
aliases:
  - SaaS Model
  - Fiyatlandırma
parent: "[[00_BugZora_Hub]]"
dg-publish: true
---

# BugZora SaaS Modeli ve Fiyatlandirma

_Guncellenme tarihi: 2026-06-05_

## 1. Deployment Modeli Secenekleri
- BugZora Cloud: tam yonetilen SaaS.
- BugZora Self-Hosted: musteri altyapisinda Kubernetes veya VM tabanli kurulum.
- BugZora Hybrid: kontrol duzlemi cloud'da, scanner execution customer network'unde.

## 2. Fiyatlandirma Planlari
| Plan | Fiyat | Kullanici | Quota | Notlar |
| --- | --- | --- | --- | --- |
| Free | $0 | 1 kullanici | 50 scan/ay | Temel image/repo tarama, community support |
| Starter | $49/ay | 5 kullanici | 500 scan/ay | Email support, Slack webhook, temel raporlar |
| Professional | $199/ay | 20 kullanici | 5000 scan/ay | Tum ozellikler, policy, SBOM analytics, role yonetimi |
| Enterprise | $999/ay+ | Sinirsiz | Ozel | SSO, SLA, private onboarding, dedicated support |
| On-Premise License | $2999/yil+ | Node bazli | Yerel sinirlar | On-prem lisans, destek opsiyonlu |

## 3. Ozellik Karsilastirma Matrisi
| Ozellik | Free | Starter | Professional | Enterprise | On-Prem |
| --- | --- | --- | --- | --- | --- |
| Image scan | Evet | Evet | Evet | Evet | Evet |
| Repo secret scan | Kisitli | Evet | Evet | Evet | Evet |
| File scan | Hayir | Kisitli | Evet | Evet | Evet |
| SBOM compare/merge | Hayir | Hayir | Evet | Evet | Evet |
| Policy enforcement | Hayir | Kisitli | Evet | Evet | Evet |
| SSO/SAML | Hayir | Hayir | Hayir | Evet | Opsiyonel |
| Audit logs | Kisitli | Kisitli | Evet | Evet | Evet |
| Dedicated support | Hayir | Hayir | Hayir | Evet | Opsiyonel |

## 4. Add-on'lar
- Extra scan paketi: 1000 ek scan / ay.
- Extra storage paketi: 100 GB artifact saklama.
- Professional services: onboarding workshop, custom policy, migration, pentest-readiness.

## 5. Trial & Freemium Stratejisi
- 14 gunluk Professional deneme.
- Free plan ile urun aktivasyonu; scan limiti ve export limiti ile yukari plan gecisi tesvik edilir.
- In-app upgrade trigger'lari quota asimi, kullanici sayisi ve entegrasyon ihtiyacinda gosterilir.

## 6. Partner/Reseller Programi
- Silver, Gold, Platinum seviyeleri tanimlanir.
- Marj, demo tenant, teknik egitim ve co-selling avantajlari sunulur.

## 7. MSP Ozel Fiyatlandirmasi
- Tenant havuzu bazli toplu lisanslama.
- Ozet dashboard ve delegated admin dahil paketler.
- Min taahhut + kullanim bazli degisken ucret karmasi.

## 8. Kurumsal SLA Taahhutleri
- Enterprise cloud icin %99.9 aylik uptime.
- P1 olaylarda 30 dakika ilk cevap, P2 olaylarda 4 saat.
- Ozel CSM/TAM opsiyonu.

## 9. Faturalandirma Dongusu
- Aylik ve yillik odeme; yillik odemede %20 indirim.
- Kredi karti, banka havalesi ve enterprise fatura secenekleri.

## 10. Churn Onleme Stratejileri
- Aktivasyon email'leri, onboarding checklist, ilk scan sihirbazi.
- Riskli musteri sinyalleri: dusuk MAU, tarama dususu, destek memnuniyetsizligi.
- CSM dokunuslari, usage review ve ROI raporlari ile yenileme guclendirilir.

## 11. Ticarilestirme Notlari
- Fiyatlandirma notu 001: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 002: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 003: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 004: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 005: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 006: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 007: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 008: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 009: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 010: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 011: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 012: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 013: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 014: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 015: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 016: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 017: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 018: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 019: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 020: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 021: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 022: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 023: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 024: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 025: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 026: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 027: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 028: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 029: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 030: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 031: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 032: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 033: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 034: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 035: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 036: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 037: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 038: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 039: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 040: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 041: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 042: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 043: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 044: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 045: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 046: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 047: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 048: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 049: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 050: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 051: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 052: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 053: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 054: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 055: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 056: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 057: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 058: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 059: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 060: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 061: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 062: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 063: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 064: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 065: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 066: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 067: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 068: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 069: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 070: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 071: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 072: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 073: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 074: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 075: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 076: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 077: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 078: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 079: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 080: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 081: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 082: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 083: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 084: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 085: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 086: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 087: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 088: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 089: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 090: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 091: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 092: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 093: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 094: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 095: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 096: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 097: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 098: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 099: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 100: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 101: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 102: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 103: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 104: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 105: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 106: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 107: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 108: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 109: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 110: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 111: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 112: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 113: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 114: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 115: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 116: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 117: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 118: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 119: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 120: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 121: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 122: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 123: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 124: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 125: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 126: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 127: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 128: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 129: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 130: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 131: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 132: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 133: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 134: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 135: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 136: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 137: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 138: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 139: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 140: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 141: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 142: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 143: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 144: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 145: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 146: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 147: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 148: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 149: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 150: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 151: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 152: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 153: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 154: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 155: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 156: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 157: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 158: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 159: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 160: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 161: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 162: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 163: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 164: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 165: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 166: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 167: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 168: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 169: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 170: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 171: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 172: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 173: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 174: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 175: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 176: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 177: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 178: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 179: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 180: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 181: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 182: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 183: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 184: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 185: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 186: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 187: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 188: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 189: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 190: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 191: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 192: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 193: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 194: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 195: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 196: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 197: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 198: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 199: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 200: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 201: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 202: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 203: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 204: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 205: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 206: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 207: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 208: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 209: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 210: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 211: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 212: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 213: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 214: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 215: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 216: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 217: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 218: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 219: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 220: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 221: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 222: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 223: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 224: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 225: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 226: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 227: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 228: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 229: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 230: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 231: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 232: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 233: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 234: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 235: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 236: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 237: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 238: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 239: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 240: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 241: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 242: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 243: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 244: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 245: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 246: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 247: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 248: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 249: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Fiyatlandirma notu 250: plan sinirlari, gross margin, destek maliyeti, rakip benchmark ve upsell tetikleyicisi birlikte gozden gecirilmelidir.
- Operasyonel not 001: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 002: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 003: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 004: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 005: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 006: saas modeli ve fiyatlandirma icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.


---

## 🔗 İlgili Notlar

- [[01_Is_Analizi]]
- [[05_Veritabani_Tasarimi]]
- [[02_Proje_Yonetimi]]
