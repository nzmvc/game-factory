# <OyunAdı> — Ekran Akışı

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A4 · Kural: UI screen-stack; ekranlar durum makinesi event'lerini dinler.
**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor *(ADR-0006)*

## 1. Akış

```
Boot → MainMenu → Gameplay(HUD) → Win → (interstitial kuralı) → sonraki seviye
                          │          └→ 2x ödül (rewarded) → Next
                          └→ Fail → rewarded devam | Retry → Gameplay
MainMenu ↔ Settings
```

## 2. Ekran kataloğu

| Ekran | İçerik | Butonlar ve davranışları | Tetiklediği event'ler |
|---|---|---|---|
| MainMenu | <Play, streak, ayar ikonu> | | |
| HUD | <level no, bar/progress, 2 booster> | | |
| Win | <coin count-up, 2x rewarded, Next> | | ad_offer(double_reward) |
| Fail | <rewarded devam, Retry> | | ad_offer(continue_fail) |
| Settings | <ses/haptik toggle, restore, gizlilik linki> | | |

## 3. Reklam akış kuralları

- Interstitial: <Win → next arası>; frequency cap (sn + level aralığı) RemoteConfig'ten.
- Rewarded: placement registry üzerinden; başarısız yüklemede buton gizlenir/disabled.
- remove_ads: interstitial kapanır, rewarded açık kalır.

## 4. Rate-us kuralı

<X başarılı seviye sonrası, oturum başına en fazla 1 kez, native in-app review.>

## 5. Değişiklik Geçmişi
*Yalnız kodu zaten yazılmış bir bölüm değişince satır ekle (ADR-0006). Kod Etkisi
"Var" ise `14-BACKLOG.md` → Tasarım Senkron Görevleri'ne T-xxx aç, rozeti 🔴/🟡 yap.*

| Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
|---|---|---|---|---|---|
| | | | | | |
