# ROADMAP — Faz Planı

**Son güncelleme:** 2026-07-12 · Gün gün plan ve gerekçeler: [docs/strategy/main_analysis.md](docs/strategy/main_analysis.md) §2

İlke: fazlar **takvimle değil, çıktıyla ve tetikle** ilerler. Sonraki faza geçmek
için önceki fazın "bitti" tanımı sağlanmalıdır.

---

## FAZ 1 — "İlk Oyun Çıkıyor" · 13–22 Temmuz 2026 (10 gün) · **AKTİF**

**Hedef cümle:** *Toy Pile cihazda temiz oynanıyor ve pazarlanabilirlik testi yayında.*

- Kapsam donmuş: tap triple-match + shockwave cascade, şasi-lite. Yeni özellik teklifi = otomatik red.
- İki paralel hat: Nazım M4/M5 (kaplama + game feel) ∥ Analist M1/M6 (kreatif analizi, test altyapısı).
- **Bitti tanımı:** cihazda temiz kurulumdan 10 dk sorunsuz oynanış ✚ test canlı ✚ sonuç panosu hazır.
- Kritik kapılar: G7 game feel (19 Tem) · G9 imza mutabakatı (21 Tem) · G10 bütçe onayı (22 Tem).

## FAZ 2 — "Karar, Standart, İkinci Tur" · 23 Temmuz – 23 Ağustos

1. **M7 kararı (Toy Pile):** analist raporu → Nazım kararı: ÖLDÜR / DÜZELT / BÜYÜT.
   BÜYÜT ise gerçek şasi yatırımı (Firebase, mediation, IAP, consent) + soft launch.
2. M1 radar rutini analist sahipliğinde oturur (haftalık).
3. **Web-First Prototipleme:** `game-dev` (Babylon.js) hattı M5 için devreye alınır.
4. **GameBrief v1 kilitlenir** (schemas/gamebrief.v1.json → durum: Kilitli).
5. A1 Producer talimatı v2 (AOS öğrenimleri: state + validation + modlar + completion score).
6. **Prototip #2 hattan geçer** — fabrika iddiasının ispatı ikinci oyundur.
7. Antigravity vs Claude Code A/B kararı → `uretim.arac` varsayılanı.

## FAZ 3 — "Orkestrasyon" · Eylül+ (takvimle değil, TETİKLE)

**Tetik koşulu (ikisi birden):** hattan ≥ 2 prototip geçti **VE**
(radar rutini 3 hafta üst üste elle aksadı **VEYA** ayda 2+ prototip ritmi hedefleniyor).

Tetik gelmeden başlamak = fabrika tuzağı. Kapsam: [orchestrator/README.md](orchestrator/README.md)

- SDK seçimi (Claude Agent SDK ↔ OpenAI Agents SDK) Faz 2 A/B sonucuna göre.
- İnsan kapıları koda gömülür: bütçe/yayın adımında agent durur. **Auto-spend yok.**
- Radar v2: zamanlanmış tarama; günlük hafif tarama ucuz modelde.
- Hedef ritim: ayda 1–2 prototip; %80–90 kill oranı normal seyir.

## Ufuk (v2+ — şimdi yapılmaz)

Meta katman, multiplayer, turnuva, LiveOps, hikâye hattı, 10+ dil lokalizasyonu.
Bunlar ancak BÜYÜT kararı almış bir oyunun kendi yol haritasında açılır.
