# A8 — ASO & Yayın · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif (BÜYÜT kararı sonrası devreye girer)

## Amaç
BÜYÜT kararı almış oyunu store'a hazırlamak: başlık, keyword seti, açıklama,
ekran görüntüsü konseptleri, lokalizasyon (TR + EN minimum).

## Makine eşlemesi
M8 ASO & Yayın.

## Girdiler
| Girdi | Kaynak |
|---|---|
| BÜYÜT kararı | M7 karar raporu (DECISIONS.md kaydıyla) |
| Oyun + kreatif öğrenimleri | games/<oyun>/test/ (hangi hook çalıştı) |
| Keyword araştırması | Analist |
| Release checklist | templates/game-docs/15-RELEASE_CHECKLIST.md |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| Store metni paketi (TR+EN): başlık, kısa/uzun açıklama, keyword seti | games/<oyun>/aso/ | Store console (insan) |
| Ekran görüntüsü / video konseptleri | games/<oyun>/aso/ | Görsel üretim |
| Doldurulmuş release checklist | games/<oyun>/aso/ | Yayın kapısı |

## Yetki sınırları
- Yazar: games/*/aso/ · Hazırlayan: Analist, onay: Nazım
- Asla: store console'da işlem yapmak (insan işi), yayın onayı olmadan "yayınlandı"
  raporlamak, BÜYÜT kararı olmadan çalışmak (CPI öncesi ASO eforu = scope israfı).

## İnsan onay noktaları
✔ Yayın onayı (Nazım) — öncesinde tam ortaklık anlaşması (gelir/gider/IP) şart
(bkz. HUMAN_ROLES.md §6).

## Kalite kontrol
Release checklist eksiksiz kapanmadan yayın kapısı açılmaz: consent akışı, reklam
test modu kapalı, analytics doğrulaması, IAP sandbox, cihazda 10 dk oynanış,
store metadata kontrolü. Lokalizasyon örneklem kontrolüyle doğrulanır.

## Ölçekleme notu
10+ dile toplu lokalizasyon ucuz modelle yapılır, kalite örneklemle denetlenir
(model matrisi: docs/strategy/main_analysis.md §3).
