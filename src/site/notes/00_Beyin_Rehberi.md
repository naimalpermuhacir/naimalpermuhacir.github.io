---
tags:
  - hub
  - meta
  - bugzora
parent: "[[00_BugZora_Hub]]"
aliases:
  - Beyin Rehberi
  - Brain Guide
dg-publish: true
---

# 🗺️ BugZora Brain — Kullanım Rehberi

---

## 🔥 ExcaliBrain — Beyin Görünümü

**Nasıl açılır:** `Ctrl+P` → "ExcaliBrain" → Enter

ExcaliBrain, notları **hiyerarşik ağaç** olarak görselleştirir.
- Üst → **parent** bağlantıları (ebeveyn)
- Yan → **sibling** (kardeş, aynı parent'a sahip)
- Alt → **child** (bu nota bağlı alt notlar)

**İpucu:** `00_BugZora_Hub` notunu merkeze al → tüm yapı açılır.

---

## 📊 Dataview — Canlı Durum Panosu

```dataview
TABLE tags, parent
FROM "BugZora"
SORT file.name ASC
```

### Mimari Notlar

```dataview
LIST
FROM "BugZora"
WHERE contains(tags, "mimari")
SORT file.name ASC
```

### Tamamlanmamış Prompt'lar

```dataview
LIST
FROM "BugZora"
WHERE contains(tags, "prompt")
SORT file.name ASC
```

---

## 🎨 Graf Görünümü İpuçları

### Global Graf (`Ctrl+G`)
- **Renk grupları** tag'lere göre ayarlı
- Sol panelde **Filters** → `path:BugZora` yazarak sadece bu vault'u gör
- **Depth** → 2 veya 3 en güzel görünüm

### Lokal Graf (daha güçlü!)
- Herhangi bir nota sağ tıkla → **"Open local graph"**
- O notun komşularını görürsün → bağlam odaklı analiz

### Graf Ayarları (şu an aktif):
| Ayar | Değer |
|------|-------|
| Node size | 1.4x |
| Link size | 1.2x |
| Repel strength | 14 |
| Link distance | 180 |
| Arrows | Açık |

---

## 🏗️ Uygulama Beyni Mimarisi

```
00_BugZora_Hub (🟠 Merkez)
├── 01_Is_Analizi (🟡 Strateji)
├── 02_Proje_Yonetimi (🟡 Strateji)
├── 08_SaaS_Modeli_Fiyatlandirma (🟡 Strateji)
├── 03_Yazilim_Mimarisi (🔵 Mimari)
│   ├── 04_Altyapi_Mimarisi (🔵)
│   │   ├── 10_DevOps_CI_CD (🔴)
│   │   └── PROMPT_04_Kubernetes (🟣)
│   ├── 05_Veritabani_Tasarimi (🔵)
│   ├── 06_API_Tasarimi (🔵)
│   │   └── PROMPT_07_Bildirim (🟣)
│   ├── PROMPT_01_Backend (🟣)
│   └── PROMPT_06_Scanner (🟣)
├── 07_Guvenlik_Mimarisi (🔴 Güvenlik)
│   └── PROMPT_03_Auth (🟣)
└── 09_UI_UX_Tasarimi (🟢 Ürün)
    └── PROMPT_02_Frontend (🟣)
```

---

## 🚀 Önerilen Eklentiler (Henüz Kurulmamış)

| Plugin | Neden? |
|--------|--------|
| **Templater** | Yeni notlarda otomatik frontmatter + parent |
| **Kanban** | Sprint ve görev yönetimi |
| **Excalidraw** (zaten var) | Mimari diyagramları not içinde |
| **DB Folder** | Notları tablo/veritabanı gibi göster |

---

*[[00_BugZora_Hub]] · [[03_Yazilim_Mimarisi]] · [[01_Is_Analizi]]*
