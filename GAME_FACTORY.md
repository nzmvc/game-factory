# GAME_FACTORY — Fabrika Modeli

**Son güncelleme:** 2026-07-12 · **Kaynak strateji:** [docs/strategy/main_analysis.md](docs/strategy/main_analysis.md) (v1.1)

Fabrikanın üst modeli budur: katmanlar, makine hattı, değişmez kurallar.
Metrik eşiklerinin tek kaynağı [ops/esikler.md](ops/esikler.md)'dir — buraya kopyalanmaz.

---

## 1. Vizyon

İnsan onaylı karar kapıları olan, AI ajan destekli bir **hyper/hybrid-casual mobil oyun üretim hattı**.
Her oyun bir ürün denemesidir; para tek oyunda değil, kill disiplinli portföydedir.
Hedef: fikirden yayına tüm sürecin aynı standartla, onlarca kez tekrarlanabilmesi.

## 2. Katman modeli

```
İNSAN KATMANI    — Nazım (Producer): yeşil ışık · para · yayın · game feel · nihai infaz
                   Analist (Veri & Pazar): radar · skorlama · test analizi · eşik bekçiliği
       │                                       ayrıntı: HUMAN_ROLES.md
AJAN KATMANI     — A1 Producer · A2 Radar · A3 GDD · A4 Görsel · A5 Kod · A6 Test
                   A7 İnfaz · A8 ASO · A9 Doküman   (Faz 1–2: prompt ile manuel ·
       │           Faz 3: SDK orkestrasyonu)         ayrıntı: AGENTS.md
MAKİNE HATTI     — M0 Şasi · M1 Radar · M2 Seçim · M3 GDD · M4 Görsel · M5 Kod
       │           M6 Pazarlanabilirlik · M7 Veri&İnfaz · M8 ASO&Yayın
VERİ SÖZLEŞMELERİ— GameBrief v1 · aday kartı · event şeması · ops/esikler.md
                                                     ayrıntı: schemas/
```

Kural: **Makine numaraları (M0–M8) fiziksel hatta aittir, değişmez. Ajanlar A-öneki alır.**
Bir ajan bir makinenin otomasyon kabuğudur; makine değildir.
Gerekçe: [ADR-0002](docs/decisions/ADR-0002-makine-ajan-katmanlari.md)

## 3. Makine kataloğu

Her makine: **Girdi → Süreç → Çıktı → İnsan kapısı**

| M | Makine | Girdi | Çıktı | Ajan | İnsan kapısı |
|---|---|---|---|---|---|
| 0 | Şasi | Unity LTS + SDK gereksinimleri | Yeniden kullanılabilir Unity template | A5 | Mimari onay |
| 1 | Pazar Radarı | Top charts, ad library'ler, AppMagic | Haftalık 10 aday kartı (kanıtlı) | A2 | — |
| 2 | Seçim Kapısı | Aday kartları | 70'lik cetvelle skorlanmış 1–2 aday | A1 | ✔ **Yeşil ışık** |
| 3 | GDD | Yeşil ışıklı GameBrief (completion ≥ 90) | 2–3 sayfa tasarım dokümanı | A3 | GDD onayı |
| 4 | Görsel | GDD | Stil rehberi + asset listesi + juice checklist | A4 | Stil onayı |
| 5 | Kod | GDD + şasi | Oynanabilir prototip (tek mekanik modülü) | A5 | Cihazda **bizzat oynama** |
| 6 | Pazarlanabilirlik | Prototip / gameplay videosu | 3–5 kreatif + CPI/CTR verisi | A6 | ✔ **Bütçe onayı** |
| 7 | Veri & İnfaz | Test verileri | ÖLDÜR / DÜZELT / BÜYÜT raporu | A7 | ✔ **Nihai karar** |
| 8 | ASO & Yayın | BÜYÜT kararı | Store metni, keyword, görseller (TR+EN) | A8 | Yayın onayı |

Süreç detayı ve aşama geçiş koşulları: [WORKFLOW.md](WORKFLOW.md)

## 4. Değişmez kurallar

*Bu bölüm yalnız Nazım onayıyla değişir.*

1. **Önce üret, sonra otomatikleştir.** Otomasyon talebi geldiğinde önce hattaki gerçek darboğaz sorgulanır.
2. **≤ 2 hafta geliştirme tavanı / prototip.** Kapsam büyüten öneri = v2 işi.
3. **Pazar-öncelikli seçim.** İnsan fikri yasak değildir; aday kartı formatına girer (`origin: insan`), aynı cetvelden geçer. Yan kapı yok.
4. **Para harcanan / yayına giden her adım = açık insan onayı.** Onaysız adım "tamamlandı" sayılmaz.
5. **Game feel devredilemez.** Her prototip cihazda bizzat oynanır; ajanlar juice'u ölçemez.
6. **Eşikler tartışılmaz** ([ops/esikler.md](ops/esikler.md)). Oyuna âşık olmak fabrikaların bir numaralı ölüm nedenidir.
7. **Veri yoksa uydurulmaz** — "doğrulanamadı" yazılır.
8. **Her kapının tek karar sahibi vardır.** Danışılır, oylanmaz. İnşa eden infaz etmez.
9. **Tek doğruluk kaynağı ilkesi:** her bilgi tek dosyada yaşar, diğerleri link verir.
10. **Şema disiplini:** ajanlar arası veri yalnız schemas/ altındaki sözleşmelerle taşınır.

## 5. İki repo modeli

| Repo | İçerik | Kim çalışır |
|---|---|---|
| **GameFactory** (bu repo) | Süreç, ajanlar, kararlar, şemalar, şablonlar, radar, test sonuçları | A1–A4, A6–A9 + insanlar |
| **Oyun repoları** (oyun başına 1) | Unity projesi: şasi + mekanik modülü + content | A5 (Claude Code / Antigravity) |

Oyun reposu, [templates/game-docs/](templates/game-docs/) şablon setiyle ve
kendi CLAUDE.md/AGENTS.md'siyle açılır. Gerekçe: [ADR-0001](docs/decisions/ADR-0001-iki-repo-modeli.md)

## 6. Kalite standardı (psikoloji spesifikasyonu)

Her tasarım çıktısı şu cetvele karşı denetlenir (kaynak: [docs/strategy/01-oyun-fabrikasi-analiz.md](docs/strategy/01-oyun-fabrikasi-analiz.md) §4):
3 saniye kuralı · tek parmak / portre / sıfır okuma · değişken ödül · juice (partikül+ses+haptik) ·
near-miss · Zeigarnik (streak, ilerleme) · 2–5 dakikalık oturum ritmi.

## 7. Model stratejisi

Pahalı model → düşük hacim/yüksek değer kararları; ucuz model → yüksek hacim taramaları.
Görsel/video üretimi LLM işi değildir. Görev→model matrisi: [docs/strategy/main_analysis.md](docs/strategy/main_analysis.md) §3.
Model adları hızla eskir — **her harcama kararından önce güncel sürüm/fiyat doğrulanır.**
