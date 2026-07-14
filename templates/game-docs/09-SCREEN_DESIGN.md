# <OyunAdı> — Ekran Tasarımı (Portre Layout)

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A4 · İlke: okunabilirlik > gerçekçilik; aşırı tasarım yapma — bu hyper-casual.
**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor *(ADR-0006)*

## 1. Genel kurallar

- Yalnız portre; safe-area uyumlu (çentik/home bar); tek el erişim bölgesi altta.
- Touch target ≥ <44pt/48dp>; kritik butonlar başparmak yayında.
- Sıfır metin hedefi: ikon + animasyon anlatır; zorunlu metin <2 kelime.
- Stil: <pastel arka plan + yüksek kontrast objeler / ...> — paused karede bile mekanik okunmalı.

## 2. Layout şablonları

| Ekran | Üst bölge | Orta | Alt bölge |
|---|---|---|---|
| HUD | <level no, ayar> | <oyun alanı> | <bar + booster'lar> |
| Win | | <ödül animasyonu> | <Next + 2x> |

## 3. Renk / font / ikon

- Palet: <ana, vurgu, uyarı — hex> · Font: <tek font ailesi, 2 ağırlık>
- İkon seti: <kaynak> — store görselleri M8 işidir, şimdi üretme.

## 4. Google Stitch Arayüz Tasarımı & Prompt Şablonu

Dokümanlar onaylandıktan sonra, arayüz prototipi Google Stitch kullanılarak üretilir. Stitch promptu aşağıdaki şablona göre hazırlanmalı ve çıktılar (HTML/CSS kodu veya JPG/PNG mockupları) `games/<oyun-adi>/gorsel/` klasörüne kopyalanmalıdır.

- **Stitch Prototip Tipi:** [HTML/CSS Web UI (Önerilen) | JPG/PNG Mockup Referansı]
- **Google Stitch Promptu:**
  ```text
  [Stitch için tasarlanmış detaylı UI/UX promptunu buraya ekle. Portre mod, buton renk paletleri, safe area mesafeleri, popup geçiş animasyonları ve responsive davranışı belirtilmelidir.]
  ```
- **Referans Taslak Dosyaları:**
  - `games/<oyun-adi>/gorsel/index.html` (Web prototipiyle doğrudan uyumlu)
  - `games/<oyun-adi>/gorsel/mockup.png` (Görsel referans)

## 5. Asset listesi (M4 çıktısı)

| # | Asset | Tip | Kaynak | Durum |
|---|---|---|---|---|
| 1 | <10–12 low-poly obje> | 3D | <Asset Store / Meshy> | ⬜ |
| 2 | <bar UI> | 2D | | ⬜ |
| 3 | <pop + konfeti partikülleri> | VFX | | ⬜ |
| 4 | <6–8 SFX> | Ses | | ⬜ |

Tavan ~10–15 kalem; üstü kapsam alarmı.

## 6. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
