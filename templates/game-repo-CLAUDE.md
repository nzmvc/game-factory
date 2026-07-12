# <OyunAdı> — Proje Bağlamı (Claude Code)

<!-- ŞABLON: repo köküne CLAUDE.md olarak kopyala, <...> alanlarını doldur. -->

## Amaç
Hyper/hybrid-casual mobil oyun: **<mekanik adı + twist>**.
Bu repo GameFactory şasisi + tek mekanik modülü + görsel kaplamadır.
Şasi oyun DEĞİLDİR; oyundan bağımsız her şey (reklam, analytics, IAP, kayıt, UI, juice) şasidedir.

## Teknik kurallar
- Unity LTS, URP, yalnızca portre, tek parmak input varsayımı.
- Klasörler: `Assets/_Chassis` (dokunulmaz çekirdek) · `Assets/_Game` (aktif mekanik
  modülü) · `Assets/_Content` (level data, ScriptableObject'ler).
- Assembly definition'lar: Chassis.Core, Chassis.Juice, Chassis.UI (+ tam şaside
  Chassis.Ads, Chassis.Analytics, Chassis.IAP) ve `Game.<Mekanik>`.
- God object yasak; sistemler arası iletişim tip güvenli merkezi EventBus (struct event).
- Üçüncü parti SDK'lar interface arkasında (IAdsProvider, IAnalyticsProvider) —
  SDK değişimi tek dosya işi. Şasi modu: <lite (Dummy/Console) | full>.
- IGameMechanic sözleşmesi: Initialize(LevelData) · StartLevel() · Tick(float dt) · EndLevel(LevelResult).
- Tüm dengeleme değerleri GameConfig/RemoteConfig'ten; koda sabit gömme.
- Analytics event'leri snake_case; `docs/02-EVENT_SCHEMA.md`'de kayıtlı olmayan event gönderilemez
  (fabrika standardı: GameFactory `schemas/event-schema.md`).

## Çalışma şekli
- Her prompt öncesi kısa plan sun, onay bekle. Onaysız geniş refactor yok.
- Bir prompt = bir iş paketi; sonunda değişen dosya listesi + commit mesajı önerisi.
- Unity Editor'de yapılacakları "**İNSAN GÖREVİ**" başlığıyla ayrı listele.
- Derleme hataları Unity Console'dan yapıştırılır; minimal diff'le düzelt.
- Geliştirme tavanı: **≤ 2 hafta efor** — kapsam büyüten öneri = "bu v2 işi".

## Yasaklar
- Multiplayer, meta katman, sunucu, turnuva (v2).
- Gerçek reklam/IAP SDK'sı (BÜYÜT kararı öncesi; interface + dummy kullan).
- Banner reklam varsayılan kapalı.
- Editor dışında çalışmayan kod bırakma; her adım cihaz build'iyle uyumlu.
- `Assets/_Chassis` içeriğini oyuna göre değiştirmek.

## Fabrika bağlantısı
Süreç/karar/eşik soruları bu repoda çözülmez → GameFactory reposu
(CONTEXT.md, ops/esikler.md, WORKFLOW.md). Oyunun hat durumu: GameFactory `games/<oyun>/README.md`.
