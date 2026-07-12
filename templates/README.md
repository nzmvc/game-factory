# templates/ — Şablonlar

Standartın kaynağı ([ADR-0005](../docs/decisions/ADR-0005-sablon-tabanli-oyun-dokumantasyonu.md)).
Şablon değişikliği = standart değişikliği → ADR gerekir.

| Şablon | Ne için |
|---|---|
| [game-docs/](game-docs/) | Yeni oyun reposunun 00–15 doküman seti |
| [game-repo-CLAUDE.md](game-repo-CLAUDE.md) | Oyun reposu Claude Code anayasası |
| [game-repo-AGENTS.md](game-repo-AGENTS.md) | Oyun reposu ajan kuralları (Antigravity vb. için) |

## Kullanım (yeni oyun açılışı)

1. Oyun Unity reposu oluşturulur (`game-<isim>`), URP + Mobile şablonu.
2. `game-docs/` seti oyun reposunun `docs/` klasörüne kopyalanır; her dosyadaki
   `<...>` alanları doldurulur, doldurulamayanlar "TBD — hangi aşamada dolacağı" notuyla bırakılır.
3. `game-repo-CLAUDE.md` → repo köküne `CLAUDE.md`, `game-repo-AGENTS.md` → `AGENTS.md`
   olarak kopyalanır ve oyuna uyarlanır (mekanik adı, asmdef adı).
4. Fabrika tarafında `games/<oyun>/` kaydı açılır (bkz. [WORKFLOW.md](../WORKFLOW.md) §3).

Kural: şablondan bilinçli sapma, oyun dokümanında "**Bilinçli sapma:**" notuyla kayıt edilir
(örnek: Toy Pile şasi-lite kararı). Sapma iyi çalışırsa A9 onu ADR'yle şablona geri işler.
