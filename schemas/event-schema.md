# Event Şeması Standardı — Tüm Oyunlar

**Son güncelleme:** 2026-07-12 · Kaynak uygulama: `game-toy-pile/docs/02-EVENT_SCHEMA.md`

Analytics event standardının fabrika seviyesi tanımı. Her oyun bu çekirdek seti
uygular; oyuna özgü ekler kendi `docs/02-EVENT_SCHEMA.md` dosyasında tanımlanır.

## Kurallar

1. Event ve parametre isimleri **snake_case**.
2. Şemada (çekirdek + oyun dosyası) kayıtlı olmayan event **gönderilemez** —
   kodda tip güvenli sabitlerle zorlanır (`AnalyticsEvents.cs`), string literal yasak.
3. Yeni çekirdek event = bu dosyada değişiklik = ADR gerekir.

## Çekirdek event seti

| Event | Parametreler | Ne zaman |
|---|---|---|
| `session_start` | — | Uygulama açılıp oturum başlayınca |
| `session_end` | `duration` (float, sn) | Kapanış / arka plana geçiş |
| `level_start` | `level_id`, `mechanic_id`, `attempt_no` (int) | Seviye başlarken |
| `level_complete` | `level_id`, `duration` (float), `moves` (int) | Kazanınca |
| `level_fail` | `level_id`, `duration` (float), `fail_reason` (string) | Kaybedince |
| `ad_offer` | `placement`, `ad_type` (`interstitial`\|`rewarded`) | Reklam gösterilebilir olunca |
| `ad_shown` | `placement`, `ad_type` | Reklam başlayınca |
| `ad_reward` | `placement` | Rewarded tamamlanıp ödül verilince |
| `iap_initiated` | `sku` | Satın alma başlatılınca |
| `iap_purchase` | `sku`, `price_usd` (float) | Satın alma tamamlanınca |
| `rate_us_shown` | — | Native review dialogu gösterilince |
| `rate_us_accepted` | — | Kullanıcı olumlu etkileşince |

## Standart placement etiketleri

`level_end` · `double_reward` · `add_slot` · `shuffle` · `continue_fail`

Yeni placement, oyunun event dosyasında tanımlanır ve A7 pano sorgularıyla uyumu kontrol edilir.
