# WORKFLOW — Fikirden Yayına Ana Akış

**Son güncelleme:** 2026-07-14 · Makine tanımları: [GAME_FACTORY.md](GAME_FACTORY.md) · Eşikler: [ops/esikler.md](ops/esikler.md)

```
Idea / Radar sinyali
   ↓  M1  (A2 Radar — haftalık tarama, 10 aday kartı)
Market Research
   ↓  M2  (A1 Producer — 70'lik cetvel)          ✔ KAPI: Yeşil ışık (Nazım)
Game Concept → GameBrief (completion ≥ 90)
   ↓  M3  (A3 GDD)                                ✔ KAPI: GDD onayı
GDD onaylandıktan sonra Google Stitch Arayüz Tasarımı ve prompt hazırlığı
Görsel referansların (HTML veya JPG/PNG) games/<oyun>/gorsel/ klasörüne atılması
   ↓  M4  (A4 Görsel — prompt hazırlar, örnekleri kopyalar) ✔ KAPI: Stil onayı
Web Prototip Geliştirme (M5-Web: Babylon.js + React ile 48 saat)
İnteraktif insan-ajan yazışmalarıyla test & iyileştirme
   ↓  M5-Web  (A5 Kod — Web Game Developer)
Web Pazarlanabilirlik Testi (Web-playable ad / soft-launch CTR)
   ↓  M6-Web  (A6 Test — web verisi)             ✔ KAPI: Unity Geçiş Onayı (CPI < $0.40 ise)
   ├─ CPI ≥ $0.40 → ÖLDÜR (ops/kill-log.md + başa dön)
   └─ CPI < $0.40 ↓
Unity Şasi Üzerine Port Etme (M5-Unity: efor ≤ 2 hafta)
   ↓  M5-Unity (A5 Kod — Unity)                   ✔ KAPI: Cihazda game feel
Gameplay kaydı → 3–5 Reklam Kreatifi
   ↓  M6-Unity (A6 Test)                          ✔ KAPI: Bütçe onayı ($100–200)
Mobil Test Kampanyası (CPI/CTR/Retention ölçümü)
   ↓  M7  (A7 İnfaz — eşik karşılaştırma raporu)  ✔ KAPI: ÖLDÜR / DÜZELT / BÜYÜT (Nazım)
   ├─ ÖLDÜR → ops/kill-log.md + sıradaki aday (başa dön)
   ├─ DÜZELT → tek hak → M6-Unity'ye dön
   └─ BÜYÜT ↓
Gerçek şasi yatırımı (Firebase, mediation, IAP, consent) + soft launch
   ↓  M8  (A8 ASO)                                ✔ KAPI: Yayın onayı
Release → Post-Release → Analytics → Continuous Improvement
   ↓  (A7 kohort takibi · A2 radar döngüsü devam eder · MEMORY.md'ye dersler)
```

---

## 1. Aşama × sorumluluk matrisi

| Aşama | Makine | Sorumlu ajan | Girdi dokümanı | Çıktı dokümanı | Kalite kontrolü | İnsan kapısı |
|---|---|---|---|---|---|---|
| Pazar taraması | M1 | A2 | [tarama promptları](agents/A2-radar/tarama-promptlari.md) | `radar/taramalar/YYYY-Www.md` (aday kartları) | Kanıtsız aday yazılmaz; "doğrulanamadı" işaretlenir | — |
| Seçim | M2 | A1 | Aday kartları | Skor tablosu + GameBrief taslağı | ≥ 50/70 + veto kuralı; completion score | ✔ Yeşil ışık |
| Tasarım | M3 | A3 | GameBrief (≥ 90) | `games/<oyun>/gdd.md` | Psikoloji spesifikasyonu denetimi | GDD onayı |
| Görsel | M4 | A4 | GDD | Google Stitch promptu + Görsel Örnekler | Stil rehberi, asset listesi, Stitch tasarımı | Stil onayı |
| Web Geliştirme | M5-Web | A5 (Web) | GDD + Stitch Prompt | Web Prototip (Babylon.js + React, 48s) | İnteraktif insan-ajan chat döngüsü ile test | Web onay / CPI testi |
| Unity Geliştirme | M5-Unity | A5 (Unity) | Web Prototip + GDD | Oyun reposunda oynanabilir build | Cihaz build uyumluluğu; QA çeklisti | Cihazda game feel |
| Pazarlanabilirlik | M6 | A6 | Gameplay kaydı | Kreatif brief'ler + kampanya + pano | 3 sn kuralı; kreatif matris | ✔ Bütçe onayı |
| Karar | M7 | A7 | Test verileri | Karar raporu (eşik karşılaştırmalı) | Deterministik eşik tablosu — LLM karar vermez | ✔ Nihai karar |
| Yayın | M8 | A8 | BÜYÜT kararı | Store metni + keyword + görsel konseptleri | Release checklist | Yayın onayı |
| Sürekli iyileştirme | — | A7+A9 | Analytics + retrolar | MEMORY.md güncellemesi, kill-log | Ders çıkarılmadan oyun kapanmaz | — |

## 2. Aşama geçiş kuralları

- Bir aşama, çıktı dokümanı **şemaya/şablona uygun ve eksiksiz** olmadan kapanmaz.
- İnsan kapısı olan aşamalarda onay kaydı DECISIONS.md'ye düşülür (tarih + karar + tek imza).
- DÜZELT hakkı **oyun başına 1'dir**; ikinci zayıf sonuç otomatik ÖLDÜR tartışması açar.
- **Web-First Prototipleme:** GDD onayının ardından Google Stitch promptları hazırlanır ve görsel örnekler `games/<oyun>/gorsel/` klasörüne kopyalanır. M5-Web aşamasında 48 saatlik web prototipi çıkarılarak insan ile karşılıklı yazışmalarla iyileştirilir.
- **Unity'ye Geçiş:** Web-playable prototip testi başarılı olursa (CPI < $0.40 veya insan onayı ile) Unity şasi geliştirmelerine başlanır.
- Her aşama sonunda CONTEXT.md ve ACTIONS.md güncellenir (bkz. CLAUDE.md kapanış ritüeli).

## 3. Yeni oyun başlatma

Tetik: M2'den yeşil ışık almış bir GameBrief.

1. `games/<oyun-adi>/` klasörü açılır: `brief.md` (GameBrief v1 şemasına uygun) + `durum.md`.
2. A3 GDD üretir → onaylanır.
3. A4 Google Stitch promptlarını ve görsel taslakları hazırlar, `games/<oyun-adi>/gorsel/` klasörüne kopyalar.
4. A5 (Web) 48 saatte Babylon.js + React tabanlı oynanabilir web prototipini hazırlar ve insan ile karşılıklı chat üzerinden onay alır.
5. Web prototipi pazarlanabilirlik testine girer. CPI < $0.40 olması durumunda Unity oyun reposu oluşturulur; [templates/game-docs/](templates/game-docs/) seti kopyalanır, oyun reposu CLAUDE.md/AGENTS.md'si şablondan uyarlanır ve Unity geliştirmelerine başlanır (efor ≤ 2 hafta).
6. `games/README.md` kayıt defterine satır eklenir; CONTEXT.md aktif oyunu gösterir.

Claude Code kısayolu: `/new-game <isim>` (bkz. [.claude/commands/new-game.md](.claude/commands/new-game.md))

## 4. Haftalık ritim (Faz 1–2)

- **Pzt:** Analist pazar radarı taraması (60–90 dk) → webpage_extract kullanarak ad library ve TikTok taraması yapılıp `radar/taramalar/` klasörüne aktarılır.
- **Salı–Çar:** A5 (Web) web prototipi üretimi (M5-Web) ve Google Stitch entegrasyonu.
- **Per–Cuma:** Web prototipi testinin yürütülmesi ve insanla karşılıklı yazışarak iyileştirilmesi. CPI < $0.40 doğrulanırsa Unity port (M5-Unity) başlatılması.
- **Cmt:** Metrik panosu sunumu; game feel'i ikisi de cihazda test eder (son söz Nazım); gerekiyorsa M7 karar oturumu.
- Yeşil ışık adaylarının referans oyunlarını **ikisi de** indirir ve 10'ar dk oynar.
