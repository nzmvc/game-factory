# CONTEXT — Anlık Durum

> Her çalışma oturumu **bu dosyayı okuyarak başlar** ve anlamlı iş sonrası
> **bu dosyayı güncelleyerek biter** (bkz. CLAUDE.md kapanış ritüeli).
> Burada yalnız güncel durum yaşar; tarihçe DECISIONS.md ve MEMORY.md'dedir.

**Son güncelleme:** 2026-07-13 · **Güncelleyen:** Claude (tasarım değişim yönetimi + Toy Pile yeniden tasarım başlangıcı)

---

## Faz ve aktif oyun

- **Faz:** 1 — "İlk Oyun Çıkıyor" (13–22 Temmuz 2026, 10 gün) · plan: [ROADMAP.md](ROADMAP.md)
- **Aktif oyun:** **Toy Pile** (tap triple-match + shockwave cascade, şasi-lite)
  - Kayıt: [games/toy-pile/](games/toy-pile/) · Unity repo: `game-toy-pile`
  - Hat durumu: M0 ✅ · M1 ✅ · M2 ✅ (53/70 bilinçli override) · M3 ✅ · **M4 🟡 (asset+SFX+game feel tamam — yalnız T-203 partikül devam)** · M5 ✅ (T-204/T-205 game feel ince ayarı tamamlandı) · **M6 🟡 (kreatif hazırlık T-301/302 tamam; T-303 store kanalları + bütçe onayı bekliyor)** · M7 🔴 · M8 🔴 — detay: `game-toy-pile/docs/00-DEVFLOW.md` (güncellenmesi gerekiyor)

## Aktif konu: Toy Pile tasarım revizyonu

Nazım cihazda test etti: "basit ama kullanışsız" bulundu (juice/game-feel bittikten
SONRA verilen bir değerlendirme — yüzeysel değil). Kök neden analizi 3 somut sorun
çıkardı, ikisi kodda düzeltildi:

1. **Bar disiplini yoktu** (✅ düzeltildi) — `DifficultyService`'te typeCount tabanı
   2→4: T≤3 iken bar (7 slot) matematiksel olarak asla dolamıyordu, near-miss/fail
   ilk ~15 seviyede imkânsızdı. Beceri/risk hissi yoktu.
2. **Gerçek 3D modeller düz renge boyanıyordu** (✅ düzeltildi) — dokulu Low-Poly
   oyuncaklar HSV tint ile "plastik" görünüyordu; artık yalnız fallback primitifler
   tintleniyor.
3. **Görsel kimlik hâlâ placeholder** (🟡 kod hazır, wiring bekliyor) — `UITheme.cs` +
   `UIThemeApplier.cs` yazıldı (sıcak krem/mercan/nane palet); Unity'de asset
   oluşturma + font import (Fredoka) insan işi (T-503).
4. **5/10 tip için model eksik** (🔴 insan işi bekliyor) — T-504.

Süreç desteği: [ADR-0006](docs/decisions/ADR-0006-tasarim-degisim-yonetimi.md)
kuruldu; `game-toy-pile/docs/04-GDD.md`, `05-GAME_MECHANICS.md`, `09-SCREEN_DESIGN.md`
gerçek Değişiklik Geçmişi kayıtlarıyla güncel. Detaylı görevler:
`game-toy-pile/docs/14-BACKLOG.md` §E. M6 (pazarlanabilirlik), T-503/504 kapanıp
Nazım yeni build'i cihazda onaylayana kadar **askıda**.

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

---

## Güncelleme kuralları

1. Bölüm başlıklarını koru; yalnız içerikleri güncelle.
2. Tarih + güncelleyen alanını her seferinde değiştir.
3. Biten faz/oyun bilgisini silme→taşı: dersler MEMORY.md'ye, kararlar DECISIONS.md'ye.
4. Bu dosya 1 ekran boyunu aşarsa detayı ilgili dosyaya taşı, burada link bırak.
