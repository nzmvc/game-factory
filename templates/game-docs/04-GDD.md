# <OyunAdı> — GDD

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A3 · **Kaynak brief:** `GameFactory/games/<oyun>/brief.md` (completion ≥ 90)
**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor *(kod yazılmadan önce boş bırak; ADR-0006)*
**Tavan: 2–3 sayfa.** Uzuyorsa kapsam alarmı — bu bir hyper-casual GDD'sidir.

## 1. Tek cümle
<Mekanik + twist: "3D fizik kutusundan aynı 3 objeyi tap'le topla; her pop yığını sarsar.">

## 2. Core loop (oturum: 2–5 dk)
<Bak → ... → ödül → tekrar. Değişken ödülün nerede olduğunu işaretle.>

## 3. Kontrol
<tap | drag | swipe | hold> · portre · sıfır metin · tek el.

## 4. Win / Fail / Near-miss
- **Win:** <koşul>
- **Fail:** <koşul>
- **Near-miss tasarımı:** <son hamlede kaybetme hissi mekaniğin neresinde?>

## 5. Zorluk eğrisi kuralları
Parametreler: <N obje, T tür, ...> — değerler GameConfig/RemoteConfig'te, burada eğri
**kuralı** yazılır: <örn. her 4–5 seviyede bir nefes seviyesi; süre baskısı yok (zen)>.

## 6. Seviye üretim algoritması (özet — detay: 06-LEVELGEN)
<seed(level_id) → ... → solver botu çözemezse reddet. Elle seviye tasarımı = 0.>

## 7. Zeigarnik / dönüş tasarımı
<level sayacı, streak, ilerleme göstergesi — v1 kapsamı>

## 8. Hybrid-Casual Monetizasyon ve Ekonomi Tasarımı
- **IAP Katmanı:**
  - Non-consumable: Remove Ads (zorunlu)
  - Consumable/Subscription: Koleksiyon/Skins paketleri, Enerji Yenileme, "Skip Level" (Seviye Atlama) paketleri.
- **Rewarded Reklam Yerleşimleri:**
  - Örn: +1 slot (fail kurtarma), shuffle/booster, win'de 2x ödül, ekstra enerji.
- **Interstitial Reklamlar:**
  - Seviye geçişleri, RemoteConfig ile sıklık limitli (frequency capping).
- **Değişken Ödül & Ekonomi (Variable Reward):**
  - "Gacha" tarzı sandık açılışları veya nadir obje toplama sistemleri.

## 9. Psikoloji spesifikasyonu denetimi (zorunlu)
| İlke | Bu oyunda nerede? |
|---|---|
| 3 saniye kuralı | |
| Değişken ödül | |
| Sıfır bilişsel yük | |
| Juice üründür | |
| Near-miss | |
| Zeigarnik | |
| Oturum ritmi 2–5 dk | |

## 10. Kapsam sınırı
v1'de OLMAYANLAR: <liste — "v2 işi" etiketiyle>. Geliştirme tavanı: ≤ 2 hafta efor.

## 11. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.
Rozeti yalnız kodu güncelleyen taraf (A5) 🟢'ye çeker.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
