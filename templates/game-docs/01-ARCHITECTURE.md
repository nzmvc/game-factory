# <OyunAdı> — Şasi Mimarisi

**Son güncelleme:** <YYYY-AA-GG> · **Üreten:** A5 (şasi kurulumunda) · **Şasi modu:** <lite | full>

## 1. Katmanlar

```
Game.<Mekanik>  →  Chassis.UI  →  Chassis.Juice  →  Chassis.Core
(aktif mekanik)    (ekranlar)     (partikül/ses/     (EventBus, GameManager,
                                   haptik)            sözleşmeler, provider'lar)
```

- **Chassis.Core:** tip güvenli EventBus (struct event) · GameManager durum makinesi
  (Boot → MainMenu → Playing → LevelEnd) · IGameMechanic/LevelData/LevelResult
  sözleşmeleri · IAdsProvider, IAnalyticsProvider (+ implementasyonlar: <Dummy/Console | gerçek>).
- **Chassis.Juice:** JuicePreset (partikül+SFX+haptik) + JuicePlayer, object pool'lu.
- **Chassis.UI:** screen-stack; durum makinesi event'lerini dinler, doğrudan referans yok.
- **Game.<Mekanik>:** IGameMechanic implementasyonu; şasiye yalnız event'le konuşur.

## 2. Durum makinesi

| Durum | Giriş koşulu | Çıkış |
|---|---|---|
| Boot | uygulama açılışı; servis init + sahne cache | MainMenu |
| MainMenu | | StartGame(mechanic, levelData) → Playing |
| Playing | mekanik Initialize+StartLevel; Tick döngüsü | LevelCompleted/FailedEvent → LevelEnd |
| LevelEnd | interstitial kontrolü, sonuç ekranı | Next/Retry → MainMenu/Playing |

## 3. Event kataloğu (mimari event'ler)

`GameStateChangedEvent` · `LevelCompletedEvent` · `LevelFailedEvent` · `LevelProgressChangedEvent`
<+ oyuna özgü event'ler — analytics event'leri değil; onlar 02'de>

## 4. Bilinçli sapmalar

| Sapma | Gerekçe | Geri alınacağı koşul |
|---|---|---|
| <örn. şasi-lite: gerçek SDK yok> | <CPI testi için gerekmez> | <BÜYÜT kararı> |
