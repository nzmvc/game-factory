# <OyunAdı> — Skor ve Ekonomi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A3 · Kural: tüm katsayılar GameConfig'te.
**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor *(ADR-0006)*

## 1. Skor

| Olay | Puan | Not |
|---|---|---|
| <eşleşme> | <base> | |
| <kombo zinciri> | <çarpan kuralı> | değişken ödülün matematiği |

## 2. Para birimi (coin)

- Kazanım: <win ödülü, kombo bonusu, rewarded 2x...>
- Harcama: <booster'lar...>
- Kural: kazanma/harcama tek noktadan (CurrencyService); her hareket analytics'e düşer.

## 3. Booster'lar

| Booster | Etki | Bedel | Rewarded alternatifi |
|---|---|---|---|
| <shuffle> | | <coin> | ✅ <placement: shuffle> |
| <+1 slot> | | | ✅ <placement: add_slot> |

## 4. Ekonomi dengesi

Hedef: oyuncu <X> seviyede bir booster'a yetecek coin biriktirir; rewarded her zaman
"bedava" alternatiftir (v1 monetizasyonu rewarded-ağırlıklı).
İlk değerler tahmindir → soft launch verisiyle RemoteConfig'ten kalibre edilir.

## 5. IAP (v1 kapsamına göre)

<remove_ads (non-consumable) · coin_pack_s/m/l (consumable) — şasi-lite'ta stub>

## 6. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
