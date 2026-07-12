# CONTRIBUTING — Katkı Kuralları (İnsan + Ajan)

**Son güncelleme:** 2026-07-12

Bu repoya katkı veren herkes — insan veya AI ajanı — aynı kurallara tabidir.

---

## 1. Genel ilkeler

- **Docs as Code:** Doküman = kod. Değişiklik git üzerinden, gözden geçirilebilir ve geri alınabilir.
- **Tek doğruluk kaynağı:** Bilgiyi kopyalama, link ver. Aynı bilgi iki dosyada yaşayamaz.
- Dil: Türkçe; teknik terimler İngilizce kalabilir. Dosya adları: kebab-case, Türkçe karaktersiz.
- Her dokümanın başında **son güncelleme tarihi**; linkler **göreli** (`file:///` ve mutlak yol yasak).

## 2. Değişiklik türü → izlenecek yol

| Değişiklik | Yol |
|---|---|
| Durum güncellemesi (CONTEXT, ACTIONS, radar, test sonuçları) | Doğrudan commit |
| Yeni oyun/doküman (şablondan) | Şablonu kopyala, doldur, kayıt defterine ekle |
| Tasarım dokümanı değişikliği (04–10) — kodu zaten yazılmış bir bölüm | **Değişiklik Geçmişi kaydı + Kod Senkron rozeti** ([ADR-0006](docs/decisions/ADR-0006-tasarim-degisim-yonetimi.md)) |
| Süreç / mimari / standart değişikliği | **ADR zorunlu** ([DECISIONS.md](DECISIONS.md) süreci) + insan onayı |
| Eşik / değişmez kural / şema değişikliği | ADR + **yalnız Nazım onayı** |
| Arşivden içerik geri getirme | ADR + fabrika terminolojisine çeviri |

## 3. Commit standartları

- Format: `<alan>: <özet>` — alan: `docs` `agents` `schemas` `templates` `ops` `radar` `games` `archive` `claude`
- Başlık ≤ 72 karakter, Türkçe, emir kipi ("ekle", "güncelle", "taşı").
- Bir commit = bir mantıksal iş. Karışık commit'e izin yok.
- Ajanlar: onay almadan commit atma; mesaj öner (bkz. CLAUDE.md).

## 4. Ajan katkıları için ek kurallar

- Ajan, yetki matrisinin ([AGENTS.md](AGENTS.md) §3) dışındaki dosyaya yazamaz.
- Üretilen her çıktı, ilgili şemaya/şablona uygunluk beyanı içerir; uymuyorsa "eksik" işaretlenir.
- Veri uydurmak yasak; kaynaksız iddia "doğrulanamadı" etiketi taşır.
- Dış AI oturağı çıktısı (ChatGPT/Gemini) önce fabrika terminolojisine çevrilir.

## 5. İnsan katkıları için ek kurallar

- Kapı onayları sözlü kalamaz — DECISIONS.md'ye satır düşülür.
- `radar/`, `games/*/test/`, `ops/kill-log.md` analistin yazma alanıdır;
  `ops/esikler.md` ve strateji yalnız Nazım onayıyla değişir.

## 6. Gözden geçirme

- Her aşama teslimi, alıcı taraf (sonraki makinenin sahibi) tarafından şema kontrolünden geçer.
- Doküman tutarlılık denetimi (link, tarih, terminoloji): A9 Doküman ajanı, aşama kapanışlarında.
