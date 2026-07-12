# <OyunAdı> — Seviye Üretimi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A3 tasarlar, A5 uygular
**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor *(ADR-0006)*

İlke: içerik %100 algoritmik; elle seviye tasarımı yoktur. Üretilen her seviye
**çözülebilirlik botundan** geçmeden kabul edilmez.

## 1. Algoritma

```
seed(level_id) → parametreleri DifficultyService'ten al →
<üretim adımları: tür seç, obje yerleştir, ...> →
solver botu simülasyonu → çözülemezse REDDET, yeni seed dene →
LevelData asset'i yaz (Assets/_Content)
```

## 2. Zorluk parametreleri (DifficultyService)

| Parametre | Başlangıç | Eğri kuralı | Config alanı |
|---|---|---|---|
| <toplam obje N> | <12> | <levelle artar: ...> | |
| <tür sayısı T> | <4> | | |
| <tuzak oranı> | | | |

Nefes kuralı: her <4–5> seviyede bir kolay seviye (near-miss ve akış için).

## 3. Çözülebilirlik botu

- Strateji: <greedy / ...> — insan stratejisinin alt sınırı olmalı (bot çözüyorsa insan kesin çözer).
- Red kriterleri: <çözümsüz / tek yollu / süre aşımı>
- Editor aracı: "Generate & Validate" — ilk <30> seviyeyi üretir.

## 4. Doğrulama metrikleri

Üretilen setin dağılımı loglanır: <ortalama hamle, kalan slot, red oranı> —
zorluk eğrisi hissi cihazda insan testiyle kalibre edilir.

## 5. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
