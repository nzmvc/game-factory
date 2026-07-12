# aos-gemini/ — Gemini AOS Oturumu Orijinalleri

**Arşivlenme:** 2026-07-12 · **Taşıyan:** framework kurulumu (eski konum: `_analiz/gemini/`)
Not: setin kendi indeks dosyası korunmak için yeniden adlandırıldı → [AOS_ORIJINAL_README.md](AOS_ORIJINAL_README.md)

## Neden arşivde?

Bu set onaylı fabrikayla **çelişiyor** ve düzeltilmeden kullanılamaz:

- `SYSTEM_ARCHITECTURE.md` — "9 makineli" hat ve farklı model matrisi; onaylı M0–M8
  tanımlarıyla ve model stratejisiyle uyuşmuyor.
- `GAME_PRODUCER_SPEC.md` — A1'in OpenAI Assistant sürümü; değerli desenleri
  [agents/A1-producer/spec.md](../../agents/A1-producer/spec.md)'e işlendi.
- `CLAUDE.md` — fabrika şasi kurallarıyla çelişen ayrı bir mimari dayatıyor
  (SO event kanalları vs EventBus, 150 satır limiti, farklı klasör düzeni).
- `AOS_ORCHESTRATOR.py` — **çalışır ama kurguyla karar verir:** `fetch_live_market_data`
  simüle veri döndürür, içindeki 10'luk cetvel onaylı 70'lik cetvelle çelişir,
  model hardcoded. Üretim kararında asla kullanılmaz.

## Gelecek değeri

Orchestrator, Faz 3 tohumudur — kullanım ön koşulları: [orchestrator/README.md](../../orchestrator/README.md)
(gerçek veri kaynakları + cetvelin ops/esikler.md'den okunması + koda gömülü insan kapıları).

Kural: buradan içerik alınacaksa önce fabrika terminolojisine çevrilir (ADR-0002).
