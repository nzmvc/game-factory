# ADR-0001 — Fabrika Reposu ↔ Oyun Repoları Ayrımı

**Tarih:** 2026-07-12 · **Durum:** Taslak (Nazım onayı bekliyor) · **Karar sahibi:** Nazım

## Bağlam
Fabrika onlarca oyun üretecek. Süreç/karar dokümanları ile Unity projeleri aynı repoda
tutulursa: repo ağırlaşır (binary asset'ler), ajan bağlamı kirlenir (kod ajanı strateji
dosyalarını, strateji ajanı kod dosyalarını taşır), oyun ölünce tarihçe karışır.

## Seçenekler
1. **Monorepo** — her şey tek yerde; + tek clone, − ağır, ajan yetki sınırları bulanık.
2. **İki katman: fabrika reposu + oyun başına Unity reposu** — + hafif karar hafızası,
   net yetki sınırı, ölen oyun arşivi kolay; − çapraz link disiplini gerekir.

## Karar
Seçenek 2: **GameFactory** (bu repo) süreç/ajan/karar/şema/şablon taşır; her oyun
kendi Unity reposunda yaşar (`game-<isim>`). Fabrikada oyun başına yalnız
`games/<oyun>/` kayıt klasörü tutulur.

## Gerekçe
main_analysis §4'te zaten onaylanan model; A5 dışındaki hiçbir ajanın Unity içeriğine
ihtiyacı yok. Claude Code oturumları da ayrışır: fabrika oturumu doküman üretir,
oyun oturumu kod üretir — iki farklı CLAUDE.md anayasası.

## Sonuçlar
- Oyun repoları templates/game-docs/ setiyle açılır; çapraz referanslar göreli değil
  repo adıyla verilir (örn. `game-toy-pile/docs/14-BACKLOG.md`).
- Bu repoda oyun kodu yazmak yasaktır (CLAUDE.md'de kayıtlı).
