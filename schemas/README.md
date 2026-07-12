# schemas/ — Veri Sözleşmeleri

Ajanlar arası her teslim buradaki şemalara uyar; uymayan çıktı "tamamlandı" sayılmaz.
Şema değişikliği = standart değişikliği → **ADR + insan onayı** gerekir.

| Şema | Ne taşır | Üreten → Tüketen | Durum |
|---|---|---|---|
| [gamebrief.v1.json](gamebrief.v1.json) | Aday kartı ⊕ tasarım çekirdeği ⊕ completion score | A1 → A3 | **Taslak** — Faz 2'de kilitlenir (F-103) |
| [aday-karti.v1.yaml](aday-karti.v1.yaml) | Radar aday kartı | A2 → A1 | Aktif |
| [event-schema.md](event-schema.md) | Analytics event standardı (tüm oyunlar) | A5 → A7 | Aktif |

## Kurallar

- Versiyonlama: dosya adında (`.v1`, `.v2`). Kırıcı değişiklik = yeni versiyon; eski dosya silinmez.
- Completion score: `score = round(100 × dolu_zorunlu / toplam_zorunlu)` — eşik ≥ 90
  ([ops/esikler.md](../ops/esikler.md)). 90 altında M3 çalıştırılmaz.
- Oyun repoları event şemasını **kopyalamaz**, kendi `docs/02-EVENT_SCHEMA.md`'sinde
  bu standardın üstüne yalnız oyuna özgü event ekler.
