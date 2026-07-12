# ADR-0003 — Docs-as-Code ve Tek Doğruluk Kaynağı Hiyerarşisi

**Tarih:** 2026-07-12 · **Durum:** Taslak (Nazım onayı bekliyor) · **Karar sahibi:** Nazım

## Bağlam
Doküman analizi ([02-toy-pile-dokuman-analizi](../strategy/02-toy-pile-dokuman-analizi.md))
üç dosyanın aynı anda "tek doğruluk kaynağı" iddia ettiğini gösterdi (main_analysis,
00-DEVFLOW, 14-BACKLOG). "SSOT" kavramı kapsam belirtilmeden kullanılınca anlamını yitiriyor.

## Seçenekler
1. Tek dev dosya her şeyin kaynağı — − pratikte güncellenemez, ajan bağlamını şişirir.
2. **Kapsamlı SSOT: her bilgi türünün tek ve ayrı kaynağı + açık çelişki hiyerarşisi.**

## Karar
Her bilgi türü tek dosyada yaşar, diğerleri link verir:

| Bilgi | Tek kaynak |
|---|---|
| Metrik eşikleri / kapı kuralları | ops/esikler.md |
| Fabrika modeli + değişmez kurallar | GAME_FACTORY.md |
| Süreç akışı | WORKFLOW.md |
| Ajan mimarisi/yetkiler | AGENTS.md (+ agents/*/spec.md) |
| İnsan rolleri/RACI | HUMAN_ROLES.md + ops/roller.md |
| Anlık durum | CONTEXT.md |
| Kararlar | DECISIONS.md + docs/decisions/ |
| Öğrenilenler | MEMORY.md (+ ops/kill-log.md) |
| Veri sözleşmeleri | schemas/ |

Çelişki hiyerarşisi: `ops/esikler.md` > `GAME_FACTORY.md` > `WORKFLOW.md`/`AGENTS.md`
> diğer kök dosyalar > `docs/strategy/*`. Çelişki bulan ajan **raporlar**, sessizce seçmez.

## Gerekçe
Docs-as-Code'un temel kuralı: kopya bilgi = bölünmüş gerçek. main_analysis'in
"eşikler tek yerde yaşar, kopyalanmaz" kuralının tüm repoya genellenmesi.

## Sonuçlar
- main_analysis.md "tek doğruluk kaynağı" rolünü kök dosyalara devreder;
  docs/strategy/ altında onaylı kuruluş stratejisi olarak yaşar.
- Mutlak/`file:///` link yasağı; tüm linkler göreli (standart: docs/standards/).
