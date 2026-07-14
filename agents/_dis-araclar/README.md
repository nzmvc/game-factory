# Dış Araç Talimatları — Manus · ChatGPT · Claude Desktop

**Son güncelleme:** 2026-07-14 · İlgili kural: [AGENTS.md](../../AGENTS.md) §4 "Dış oturum kuralı"

Faz 1–2'de ajanlar LLM oturumlarında elle işletilir. Bu klasör, fabrika dışındaki
araçlarda oturum açarken kullanılacak **yapıştırılmaya hazır talimatların tek kaynağıdır**.

## Araç → görev eşlemesi

| Araç | Dosya | Uygun işler | İşleten |
|---|---|---|---|
| Claude Desktop (Proje) | [claude-desktop.md](claude-desktop.md) | A1 Producer şapkası: seçim, GDD, görsel, karar paketi — repo erişimli ana sohbet oturumu | Nazım |
| ChatGPT (Proje / Custom GPT) | [chatgpt.md](chatgpt.md) | Taslak atölyesi: GDD eskizi, kreatif brief, ASO metni, rakip özeti | Nazım / Analist |
| Manus (otonom görev ajanı) | [manus.md](manus.md) | Web araştırması: M1 radar taraması, rakip kreatif analizi, kısıt doğrulama | Analist |

## Ortak değişmez kurallar (üç araç için)

1. **Dış çıktı doğrudan repoya girmez.** Önce fabrika terminolojisine ve şemalara
   uygunluk denetlenir (M/A katmanları, şema alanları); denetim A9 / Claude Code
   oturumunda yapılır. Gerekçe: [MEMORY.md](../../MEMORY.md) "Machine 0 çakışması" dersi.
2. **Eşik kopyaları sürüm damgalıdır.** Talimat bloklarındaki eşikler
   [ops/esikler.md](../../ops/esikler.md)'nin damgalı kopyasıdır — dış araçlar repo
   linki izleyemediği için "kopyalanmaz, link verilir" kuralına **bilinçli istisnadır**.
   esikler.md değişirse bu klasördeki üç dosya da aynı oturumda güncellenir.
3. **Karar ve para bu araçlarda yaşamaz.** Hiçbir dış oturum kampanya başlatamaz,
   hesap açamaz, harcama yapamaz, insan kapısını "geçildi" sayamaz.

## Bakım

- `agents/A1-producer/instruction.md` (eski Claude Projesi talimatı) 2026-07-14'te
  güncellenerek [claude-desktop.md](claude-desktop.md)'ye taşındı; eski dosya işaretçi olarak durur.
- Talimat metni değişikliği standart değişikliği değildir (ADR gerekmez); ancak eşik
  veya değişmez kural bölümüne dokunan her düzenleme esikler.md / GAME_FACTORY.md §4
  ile senkron olmak zorundadır.
