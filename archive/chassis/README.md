# chassis/ — Eski Kök CLAUDE.md ve AGENTS.md

**Arşivlenme:** 2026-07-12 · **Taşıyan:** framework kurulumu (eski konum: repo kökü)

## Neden arşivde?

Bu iki dosya **Unity şasi/oyun projesinin** kurallarını anlatıyordu (asmdef'ler,
IGameMechanic, EventBus, Toy Pile mekaniği) ama **fabrika reposunun kökünde**
duruyordu. Fabrika reposunda oyun kodu yazılmaz ([ADR-0001](../../docs/decisions/ADR-0001-iki-repo-modeli.md));
Claude Code bu repoda açıldığında şasi kurallarını yüklemesi yanlış bağlamdı.

## Yerine ne geldi?

- Fabrika kökü: yeni [CLAUDE.md](../../CLAUDE.md) (fabrika anayasası) ve
  [AGENTS.md](../../AGENTS.md) (ajan mimarisi).
- Şasi kuralları şablonlaştı: [templates/game-repo-CLAUDE.md](../../templates/game-repo-CLAUDE.md)
  ve [templates/game-repo-AGENTS.md](../../templates/game-repo-AGENTS.md) — her yeni
  oyun reposu bunları kopyalar. İçerikleri buradaki orijinallerin genelleştirilmiş hali.
- Toy Pile'a özgü kısımlar zaten `game-toy-pile` reposunda yaşıyor.
