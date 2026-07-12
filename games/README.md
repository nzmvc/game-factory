# games/ — Oyun Kayıt Defteri

Fabrikadan geçen her oyunun karar/doküman kaydı. **Kod burada yaşamaz** — her oyunun
kendi Unity reposu vardır ([ADR-0001](../docs/decisions/ADR-0001-iki-repo-modeli.md)).

## Kayıt defteri

| Oyun | Durum | Hat konumu | Unity repo | Brief | Karar |
|---|---|---|---|---|---|
| [Toy Pile](toy-pile/) | 🟢 Aktif (Faz 1) | M4 🟡 (asset kaplama) | `game-toy-pile` | [gdd-lite.md](toy-pile/gdd-lite.md) | Yeşil ışık 53/70 override (2026-07-11) |

Durumlar: 🟢 Aktif · 🔵 BÜYÜT (soft launch/yayın) · 🟡 DÜZELT (tek hak) · ⚫ ÖLDÜRÜLDÜ (kill-log'a bakınız) · ⚪ Beklemede

## Oyun klasörü standardı

```
games/<oyun-adi>/
├── README.md        # durum kartı: hat konumu, linkler, kapı geçmişi
├── brief.md         # GameBrief (schemas/gamebrief.v1.json şemasına uygun)
├── gdd.md           # M3 çıktısı (şablon: templates/game-docs/04-GDD.md)
├── test/            # M6 kreatif brief'leri + kampanya sonuçları + M7 karar raporu
└── aso/             # M8 store paketi (yalnız BÜYÜT sonrası)
```

Yeni oyun açma prosedürü: [WORKFLOW.md](../WORKFLOW.md) §3 veya `/new-game <isim>`.
Oyun öldürüldüğünde klasör **silinmez**; README'sine karar linki eklenir, dersler
[ops/kill-log.md](../ops/kill-log.md)'a işlenir.
