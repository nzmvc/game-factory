# aos-chatgpt/ — ChatGPT AOS Oturumu Orijinalleri

**Arşivlenme:** 2026-07-12 · **Taşıyan:** framework kurulumu (eski konum: `_analiz/`)
**Güncelleme:** 2026-07-12 · `AOS_ORCHESTRATOR_SPEC.md` eklendi (kaynak: `game-toy-pile/_analiz/`,
oyun reposunda tek kopyaydı — ADR-0001 gereği fabrika reposuna taşındı)

## Neden arşivde?

`AOS_GameProducer_Analysis_v0.2.md`, ChatGPT oturumunda tasarlanan "AI Native Game
Studio OS" analizi. Onaylı fabrikayla çakışan 5 nokta [main_analysis](../../docs/strategy/main_analysis.md)
§1.1'de karara bağlandı (Machine 0 isim çarpışması, fikir-öncelikli akış, çifte cetvel,
paralel şema, erken otomasyon).

`AOS_ORCHESTRATOR_SPEC.md`, aynı oturumun A0 Orkestratör Ajanı için yazdığı detaylı
davranış spesifikasyonu ("Machine" isimlendirmesi, `docs/BACKLOG.md` tekil SSOT
iddiası, kendi eşik/karar mantığı — onaylı `ops/esikler.md` ile çelişiyor).

## Nesi hâlâ değerli? (nereye işlendi)

- Conversation State + User Input Validation + Discovery/Validation/Brief modları +
  Completion Score kalite kapısı + Executive Producer kişiliği →
  [agents/A1-producer/spec.md](../../agents/A1-producer/spec.md) (Faz 2'de v2 talimatına girecek)
- GameBrief ortak veri sözleşmesi fikri → [schemas/gamebrief.v1.json](../../schemas/gamebrief.v1.json)
- 20. bölümdeki doküman listesi (PRD, Agent Specification, Message Protocol) → Faz 3 işi
- `AOS_ORCHESTRATOR_SPEC.md`'nin handoff/quality-gate akışı ve kill kriterleri kontrolü →
  Faz 3'te [orchestrator/README.md](../../orchestrator/README.md) tohumuna referans

Kural: buradan içerik alınacaksa önce fabrika terminolojisine çevrilir (ADR-0002).
