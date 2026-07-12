# Eşikler — Tek Doğruluk Kaynağı

> **Bu dosya tartışılmaz ve yalnız Nazım onayıyla değişir.**
> Başka dosyaya kopyalanmaz — link verilir. Karar mantığı LLM'e bırakılmaz;
> A7 raporu bu tabloyla deterministik karşılaştırma yapar.

**Son güncelleme:** 2026-07-12 · Kaynak: [main_analysis](../docs/strategy/main_analysis.md) §5 (v1.1, onaylı)

---

## Metrik eşikleri

| Metrik / Kural | Eşik |
|---|---|
| CPI (test) | < $0.40 hedef · < $0.30 mükemmel |
| Reklam CTR | > %1.5–2 |
| D1 retention | > %45 |
| D7 retention | > %15–20 |
| İlk gün playtime | > 15–20 dk |

## Kapı kuralları

| Kapı | Kural |
|---|---|
| Yeşil ışık (M2) | Cetvel toplamı **≥ 50/70** VE hiçbir kriter 1–2 puan değil (kritik zayıflık vetosu) |
| GameBrief kapısı (M2→M3) | Completion score **≥ 90** — altında M3 çalıştırılmaz |
| Geliştirme tavanı (M5) | **≤ 2 hafta efor** / prototip |
| Karar mantığı (M7) | Hepsi yeşil → **BÜYÜT** · tek zayıf → **DÜZELT** (oyun başına 1 hak) · çoklu kırmızı → **ÖLDÜR** |

## Skorlama cetveli (M2 — 70 puan)

| Kriter | Ağırlık | Dönüşüm |
|---|---|---|
| 3 saniye okunabilirlik | ×3 | 1–5 puan |
| Geliştirme maliyeti | ×3 | 1–5 (ucuz = yüksek puan) |
| Juice potansiyeli | ×2 | 1–5 |
| Reklam izlenebilirlik | ×2 | 1–5 |
| Rekabet yoğunluğu | ×2 | düşük=5 · orta=3 · yüksek=1 |
| Trend ivmesi | ×2 | yükseliyor=5 · plato=3 · düşüşte=1 |

## Kayıtlı istisnalar

| Tarih | İstisna | Sigorta |
|---|---|---|
| 2026-07-11 | Toy Pile 53/70 ile bilinçli override (Nazım) | M6 CPI testi — sonuç kötüyse âşık olma lüksü yok; tekrarı otomatik değildir |

## Fallback kuralları

- Google Play yeni hesap kısıtı store sayfasını geciktirirse: **CTR-proxy testi** —
  video kreatif yayınla, CTR/CPC ölç. CTR eşiği (>%1.5) Faz 1'de karar verdirir;
  CPI eşiği soft launch aşamasında uygulanır.
