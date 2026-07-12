# <OyunAdı> — Juice Rehberi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A4 · İlke: **juice üründür** — "satisfying" his süs değil, oyunun kendisi.

Her etkileşim üçlüsü: **partikül + ses + haptik** (JuicePreset olarak tek varlıkta).

## 1. Juice checklist

| An | Görsel | Ses | Haptik | Preset | Durum |
|---|---|---|---|---|---|
| <tap> | <squash-punch> | <tık> | <hafif> | ClickPreset | ⬜ |
| <eşleşme/pop> | <partikül> | <pop> | <orta> | MatchPreset | ⬜ |
| <kombo zinciri> | <trail> | **pitch kademeli artar (±%5 varyasyon)** | | ComboPreset | ⬜ |
| <twist anı> | <mikro kamera shake> | | | | ⬜ |
| <near-miss> | <bar titremesi> | <gerilim> | | NearMissPreset | ⬜ |
| <win> | <konfeti> | <fanfar> | <güçlü> | WinPreset | ⬜ |

## 2. Teknik kurallar

- Object pool zorunlu (Instantiate/Destroy yasak); SFX havuzu + pitch varyasyonu.
- Haptik ayarlardan kapatılabilir; müzik ducking (SFX önceliği).
- Parametre değerleri config'te; **son değerler cihazda elle ayarlanır** (game feel günü).

## 3. Game feel günü protokolü

1. Temiz kurulum, gerçek cihaz, ses açık.
2. Her checklist satırı tek tek: "hissettiriyor mu?" — not al.
3. Düzeltme listesi çıkar → uygula → tekrar test → **scope freeze**.
Son söz: Nazım (devredilemez).
