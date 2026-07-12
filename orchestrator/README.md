# orchestrator/ — KİLİTLİ (Faz 3)

> ⛔ **Faz 3 tetiklenmeden bu klasöre kod yazılmaz.**
> SDK oynamak oyun çıkarmaktan tatlıdır; bu klasörün kilidi fabrika tuzağına karşı panzehirdir.
> Gerekçe: [ADR-0004](../docs/decisions/ADR-0004-once-prompt-sonra-sdk.md)

## Tetik koşulu (ikisi birden sağlanmalı)

1. Hattan en az **2 prototip** geçti, **VE**
2. Radar rutini **3 hafta üst üste elle aksadı** VEYA **ayda 2+ prototip** ritmi hedefleniyor.

## Faz 3 geldiğinde yapılacaklar

- SDK seçimi: Claude Agent SDK ↔ OpenAI Agents SDK (Faz 2 A/B sonucuna göre).
- Ajan spec'leri (`agents/`) aynen taşınır — spec değişmez, işletim değişir.
- Tohum: [archive/aos-gemini/AOS_ORCHESTRATOR.py](../archive/aos-gemini/AOS_ORCHESTRATOR.py),
  üç zorunlu ameliyatla:
  1. Simüle `fetch_live_market_data` → gerçek kaynaklar (resmî API'ler; ToS ihlali scraping yok).
  2. 10'luk cetvel → 70'lik cetvel + veto (koddan değil, [ops/esikler.md](../ops/esikler.md)'den okunur).
  3. **İnsan kapıları koda gömülür:** bütçe/yayın adımında agent durur, onay bekler. **Auto-spend yok.**
- Model adı koda hardcode edilmez; model seçimi konfigürasyondan.
