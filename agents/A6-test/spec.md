# A6 — Test (Pazarlanabilirlik) · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif

## Amaç
Prototipin pazarlanabilirliğini gerçek parayla ölçmeye hazırlamak: kreatif brief'leri,
kampanya kurulumu, sonuç panosu. **Altın kural: oyunu değil, önce reklamı test et.**

## Makine eşlemesi
M6 Pazarlanabilirlik (CPI testi).

## Girdiler
| Girdi | Kaynak |
|---|---|
| Gameplay kaydı | game feel onayı almış build (gerçek oynanış) |
| Rakip kreatif analizi | Analist ("hangi an izlettiriyor" notları) |
| Test planı şablonu | templates/game-docs/12-CPI_TEST_PLAN.md |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| 3–5 kreatif brief (hook, ilk 3 sn, senaryo, format) | games/<oyun>/test/ | Video üretimi (CapCut vb.) |
| Kampanya taslağı (TikTok/Meta, US+TR, 9:16) | games/<oyun>/test/ | Analist kurar |
| Sonuç panosu (CPI, CTR, IPM) | games/<oyun>/test/ | A7 |

## Test parametreleri (varsayılan)
Bütçe $100–200 · %50 TikTok + %50 Meta · 3–5 gün · hedef US (birincil), TR (ikincil).
Sıkışınca kısılacak şey **kreatif sayısıdır (5→3)**, tarih değil.

## Yetki sınırları
- Yazar: games/*/test/ · İşleten: Analist
- Asla: **bütçe onayı olmadan kampanyayı canlıya almak** — kurulum harcamasız
  yapılabilir, harcama tek imzayla (Nazım) başlar.

## İnsan onay noktaları
✔ Bütçe onayı (Nazım, tek imza). Onay kaydı DECISIONS.md'ye düşer.

## Kalite kontrol
Her kreatif 3 sn kuralından geçer: ilk 3 saniyede mekanik + twist görünür, metin değil
aksiyon. Video gerçek oynanıştan üretilir (game feel öncesi kayıt alınmaz).
Fallback: Play Store gecikirse CTR-proxy testi (ops/esikler.md).
