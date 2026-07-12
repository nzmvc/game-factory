# agents/ — Ajan Spec'leri

Her ajan bir klasördür: `A<numara>-<isim>/`. İçinde en az bir `spec.md`
(rol kartının tam hali) ve varsa işletim promptları bulunur.

**İlke: önce prompt, sonra kod.** Faz 1–2'de bu spec'ler LLM oturumlarında elle
işletilir; Faz 3'te SDK orkestrasyonuna aynen taşınır. Mimari kurallar (haberleşme,
yetki matrisi, doğrulama): [AGENTS.md](../AGENTS.md) · Özet kartlar: [AGENT_ROLES.md](../AGENT_ROLES.md)

| Klasör | Makine | İşleten (Faz 1–2) | İçerik |
|---|---|---|---|
| [A1-producer/](A1-producer/) | M2→M3 arayüzü | Nazım (Claude Projesi) | spec + Claude Projesi talimatı |
| [A2-radar/](A2-radar/) | M1 | Analist | spec + haftalık/günlük tarama promptları |
| [A3-gdd/](A3-gdd/) | M3 | Nazım | spec |
| [A4-gorsel/](A4-gorsel/) | M4 | Nazım | spec |
| [A5-kod/](A5-kod/) | M0+M5 | Nazım (Claude Code/Antigravity) | spec + şasi kurulum prompt seti |
| [A6-test/](A6-test/) | M6 | Analist | spec |
| [A7-infaz/](A7-infaz/) | M7 | Analist | spec |
| [A8-aso/](A8-aso/) | M8 | Analist hazırlar, Nazım onaylar | spec |
| [A9-dokuman/](A9-dokuman/) | — (yatay) | Claude Code | spec |
| A0 orchestrator | — | ⛔ KİLİTLİ | [orchestrator/README.md](../orchestrator/README.md) |

Yeni ajan ekleme prosedürü: [AGENTS.md](../AGENTS.md) §5 · Şablon: [_sablon/spec.md](_sablon/spec.md)
