# <OyunAdı> — Mobil Cihaz Test Rehberi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A5 · Kural: her akşam cihaz build'i; editor-only kod bırakılmaz.

## 1. Build alma

- Android: <IL2CPP, ARM64, portre kilidi, sürüm şeması vX.Y.Z+build> — `adb install` adımları: <...>
- iOS (varsa): <TestFlight / geliştirici profili adımları>

## 2. Test cihazları

| Cihaz | OS | Sınıf | Not |
|---|---|---|---|
| <model> | <sürüm> | <alt/orta/üst> | referans cihaz |

## 3. Kontrol listesi (her build)

- [ ] Temiz kurulumdan açılış < <3> sn; crash yok
- [ ] FPS: oyun alanı dolu sahnede <60/30> hedefi; frame-drop anları not edilir
- [ ] Input gecikmesi hissedilmiyor (tap→tepki)
- [ ] <fizik/mekanik yoğun an> performansı
- [ ] Safe-area: çentikli cihazda UI taşması yok
- [ ] Event logları konsola doğru parametrelerle düşüyor
- [ ] Rewarded/interstitial stub akışları çalışıyor
- [ ] Arka plana at / geri gel: durum korunuyor, session_end/start atılıyor

## 4. Sorun kaydı

| Tarih | Build | Sorun | Ciddiyet | Durum |
|---|---|---|---|---|
