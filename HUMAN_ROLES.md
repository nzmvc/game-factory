# HUMAN_ROLES — İnsan Görevleri ve Onay Mekanizmaları

**Son güncelleme:** 2026-07-12 · RACI tablosu: [ops/roller.md](ops/roller.md)

Fabrika otonom görünse de para, yayın ve his kararları insandadır.
Bu dosya insan/AI iş bölümünün ve onay mekanizmalarının tek kaynağıdır.

---

## 1. Ekip

| Kişi | Rol | Sahiplik |
|---|---|---|
| **Nazım** | Producer | M0/M5 (şasi + kod), game feel son sözü, **tüm ✔ kapıları (tek imza)** |
| **Analist** | Veri & Pazar | M1 radar, M2 skorlama, M6 test/pano, M7 raporu, kill-log |

İlkeler (tartışmaya kapalı):
- **Her kapının tek karar sahibi (A) vardır.** Danışılır, oylanmaz — komite hyper-casual hızını öldürür.
- **İnşa eden infaz etmez.** M7 raporu ve eşik karşılaştırması analistten çıkar; nihai karar tek imzada.
- **Para tek imzada.** Analistin kampanya kurma yetkisi var, harcamayı başlatma yetkisi yok.
- **Game feel ikiye katlanır, son söz teke iner.** İkisi de cihazda oynar; son söz Nazım'da.

## 2. Devredilemez insan görevleri

1. **Yeşil ışık onayları** (M2) — hangi fikre kaynak akacağı.
2. **Para harcama kararları** (M6 bütçe, UA ölçekleme).
3. **Game feel** — juice'un tuttuğu ancak telefonda parmakla hissedilir; ajan ölçemez.
4. **Nihai infaz kararı** (M7) — rapor ajandan/analistten, imza Nazım'dan.
5. **Yayın onayı** (M8) ve store hesap işlemleri.
6. Referans oyunları **bizzat indirip oynamak** (his rapordan okunmaz).
7. Eşik ve değişmez kural değişiklikleri (ops/esikler.md, GAME_FACTORY.md §4).

## 3. AI görevleri (ajan katmanı)

Tarama, skorlama hazırlığı, GDD/stil/kreatif/ASO üretimi, kod (oyun reposunda),
eşik karşılaştırma raporları, doküman bakımı. Sınırlar: [AGENTS.md](AGENTS.md) §3.

## 4. Onay mekanizması

Her ✔ kapısında akış aynıdır:

1. Sorumlu ajan/analist **karar paketi** hazırlar: veri + eşik karşılaştırması + öneri + riskler.
2. Karar sahibi (Nazım) paketi inceler; gerekirse soru turu (A1 üzerinden).
3. Karar verilir: **onay / red / şartlı onay**. Sözlü onay yeterli değildir —
   [DECISIONS.md](DECISIONS.md)'ye tarih + karar + gerekçe satırı düşülür.
4. Onaysız adım "tamamlandı" sayılmaz; para harcayan adım onaysız **başlatılamaz**.

## 5. Review süreçleri

| Ne | Kim inceler | Sıklık |
|---|---|---|
| Radar çıktısı + hafta planı | Nazım + Analist senkron | Haftalık (Pzt, 20 dk) |
| Metrik panosu | Analist sunar, Nazım karar | Haftalık (Cmt) |
| Game feel | İkisi de cihazda, son söz Nazım | Her build sonrası |
| Doküman/şema tutarlılığı | A9 raporlar, Nazım onaylar | Aşama kapanışlarında |
| Ajan çıktı kalitesi | Sonraki aşamanın sahibi (şema kontrolü) | Her teslimde |

## 6. Açık maddeler

- **İmza modeli geçici varsayılandır** (test bütçesini ödeyen imzalar); kalıcı karar
  son tarihi **21 Temmuz 2026 (G9)** — bkz. [docs/strategy/main_analysis.md](docs/strategy/main_analysis.md) §1.4.
- Analist saat bütçesi netleşene kadar öncelik sırası: kreatif analizi → test altyapısı → radar.
