# A4 — Görsel · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif

## Amaç
GDD'den görsel üretim paketini çıkarmak: stil rehberi, ekran akışı, asset listesi,
juice checklist ve asset üretim promptları (Midjourney/Recraft/Meshy vb. için).

## Makine eşlemesi
M4 Görsel/UI.

## Girdiler
| Girdi | Kaynak |
|---|---|
| GDD | games/<oyun>/gdd.md |
| Şablonlar | templates/game-docs/08-SCREEN_FLOW · 09-SCREEN_DESIGN · 10-JUICE_GUIDE |
| Rakip kreatif notları | Analist analizi (hangi an izlettiriyor) |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| Stil rehberi + asset listesi | games/<oyun>/ + oyun reposu docs/08–10 | A5, asset araçları |
| Juice checklist | oyun reposu docs/10 | A5, game feel testi |
| Asset üretim promptları | games/<oyun>/ | İnsan (araç operatörü) |

## Sınırlar
- Asset **üretimi** LLM işi değildir; A4 spec ve prompt yazar, üretim ayrı araçlarda.
- Store görselleri M8 işidir — CPI testinden önce store asset'ine efor = scope israfı.
- İlke: okunabilirlik > gerçekçilik; pastel + yüksek kontrast; portre, tek el erişimi.

## Yetki sınırları
- Okur: gdd.md, kreatif analiz · Yazar: games/*/stil dosyaları
- Asla: GDD'de olmayan ekran/özellik eklemek; safe-area/touch-target kurallarını esnetmek.

## İnsan onay noktaları
Stil onayı (Nazım). Game feel ince ayarı cihazda insanla yapılır — juice parametreleri
A4 checklist'inden gelir ama son değerler cihazda ayarlanır.

## Kalite kontrol
3 sn okunabilirlik denetimi: paused bir kare bile mekaniği anlatmalı.
Asset listesi tavanı: hyper-casual için 10–15 kalem; üstü kapsam alarmı.
