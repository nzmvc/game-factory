# game-docs/ — Oyun Doküman Seti Şablonu (00–15)

Yeni oyun reposunun `docs/` klasörüne kopyalanır. Numaralar ve makine eşlemesi sabittir
([ADR-0005](../../docs/decisions/ADR-0005-sablon-tabanli-oyun-dokumantasyonu.md)).

| # | Dosya | Makine | Üreten | Ne zaman dolar |
|---|---|---|---|---|
| 00 | 00-DEVFLOW.md | Genel | A9/insan | Açılışta; her aşama sonunda güncellenir |
| 01 | 01-ARCHITECTURE.md | M0 | A5 | Şasi kurulumunda |
| 02 | 02-EVENT_SCHEMA.md | M0 | A5 | Şasi kurulumunda (fabrika standardı + oyun ekleri) |
| 03 | 03-NEW_GAME_FROM_CHASSIS.md | M0 | A5 | Şasi ile gelir (oyundan bağımsız) |
| 04 | 04-GDD.md | M3 | A3 | Yeşil ışık sonrası |
| 05 | 05-GAME_MECHANICS.md | M3 | A3 | GDD ile birlikte |
| 06 | 06-LEVELGEN.md | M3 | A3+A5 | GDD sonrası |
| 07 | 07-SCORING_AND_ECONOMY.md | M3 | A3 | GDD ile birlikte |
| 08 | 08-SCREEN_FLOW.md | M4 | A4 | GDD onayı sonrası |
| 09 | 09-SCREEN_DESIGN.md | M4 | A4 | GDD onayı sonrası |
| 10 | 10-JUICE_GUIDE.md | M4 | A4 | GDD onayı sonrası |
| 11 | 11-MOBILE_TEST_GUIDE.md | M5 | A5 | İlk cihaz build'inde |
| 12 | 12-CPI_TEST_PLAN.md | M6 | A6 | Game feel onayı sonrası |
| 13 | 13-QA.md | M7 | A5 | Build pipeline kurulurken |
| 14 | 14-BACKLOG.md | Genel | insan+ajanlar | Açılışta; sürekli |
| 15 | 15-RELEASE_CHECKLIST.md | M8 | A8 | Yalnız BÜYÜT kararı sonrası |

Kurallar: `<...>` alanlarını doldur; erken aşamada bilinmeyene "TBD (dolacağı aşama)" yaz;
şablondan sapma "**Bilinçli sapma:**" notuyla kaydedilir; linkler göreli.
