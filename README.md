# GameFactory 🏭

**Agent-First oyun üretim fabrikası.** İki kişilik çekirdek ekip (Producer + Analist) ve AI ajan katmanıyla çalışan hyper/hybrid-casual mobil oyun üretim hattının **karar hafızası ve işletim sistemi**.

Her oyun bir ürün denemesidir: hızlı üret → gerçek parayla test et → **ÖLDÜR ya da BÜYÜT**.
Mobil oyun bir "oyun yapma" işi değil, kullanıcı edinme işidir; tek denklem: **LTV > CPI**.

> **Durum:** güncel durum için tek kaynak → [CONTEXT.md](CONTEXT.md)

---

## Bu repo nedir, ne değildir?

| Budur | Bu değildir |
|---|---|
| Fabrikanın işletim sistemi: süreç, ajanlar, kararlar, şemalar, şablonlar | Bir oyun projesi (oyunlar kendi Unity repolarında yaşar) |
| Claude Code ve diğer ajanların çalışma anayasası | Kod deposu (orchestrator Faz 3'e kadar kilitli) |
| Onlarca oyunun aynı standartla üretileceği altyapı | Tek oyunluk dokümantasyon |

## 60 saniyede fabrika

Pazar radarı kanıtlı aday üretir → 70 puanlık cetvel + insan yeşil ışığı → GameBrief (completion ≥ 90) → GDD → şasi + **tek mekanik modülü** (≤ 2 hafta) → cihazda game feel (devredilemez) → $100–200 reklam testi → eşikler karar verir. %80–90 kill oranı normaldir; fikri kod yazmadan öldürmek fabrikanın en kârlı işlemidir.

## Hızlı başlangıç

**İnsan için:**
1. [CONTEXT.md](CONTEXT.md) — şu an neredeyiz, sıradaki kapı ne?
2. [GAME_FACTORY.md](GAME_FACTORY.md) — fabrika modeli (makineler + ajanlar)
3. [WORKFLOW.md](WORKFLOW.md) — fikirden yayına akış ve onay kapıları

**Claude Code / ajan için:**
[CLAUDE.md](CLAUDE.md) her oturumda otomatik yüklenir; okuma sırası ve kurallar orada.
Claude dışı kod ajanları (Antigravity vb.) için giriş noktası: [AGENTS.md](AGENTS.md).

## Bu yapı nasıl kullanılır? (senaryolar)

### S1 — Günlük çalışma oturumu (Claude Code)
1. Repo kökünde Claude Code aç — CLAUDE.md otomatik yüklenir.
2. Claude önce [CONTEXT.md](CONTEXT.md) + [ACTIONS.md](ACTIONS.md)'yi okur, işin hangi
   ajana ait olduğunu bulur ve o spec'le çalışır.
3. Oturum sonunda kapanış ritüeli: CONTEXT/ACTIONS güncellenir, karar varsa
   DECISIONS.md'ye satır düşülür, commit mesajı önerilir.

### S2 — Haftalık radar taraması (Pzt, Analist)
`/radar` yaz → A2 web taramasıyla 10 kanıtlı aday kartını `radar/taramalar/`e üretir
→ Pzt senkronunda sunulur → beğenilen kart M2 skorlamasına gider.

### S3 — Yeni oyun başlatma (yeşil ışık sonrası)
1. Yeşil ışık kararını DECISIONS.md'ye işle (insan).
2. `/new-game <isim>` → `games/<isim>/` kaydı + brief iskeleti + görev listesi açılır.
3. Unity reposunu kur (`game-<isim>`), [templates/](templates/) setini kopyala
   (game-docs → `docs/`, game-repo-CLAUDE/AGENTS → köke).
4. A3 GDD üretir → GDD onayı → A5 oyun reposunda kodlar (≤ 2 hafta sayacı işler).

### S4 — Karar kapısı (CPI testi sonrası)
`/karar <oyun> <metrikler>` → A7, [ops/esikler.md](ops/esikler.md) ile deterministik
karşılaştırma raporu üretir → nihai kararı Nazım verir → ÖLDÜR ise kill-log + ders MEMORY'ye.

### S5 — Durum kontrolü / bakım
`/durum` → tek ekran durum raporu + tutarlılık denetimi (kırık link, bayat tarih,
çelişen durum dosyaları).

### S6 — Süreç/standart değiştirmek
Eşik, şema, şablon veya kural değişikliği = ADR: [docs/decisions/_sablon.md](docs/decisions/_sablon.md)
kopyala → doldur → [DECISIONS.md](DECISIONS.md)'ye satır → Nazım onayı. Onaysız değişmez.

### S7 — Claude dışı bir AI ajanıyla çalışmak
Ajanın giriş dosyası [AGENTS.md](AGENTS.md)'dir (yetki matrisi + haberleşme kuralları);
operasyonel kurallar için CLAUDE.md'deki anayasa geçerlidir. Dış oturum (ChatGPT/Gemini)
çıktıları entegre edilmeden önce fabrika terminolojisine çevrilir.

**Yeni oyun başlatmanın el ile tam prosedürü:** [WORKFLOW.md](WORKFLOW.md) §3

## Depo yapısı (her klasör neden var?)

```
GameFactory/
├── README.md            # vitrin — bu dosya
├── CLAUDE.md            # Claude Code çalışma anayasası (her oturumda otomatik okunur)
├── CONTEXT.md           # ANLIK DURUM — aktif oyun, faz, sıradaki kapı (her oturum sonunda güncellenir)
├── GAME_FACTORY.md      # fabrika modeli: katmanlar, makine kataloğu, değişmez kurallar
├── WORKFLOW.md          # fikir → yayın ana akışı; aşama × ajan × kapı matrisi
├── AGENTS.md            # ajan mimarisi: haberleşme, yetki sınırları, doğrulama
├── AGENT_ROLES.md       # her ajanın rol kartı özeti (detay: agents/)
├── HUMAN_ROLES.md       # insan görevleri, devredilemezler, onay mekanizmaları
├── ACTIONS.md           # aktif eylem kuyruğu — kim, ne, hangi makinede
├── DECISIONS.md         # karar günlüğü + ADR süreci (kayıtlar: docs/decisions/)
├── MEMORY.md            # fabrikanın kalıcı hafızası: öğrenilenler, retro notları
├── ROADMAP.md           # 3 faz planı ve tetik koşulları
├── CONTRIBUTING.md      # insan + ajan katkı kuralları, commit standartları
│
├── .claude/             # Claude Code entegrasyonu: slash-komutlar + subagent tanımları
├── agents/              # ajan spec'leri (A1–A9): amaç, girdi/çıktı, dosya yetkileri, promptlar
├── schemas/             # veri sözleşmeleri: GameBrief v1, aday kartı, event şeması
├── templates/           # yeni oyun doküman şablonları (00–15) — standartın kaynağı
├── games/               # oyun kayıt defteri; oyun başına brief + durum (kod ayrı repoda)
├── radar/               # M1 haftalık tarama çıktıları + aday kartları (analist yazar)
├── ops/                 # esikler.md (TARTIŞILMAZ) · roller.md (RACI) · kill-log.md
├── docs/                # strateji dokümanları, ADR kayıtları, standartlar
├── orchestrator/        # Faz 3'e kadar KİLİTLİ — yalnız README + tetik koşulları
└── archive/             # kullanılmayan orijinaller, gerekçeli README'lerle
```

## Ekip ve tek imza ilkesi

| Kişi | Rol | Onay yetkisi |
|---|---|---|
| Nazım | Producer — şasi + kod, game feel son sözü | **Tüm ✔ kapıları:** yeşil ışık · bütçe · nihai infaz · yayın |
| Analist | Veri & Pazar — radar, skorlama, test analizi, kill-log | Rapor eder, karar vermez (eşik bekçisi) |

İlke: **inşa eden infaz etmez.** Ayrıntı: [HUMAN_ROLES.md](HUMAN_ROLES.md) · [ops/roller.md](ops/roller.md)

## Değişmez kurallar (özet)

1. **Önce üret, sonra otomatikleştir** — darboğazı üretim gösterir, hayal değil.
2. **≤ 2 hafta** geliştirme tavanı / prototip.
3. **Pazar-öncelikli seçim** — insan fikri de aynı cetvelden geçer; yan kapı yok.
4. **Para harcanan / yayına giden her adım = açık insan onayı.**
5. **Game feel devredilemez** — her prototip cihazda bizzat oynanır.
6. **Eşikler tartışılmaz** → [ops/esikler.md](ops/esikler.md)
7. Veri yoksa uydurulmaz; "doğrulanamadı" yazılır.
8. Her kapının **tek karar sahibi** vardır — danışılır, oylanmaz.

Tam liste ve gerekçeler: [GAME_FACTORY.md](GAME_FACTORY.md)
