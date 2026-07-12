# Oyun Fabrikası — Ana Analiz (main_analysis)

**Tarih:** 12 Temmuz 2026 · **Sürüm:** v1.1 · **Hazırlayan:** Fabrika OS
**Ekip:** Nazım (Producer — para · yayın · nihai karar) + Analist (Veri & Pazar — radar · skorlama · eşik bekçisi)
**Durum:** Onay bekliyor — §1.1'deki 5 uzlaştırma kararı + §1.4 rol tablosu onaylanınca yürürlüğe girer
**v1.1 değişikliği:** Ekip 2 kişiye çıktı. §1.4 (Roller & RACI) eklendi; Faz planı, repo kuralları ve riskler güncellendi. Eşikler ve 2 hafta tavanı DEĞİŞMEDİ.
**Kaynaklar:** 01/02/03 fabrika dokümanları · AOS_GameProducer_Analysis_v0.2 (ChatGPT oturumu) · AOS_ORCHESTRATOR.py
**Çelişki kuralı:** Bu dosya ile diğer dokümanlar çelişirse **bu dosya esastır**; metrik eşiklerinde 01 dosyası ile bu dosya birebir aynıdır.

---

## 0. Yönetici Özeti (para nerede?)

- İş modeli değişmedi: mobil oyun bir UA işidir, tek denklem **LTV > CPI**. Para tek oyunda değil, kill disiplinli portföydedir. %80–90 kill oranı sağlıktır.
- ChatGPT oturumunda tasarlanan **AOS (AI Native Game Studio OS)** ile onaylı fabrika **rakip iki sistem değil, aynı sistemin iki katmanıdır**: Makineler = üretim adımları, Ajanlar = o adımların otomasyon kabuğu. Bu dosya ikisini tek isimlendirme altında birleştirir.
- **Faz 1 (10 gün):** Yeni "daha basit bir oyun" başlatılmaz. Hattaki oyun **Toy Pile** bitirilir: cihazda oynanır durum + pazarlanabilirlik testi canlı. "Oyun çıktı"nın dürüst tanımı budur; store yayını CPI doğrulamasından **sonra** gelir (şasi-lite kararının zaten var olma sebebi).
- **AOS_ORCHESTRATOR.py bugün çalıştırılamaz durumda değil — daha kötüsü, çalışır ama kurguyla karar verir:** `fetch_live_market_data` simüle (uydurma) veri döndürüyor ve içindeki skorlama cetveli onaylı cetvelle çelişiyor. Faz 3 tohumu olarak arşive kalkar. Bu, senin kendi cümlenle uyumlu: *"ilk aşamada her adım promptlarla manuel işletilebilir."*
- **v1.1 — Ekip 2 kişi:** Analistin asıl değeri kapasite değil, **denetimdir**: inşa eden ile infaz eden ayrıldı (analist = eşik bekçisi, M7 raportörü). Değişmeyenler: eşikler, 2 hafta tavanı, pazar-öncelikli akış, tek-imza kapıları. Ekstra kapasite oyunu büyütmeye değil, hattı hızlandırmaya gider.

---

## 1. Mimari Uzlaştırma — AOS ↔ Fabrika

Senin mesajındaki akış (fikir → insan onayı → analiz: psikoloji/gamification/monetizasyon → developer agent'lara aksiyon dosyası → geliştirme → test → raporlama) **birebir M1→M8 hattıdır**. Psikoloji/gamification analizi 01 dosyası §4'te kalite standardı olarak zaten kodlu; yeni makine gerekmez. Yeni olan tek şey ajan katmanının adlandırılması ve ChatGPT oturumundan gelen çakışmaların temizlenmesi.

### 1.1 Tespit edilen çakışmalar ve kararlar

| # | Çakışma | AOS (ChatGPT oturumu) | Onaylı Fabrika | KARAR |
|---|---|---|---|---|
| 1 | **"Machine 0" isim çarpışması** | Machine 0 = "Studio Architect" ajanı (GameBrief → Blueprint) | Makine 0 = Unity Şasisi (fiziksel template) | Makine numaraları (M0–M8) **fiziksel hatta aittir**, değişmez. Ajanlar **A-öneki** alır. AOS'un "Studio Architect"i ayrı bir makine değil, M3-GDD'nin otomasyon kabuğudur → adı **A3**. |
| 2 | **Fikir-öncelikli vs pazar-öncelikli akış** | İnsan fikri → Game Producer → GameBrief ("terk edilmiş adaları restore et" örneği) | Radar kanıtı → 70'lik cetvel → seçim | **Pazar-öncelikli kalır.** İnsan fikri yasak değil; aday kartı formatına sokulur (`origin: insan`), aynı cetvelden geçer. Yan kapı yok. Not: "ada restorasyonu" örneği meta/LiveOps ağırlıklı — Hat 1 eleme filtresine zaten takılırdı. |
| 3 | **Çifte skorlama cetveli** | 10 üzerinden, ≥7.5 yeşil ışık, 4 hafta dev tavanı, CPI kriterleri farklı | 70 üzerinden, ≥50 + kritik zayıflık vetosu, **2 hafta** tavan | 70'lik cetvel ve 2 hafta tavan **tek doğruluk kaynağıdır**. Orchestrator'daki cetvel silinir. İki cetvel yaşatmak fabrikayı ikiye böler. |
| 4 | **Paralel veri şemaları** | GameBrief.json (alanları tanımsız) | Aday kartı (YAML, 03 dosyası) | Tek sözleşme: **GameBrief v1 = aday kartı ⊕ tasarım çekirdeği ⊕ completion score** (§1.3). AOS'un "GameBrief ortak veri sözleşmesidir" kararı korunur — şema fabrikanınkiyle birleşir. |
| 5 | **Otomasyon zamanlaması** | SDK orkestrasyonu + agent handoff şimdi | "Önce üret, sonra otomatikleştir"; tetik: ritim veya aksama | Orchestrator **Faz 3 tohumu** olarak `agents/_arsiv/`e kalkar. Simüle veri üretim kararında asla kullanılmaz. Tetik koşulları §2 Faz 3'te. |

Küçük hijyen notları: orchestrator'da model hardcoded (`gpt-4o`) — model seçimi Faz 3'te A/B ile yapılır, koda gömülmez; instruction içinde `[cite: 8]` kalıntısı var (kopyala-yapıştır artığı, güven verici değil).

### 1.2 Birleşik katman modeli

```
İNSAN KATMANI — Nazım (Producer): yeşil ışık · para · yayın · game feel son sözü · nihai infaz
                Analist (Veri & Pazar): radar · skorlama · test analizi · eşik bekçiliği · kill-log
   │
AJAN KATMANI (AOS)  — A1 Producer · A2 Radar · A3 GDD · A5 Kod · A6 Test · A7 İnfaz · A8 ASO
   │                   Faz 1–2: prompt ile manuel · Faz 3: SDK orkestrasyonu
MAKİNE HATTI        — M0 Şasi · M1 Radar · M2 Seçim · M3 GDD · M4 Görsel · M5 Kod
   │                   M6 Pazarlanabilirlik · M7 Veri&İnfaz · M8 ASO&Yayın
VERİ SÖZLEŞMELERİ   — GameBrief v1 · EventSchema · ops/esikler.md
```

**AOS oturumundan korunan değerli parçalar** (Faz 2'de A1 talimatına işlenecek):
- Conversation State (workflow unutulmaz, "devam et" başa sarmaz)
- User Input Validation (yeni bilgi yoksa workflow ilerlemez)
- Mod ayrımı: Discovery / Validation / Brief Generation — Discovery'de JSON üretilmez
- Completion Score kalite kapısı (≥90 olmadan M3 çalışmaz)
- "İnsanla konuşan tek ajan A1 Producer'dır" ilkesi (otomasyon fazında geçerli)
- Executive Producer kişiliği: sekreter değil; risk gösterir, öneri sunar

**A1 Producer'ın hattaki yeri:** M2→M3 arayüzü. Radar kartı yeşil ışık aldıktan sonra eksik alanları insanla diyalogla tamamlar ve GameBrief'i kilitler. Bu rolü şu an **bu Claude Projesi** oynuyor; Faz 2'de talimat AOS öğrenimleriyle yeniden yazılır (kod değil, prompt). OpenAI Assistants API yolu kapalı (deprecate); kod gerekirse doğru yol Responses API + Agents SDK'dır ve o Faz 3 işidir.

### 1.3 GameBrief Schema v1 — taslak (Faz 2'de kilitlenir)

```json
{
  "schema_version": "1.0",
  "brief_id": "GB-2026-07-XX-001",
  "origin": "radar | insan",
  "radar_card_id": "R-2026-07-11-01",

  "mekanik": {
    "adi": "",
    "referans_oyunlar": [],
    "kanit": "",
    "kontrol_semasi": "tap | drag | swipe | hold",
    "icerik_uretimi": "algoritmik | yari-elle",
    "twist": ""
  },

  "skorlar": {
    "cetvel_70": 0,
    "yesil_isik": false,
    "override": null
  },

  "tasarim_cekirdegi": {
    "core_loop": "",
    "oturum_hedefi_dk": [2, 5],
    "zorluk_kurali": "",
    "monetizasyon": { "rewarded_yerlesimler": [], "interstitial_kurali": "RemoteConfig" }
  },

  "uretim": {
    "tavan_gun": 14,
    "sasi_modu": "lite | full",
    "arac": "antigravity | claude-code"
  },

  "completion": { "zorunlu_alan": 0, "dolu": 0, "score": 0 },
  "onaylar": { "secim": null, "butce": null }
}
```

**Completion score kuralı (checklist tabanlı):** `score = round(100 × dolu_zorunlu / toplam_zorunlu)`. Eşik **≥ 90** — AOS Quality Gate aynen korunur. 90 altında M3 (GDD) çalıştırılmaz; A1 yalnızca bekleyen soruları hatırlatır.

### 1.4 Roller & RACI (v1.1 — çekirdek ekip 2 kişi)

**İlkeler (tartışmaya kapalı):**
- **Her kapının tek karar sahibi (A) vardır.** Danışılır, oylanmaz — komite, hyper-casual hızını öldürür.
- **İnşa eden infaz etmez.** M7 raporunu ve eşik karşılaştırmasını analist hazırlar; oyunu yapanın "bir şans daha" refleksine karşı yapısal panzehir. Nihai karar yine tek imzada.
- **Para tek imzada.** Reklam hesapları ve tüm harcamalar Nazım'da; analistin kampanya kurma yetkisi var, harcamayı başlatma yetkisi yok.
- **Game feel ikiye katlanır, son söz teke iner.** İkiniz de cihazda oynarsınız (daha çok veri); son söz Nazım'da.
- **Dış AI oturumu kuralı kişiden bağımsızdır.** Analistin ChatGPT/Gemini oturumlarından gelen dokümanlar da entegrasyondan önce bu dosyanın isimlendirmesine çevrilir.

| Makine / Kapı | Analist | Nazım |
|---|---|---|
| M1 Radar (haftalık tarama + aday kartları) | **Sahibi (R/A)** | Referans oyunları o da oynar |
| M2 Seçim (70'lik cetvel skorlaması) | Hazırlar (R) | **Yeşil ışık kararı (A)** |
| M3 GDD · M4 Görsel | Pazar/rakip girdisi (C) | Onay (A) — üretim ajanlarda |
| M5 Kod (Antigravity + Unity + cihaz) | — | **Sahibi (R/A)** |
| M6 Test (kreatif analizi · kampanya kurulumu · pano) | Sahibi (R) | **Bütçe onayı (A)** |
| M7 Veri & İnfaz | **Raportör + eşik bekçisi (R)** | **Nihai karar (A)** |
| M8 ASO (keyword araştırması, lokalizasyon kontrolü) | Hazırlar (R) | Yayın onayı (A) |
| Game feel | Oynar, not verir (C) | **Son söz (A)** |

**Açık maddeler (son tarih: G9 — 21 Temmuz):**
- **Analist saat bütçesi: bilinmiyor.** Netleşene kadar analist işleri öncelik sırasıyla yürür: (1) rakip kreatif analizi (G8'den önce bitmeli), (2) test altyapısı + Google Play kısıt doğrulaması (G10'dan önce), (3) ilk radar taraması (Faz 2'ye sarkabilir — Toy Pile'ın kritik yolunda değil). Saat belli olunca Faz 2 dağılımı buna göre kalibre edilir.
- **Para/yayın imza modeli: henüz netleşmedi.** Geçici varsayılan: **test bütçesini kim ödüyorsa imza onda.** G9'a kadar asgari yazılı mutabakat şart — iki cümle yeter: kim ödüyor + "gelir/IP modeli yayından önce netleşecek." Bu yoksa G10 testi başlamaz: **tarih kayar, para kaymaz.** Tam ortaklık anlaşması (gelir/gider/IP) en geç M8 yayın kapısından önce. Oyuna âşık olmak fabrikaların bir numaralı ölüm nedeniyse, "arkadaşız, hallederiz" iki numaralı nedenidir.

---

## 2. Üç Faz Planı

### FAZ 1 — "İlk Oyun Çıkıyor" · 13–22 Temmuz (10 gün)

**Hedef cümle:** *Toy Pile cihazda temiz oynanıyor ve pazarlanabilirlik testi yayında.*
Kapsam donmuş: tap triple-match + shockwave cascade, şasi-lite (Dummy/Console stub), Antigravity 6 prompt seti. Yeni özellik teklifi = otomatik red.

| Gün | İş | Sorumlu |
|---|---|---|
| G1–G2 (13–14 Tem) | Antigravity Prompt 1–2: şasi-lite iskelet + TileMatch çekirdeği | Agent kod yazar; sen Unity Editor + her akşam cihaz build |
| G3–G4 (15–16 Tem) | Prompt 3–4: level generator + solvability validator, juice (cascade hissi) | Agent + sen |
| G5–G6 (17–18 Tem) | Prompt 5–6: UI/ad stub akışı + Android build config; ilk uçtan uca akış | Agent + sen |
| G7 (19 Tem) | **Game feel günü** — cihazda oynama, düzeltme listesi, sonra **scope freeze** | Nazım + Analist cihazda oynar; **son söz Nazım** (devredilemez) |
| G8–G9 (20–21 Tem) | Gerçek gameplay kaydı → 3–5 reklam kreatifi (CapCut; ilk 3 saniyede mekanik). TEST modu brief'leri bu projede üretilir | Sen + Claude (TEST modu) |
| G10 (22 Tem) | Pazarlanabilirlik testi canlı: TikTok/Meta, $100–200 | ⛔ **İnsan kapısı: bütçe onayı (tek imza: Nazım)** — onaysız harcama yok |

**Paralel hat — Analist (G1–G10, v1.1):** Toy Pile takvimi değişmez; analist ikinci bir hat açar.
- **G1–G5:** M1 ilk tam taraması (10 aday kartı) + rakip kreatif analizi (TikTok Creative Center: Zen Match, Triple Match 3D, Match Factory!, Tile Busters) — "hangi an izlettiriyor" notları G8–G9 kreatif brief'lerinin doğrudan girdisidir.
- **G6–G7:** Test altyapısı: TikTok/Meta kampanya taslağı (harcamasız), sonuç panosu iskeleti, Google Play yeni hesap kısıtının doğrulanması → CTR-proxy'ye düşüp düşmeyeceğimiz G7'de netleşir.
- **G8–G10:** Pano canlı; bütçe onayı sonrası kampanyayı analist yayına alır ve ilk 48 saat okumasını raporlar.
- **Saat kısıtı kuralı:** Analistin saati yetmezse sıra: kreatif analizi → test altyapısı → radar. Radar Faz 2'ye sarkabilir; test hattı sarkamaz.

**Gerçekçilik notları:**
- 10 günde elinde ~15–30 saat var (10–20 saat/hafta gerçeği). Sıkışırsa kısılacak şey **kreatif sayısıdır (5→3)**, mekanik kapsam değil; tarih kaymaz.
- **Google Play riski:** Yeni bireysel geliştirici hesabı kısıtları (kapalı test / tester zorunluluğu) store sayfasını 10 güne sığdırmayabilir. Fallback: **CTR-proxy testi** — video kreatif yayınla, CTR/CPC ölç; 01 dosyası bunu zaten meşru sayıyor ("kod yazmadan, sahte gameplay videosuyla bile test"). CPI eşiği ($0.40) bu durumda soft launch aşamasında uygulanır, CTR eşiği (>%1.5) Faz 1'de karar verdirir.
- Toy Pile'ın 53/70 skoru bilinçli override'dı; **sigortası bu test.** Test sonucu kötüyse oyuna âşık olma lüksü yok.

**Faz 1 "bitti" tanımı:** cihazda temiz kurulumdan 10 dk sorunsuz oynanış ✚ test canlı ✚ sonuçların okunacağı pano hazır.

### FAZ 2 — "Karar, Standart, İkinci Tur" · 23 Temmuz – 23 Ağustos

1. **M7 kararı (Toy Pile):** test verilerini eşiklere **analist** vurur ve raporu yazar (inşa eden infaz etmez); nihai karar Nazım'ın → ÖLDÜR / DÜZELT / BÜYÜT. Tek DÜZELT hakkı, tartışma yok.
   - BÜYÜT ise: ertelenen **gerçek şasi** ancak şimdi kurulur (Firebase, mediation, IAP, consent — 02 dosyası prompt seti) + soft launch.
   - ÖLDÜR ise: `ops/kill-log.md`'ye öğrenilenler (kill-log'u analist tutar) + radar'dan sıradaki aday. Bu bir başarısızlık değil, fabrikanın en kârlı işlemidir.
2. **M1 rutini analistin sahipliğinde oturur:** haftalık 60–90 dk tarama + M2 skorlama tabloları analistten; yeşil ışık Nazım'da. (İlk tam tarama Faz 1'in paralel hattında zaten yapılmış olur.)
3. **GameBrief v1 kilitlenir** (§1.3 taslağı → `schemas/gamebrief.v1.json`).
4. **A1 Producer talimatı v2:** AOS öğrenimleri (state + validation + modlar + completion score) Claude Projesi talimatı olarak yazılır. Kod yok.
5. **Prototip #2 hattan geçer** (2 hafta tavan). Fabrika iddiasının ispatı ilk oyun değil, **ikinci** oyundur — tekrarlanabilirlik.
6. **Antigravity vs Claude Code A/B kararı** verilir; kazanan `uretim.arac` varsayılanı olur.

### FAZ 3 — "AOS Otomasyonu + Çoklu Model Orkestrasyon" · Eylül+ (takvimle değil, tetikle)

**Tetik koşulu (ikisi birden):** hattan en az 2 prototip geçti **VE** (radar rutini 3 hafta üst üste elle aksadı **VEYA** ayda 2+ prototip ritmi hedefleniyor). Tetik gelmeden bu faza başlamak = fabrika tuzağı.

**v1.1 notu:** Radar artık analistin sahipliğinde — "elle aksama" tetiği hâlâ geçerli ama otomasyonun aciliyeti düştü. İnsan kapasitesi varken SDK yazmak yine fabrika tuzağıdır; tetik koşulları aynen korunur.

1. **Orkestrasyon iskeleti:** OpenAI Agents SDK (Responses API) ↔ Claude Agent SDK — seçim Faz 2 A/B sonucuna göre. `AOS_ORCHESTRATOR.py` tohumdur, üç ameliyatla:
   - simüle `fetch_live_market_data` → gerçek kaynaklar (resmî API'ler; ToS ihlali scraping yok),
   - 10'luk cetvel → 70'lik cetvel + veto kuralı (koddan okunur, `ops/esikler.md` tek kaynak),
   - **insan kapıları koda gömülür:** bütçe/yayın adımında agent durur, onay bekler. Auto-spend yok.
2. **Radar v2:** zamanlanmış tarama (cron/n8n) → kartlar sheet/DB'ye; günlük hafif tarama ucuz modelde.
3. **A-katmanı spec'leri:** AOS oturumunun 20. bölümündeki doküman listesi (PRD, Agent Specification, Message Protocol, Agent Manifest) bu fazın işidir — önce değil.
4. **Hedef ritim:** ayda 1–2 prototip; kill oranı %80–90 normal seyir.

---

## 3. Çoklu Model Stratejisi (Claude · OpenAI · Gemini · DeepSeek)

İlke: pahalı model → düşük hacim/yüksek değer kararları; ucuz model → yüksek hacim taramaları. Görsel/video üretimi LLM işi değildir (ayrı sütun: Midjourney/Flux, Veo/Runway, Meshy).

**v1.1:** Matris ekip boyutundan bağımsızdır; değişen şey operatörlük — A2 (radar), A6 (test analizi) ve A7 (rapor) ajanlarını **analist** işletir.

| Görev | Birincil | Alternatif / Ucuz | Neden |
|---|---|---|---|
| Mimari + mekanik kod (M0, M5) | Claude (Opus / Claude Code / Antigravity) | Rutinde Sonnet | Mevcut akışta ispatlı; şasi kalitesinden kısılmaz |
| Seçim kapısı muhakemesi (M2) | Claude extended thinking | **OpenAI reasoning sınıfı — ikinci görüş A/B** | Fabrikanın en kritik kararı; çifte kontrol ucuz sigorta |
| GDD / ASO metin (M3, M8) | Claude Sonnet | **DeepSeek** — 10+ dile toplu lokalizasyon | Maliyet tabanı; kalite kontrolü örneklemle |
| Günlük radar taraması (M1) | Claude Haiku | **Gemini Flash** veya DeepSeek | Hacim işi; en ucuz + web erişimi kazanır |
| Rakip reklam kreatifi analizi (M1/M6) | **Gemini (multimodal video)** | — | Video anlama bu iş için biçilmiş kaftan; "hangi an izlettiriyor" sorusu |
| Kreatif hook/senaryo metni (M6) | Claude | DeepSeek | Düşük risk, ucuza kaçılabilir |
| Orkestrasyon (Faz 3) | OpenAI Agents SDK | Claude Agent SDK | Handoff/guardrail olgunluğuna göre Faz 2'de seçilir |
| Veri & İnfaz (M7) | **Deterministik kod + eşik tablosu** | Yorum katmanı: Claude Sonnet | Karar LLM'e bırakılmaz; LLM yalnızca "neden" raporu yazar |

**Dürüstlük notu:** Bu tabloyu bir Claude yazdı. Model adları ve fiyatlar hızla eskir — **her harcama kararından önce güncel sürüm/fiyat doğrula** ve kendi iş yükünde rakip A/B'sini gerçekten yap.

---

## 4. Depo, Dosya ve Klasör Yapısı

İki repo modeli: fabrika (hafif, doküman + ajan + veri) ve Unity oyun repoları (ağır, oyun başına bir tane). Antigravity/Claude Code oyun reposunda çalışır; fabrika reposu karar hafızasıdır.

```
oyun-fabrikasi/                        # REPO 1 — Fabrika (bu repo)
├── README.md                          # vitrin + hızlı başlangıç
├── main_analysis.md                   # TEK DOĞRULUK KAYNAĞI (bu dosya)
├── docs/
│   ├── 01-oyun-fabrikasi-analiz.md
│   ├── 02-makine-0-sasi-kurulum-promptlari.md
│   ├── 03-makine-1-radar-kurulum-promptlari.md
│   └── kararlar/                      # ADR: her mimari karar tek md dosyası
├── schemas/
│   ├── gamebrief.v1.json              # birleşik veri sözleşmesi (Faz 2'de kilit)
│   └── event-schema.md                # analytics event şeması (M0 ile senkron)
├── agents/                            # ajan talimatları — önce prompt, sonra kod
│   ├── A1-producer/instruction.md
│   ├── A2-radar/haftalik.md · gunluk.md
│   ├── A3-gdd/  A6-test/  A7-infaz/  A8-aso/
│   └── _arsiv/aos-chatgpt/            # AOS_GameProducer_Analysis + ORCHESTRATOR.py
├── radar/
│   └── taramalar/2026-W29.md          # haftalık tarama çıktıları + aday kartları
├── games/
│   └── toy-pile/
│       ├── brief.md                   # GameBrief (v1 şemasına geçirilecek)
│       ├── gdd.md
│       ├── antigravity-promptlar/     # 6 prompt seti
│       └── test/                      # kreatifler + CPI/CTR sonuçları
├── orchestrator/
│   └── README.md                      # "Faz 3 tetiklenmeden dokunma" + tetik koşulları
└── ops/
    ├── esikler.md                     # metrik eşikleri — kod/tablo, tartışılmaz
    ├── roller.md                      # RACI + onay yetkileri (kaynak: §1.4)
    └── kill-log.md                    # öldürülen oyunlar + öğrenilenler (sahibi: analist)

ToyPile/                               # REPO 2 — Unity projesi (Antigravity workspace)
├── AGENTS.md
├── Assets/_Chassis  _Game  _Content
└── ...
```

Taşıma kuralları: `AOS_*` orijinalleri `agents/_arsiv/aos-chatgpt/`e; `orchestrator/` klasörü Faz 3'e kadar yalnızca README içerir; eşikler tek yerde (`ops/esikler.md`) yaşar, başka dosyaya kopyalanmaz (link verilir).

**İki kişilik depo kuralı (v1.1):** `main_analysis.md` ve `ops/esikler.md` yalnızca Nazım onayıyla değişir. `radar/`, `games/*/test/` ve `ops/kill-log.md` analistin yazma alanıdır. Karar hafızası tektir; herkes kendi kopyasında ayrı gerçek yaşatmaz.

---

## 5. Eşikler — Tek Doğruluk Kaynağı (değişmedi)

| Metrik / Kural | Eşik |
|---|---|
| CPI (test) | < $0.40 hedef · < $0.30 mükemmel |
| Reklam CTR | > %1.5–2 |
| D1 retention | > %45 |
| D7 retention | > %15–20 |
| İlk gün playtime | > 15–20 dk |
| Yeşil ışık | Cetvel toplam ≥ 50/70 **ve** hiçbir kriter 1–2 değil (veto) |
| Geliştirme tavanı | ≤ 2 hafta / prototip |
| GameBrief kapısı | Completion score ≥ 90 |
| Karar mantığı | Hepsi yeşil → BÜYÜT · tek zayıf → DÜZELT (1 hak) · çoklu kırmızı → ÖLDÜR |

Kayıtlı istisna: Toy Pile 53/70 ile bilinçli override — sigortası M6 testi. Kural değişmedi; istisna kayıt altında ve tekrarı otomatik değildir.

---

## 6. Riskler ve Panzehirler

1. **Fabrika tuzağı (orchestrator hevesi):** SDK oynamak oyun çıkarmaktan tatlıdır. Panzehir: Faz 3 tetik koşulu; `orchestrator/` klasörü kilitli.
2. **İkinci "Machine 0" sızıntısı:** Dış AI oturumlarından (ChatGPT vb.) gelen her doküman entegrasyondan önce bu dosyanın isimlendirmesine çevrilir; çeviri yapılmadan repoya giremez. Kural kişiden bağımsızdır — analistin dış oturumları dahil.
3. **Play Console gecikmesi:** Yeni hesap kısıtları store sayfasını geciktirirse CTR-proxy fallback (§2 Faz 1).
4. **Zaman bütçesi:** 10 gün sıkışırsa kreatif sayısı kısılır; mekanik kapsam ve tarih sabittir.
5. **Model/fiyat churn:** Harcama öncesi güncel doğrulama; hardcoded model adı koda girmez.
6. **Oyuna âşık olma:** Toy Pile'a override verildi diye ikinci tavizin gerekçesi yapılamaz. M7 çıktısı tartışılmaz.
7. **Karar difüzyonu (komite tuzağı):** İki kişi = iki oy değildir. Her kapının tek A'sı vardır (§1.4); "ikimiz de ikna olalım" beklemek kill kararlarını geciktirir.
8. **"İki kişiyiz, kapsam büyüsün" tuzağı:** Ekstra kapasite oyun boyutuna değil, hat hızına gider. 2 hafta tavanı ve şasi-lite kararı aynen geçerli.
9. **Ortaklık belirsizliği:** İki kademeli kapı — G10 (test) için asgari yazılı mutabakat: kim ödüyor + gelir modelinin yayından önce netleşeceği taahhüdü; M8 (yayın) için tam anlaşma: gelir/gider/IP. Asgarisi yoksa test tarihi kayar, para kaymaz. Arkadaşlık ile muhasebe ayrı defterlerdir.

---

## 7. İlk 72 Saat (bugünden itibaren)

1. **Bu dosyayı onayla** — §1.1'deki 5 karar + §1.4 rol tablosu. Onay = "main_analysis v1.1 onay" yazman yeterli.
2. **Analist onboarding'i:** bu dosya + `docs/01` + eşikler okunur; saat bütçesi ve gelir/gider modeli netleşir, §1.4'teki [BELİRLENECEK] alanlar doldurulur (yazılı).
3. Repo yapısını kur (§4); `AOS_*` dosyalarını `agents/_arsiv/`e taşı; `ops/esikler.md` + `ops/roller.md` oluştur.
4. **G1 — iki hat aynı anda:** Nazım Antigravity Prompt 1'i çalıştırır (akşam cihaz build'i); analist ilk radar taramasına ve rakip kreatif analizine başlar.

→ Aktif makineler: **M5 (Kod — Nazım)** ∥ **M1 (Radar — Analist)**. Sıradaki insan kapısı: **G10 bütçe onayı** ($100–200, tek imza: Nazım).
