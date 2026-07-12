# <OyunAdı> — Yayın Öncesi Kontrol Listesi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A8 · ⛔ Ön koşul: M7 **BÜYÜT** kararı (DECISIONS.md kaydı) + tam ortaklık anlaşması

## 1. Teknik

- [ ] Gerçek şasi yatırımı tamam: Firebase, mediation (<LevelPlay|MAX>), IAP, consent
- [ ] Consent akışı (ATT/GDPR-UMP) boot'ta doğru sırada; consent'siz reklam init yok
- [ ] Reklam test modu KAPALI; gerçek ad unit id'leri
- [ ] Analytics: tüm event'ler Firebase DebugView'da doğrulandı
- [ ] IAP sandbox testi + restore purchases (iOS)
- [ ] remove_ads interstitial'ları kapatıyor, rewarded açık
- [ ] AAB imzalı (IL2CPP, ARM64); sürüm şeması doğru
- [ ] Cihazda temiz kurulumdan 10 dk sorunsuz oynanış (final build ile)
- [ ] Crash raporlama aktif

## 2. Store (TR + EN minimum)

- [ ] Başlık + kısa/uzun açıklama (keyword setiyle uyumlu)
- [ ] Ekran görüntüleri (<6–8>) + varsa tanıtım videosu
- [ ] İkon A/B adayları
- [ ] Yaş derecelendirme anketi; veri güvenliği formu
- [ ] Gizlilik politikası URL canlı

## 3. Operasyon

- [ ] RemoteConfig başlangıç değerleri yüklü (interstitial cap, zorluk eğrisi)
- [ ] Soft launch ülke listesi: <...>
- [ ] Pano hazır: D1/D7, playtime, ARPDAU takibi (A7)
- [ ] Rollback planı: <kritik hata durumunda ne yapılır>

## 4. Kapı

- [ ] ✔ **Yayın onayı — Nazım** (tarih: <...>, DECISIONS.md kaydı: <link>)
