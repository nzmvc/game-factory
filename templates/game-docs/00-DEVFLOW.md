# <OyunAdı> — Geliştirme Akışı ve Hat Durumu

**Son güncelleme:** <YYYY-AA-GG> · **Fabrika modeli:** GameFactory `GAME_FACTORY.md` (burada anlatma, link ver)

## 1. Hat durumu

```
M0 <⬜/✅> → M1 <> → M2 <> → M3 <> → M4 <> → M5 <> → M6 <> → M7 <> → M8 <>
Şasi   Radar  Seçim   GDD   Görsel   Kod    CPI    Karar   Yayın
                              ↑ ŞU AN: <konum + tek cümle durum>
```

🟢 tamam · 🟡 devam · 🔴 başlamadı · ⛔ insan kapısı bekliyor

## 2. Makine × doküman eşlemesi

| Makine | Durum | İlgili dokümanlar | Kalan işler |
|---|---|---|---|
| M0 Şasi | | 01, 02, 03 | |
| M3 GDD | | 04, 05, 06, 07 | |
| M4 Görsel | | 08, 09, 10 | |
| M5 Kod | | 11 | |
| M6 CPI | | 12 | |
| M7 Karar | | 13 | |
| M8 Yayın | | 15 | |

## 3. Paralel iş matrisi

| İş A | İş B | Paralel? | Not |
|---|---|---|---|
| Asset tedariği (M4) | Mekanik kodu (M5) | ✅ | |
| Game feel testi | CPI kreatifi | ❌ | Video gerçek oynanıştan |
| CPI testi (M6) | Karar (M7) | ❌ | Veri gerekli |

## 4. Sıradaki insan kapısı

⛔ **<kapı adı>** — <tarih> — karar sahibi: <isim> — ön koşullar: <...>
