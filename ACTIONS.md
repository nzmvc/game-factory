# ACTIONS — Aktif Eylem Kuyruğu

> Fabrika seviyesi iş kuyruğu. Oyun-içi görevler oyun reposundaki BACKLOG'da yaşar
> (Toy Pile: `game-toy-pile/docs/14-BACKLOG.md`); burada yalnız hat/kapı seviyesi işler tutulur.
> Durumlar: ⬜ TODO · ⏳ IN_PROGRESS · ✅ DONE · ⛔ BLOKE (insan kapısı bekliyor)

**Son güncelleme:** 2026-07-14

---

## Şimdi (Faz 1 kritik yolu — hat tasarım revizyonu için durdu)

| ID | İş | Makine | Sorumlu | Durum | Son tarih |
|---|---|---|---|---|---|
| F-000 | **Tasarım revizyonu:** kök neden analizi tamam (bar disiplini + görsel kimlik). Kod tarafı: T-501/502 ✅ DONE. İnsan tarafı: T-503/504/505/506 ✅ DONE (2026-07-14 doğrulandı) — bkz. `game-toy-pile/docs/14-BACKLOG.md` §E. Yeni açık madde: T-507 (TileBar/kamera FOV Play Mode doğrulaması) ⬜ | M3 | Nazım (+A3/A5) | ⏳ | — |
| F-001 | Toy Pile asset kaplama + juice (3D modeller ✅, SFX ✅, partikül ⏳ T-203) | M4 | Nazım (+A4) | ⏳ | 18 Tem |
| F-001b | Kombo pitch testi (T-204) + şok dalgası/kamera game feel ince ayarı (T-205) | M5 | Nazım | ✅ | 19 Tem |
| F-002 | Rakip kreatif analizi (Zen Match, Triple Match 3D, Match Factory!, Tile Busters) | M1/M6 | Analist (+A2) | ⏳ | 19 Tem |
| F-003 | Test altyapısı: kampanya taslağı (harcamasız) + sonuç panosu iskeleti | M6 | Analist (+A6) | ⬜ | 20 Tem |
| F-004 | Google Play yeni hesap kısıtı doğrulaması (CTR-proxy fallback kararı) | M6 | Analist | ⬜ | 19 Tem |
| F-005 | Game feel günü: cihazda oynama + düzeltme listesi + scope freeze | M5 | Nazım + Analist | ✅ | 19 Tem |
| F-006 | Gameplay kaydı → 3–5 reklam kreatifi (3 sn kuralı) | M6 | Nazım (+A6) | ✅ (T-301/302) | 21 Tem |
| F-007 | İmza mutabakatı (kim ödüyor + gelir modeli taahhüdü) — yazılı | Kapı | Nazım + Analist | ⬜ | 21 Tem |
| F-008 | Pazarlanabilirlik testi canlıya alma ($100–200) | M6 | Analist | ⛔ **F-000 + F-007 ön koşul** — tasarımı beğenmediğin haliyle test için para harcama | 22 Tem (kayabilir) |

## Sırada (Faz 1 sonrası)

| ID | İş | Makine | Sorumlu | Durum |
|---|---|---|---|---|
| F-101 | İlk 48 saat test okuması + pano raporu | M6 | Analist (+A6) | ⬜ |
| F-102 | M7 karar paketi: eşik karşılaştırma raporu | M7 | Analist (+A7) | ⬜ |
| F-103 | GameBrief v1 şemasının kilitlenmesi (schemas/gamebrief.v1.json) | — | A1 + Nazım | ⬜ |
| F-104 | İlk tam radar taraması (10 aday kartı) | M1 | Analist (+A2) | ⬜ |
| F-105 | Antigravity vs Claude Code A/B kararı (`uretim.arac` varsayılanı) | — | Nazım | ⬜ |
| F-106 | Dış araç kurulumları: Claude Desktop projesi + ChatGPT projesi + ilk Manus görev denemesi (talimatlar: `agents/_dis-araclar/`) | — | Nazım + Analist | ⬜ |

## Kural

- Her satırın tek sorumlusu vardır; ⛔ satırları hangi kapıyı beklediğini yazar.
- İş bittiğinde ✅ işaretle + tarihi ekle; hafta kapanışında ✅ satırları silinir
  (öğrenilen varsa MEMORY.md'ye taşınır).
- Yeni iş eklerken makine ve sorumlu boş bırakılamaz.
