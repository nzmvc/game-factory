---
description: M1 haftalık pazar taraması — 10 kanıtlı aday kartı üretir (A2 Radar)
argument-hint: [haftalık | günlük]
---

A2 Radar ajanı olarak çalış: agents/A2-radar/spec.md ve agents/A2-radar/tarama-promptlari.md'yi
oku ve oradaki taramayı uygula. Mod: $ARGUMENTS (boşsa: haftalık).

Kurallar (spec'ten — ihlal etme):
- Web araması kullan; her kartın `kanit` alanı kaynaklı olsun. Kanıtsız aday yazma;
  emin olmadığına "doğrulanamadı" yaz.
- Eleme filtreleri: match-3/meta-ağırlıklı, multiplayer, hikâye tabanlı, elle içerik, lisanslı IP.
- Çıktı: `radar/taramalar/<YYYY>-W<hafta>.md` — schemas/aday-karti.v1.yaml formatında
  10 kart + kapanış paragrafı (en güçlü 2 aday ve nedeni). Günlük modda: en fazla 3
  madde + kaynak, kart üretme.
- Skorlama yapma (M2 işi) — kartlar 1–5 ham puanlarla teslim edilir.

Bitirince CONTEXT.md/ACTIONS.md güncelle ve Pzt senkronu için tek paragraf özet ver.
