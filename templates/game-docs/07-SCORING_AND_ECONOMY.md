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

Hedef: oyuncu <X> seviyede bir booster'a yetecek coin biriktirir; rewarded her zaman "bedava" alternatiftir.
- **LTV / ARPU Hedefleri:**
  - LTV Hedefi: `> $0.50` (veya > CPI)
  - ARPU Hedefi: `> $0.45`
  - IAP Gelir Payı Oranı: Toplam gelirin ≥ %20–30'u
- **Enerji / Can Sistemi:**
  - Maksimum enerji: <örn. 5 can>. Seviye fail edildiğinde 1 can eksilir. Yenilenme hızı: <örn. 30 dk/can>.
  - Satın alma: Can yenileme <coin bedeli> veya rewarded reklam.
İlk değerler tahmindir → soft launch verisiyle RemoteConfig'ten kalibre edilir.

## 5. IAP (Hybrid-Casual Yapısı)

- **Skins / Koleksiyon Paketleri:** <özelleştirme ögeleri ve coin içeren consumable paketler, örn: $1.99 - Starter Pack>
- **Can / Enerji Yenileme Paketleri:** <örn: 2 saat sınırsız can, $0.99>
- **"Skip Level" (Seviye Atlama) Paketleri:** <zor seviyelerde kullanıcıyı tutmak için seviye atlama ve booster paketi, örn: $0.49 veya 5x skip $1.99>
- **Remove Ads:** <reklam kaldırma ve asgari booster, örn: $2.99>

## 6. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
