# A5 — Kod · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif · **Prompt seti:** [sasi-kurulum-promptlari.md](sasi-kurulum-promptlari.md)

## Amaç
Öncelikle web prototip aşamasında (M5-Web) Babylon.js + React kullanarak 48 saatte oynanabilir web prototipi yazmak; web testleri ve insan onayı başarılı olursa bu prototipi Unity şasisi üzerine port etmek (M5-Unity).

## Makine eşlemesi
M0 Şasi (tek seferlik + bakım), M5-Web (Web Prototip) ve M5-Unity (Unity Port).

## Çalışma yeri
- **Web Prototip için:** Web çalışma dizini (Vite / React + Babylon.js).
- **Unity Port için:** Oyun reposu (Claude Code veya Antigravity ile).
Bu fabrika reposunda A5 yalnız prompt setleri ve spec tutar — buraya oyun kodu yazılmaz.

## Girdiler
| Girdi | Kaynak |
|---|---|
| GDD + mekanik detayları | games/<oyun>/gdd.md, oyun repo docs/04–07 |
| Stitch Taslakları / Örnekleri | games/<oyun>/gorsel/ (HTML veya JPG) |
| Şasi mimarisi | oyun repo docs/01-ARCHITECTURE.md |
| Event standardı | schemas/event-schema.md |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| Oynanabilir Web Prototip | Vite / Web Deploy | Nazım (Web onay), A6 (Web test) |
| Oynanabilir Unity build (APK/TestFlight) | oyun reposu | game feel testi, A6 |
| docs/ güncellemeleri (ARCHITECTURE, LEVELGEN, QA) | oyun reposu | A9, insan |

## Mimari kurallar (Unity reposunda zorunlu)
- `Assets/_Chassis` dokunulmaz; yeni oyun = `_Game` modülü + `_Content` level data.
- IGameMechanic sözleşmesi: Initialize(LevelData) · StartLevel() · Tick(dt) · EndLevel(LevelResult).
- Sistemler arası iletişim tip güvenli EventBus (struct event); god object yasak.
- SDK'lar interface arkasında (IAdsProvider, IAnalyticsProvider); şasi-lite'ta Dummy/Console.
- Dengeleme değerleri config'te (GameConfig/RemoteConfig), koda gömülmez.
- EventSchema dışında event gönderilemez (tip güvenli sabitler).
- Editor dışında çalışmayan kod bırakılmaz; her adım cihaz build'iyle uyumlu.

## Yetki sınırları
- Asla: şasiyi oyuna göre değiştirmek, ≤ 2 hafta Unity / ≤ 48 saat Web geliştirme tavanını aşan iş planlamak,
  gerçek SDK entegrasyonu (BÜYÜT kararı öncesi), onaysız geniş refactor.

## İnsan onay noktaları
Mimari onay (M0) · **Web prototip onayı** (M5-Web — interaktif chat ile) · **cihazda game feel** (M5-Unity — devredilemez; Unity Editor işleri "İNSAN GÖREVİ" başlığıyla ayrı listelenir).

## Kalite kontrol
Bir prompt = bir iş paketi; sonunda değişen dosya listesi + commit önerisi.
QA çeklisti (oyun repo docs/13): temiz kurulum + 10 dk oynanış.

## Faz 2 işi
Antigravity vs Claude Code A/B → kazanan `uretim.arac` varsayılanı olur (F-105).

## Tasarım senkron sorumluluğu (ADR-0006)
İşe başlamadan önce oyun reposundaki 04–10 dokümanlarının başlığında 🔴/🟡 rozet
var mı kontrol et — varsa önce onu netleştir, üstüne kod yazma. Bir T-5xx (Tasarım
Senkron) görevini bitirince: kodu güncelle → dokümandaki ilgili "Değişiklik
Geçmişi" satırının Durum'unu 🟢 yap → dosya başlığındaki rozeti 🟢 Senkron'a çek →
`14-BACKLOG.md`'de görevi kapat. Rozeti yeşile çekmek yalnız buradan, kodun
gerçekten güncellendiği doğrulandıktan sonra yapılır.
