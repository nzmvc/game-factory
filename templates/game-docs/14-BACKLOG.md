# <OyunAdı> — İş Listesi (Backlog)

**Son güncelleme:** <YYYY-AA-GG> · Fabrika seviyesi işler burada değil, GameFactory `ACTIONS.md`'de.
Durumlar: ⬜ TODO · ⏳ IN_PROGRESS · ✅ DONE · ⛔ BLOKE

## Görev ID şeması

`T-<aşama><sıra>` — 1xx: entegrasyon/QA · 2xx: görsel/juice · 3xx: pazarlama · 4xx: veri/karar
5xx: tasarım senkron görevi (bkz. §E, ADR-0006)

## A. Entegrasyon ve lokal doğrulama

| ID | Görev | Makine | Öncelik | Durum |
|---|---|---|---|---|
| T-101 | <Editor'de seviye akışı testi> | M5 | Yüksek | ⬜ |
| T-102 | <QA 10 dk çeklisti> | M7 | Yüksek | ⬜ |
| T-103 | <event loglarının doğrulanması> | M7 | Yüksek | ⬜ |
| T-104 | <ilk cihaz build + performans> | M0 | Orta | ⬜ |

## B. Görsel kaplama ve juice

| ID | Görev | Makine | Öncelik | Durum |
|---|---|---|---|---|
| T-201 | <asset tedariği> | M4 | Yüksek | ⬜ |
| T-202 | <SFX seçimi + preset ataması> | M5 | Yüksek | ⬜ |
| T-203 | <partikül prefab'ları> | M4 | Orta | ⬜ |
| T-204 | <game feel ince ayar (cihazda)> | M5 | Yüksek | ⬜ |

## C. Pazarlanabilirlik hazırlığı

| ID | Görev | Makine | Öncelik | Durum |
|---|---|---|---|---|
| T-301 | <3–5 gameplay videosu (9:16, 3 sn kuralı)> | M6 | Yüksek | ⬜ |
| T-302 | <kreatif brief + reklam metinleri> | M6 | Orta | ⬜ |
| T-303 | <test kanalları + bütçe hazırlığı> | M6 | Yüksek | ⬜ |

## D. Veri ve karar

| ID | Görev | Makine | Öncelik | Durum |
|---|---|---|---|---|
| T-401 | <kampanya metriklerini çek> | M7 | Yüksek | ⬜ |
| T-402 | <retention/playtime analizi> | M7 | Yüksek | ⬜ |
| T-403 | <karar paketi (eşik karşılaştırmalı)> | M7 | Yüksek | ⬜ |

## E. Tasarım Senkron Görevleri

Kaynak: bir tasarım dokümanının (04–10) "Değişiklik Geçmişi" tablosunda
"Kod Etkisi: Var" işaretlenen her satır burada bir göreve dönüşür (ADR-0006).
Görev kapanınca hem burası hem kaynak dokümanın rozeti/tablo durumu 🟢 yapılır.

| ID | Görev | Kaynak doküman (tarih) | Öncelik | Durum |
|---|---|---|---|---|
| T-501 | <örn. şok dalgası gücünü GDD'deki yeni değere göre kalibre et> | <04-GDD.md, YYYY-AA-GG> | Yüksek | ⬜ |
