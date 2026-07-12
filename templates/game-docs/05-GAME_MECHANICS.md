# <OyunAdı> — Mekanik Detay Referansı

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A3 (A5 uygular) · GDD: [04-GDD.md](04-GDD.md)

Her etkileşimin teknik parametreleri. Kural: burada yazılan her sayı GameConfig'ten
okunur; kodda sabit yaşamaz.

## 1. Etkileşim tablosu

| Etkileşim | Girdi | Davranış | Parametreler (GameConfig) | Juice preset |
|---|---|---|---|---|
| <tap seçim> | <raycast> | <obje bara tween ile uçar> | <uçuş süresi, eğri> | <ClickPreset> |
| <eşleşme> | <bar'da 3 aynı tür> | <pop + skor + event> | <pop gecikmesi> | <MatchPreset> |
| <twist: ...> | | | | |

## 2. Durum ve kurallar

- <bar kapasitesi / grid boyutu / ...>: <değer aralığı + hangi config alanı>
- Fail koşulu değerlendirme sırası: <...>
- Edge case'ler: <aynı anda çift tap, boş kutu, ...>

## 3. Fizik / hareket parametreleri

| Parametre | Varsayılan | Aralık | Not |
|---|---|---|---|
| <shockwave force> | | | game feel'de cihazda ayarlanır |

## 4. Event tetikleme haritası

| Oyun anı | Mimari event | Analytics event |
|---|---|---|
| <seviye başlar> | — | level_start |
| <near-miss anı> | <NearMissEvent> | <near_miss> |
