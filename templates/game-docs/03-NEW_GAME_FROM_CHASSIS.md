# Şasiden Yeni Mekanik Türetme Rehberi

**Son güncelleme:** <YYYY-AA-GG> · Bu doküman şasiyle birlikte gelir; oyundan bağımsızdır.

Amaç: `Assets/_Chassis`'e dokunmadan yeni oynanış modülü eklemek.

## Adımlar

1. **Klasör:** `Assets/_Game/<YeniMekanik>/` → `Scripts/` + `Game.<YeniMekanik>.asmdef`
   (referanslar: Chassis.Core zorunlu; Chassis.Juice/UI opsiyonel).
2. **Sözleşme:** `IGameMechanic` implement et — Initialize(LevelData) temizlik + kurulum,
   StartLevel() oynanışı açar, Tick(dt) input/döngü, EndLevel(LevelResult) temizlik.
3. **Event akışı:** UI'a/GameManager'a doğrudan referans YOK. Yayınla:
   `LevelCompletedEvent` / `LevelFailedEvent` / `LevelProgressChangedEvent`.
   Dinle (destekliyorsan): `RequestShuffleEvent`, `RequestExpandSlotsEvent`.
4. **Level data:** `Assets/_Content` altında LevelData ScriptableObject'leri;
   oyuna özgü konfigürasyon `jsonData` alanında (JSON şemasını mekanik tanımlar).
5. **Bağlama:** bootstrap sahnesinde mekanik controller'ı GameManager'ın mekanik
   soketine ata.
6. **Doğrulama:** dummy level ile uçtan uca akış — aç → oyna → win → interstitial
   (log) → next. EventSchema event'lerinin konsola düştüğünü kontrol et.

## Yasaklar

- `Assets/_Chassis` değişikliği (şasi ihtiyacı çıktıysa fabrikada ADR aç).
- Şemasız analytics event'i; string literal event adı.
- Mekanik içinde reklam/IAP SDK çağrısı — yalnız provider interface'leri.
