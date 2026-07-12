# WORKFLOW — Fikirden Yayına Ana Akış

**Son güncelleme:** 2026-07-12 · Makine tanımları: [GAME_FACTORY.md](GAME_FACTORY.md) · Eşikler: [ops/esikler.md](ops/esikler.md)

```
Idea / Radar sinyali
   ↓  M1  (A2 Radar — haftalık tarama, 10 aday kartı)
Market Research
   ↓  M2  (A1 Producer — 70'lik cetvel)          ✔ KAPI: Yeşil ışık (Nazım)
Game Concept → GameBrief (completion ≥ 90)
   ↓  M3  (A3 GDD)                                ✔ KAPI: GDD onayı
GDD + Architecture (şasi zaten hazır: M0)
   ↓  M4 ∥ M5  (A4 Görsel ∥ A5 Kod — paralel)     ✔ KAPI: Stil onayı · cihazda game feel
Playable Prototype (≤ 2 hafta)
   ↓  M6  (A6 Test — kreatifler + kampanya)       ✔ KAPI: Bütçe onayı ($100–200)
CPI / CTR verisi
   ↓  M7  (A7 İnfaz — eşik karşılaştırma raporu)  ✔ KAPI: ÖLDÜR / DÜZELT / BÜYÜT (Nazım)
   ├─ ÖLDÜR → ops/kill-log.md + sıradaki aday (başa dön)
   ├─ DÜZELT → tek iterasyon hakkı → M6'ya dön
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
| Görsel | M4 | A4 | GDD | Stil rehberi + asset listesi + juice checklist | 3 sn okunabilirlik; okunabilirlik > gerçekçilik | Stil onayı |
| Geliştirme | M5 | A5 | GDD + şablon prompt seti | Oyun reposunda oynanabilir build | Her adım cihaz build'iyle uyumlu; QA çeklisti | Cihazda game feel |
| Pazarlanabilirlik | M6 | A6 | Gameplay kaydı | Kreatif brief'ler + kampanya + pano | 3 sn kuralı; kreatif matris | ✔ Bütçe onayı |
| Karar | M7 | A7 | Test verileri | Karar raporu (eşik karşılaştırmalı) | Deterministik eşik tablosu — LLM karar vermez | ✔ Nihai karar |
| Yayın | M8 | A8 | BÜYÜT kararı | Store metni + keyword + görsel konseptleri | Release checklist | Yayın onayı |
| Sürekli iyileştirme | — | A7+A9 | Analytics + retrolar | MEMORY.md güncellemesi, kill-log | Ders çıkarılmadan oyun kapanmaz | — |

## 2. Aşama geçiş kuralları

- Bir aşama, çıktı dokümanı **şemaya/şablona uygun ve eksiksiz** olmadan kapanmaz.
- İnsan kapısı olan aşamalarda onay kaydı DECISIONS.md'ye düşülür (tarih + karar + tek imza).
- DÜZELT hakkı **oyun başına 1'dir**; ikinci zayıf sonuç otomatik ÖLDÜR tartışması açar.
- Paralellik: M4 ∥ M5 çalışabilir; M6 gerçek oynanış kaydı gerektirir (game feel'den sonra).
- Her aşama sonunda CONTEXT.md ve ACTIONS.md güncellenir (bkz. CLAUDE.md kapanış ritüeli).

## 3. Yeni oyun başlatma

Tetik: M2'den yeşil ışık almış bir GameBrief.

1. `games/<oyun-adi>/` klasörü açılır: `brief.md` (GameBrief v1 şemasına uygun) + `durum.md`.
2. Oyun Unity reposu oluşturulur; [templates/game-docs/](templates/game-docs/) seti kopyalanır,
   oyun reposu CLAUDE.md/AGENTS.md'si şablondan uyarlanır.
3. `games/README.md` kayıt defterine satır eklenir; CONTEXT.md aktif oyunu gösterir.
4. A3 GDD üretir → onay → A5 prompt setiyle geliştirme başlar (≤ 2 hafta sayacı işler).

Claude Code kısayolu: `/new-game <isim>` (bkz. [.claude/commands/new-game.md](.claude/commands/new-game.md))

## 4. Haftalık ritim (Faz 1–2)

- **Pzt:** Analist radar taraması (60–90 dk) → `radar/taramalar/` · 20 dk senkron.
- **Salı–Cuma:** Nazım aktif prototipte üretim (M5), her akşam cihaz build ·
  Analist rakip kreatif analizi + test/pano işleri.
- **Cmt:** Metrik panosu sunumu; game feel'i ikisi de cihazda test eder (son söz Nazım);
  gerekiyorsa M7 karar oturumu.
- Yeşil ışık adaylarının referans oyunlarını **ikisi de** indirir ve 10'ar dk oynar.
