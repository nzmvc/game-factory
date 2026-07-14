# DECISIONS — Karar Günlüğü

> Fabrikanın karar hafızası. İki seviye vardır:
> 1. **Karar satırı** (aşağıdaki tablo): kapı onayları ve küçük kararlar — tek satır.
> 2. **ADR** (Architecture Decision Record, [docs/decisions/](docs/decisions/)): mimari /
>    süreç / standart kararları — kalıcı gerekçe dokümanı.
>
> Kural: Ajan karar satırını **taslak** olarak ekleyebilir; "onaylı" işaretini yalnız
> karar sahibi insan koyar. Kayıtsız karar yok sayılır.

**Son güncelleme:** 2026-07-14

---

## Karar satırları

| Tarih | Karar | Kapı/Konu | Karar sahibi | Durum | Kaynak |
|---|---|---|---|---|---|
| 2026-07-10 | Fabrika stratejisi v1.0 onayı (iş modeli, makine hattı, eşikler) | Strateji | Nazım | ✅ Onaylı | [01-analiz](docs/strategy/01-oyun-fabrikasi-analiz.md) |
| 2026-07-11 | Toy Pile yeşil ışık — 53/70 **bilinçli override**, sigortası M6 testi | M2 | Nazım | ✅ Onaylı | [main_analysis](docs/strategy/main_analysis.md) §5 |
| 2026-07-12 | main_analysis v1.1: 2 kişilik ekip, RACI, AOS↔Fabrika uzlaştırma (5 karar) | Strateji | Nazım | ✅ Onaylı | [main_analysis](docs/strategy/main_analysis.md) §1 |
| 2026-07-12 | GameFactory framework yapısı kuruldu (ADR-0001…0005) | Repo | Nazım | 🕐 Taslak — onay bekliyor | ADR'ler ↓ |
| 2026-07-12 | `game-toy-pile` reposu framework standardına hizalandı: doküman path/link düzeltmeleri, `_analiz`/`_prompt` kopyaları silindi, `AOS_ORCHESTRATOR_SPEC.md` arşive taşındı, CLAUDE/AGENTS'a Fabrika Bağlantısı eklendi | Repo hijyen | Claude (uygulama) | ✅ Uygulandı | Bu satır |
| 2026-07-14 | Web-First Prototipleme & Hibrit-Casual Monetizasyon entegrasyonu (GAME_FACTORY.md, WORKFLOW.md, ops/esikler.md, ajan spec'leri ve templates güncellendi) | Strateji | Nazım (otomatik onay) | ✅ Uygulandı | Bu satır |
| — | G10 pazarlanabilirlik testi bütçesi ($100–200) | M6 | Nazım | ⬜ Bekliyor (22 Tem) | [ACTIONS.md](ACTIONS.md) F-008 |

## ADR kayıtları

| ADR | Başlık | Durum |
|---|---|---|
| [ADR-0001](docs/decisions/ADR-0001-iki-repo-modeli.md) | Fabrika reposu ↔ oyun repoları ayrımı | Taslak |
| [ADR-0002](docs/decisions/ADR-0002-makine-ajan-katmanlari.md) | Makine (M) ve Ajan (A) katman ayrımı ve isimlendirme | Taslak |
| [ADR-0003](docs/decisions/ADR-0003-dogruluk-hiyerarsisi.md) | Docs-as-Code + tek doğruluk kaynağı hiyerarşisi | Taslak |
| [ADR-0004](docs/decisions/ADR-0004-once-prompt-sonra-sdk.md) | Önce prompt, sonra SDK (orchestrator Faz 3 kilidi) | Taslak |
| [ADR-0005](docs/decisions/ADR-0005-sablon-tabanli-oyun-dokumantasyonu.md) | Şablon tabanlı oyun dokümantasyonu (templates/game-docs) | Taslak |
| [ADR-0006](docs/decisions/ADR-0006-tasarim-degisim-yonetimi.md) | Tasarım Değişiklik Kaydı ve Kod Senkron Durumu (04–10 dokümanları) | Taslak |

## ADR süreci

1. Şablonu kopyala: [docs/decisions/_sablon.md](docs/decisions/_sablon.md) → `ADR-XXXX-kisa-baslik.md`.
2. Bağlam → seçenekler → karar → gerekçe → sonuçlar bölümlerini doldur (1 sayfa tavan).
3. Bu dosyadaki tabloya satır ekle; durum: Taslak → (insan onayı) → Onaylı / Reddedildi.
4. Bir ADR'yi değiştirme; yeni ADR yaz ve eskisini "Yerini aldı: ADR-YYYY" ile işaretle.
