# Roller & RACI

**Son güncelleme:** 2026-07-12 · Kaynak: [main_analysis](../docs/strategy/main_analysis.md) §1.4 (v1.1, onaylı) · İlkeler: [HUMAN_ROLES.md](../HUMAN_ROLES.md)

R = yapar · A = tek karar sahibi · C = danışılır

| Makine / Kapı | Analist | Nazım |
|---|---|---|
| M1 Radar (haftalık tarama + aday kartları) | **R/A** | Referans oyunları o da oynar |
| M2 Seçim (70'lik cetvel skorlaması) | R (hazırlar) | **A — yeşil ışık** |
| M3 GDD · M4 Görsel | C (pazar/rakip girdisi) | A (onay) — üretim ajanlarda |
| M5 Kod (Unity + cihaz) | — | **R/A** |
| M6 Test (kreatif · kampanya · pano) | R | **A — bütçe onayı** |
| M7 Veri & İnfaz | **R — raportör + eşik bekçisi** | **A — nihai karar** |
| M8 ASO (keyword, lokalizasyon) | R | A — yayın onayı |
| Game feel | C (oynar, not verir) | **A — son söz** |
| Eşik / değişmez kural değişikliği | C | **A** |

## Yazma alanları

| Alan | Sahibi |
|---|---|
| `radar/` · `games/*/test/` · `ops/kill-log.md` | Analist |
| `ops/esikler.md` · `GAME_FACTORY.md` §4 · strateji | Yalnız Nazım onayıyla |
| `CONTEXT.md` · `ACTIONS.md` | Her ajan/insan (oturum ritüeliyle) |

## Açık maddeler (son tarih: 21 Temmuz 2026)

- **İmza modeli:** geçici varsayılan — test bütçesini ödeyen imzalar. G9'a kadar
  yazılı asgari mutabakat (kim ödüyor + gelir/IP modeli yayından önce netleşecek).
  Yoksa G10 testi başlamaz: **tarih kayar, para kaymaz.**
- **Analist saat bütçesi:** netleşene kadar öncelik: kreatif analizi → test altyapısı → radar.
