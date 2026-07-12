# Toy Pile Doküman Seti Analizi → Framework Standartları

**Tarih:** 2026-07-12 · **Analiz kapsamı:** `game-toy-pile/docs/` (16 dosya, 00–15) + `GameFactory/_analiz/` orijinalleri
**Amaç:** İlk oyunun geliştirme sürecinden, sonraki tüm oyunlara taşınacak ortak standartları türetmek.

---

## 1. Ne vardı? (envanter)

| Aralık | Dokümanlar | Makine | Değerlendirme |
|---|---|---|---|
| 00 | DEVFLOW (fabrika haritası + durum) | Genel | Güçlü desen: hat durumu tek bakışta |
| 01–03 | ARCHITECTURE · EVENT_SCHEMA · NEW_GAME_FROM_CHASSIS | M0 | Şasi sözleşmeleri net; event şeması tip güvenli |
| 04–07 | GDD · GAME_MECHANICS · LEVELGEN · SCORING_AND_ECONOMY | M3 | Tasarım → parametre → algoritma zinciri iyi ayrışmış |
| 08–10 | SCREEN_FLOW · SCREEN_DESIGN · JUICE_GUIDE | M4 | Juice'un ayrı doküman olması doğru (üründür) |
| 11–13 | MOBILE_TEST_GUIDE · CPI_TEST_PLAN · QA | M5–M7 | Eşikler ve karar akışı işlenmiş |
| 14–15 | BACKLOG · RELEASE_CHECKLIST | Genel/M8 | Görev ID'leri (T-xxx) + durum işaretleri işliyor |

## 2. İşleyen desenler (framework'e alındı)

1. **Numaralı, makineye eşlenmiş doküman seti** — her dokümanın hattaki yeri belli.
   → [templates/game-docs/](../../templates/game-docs/) şablon seti ([ADR-0005](../decisions/ADR-0005-sablon-tabanli-oyun-dokumantasyonu.md))
2. **Girdi→Süreç→Çıktı→İnsan kapısı** makine kartı formatı. → GAME_FACTORY.md §3
3. **Durum işaretleri** (🟢🟡🔴, T-xxx ID'leri, TODO/DONE). → ortak sözlük: [dokuman-standartlari](../standards/dokuman-standartlari.md)
4. **Tip güvenli event şeması** (şemada olmayan event gönderilemez). → [schemas/event-schema.md](../../schemas/event-schema.md)
5. **Eşiklerin tabloyla, tartışmasız yazılması.** → [ops/esikler.md](../../ops/esikler.md)
6. **Paralel iş matrisi** (ne ne ile paralel yürür). → WORKFLOW.md + şablon 00
7. **"İNSAN GÖREVİ" ayrımı** (agent'ın yapamayacağı Unity Editor işleri açıkça etiketli). → A5 spec

## 3. Tespit edilen sorunlar (framework'te çözüldü)

| # | Sorun | Kanıt | Çözüm |
|---|---|---|---|
| 1 | **Çoklu "tek doğruluk kaynağı"** — 00-DEVFLOW, 14-BACKLOG ve main_analysis aynı iddiada | üç dosyanın kapanış notları | Kapsamlı SSOT hiyerarşisi ([ADR-0003](../decisions/ADR-0003-dogruluk-hiyerarsisi.md)) |
| 2 | **Mutlak `file:///` linkler** — repo taşınınca/klonlanınca kırılır | 00-DEVFLOW referansları | Göreli link standardı |
| 3 | **Terminoloji sızıntısı** — "Machine 0", "AOS 9 makine" (Gemini oturumu) onaylı M0–M8 ile çelişiyor | 00-DEVFLOW "9 Makineli", gemini/CLAUDE.md farklı klasör yapısı dayatıyor | M/A katman ayrımı ([ADR-0002](../decisions/ADR-0002-makine-ajan-katmanlari.md)) + dış oturum çeviri kuralı |
| 4 | **Şablonsuzluk** — set Toy Pile'a gömülü; ikinci oyun sıfırdan yazacaktı | tüm set | templates/game-docs/ |
| 5 | **Dil tutarsızlığı** — 01/02/03 İngilizce, kalanı Türkçe | dosyalar | Standart: Türkçe + İngilizce teknik terim |
| 6 | **Fabrika/oyun bilgisi karışımı** — DEVFLOW'da fabrika modeli anlatımı oyun reposunda | 00-DEVFLOW §1 | İki repo modeli ([ADR-0001](../decisions/ADR-0001-iki-repo-modeli.md)): model fabrikada, oyun reposu yalnız kendi durumunu tutar |
| 7 | **Karar kayıtlarının dağınıklığı** — override (53/70), şasi-lite sapması gibi kararlar metin içinde gömülü | 12-CPI, prompt dosyaları | DECISIONS.md + ADR süreci |
| 8 | **İki AI oturağı, iki mimari** — gemini/CLAUDE.md (SO event kanalları, 150 satır limiti) ile fabrika CLAUDE.md (EventBus, asmdef) çelişiyor | gemini klasörü | Çelişen set arşive, gerekçeli README ile |

## 4. Süreçten çıkarılan işleyiş gözlemleri

- **Karar mekanizması:** eşik tablosu + tek imza modeli pratikte işledi (Toy Pile override'ı bile kayıtlı ve sigortalı).
- **Görev dağılımı:** M4 (asset/juice) insan+araç işi olarak darboğaz; M5 (kod) agent'la hızlı. → İkinci oyunda M4'e şablon ve promptlarla daha erken başlanmalı.
- **Tekrarlanan yapı:** her makine dokümanında aynı üçlü (girdi/çıktı/kapı) elle tekrar yazılmış → şablonlarda hazır blok.
- **Eksikler:** oyun-üstü hafıza yoktu (kill-log, ders defteri) → MEMORY.md + ops/kill-log.md; ajan yetki sınırları örtüktü → AGENTS.md §3 matrisi.

## 5. Sonuç

Toy Pile seti "ilk oyunun dokümantasyonu" olarak başarılı, "fabrika standardı" olarak
eksikti. Framework, işleyen desenleri şablonlaştırdı, sorunları ADR'lerle yapısal
çözüme bağladı. İkinci oyun (Faz 2 §5) bu standartların gerçek testi olacak.
