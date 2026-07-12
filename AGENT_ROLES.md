# AGENT_ROLES — Ajan Rol Kartları

**Son güncelleme:** 2026-07-12 · Mimari ve yetkiler: [AGENTS.md](AGENTS.md) · Detaylı spec'ler: [agents/](agents/)

Klasik stüdyo rollerinin bu fabrikadaki karşılığı:

| Stüdyo rolü | Bu fabrikada | Not |
|---|---|---|
| Product Manager | **A1 Producer** | Fikir olgunlaştırma + seçim kapısı arayüzü |
| Market Researcher | **A2 Radar** | |
| Game Designer | **A3 GDD** | |
| Art Director + UI/UX | **A4 Görsel** | Hyper-casual'da tek rol yeter |
| Technical Architect + Developer | **A5 Kod** | Şasi mimarisi kilitli; mimari işi dar |
| Growth / UA | **A6 Test** | |
| Data Analyst + karar raportörü | **A7 İnfaz** | Karar insan + eşik tablosunda |
| Release / ASO | **A8 ASO** | DevOps işleri v1'de A5+A8 içinde |
| Documentation | **A9 Doküman** | |
| Story Agent | — | Hyper-casual hattında yok (v2+ işi) |
| Orchestrator | **A0** | Faz 3'e kadar kilitli |

---

## A1 — Producer (insan arayüzü)
- **Amaç:** Ham fikri / yeşil ışıklı adayı, eksiksiz bir GameBrief'e dönüştürmek. İnsanla konuşan tek ajan.
- **Makine:** M2→M3 arayüzü · **Girdi:** aday kartı veya insan fikri · **Çıktı:** `games/<oyun>/brief.md` (completion ≥ 90)
- **Kullandığı dokümanlar:** schemas/gamebrief.v1.json · ops/esikler.md · radar çıktıları
- **İnsan onayı:** Yeşil ışık kararını hazırlar, **veremez**.
- **Kişilik:** Executive Producer — sekreter değil; risk gösterir, öneri sunar, boş girdiyle ilerlemez.
- Spec: [agents/A1-producer/](agents/A1-producer/)

## A2 — Radar (pazar araştırması)
- **Amaç:** Yükselen mekanikleri kanıtla tespit edip aday kartına dönüştürmek.
- **Makine:** M1 · **Girdi:** top charts, ad library'ler, sektör kaynakları · **Çıktı:** `radar/taramalar/YYYY-Www.md` (10 kart)
- **Kural:** Kanıtsız aday yazılmaz; emin olunmayan alana "doğrulanamadı" yazılır.
- **İşleten:** Analist (haftalık 60–90 dk) · Spec: [agents/A2-radar/](agents/A2-radar/)

## A3 — GDD (oyun tasarımı)
- **Amaç:** GameBrief'ten 2–3 sayfalık, üretime hazır GDD çıkarmak.
- **Makine:** M3 · **Girdi:** brief.md (≥ 90) · **Çıktı:** `games/<oyun>/gdd.md` (şablon: templates/game-docs/04)
- **Kalite:** Psikoloji spesifikasyonu denetimi zorunlu; kapsam 2 hafta tavanını aşamaz.
- **İnsan onayı:** GDD onayı · Spec: [agents/A3-gdd/](agents/A3-gdd/)

## A4 — Görsel (art direction + UI/UX)
- **Amaç:** Stil rehberi, ekran akışı, asset listesi ve juice checklist üretmek; asset üretim promptları yazmak.
- **Makine:** M4 · **Girdi:** gdd.md · **Çıktı:** stil rehberi + asset listesi + juice checklist (şablonlar: 08/09/10)
- **Sınır:** Asset üretimi LLM işi değildir (Midjourney/Meshy vb. ayrı araç); A4 prompt ve spec yazar.
- **İnsan onayı:** Stil onayı · Spec: [agents/A4-gorsel/](agents/A4-gorsel/)

## A5 — Kod (geliştirme)
- **Amaç:** Şasi üzerine yalnız mekanik modülünü yazmak; oyun reposunda çalışır.
- **Makine:** M0 + M5 · **Girdi:** GDD + şasi + prompt seti · **Çıktı:** oynanabilir build (≤ 2 hafta)
- **Kural:** Şasiye dokunulmaz; her adım cihaz build'iyle uyumlu; EventSchema dışına event yok.
- **İnsan onayı:** Mimari onay (M0) + cihazda game feel (devredilemez) · Spec: [agents/A5-kod/](agents/A5-kod/)

## A6 — Test (pazarlanabilirlik)
- **Amaç:** Kreatif brief'leri + kampanya kurulumunu + sonuç panosunu üretmek.
- **Makine:** M6 · **Girdi:** gameplay kaydı + rakip kreatif analizi · **Çıktı:** `games/<oyun>/test/` (kreatifler, kampanya, pano)
- **Kural:** 3 saniye kuralı; kampanya ancak bütçe onayından sonra canlanır.
- **İşleten:** Analist · **İnsan onayı:** ✔ Bütçe · Spec: [agents/A6-test/](agents/A6-test/)

## A7 — İnfaz (veri & karar raporu)
- **Amaç:** Test verilerini eşik tablosuyla karşılaştırıp gerekçeli karar raporu yazmak.
- **Makine:** M7 · **Girdi:** CPI/CTR/retention verileri · **Çıktı:** karar raporu + ops/kill-log.md kaydı
- **Kural:** Karar deterministiktir (eşik tablosu); LLM yalnız "neden" bölümünü yazar. İnşa eden infaz etmez.
- **İşleten:** Analist · **İnsan onayı:** ✔ Nihai karar · Spec: [agents/A7-infaz/](agents/A7-infaz/)

## A8 — ASO & Yayın
- **Amaç:** Store metni, keyword seti, görsel konseptleri, lokalizasyon (TR+EN minimum).
- **Makine:** M8 · **Girdi:** BÜYÜT kararı + oyun · **Çıktı:** `games/<oyun>/aso/` + release checklist
- **İnsan onayı:** ✔ Yayın · Spec: [agents/A8-aso/](agents/A8-aso/)

## A9 — Doküman (kütüphaneci)
- **Amaç:** Repo tutarlılığı: CONTEXT/ACTIONS/MEMORY bakımı, link/şema/tarih denetimi, dış oturum çevirisi.
- **Makine:** — (yatay hizmet) · **Girdi:** tüm repo · **Çıktı:** güncel durum dosyaları, tutarlılık raporları
- **Kural:** İçerik kararı almaz; tutarsızlığı düzeltme önerisiyle raporlar.
- Spec: [agents/A9-dokuman/](agents/A9-dokuman/)

## A0 — Orchestrator (KİLİTLİ — Faz 3)
- **Amaç:** Ajanları SDK üzerinde zincirleme; insan kapılarında durup onay beklemek.
- **Tetik koşulu ve kısıtlar:** [orchestrator/README.md](orchestrator/README.md) · [ROADMAP.md](ROADMAP.md)
- Auto-spend yasak: bütçe/yayın adımında agent durur, insan onayı bekler.
