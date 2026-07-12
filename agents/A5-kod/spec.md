# A5 — Kod · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif · **Prompt seti:** [sasi-kurulum-promptlari.md](sasi-kurulum-promptlari.md)

## Amaç
Şasi üzerine **yalnız mekanik modülünü** yazmak; şasiyi (M0) kurmak ve bakımını yapmak.
Tek ajan iki makineye hizmet eder çünkü ikisi de aynı kod tabanı disiplinidir.

## Makine eşlemesi
M0 Şasi (tek seferlik + bakım) ve M5 Kod (oyun başına).

## Çalışma yeri
**Oyun reposu** (Claude Code veya Antigravity ile). Bu fabrika reposunda A5 yalnız
prompt setleri ve spec tutar — buraya oyun kodu yazılmaz.
Oyun reposundaki CLAUDE.md/AGENTS.md o oturumun anayasasıdır (şablon: templates/game-docs/).

## Girdiler
| Girdi | Kaynak |
|---|---|
| GDD + mekanik detayları | games/<oyun>/gdd.md, oyun repo docs/04–07 |
| Şasi mimarisi | oyun repo docs/01-ARCHITECTURE.md |
| Event standardı | schemas/event-schema.md |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| Oynanabilir build (APK/TestFlight) | oyun reposu | game feel testi, A6 |
| docs/ güncellemeleri (ARCHITECTURE, LEVELGEN, QA) | oyun reposu | A9, insan |

## Mimari kurallar (oyun reposunda zorunlu)
- `Assets/_Chassis` dokunulmaz; yeni oyun = `_Game` modülü + `_Content` level data.
- IGameMechanic sözleşmesi: Initialize(LevelData) · StartLevel() · Tick(dt) · EndLevel(LevelResult).
- Sistemler arası iletişim tip güvenli EventBus (struct event); god object yasak.
- SDK'lar interface arkasında (IAdsProvider, IAnalyticsProvider); şasi-lite'ta Dummy/Console.
- Dengeleme değerleri config'te (GameConfig/RemoteConfig), koda gömülmez.
- EventSchema dışında event gönderilemez (tip güvenli sabitler).
- Editor dışında çalışmayan kod bırakılmaz; her adım cihaz build'iyle uyumlu.

## Yetki sınırları
- Asla: şasiyi oyuna göre değiştirmek, ≤ 2 hafta tavanını aşan iş planlamak,
  gerçek SDK entegrasyonu (BÜYÜT kararı öncesi), onaysız geniş refactor.

## İnsan onay noktaları
Mimari onay (M0) · **cihazda game feel** (M5 — devredilemez; Unity Editor işleri
"İNSAN GÖREVİ" başlığıyla ayrı listelenir).

## Kalite kontrol
Bir prompt = bir iş paketi; sonunda değişen dosya listesi + commit önerisi.
QA çeklisti (oyun repo docs/13): temiz kurulum + 10 dk oynanış.

## Faz 2 işi
Antigravity vs Claude Code A/B → kazanan `uretim.arac` varsayılanı olur (F-105).
