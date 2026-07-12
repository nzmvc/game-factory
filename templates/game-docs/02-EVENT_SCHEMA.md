# <OyunAdı> — Event Şeması

**Son güncelleme:** <YYYY-AA-GG> · **Standart:** GameFactory `schemas/event-schema.md` (çekirdek set oradan; buraya kopyalama)

Kural: snake_case; bu dosyada (çekirdek + ekler) kayıtlı olmayan event **gönderilemez** —
kodda tip güvenli sabitlerle zorlanır (`AnalyticsEvents.cs`).

## 1. Çekirdek set uygulaması

| Çekirdek event | Uygulandı mı | Not |
|---|---|---|
| session_start / session_end | ⬜ | |
| level_start / level_complete / level_fail | ⬜ | fail_reason değerleri: <örn. board_full, time_out> |
| ad_offer / ad_shown / ad_reward | ⬜ | placement'lar: §2 |
| iap_initiated / iap_purchase | ⬜ | <şasi-lite'ta stub> |
| rate_us_shown / rate_us_accepted | ⬜ | |

## 2. Placement etiketleri (bu oyun)

| Placement | Tip | Nerede |
|---|---|---|
| level_end | interstitial | Win → next arası, frequency cap config'ten |
| <double_reward> | rewarded | <Win ekranı 2x ödül> |
| <continue_fail> | rewarded | <Fail ekranı devam teklifi> |

## 3. Oyuna özgü ek event'ler

| Event | Parametreler | Ne zaman | Gerekçe |
|---|---|---|---|
| <örn. near_miss> | <level_id, slots_filled> | <bar 6/7 olunca> | <retry funnel analizi> |
