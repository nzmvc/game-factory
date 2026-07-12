# Oyun Fabrikası 🏭

İki kişilik çekirdek ekip (Producer + Analist) ve agent katmanıyla çalışan **hyper/hybrid-casual mobil oyun üretim hattı**.
Her oyun bir ürün denemesidir: hızlı üret → gerçek parayla test et → **ÖLDÜR ya da BÜYÜT**.
Mobil oyun bir "oyun yapma" işi değil, kullanıcı edinme işidir; tek denklem: **LTV > CPI**.

> **Durum:** Faz 1 · Aktif oyun: **Toy Pile** (tap triple-match + shockwave cascade, şasi-lite)
> Sıradaki insan kapısı: pazarlanabilirlik testi bütçe onayı ($100–200)

---

## 60 saniyede fabrika

Pazar radarı kanıtlı aday üretir → 70 puanlık cetvel + insan yeşil ışığı → GameBrief (completion ≥ 90) → GDD → şasi + **tek mekanik modülü** (≤ 2 hafta) → cihazda game feel (devredilemez) → $100–200 reklam testi → eşikler karar verir. %80–90 kill oranı normaldir; fikri kod yazmadan öldürmek fabrikanın en kârlı işlemidir.

## Ekip ve roller

| Kişi | Rol | Sahiplik | Onay yetkisi |
|---|---|---|---|
| Nazım | Producer | M0/M5 (şasi + kod), game feel son sözü | **Tüm ✔ kapıları, tek imza:** yeşil ışık · bütçe · nihai infaz · yayın |
| Analist | Veri & Pazar | M1 radar, M2 skorlama, M6 test analizi/pano, M7 raporu, kill-log | — (rapor eder, karar vermez) |

İlke: **inşa eden infaz etmez** — metrik raporu ve eşik karşılaştırması analistten çıkar, karar tek imzada kalır. RACI ayrıntısı: `main_analysis.md` §1.4 / `ops/roller.md`.
İmza modeli **geçici varsayılandır** (test bütçesini ödeyen imzalar); kalıcı karar son tarihi **G9 (21 Tem)** — ayrıntı: `main_analysis.md` §1.4.

## Makine hattı (M0–M8)

| M | Makine | Çıktı | İnsan kapısı |
|---|---|---|---|
| 0 | Şasi | Yeniden kullanılabilir Unity template (v1: şasi-lite stub) | Mimari onay |
| 1 | Pazar Radarı | Haftalık 10 aday kartı (kanıtlı) | — |
| 2 | Seçim Kapısı | Skorlanmış 1–2 yeşil ışık adayı | ✔ Yeşil ışık |
| 3 | GDD | 2–3 sayfa tasarım dokümanı | GDD onayı |
| 4 | Görsel | Stil rehberi + asset listesi + juice checklist | Stil onayı |
| 5 | Kod | Oynanabilir prototip (yalnız mekanik modülü) | Cihazda bizzat oynama |
| 6 | Pazarlanabilirlik | 3–5 kreatif + CPI/CTR testi | ✔ Bütçe onayı |
| 7 | Veri & İnfaz | ÖLDÜR / DÜZELT / BÜYÜT | ✔ Nihai karar |
| 8 | ASO & Yayın | Store metni, keyword, görseller (TR+EN) | Yayın onayı |

## Ajan katmanı (AOS)

Makinelerin otomasyon kabuğu. Ajanlar **A-öneki** alır (makine numaralarıyla çakışmaz): **A1 Producer** (insanla konuşan tek ajan, M2→M3 arayüzü), A2 Radar, A3 GDD, A6 Test, A7 İnfaz, A8 ASO.
Faz 1–2: promptlarla manuel işletim (A1 rolünü Claude Projesi oynar). Faz 3: SDK orkestrasyonu — tetik koşulu sağlanmadan başlamaz. Ayrıntı: `main_analysis.md` §1–2.

Ortak veri sözleşmesi: **GameBrief v1** (`schemas/gamebrief.v1.json`) = radar aday kartı ⊕ tasarım çekirdeği ⊕ completion score.

## Değişmez kurallar

1. **Önce üret, sonra otomatikleştir** — darboğazı üretim gösterir, hayal değil.
2. **≤ 2 hafta** geliştirme tavanı / prototip. Kapsam büyüten öneri = v2 işi.
3. **Pazar-öncelikli seçim** — insan fikri de aynı cetvelden geçer; yan kapı yok.
4. **Para harcanan / yayına giden her adım = açık insan onayı.** Onaysız adım "tamamlandı" sayılmaz.
5. **Game feel devredilemez** — her prototip cihazda bizzat oynanır.
6. **Eşikler tartışılmaz** (`ops/esikler.md`); oyuna âşık olmak fabrikaların bir numaralı ölüm nedenidir.
7. Veri yoksa uydurulmaz; "doğrulanamadı" yazılır.
8. Her kapının **tek karar sahibi** vardır — danışılır, oylanmaz. İnşa eden infaz etmez.

## Klasör yapısı

```
oyun-fabrikasi/
├── README.md                    # bu dosya
├── main_analysis.md             # TEK DOĞRULUK KAYNAĞI — strateji + fazlar + uzlaştırma
├── docs/                        # 01/02/03 kuruluş dokümanları + kararlar/ (ADR)
├── schemas/                     # gamebrief.v1.json · event-schema.md
├── agents/                      # A1-producer, A2-radar, ... (talimatlar; önce prompt)
│   └── _arsiv/aos-chatgpt/      # AOS_* orijinalleri (Faz 3 tohumu)
├── radar/taramalar/             # haftalık tarama çıktıları + aday kartları
├── games/toy-pile/              # brief · gdd · antigravity-promptlar · test sonuçları
├── orchestrator/                # Faz 3'e kadar kilitli (yalnız README)
└── ops/                         # esikler.md · roller.md · kill-log.md

ToyPile/                         # ayrı repo — Unity projesi (Antigravity workspace)
```

## Faz planı (özet)

| Faz | Süre | Hedef |
|---|---|---|
| 1 | 10 gün (13–22 Tem) | Toy Pile cihazda oynanır + pazarlanabilirlik testi canlı |
| 2 | Hafta 3–6 | M7 kararı → (BÜYÜT ise gerçek şasi + soft launch) · GameBrief v1 kilidi · A1 talimatı v2 · Prototip #2 |
| 3 | Tetikleyicili (Eylül+) | SDK orkestrasyonu · radar v2 otomasyonu · ayda 1–2 prototip ritmi |

Faz 3 tetiği: 2 prototip hattan geçti **VE** (radar 3 hafta elle aksadı **VEYA** ay 2+ prototip hedefi). Gün gün plan: `main_analysis.md` §2.

## Haftalık ritim (Faz 1–2)

- **Pzt:** Analist: radar taraması 60–90 dk (A2 promptu) → aday kartları `radar/taramalar/`e · ardından 20 dk senkron (radar sonuçları + hafta planı)
- **Salı–Cuma:** Nazım: aktif prototipte üretim (M5), her akşam cihaz build · Analist: rakip kreatif analizi + test/pano işleri
- **Cmt:** Metrik panosunu analist sunar; game feel'i ikisi de cihazda test eder (son söz Nazım); gerekiyorsa M7 karar oturumu
- Yeşil ışık adaylarının referans oyunlarını **ikiniz de** indirin, 10'ar dk oynayın — his rapordan okunmaz

## Eşikler (özet — kaynak: `ops/esikler.md`)

CPI < $0.40 · CTR > %1.5 · D1 > %45 · D7 > %15 · playtime > 15 dk · yeşil ışık ≥ 50/70 + veto · completion ≥ 90 · tek zayıf = DÜZELT (1 hak) · çoklu kırmızı = ÖLDÜR

## Belgeler

- `main_analysis.md` — strateji, AOS↔Fabrika uzlaştırması, 3 faz, çoklu model matrisi
- `docs/01-oyun-fabrikasi-analiz.md` — kuruluş analizi (pazar, psikoloji spesifikasyonu, LLM eşleştirme)
- `docs/02-…` / `docs/03-…` — M0 şasi ve M1 radar kurulum promptları
- `agents/_arsiv/aos-chatgpt/` — ChatGPT oturumu orijinalleri (Game Producer analizi + orchestrator)
