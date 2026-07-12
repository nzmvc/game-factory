# A2 — Radar · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif · **Promptlar:** [tarama-promptlari.md](tarama-promptlari.md)

## Amaç
Hyper/hybrid-casual pazarında yükselen, tek parmakla oynanan "satisfying" mekanikleri
**kanıtla** tespit edip aday kartlarına dönüştürmek.

## Makine eşlemesi
M1 Pazar Radarı.

## Girdiler
| Girdi | Kaynak |
|---|---|
| Top chart hareketleri | Google Play / App Store (US + TR) |
| Reklam yoğunluğu sinyalleri | Meta Ad Library, TikTok Creative Center |
| İndirme tahminleri | AppMagic (ücretsiz tier) |
| Sektör analizi | PocketGamer.biz, Deconstructor of Fun, publisher blogları |

Takip listesi: Voodoo, Rollic, SayGames, Homa, Supersonic, Azur Games, Kwalee, Lion Studios.

## Çıktılar
| Çıktı | Konum | Şema | Tüketen |
|---|---|---|---|
| Haftalık tarama (10 kart) | radar/taramalar/YYYY-Www.md | aday-karti.v1.yaml | A1 / Nazım |
| Günlük hızlı sinyal (ops.) | Pzt senkron notu | ≤ 3 madde + kaynak | Analist |

## Eleme filtreleri (listeye hiç girmez)
Match-3 / meta-ağırlıklı türler · multiplayer · hikâye tabanlı · elle yoğun içerik ·
lisanslı IP gerektiren konseptler.

## Yetki sınırları
- Okur: ops/esikler.md, schemas/ · Yazar: radar/taramalar/
- Asla: kanıtsız aday yazmak (kural: emin değilsen "doğrulanamadı"), skorlamak
  (M2 işi), ToS ihlali scraping.

## İnsan onay noktaları
Kapı yok; ancak yeşil ışık adaylarının referans oyunlarını insanlar **bizzat oynar**.

## Kalite kontrol
Her kartın `kanit` alanı kaynaklı olmalı; A1, kanıtsız kartı iade eder.
Sıfır aday geçerli bir sonuçtur — kart doldurmak için kalite düşürülmez.

## İşletim (Faz 1–2)
Analist, haftalık 60–90 dk (Pzt); model: web erişimli orta sınıf model (haftalık derin) +
ucuz model (günlük hafif). Faz 3: zamanlanmış tarama (orchestrator).
