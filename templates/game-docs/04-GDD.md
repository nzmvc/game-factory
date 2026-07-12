# <OyunAdı> — GDD

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A3 · **Kaynak brief:** `GameFactory/games/<oyun>/brief.md` (completion ≥ 90)
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

## 8. Monetizasyon yerleşimleri
- Rewarded: <+1 slot, shuffle, 2x ödül...> · Interstitial: <level sonu, cap RemoteConfig'ten>
- IAP: <v1'de stub / remove_ads...>

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
