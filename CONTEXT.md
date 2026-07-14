# CONTEXT — Anlık Durum

> Her çalışma oturumu **bu dosyayı okuyarak başlar** ve anlamlı iş sonrası
> **bu dosyayı güncelleyerek biter** (bkz. CLAUDE.md kapanış ritüeli).
> Burada yalnız güncel durum yaşar; tarihçe DECISIONS.md ve MEMORY.md'dedir.

**Son güncelleme:** 2026-07-14 · **Güncelleyen:** Antigravity (Web-First Prototipleme & Hibrit-Casual Monetizasyon entegrasyonu)

---

## Faz ve aktif oyun

- **Faz:** 1 — "İlk Oyun Çıkıyor" (13–22 Temmuz 2026, 10 gün) · plan: [ROADMAP.md](ROADMAP.md)
- **Aktif oyun:** **Toy Pile** (tap triple-match + shockwave cascade, şasi-lite)
  - Kayıt: [games/toy-pile/](games/toy-pile/) · Unity repo: `game-toy-pile`
  - Hat durumu: M0 ✅ · M1 ✅ · M2 ✅ (53/70 bilinçli override) · M3 ✅ · **M4 🟡 (asset+SFX+game feel tamam — yalnız T-203 partikül devam)** · M5 ✅ (T-204/T-205 game feel ince ayarı tamamlandı) · **M6 🟡 (kreatif hazırlık T-301/302 tamam; T-303 store kanalları + bütçe onayı bekliyor)** · M7 🔴 · M8 🔴 — detay: `game-toy-pile/docs/00-DEVFLOW.md` (güncellenmesi gerekiyor)

## Aktif konu: Toy Pile tasarım revizyonu

Nazım cihazda test etti: "basit ama kullanışsız" bulundu (juice/game-feel bittikten
SONRA verilen bir değerlendirme). İki dalgada düzeltildi:

**Dalga 1 — kök neden (kod tarafı bitti):**
1. ✅ Bar disiplini yoktu — `DifficultyService` typeCount tabanı 2→4 (T≤3 iken
   near-miss/fail matematiksel olarak imkânsızdı).
2. ✅ Gerçek 3D modeller düz renge boyanıyordu — artık yalnız fallback primitifler tintleniyor.

**Dalga 2 — A3 (GDD/Mekanik) + A4 (Görsel) ajan incelemesi** (`agents/A3-gdd`,
`agents/A4-gorsel` personalarıyla, subagent olarak çalıştırıldı) 10 ek bulgu çıkardı,
8'i kodda uygulandı:
3. ✅ Coin ekonomisi işlevsizdi (kazanılıp hiç saklanmıyordu) → `CurrencyService.cs`
   ile kalıcı; Shuffle artık coin ile de açılabiliyor.
4. ✅ Kombo yalnız ses pitch'iyle tepki veriyordu → partikül ölçeği + haptik escalasyonu eklendi.
5. ✅ Fail anı tamamen sessizdi → haptik atandı (ses/partikül insan işi, T-506).
6. ✅ HUD skoru statikti (yalnız Win ekranında count-up) → canlı skor + punch-tween.
7. ✅ Buton metin kontrastı tanımsızdı (~2:1, WCAG 4.5:1 ister) → `UITheme.buttonTextColor`.
8. ✅ Streak'te ara kilometre taşı yoktu → 5'in katlarında milestone shake.
9. 🟡 Tile bar ölçüsü dokümanda kendi kendiyle çelişiyordu (700dp/~360dp ekran) →
   doküman düzeltildi, gerçek görünüm Play Mode'da doğrulanmalı.
10. Nefes seviyesi + level 1 süresi hedefleri → yalnız doküman düzeltmesi (kod zaten doğruydu).

**İnsan işi tamamlandı (`game-toy-pile/docs/14-BACKLOG.md` §E):**
T-503 (UITheme wiring + Fredoka font import) ✅ · T-504 (5 model daha ata, typeId 6-10) ✅ ·
T-505 (rewarded rozeti) ✅ · T-506 (fail sesi + partikül) ✅ — 2026-07-14 dosya incelemesiyle
doğrulandı (Canvas/UIThemeApplier wiring, tilePrefabs 10/10, AdBadge x3, FailPreset dolu).

**Yeni açık madde:** TileBar 7 slotun Play Mode'da göründüğü/kamera FOV'unun doğru olduğu
henüz doğrulanmadı (`09-SCREEN_DESIGN.md` §5 İNSAN GÖREVİ, backlog karşılığı yoktu → T-507
açılması gerekiyor).

Süreç desteği: [ADR-0006](docs/decisions/ADR-0006-tasarim-degisim-yonetimi.md).
M6 (pazarlanabilirlik), T-507 kapanıp Nazım yeni build'i cihazda onaylayana kadar **askıda**
(bkz. HUMAN_ROLES.md §2.3 — game feel devredilemez).

## Sıradaki insan kapısı

⛔ **G10 (22 Tem): pazarlanabilirlik testi bütçe onayı ($100–200, tek imza: Nazım)**
Ön koşul: G9'a (21 Tem) kadar asgari yazılı imza mutabakatı (kim ödüyor + gelir modeli taahhüdü) — yoksa **tarih kayar, para kaymaz**.

## Bu haftanın işleri

Aktif kuyruk: [ACTIONS.md](ACTIONS.md) · Toy Pile görev detayı: `game-toy-pile/docs/14-BACKLOG.md`

- Nazım: M4/M5 — asset kaplama + juice + her akşam cihaz build; G7 (19 Tem) game feel günü.
- Analist: rakip kreatif analizi (G8 öncesi) → test altyapısı + Play Store kısıt doğrulaması → radar taraması.

## Repo durumu

- 2026-07-12: GameFactory framework yapısı kuruldu (bu düzenleme). Eski dosyalar
  taşındı; gerekçeler [archive/README.md](archive/README.md) ve [DECISIONS.md](DECISIONS.md)'de.
- 2026-07-12: `game-toy-pile` reposu framework standardına hizalandı — doküman
  numaralandırması, `file:///` link temizliği, `CLAUDE.md`/`AGENTS.md`'ye "Fabrika
  Bağlantısı" bölümü, `_analiz/`+`_prompt/` kopyalarının temizliği,
  `AOS_ORCHESTRATOR_SPEC.md`'nin arşive kurtarılması. Detay: [DECISIONS.md](DECISIONS.md).
- `orchestrator/` kilitli (Faz 3 tetiği bekliyor).
- 2026-07-14: Dış araç talimatları açıldı — [agents/_dis-araclar/](agents/_dis-araclar/)
  (Manus · ChatGPT · Claude Desktop); eski `A1-producer/instruction.md` oraya taşındı.
  Araçlara kurulum insan işi: ACTIONS F-106.

---

## Güncelleme kuralları

1. Bölüm başlıklarını koru; yalnız içerikleri güncelle.
2. Tarih + güncelleyen alanını her seferinde değiştir.
3. Biten faz/oyun bilgisini silme→taşı: dersler MEMORY.md'ye, kararlar DECISIONS.md'ye.
4. Bu dosya 1 ekran boyunu aşarsa detayı ilgili dosyaya taşı, burada link bırak.
