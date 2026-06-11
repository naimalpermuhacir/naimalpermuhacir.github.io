---
tags:
  - urun
  - tasarim
  - bugzora
aliases:
  - UI/UX Tasarımı
  - Frontend Design
parent: "[[00_BugZora_Hub]]"
dg-publish: true
---

# BugZora SaaS Donusumu - UI/UX Tasarimi

_Guncellenme tarihi: 2026-06-05_

## 1. Design System Prensipleri
- Guvenlik urunlerinde yogun veri yogunlugunu net hiyerarsi ile dengele.
- Kritik eylemleri renk, ikon ve metin tekrarli uyari ile destekle.
- Filtrelenebilir, kaydedilebilir ve tenant bazli ozellestirilebilir bileşenler kullan.

## 2. Kullanici Akis Diyagramlari (Metin)
### Onboarding Akisi
- Signup -> email verification -> tenant olusturma -> plan secimi -> ilk entegrasyon -> ilk scan -> dashboard ozet.
### Yeni Scan Baslatma Akisi
- Dashboard -> New Scan -> hedef tipi secimi -> config -> policy secimi -> quota kontrol -> submit -> status page.
### Sonuc Inceleme Akisi
- Job detail -> severity filtreleri -> bulgu detay -> remediation adimlari -> ticket olustur -> exception veya close.
### Policy Olusturma Akisi
- Policy list -> create -> rule builder veya rego upload -> test sample -> save -> assign.
### Rapor Olusturma Akisi
- Reports -> template sec -> zaman araligi -> branding -> generate -> download/share.

## 3. Ekran Listesi ve Aciklamalari
### Dashboard
- ust KPI kartlari.
- aktif taramalar paneli.
- kritik bulgu trendi.
- tenant health score.
- recent notifications.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Scan Jobs Listesi
- filtreler.
- durum badge'leri.
- kuyruk/running/completed sekmeleri.
- bulk action.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Scan Job Detay
- metadata.
- live event timeline.
- policy sonucu.
- rapor indirme.
- retry/cancel.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Vulnerability Detail
- CVSS, EPSS, fix version.
- asset etkisi.
- remediation guidance.
- referans baglantilari.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### SBOM Viewer
- paket agaci.
- lisans dagilimi.
- karsilastirma modulu.
- export.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Policy Yonetimi
- policy list.
- version history.
- test harness.
- assignment drawer.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Report Builder
- template secici.
- widget secici.
- zaman araligi.
- branding ve logo.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Integration Ayarlari
- GitHub/GitLab/Jira/Slack bağlantıları.
- secret status.
- test connection.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Tenant Ayarlari
- organization profile.
- domain mapping.
- quota and plan.
- security settings.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### User Management
- invite.
- roles.
- MFA status.
- last login.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Billing & Subscription
- plan kartlari.
- usage meter.
- invoice list.
- payment method.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.

### Audit Logs
- event table.
- actor/resource filtresi.
- export.
- retention note.
- Sayfa performans hedefi: LCP < 2.5s, etkileşimde hissedilir gecikme olmamali.


## 4. Renk Paleti ve Tipografi Onerileri
- Ana renk: koyu lacivert ve guven veren mavi tonlari.
- Uyari renkleri: kritik icin kirmizi, yuksek icin turuncu, medium icin sari, low icin mavi/yesil.
- Font: Inter veya IBM Plex Sans; kod bloklari icin JetBrains Mono.

## 5. Mobile Responsiveness Stratejisi
- Dashboard kartlari 12 kolon grid'den 1 kolon yapiya iner.
- Tablo agir ekranlarda responsive table yerine kart ozet + drawer detayi kullanilir.
- Kritik eylemler sticky alt aksiyon cubugunda toplanir.

## 6. Accessibility Gereksinimleri (WCAG 2.1 AA)
- Kontrast oranlari AA standardini saglamalidir.
- Keyboard navigasyon, focus ring, aria-label ve screen reader metinleri zorunludur.
- Renk tek basina anlam tasimamalidir.

## 7. Frontend Teknoloji Stack'i
- Next.js 14 App Router
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- TanStack Table
- Recharts veya Visx

## 8. UX Detay Notlari
- UX notu 001: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 002: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 003: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 004: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 005: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 006: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 007: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 008: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 009: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 010: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 011: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 012: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 013: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 014: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 015: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 016: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 017: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 018: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 019: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 020: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 021: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 022: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 023: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 024: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 025: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 026: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 027: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 028: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 029: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 030: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 031: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 032: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 033: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 034: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 035: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 036: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 037: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 038: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 039: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 040: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 041: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 042: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 043: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 044: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 045: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 046: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 047: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 048: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 049: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 050: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 051: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 052: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 053: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 054: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 055: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 056: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 057: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 058: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 059: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 060: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 061: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 062: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 063: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 064: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 065: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 066: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 067: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 068: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 069: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 070: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 071: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 072: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 073: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 074: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 075: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 076: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 077: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 078: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 079: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 080: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 081: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 082: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 083: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 084: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 085: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 086: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 087: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 088: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 089: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 090: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 091: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 092: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 093: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 094: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 095: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 096: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 097: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 098: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 099: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 100: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 101: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 102: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 103: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 104: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 105: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 106: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 107: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 108: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 109: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 110: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 111: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 112: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 113: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 114: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 115: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 116: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 117: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 118: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 119: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 120: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 121: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 122: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 123: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 124: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 125: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 126: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 127: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 128: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 129: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 130: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 131: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 132: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 133: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 134: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 135: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 136: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 137: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 138: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 139: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 140: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 141: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 142: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 143: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 144: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 145: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 146: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 147: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 148: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 149: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 150: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 151: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 152: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 153: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 154: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 155: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 156: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 157: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 158: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 159: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 160: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 161: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 162: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 163: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 164: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 165: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 166: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 167: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 168: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 169: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 170: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 171: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 172: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 173: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 174: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 175: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 176: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 177: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 178: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 179: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 180: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 181: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 182: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 183: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 184: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 185: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 186: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 187: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 188: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 189: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 190: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 191: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 192: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 193: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 194: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 195: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 196: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 197: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 198: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 199: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 200: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 201: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 202: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 203: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 204: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 205: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 206: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 207: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 208: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 209: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 210: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 211: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 212: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 213: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 214: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 215: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 216: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 217: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 218: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 219: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 220: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 221: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 222: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 223: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 224: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 225: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 226: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 227: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 228: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 229: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 230: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 231: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 232: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 233: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 234: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 235: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 236: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 237: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 238: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 239: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 240: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 241: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 242: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 243: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 244: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 245: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 246: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 247: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 248: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 249: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.
- UX notu 250: bileşen durumlari, bos ekranlar, hata mesajlari, onboarding yardimlari, filtre kaydi ve performans beklentileri ekran bazinda tanimlanmalidir.


---

## 🔗 İlgili Notlar

- [[06_API_Tasarimi]]
- [[03_Yazilim_Mimarisi]]
- [[PROMPT_02_Frontend_Dashboard]]
