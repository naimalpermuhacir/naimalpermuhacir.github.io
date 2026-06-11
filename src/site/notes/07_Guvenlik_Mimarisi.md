---
tags:
  - mimari
  - guvenlik
  - bugzora
aliases:
  - Güvenlik Mimarisi
  - Security Architecture
parent: "[[00_BugZora_Hub]]"
dg-publish: true
---

# BugZora SaaS Donusumu - Guvenlik Mimarisi

_Guncellenme tarihi: 2026-06-05_

## 1. Security-by-Design Prensipleri
- Varsayilan olarak en az yetki, sifir guven ve guvenli varsayilanlar uygulanir.
- Her yeni ozellik icin threat model, abuse case ve veri siniflandirma notu zorunludur.
- Secure SDLC, kod inceleme, bagimlilik taramasi ve release quality gate ile desteklenir.

## 2. Authentication Mimarisi
- Email/password + MFA
- OAuth2/OIDC ile Google, GitHub, GitLab, Microsoft
- Enterprise icin SAML 2.0 SSO
- Session revocation ve device-level login gorunurlugu

## 3. Authorization Modeli (RBAC + ABAC Hybrid)
- Rol tabanli yetkiler temel izinleri saglar.
- ABAC katmani tenant, plan, ortam, kaynak etiketi ve saat bazli kisitlamalari uygular.
- Policy exceptions sadece onayli workflow ile verilir.

## 4. Rol Tanimlari
- Super Admin: platform capinda operasyon ve destek yetkisi.
- Tenant Admin: tenant ayarlari, kullanici, entegrasyon ve billing yonetimi.
- Security Engineer: scan, policy, rapor ve bildirim yonetimi.
- Developer: kendi projeleri icin scan baslatma ve sonuc gorme.
- Viewer: salt okunur dashboard ve rapor erisimi.
- Auditor: audit log ve compliance raporlarina zaman kisitli erisim.

## 5. Permission Matrix Tablosu
| Gorunum | Super Admin | Tenant Admin | Security Engineer | Developer | Viewer | Auditor |
| --- | --- | --- | --- | --- | --- | --- |
| Tenant ayarlari guncelle | Evet | Evet | Hayir | Hayir | Hayir | Hayir |
| Kullanici yonetimi | Evet | Evet | Kisitli | Hayir | Hayir | Hayir |
| Scan baslat | Evet | Evet | Evet | Evet | Hayir | Hayir |
| Policy yonet | Evet | Evet | Evet | Hayir | Hayir | Hayir |
| Rapor indir | Evet | Evet | Evet | Kisitli | Evet | Evet |
| Billing goruntule | Evet | Evet | Hayir | Hayir | Hayir | Hayir |
| Audit log goruntule | Evet | Kisitli | Kisitli | Hayir | Hayir | Evet |

## 6. API Security
- Rate limiting, bot korumasi, WAF ve IP reputation kontrolleri uygulanir.
- OWASP Top 10 risklerine karsi input validation, output encoding ve secure headers zorunludur.
- SSRF ve command injection riskleri tarama hedeflerinde ayrica kontrol edilir.

## 7. Data Security
- At rest: disk, object storage ve veritabani seviyesinde sifreleme.
- In transit: TLS 1.2+, tercihen 1.3, ic trafik icin mTLS.
- Hassas alanlar uygulama seviyesinde envelope encryption ile korunabilir.

## 8. Secrets Management
- Vault merkezidir; sirlar source code ve CI log'larina yazdirilmaz.
- Rotasyon periyotlari secret tipine gore ayrilir.
- Break glass erisimi audit ile izlenir.

## 9. Network Security (Zero Trust Architecture)
- Kimliksiz servis iletisimine izin verilmez.
- East-west trafik policy ile sinirlandirilir.
- Egress sadece izinli hedeflere aciktir.

## 10. Container Security
- Base image hardening, non-root runtime, read-only filesystem, seccomp/apparmor profilleri.
- Image signing ve provenance (cosign/SLSA) roadmap'e alinmalidir.
- Runtime anomaly detection enterprise fazda genisletilir.

## 11. Compliance Gereksinimleri
- SOC2 icin access control, logging, change management ve DR kontrolleri.
- ISO 27001 icin ISMS policy map'i ve asset envanteri.
- GDPR icin veri minimizasyonu, DSR surecleri, retention ve regional options.

## 12. Audit Logging Gereksinimleri
- Login, role degisikligi, policy update, scan create/cancel, report indirme, billing degisiklikleri loglanir.
- Loglar degistirilemez, zaman damgali ve butunluk kanitli tutulur.

## 13. Penetration Testing Plani
- MVP oncesi black-box ve authenticated web/API testleri.
- Yilda en az bir kez harici pentest ve her buyuk release sonrasi hedefli retest.
- Bulunan kritik aciklar 7 gun, yuksek aciklar 30 gun icinde kapatilacak sekilde SLA tanimlanir.

## 14. Security Incident Response Plani
- Hazirlik, tespit, sinirlama, eradication, recovery ve postmortem asamalari tanimlidir.
- Severity siniflari ve rota eskalasyonlari PagerDuty ile otomatiklestirilir.

## 15. Vulnerability Disclosure Policy
- Guvenlik arastirmacilari icin sorumlu ifsa kanali aciklanir.
- Teyit, triage, remediation ve public advisory takvimi net tanimlanir.

- Guvenlik kontrolu 001: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 002: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 003: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 004: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 005: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 006: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 007: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 008: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 009: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 010: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 011: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 012: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 013: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 014: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 015: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 016: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 017: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 018: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 019: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 020: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 021: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 022: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 023: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 024: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 025: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 026: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 027: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 028: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 029: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 030: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 031: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 032: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 033: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 034: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 035: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 036: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 037: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 038: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 039: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 040: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 041: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 042: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 043: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 044: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 045: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 046: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 047: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 048: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 049: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 050: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 051: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 052: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 053: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 054: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 055: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 056: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 057: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 058: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 059: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 060: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 061: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 062: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 063: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 064: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 065: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 066: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 067: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 068: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 069: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 070: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 071: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 072: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 073: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 074: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 075: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 076: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 077: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 078: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 079: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 080: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 081: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 082: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 083: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 084: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 085: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 086: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 087: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 088: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 089: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 090: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 091: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 092: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 093: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 094: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 095: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 096: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 097: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 098: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 099: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 100: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 101: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 102: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 103: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 104: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 105: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 106: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 107: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 108: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 109: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 110: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 111: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 112: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 113: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 114: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 115: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 116: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 117: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 118: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 119: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 120: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 121: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 122: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 123: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 124: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 125: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 126: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 127: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 128: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 129: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 130: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 131: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 132: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 133: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 134: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 135: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 136: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 137: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 138: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 139: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 140: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 141: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 142: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 143: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 144: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 145: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 146: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 147: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 148: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 149: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 150: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 151: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 152: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 153: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 154: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 155: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 156: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 157: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 158: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 159: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 160: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 161: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 162: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 163: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 164: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 165: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 166: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 167: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 168: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 169: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 170: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 171: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 172: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 173: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 174: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 175: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 176: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 177: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 178: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 179: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 180: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 181: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 182: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 183: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 184: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 185: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 186: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 187: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 188: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 189: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 190: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 191: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 192: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 193: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 194: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 195: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 196: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 197: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 198: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 199: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 200: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 201: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 202: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 203: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 204: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 205: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 206: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 207: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 208: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 209: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 210: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 211: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 212: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 213: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 214: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 215: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 216: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 217: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 218: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 219: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 220: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 221: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 222: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 223: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 224: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 225: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 226: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 227: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 228: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 229: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Guvenlik kontrolu 230: owner, kontrol amaci, kanit tipi, test periyodu, istisna sureci ve iyilestirme backlog baglantisi belirtilmelidir.
- Operasyonel not 001: guvenlik mimarisi icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 002: guvenlik mimarisi icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 003: guvenlik mimarisi icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.
- Operasyonel not 004: guvenlik mimarisi icin karar, sahip, zamanlama, risk ve cikti netlestirilmelidir.


---

## 🔗 İlgili Notlar

- [[03_Yazilim_Mimarisi]]
- [[06_API_Tasarimi]]
- [[04_Altyapi_Mimarisi]]
- [[PROMPT_03_Auth_MultiTenancy]]
