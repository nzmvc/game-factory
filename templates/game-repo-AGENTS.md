# <OyunAdı> — Ajan Kuralları

<!-- ŞABLON: repo köküne AGENTS.md olarak kopyala (Antigravity ve diğer kod ajanları için).
     İçerik CLAUDE.md ile aynı kuralları paylaşır; iki dosyada da güncel tut ya da
     birinden diğerine link ver. -->

## Proje
<Mekanik + twist tek cümle>. Unity LTS, URP, yalnızca portre, tek parmak.

## Mimari kurallar
- Klasörler: `Assets/_Chassis` (dokunulmaz) · `Assets/_Game` · `Assets/_Content`.
- Assembly definition'lar: Chassis.Core, Chassis.Juice, Chassis.UI, `Game.<Mekanik>`.
- Tip güvenli merkezi EventBus (struct event); god object yasak.
- SDK'lar interface arkasında (IAdsProvider, IAnalyticsProvider); şasi-lite'ta
  YALNIZCA Dummy/Console implementasyonları.
- IGameMechanic: Initialize(LevelData), StartLevel(), Tick(float dt), EndLevel(LevelResult).
- Dengeleme değerleri GameConfig ScriptableObject'te; koda sabit gömme.
- Analytics event'leri snake_case; `docs/02-EVENT_SCHEMA.md` dışına event yok.

## Çalışma şekli
- Her prompt öncesi kısa plan sun, onay bekle. Onaysız geniş refactor yok.
- Bir prompt = bir iş paketi; sonunda değişen dosyalar + commit mesajı önerisi.
- Unity Editor işleri "İNSAN GÖREVİ" başlığıyla ayrı listelenir.

## Yasaklar
- Multiplayer, meta katman, gerçek reklam/IAP SDK'sı, sunucu (v2).
- Editor dışında çalışmayan kod bırakma; her adım cihaz build'iyle uyumlu.
