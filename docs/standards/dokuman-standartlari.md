# Doküman Standartları

**Son güncelleme:** 2026-07-12 · Commit kuralları: [CONTRIBUTING.md](../../CONTRIBUTING.md)

Bu repo ve tüm oyun repolarının doküman yazım standardı. Denetleyen: A9.

## Dil ve üslup
- Türkçe; teknik terimler İngilizce kalabilir. Net, gerekçeli, pohpohlamasız.
- Veri ile yorum ayrı bölümlerde; kaynaksız iddia "doğrulanamadı" / "izlenim" etiketi taşır.

## Dosya ve isimlendirme
- Dosya adları kebab-case, Türkçe karaktersiz (`adr-0001-...` değil `ADR-0001-...` yalnız ADR'lerde büyük).
- Oyun doküman seti numaralıdır (00–15) ve makine eşlemesini korur ([ADR-0005](../decisions/ADR-0005-sablon-tabanli-oyun-dokumantasyonu.md)).
- Tarih formatı: `YYYY-AA-GG`. Göreli tarih ("gelecek hafta") yasak — mutlak tarih yazılır.

## Yapı
- Her dokümanın başında: başlık + **son güncelleme tarihi** + (varsa) kaynak/ilgili linkler.
- Linkler **göreli** (`../ops/esikler.md`); `file:///` ve mutlak yol yasak.
  Repo dışına referans repo adıyla: `game-toy-pile/docs/04-GDD.md`.
- Bilgi kopyalanmaz, link verilir ([ADR-0003](../decisions/ADR-0003-dogruluk-hiyerarsisi.md)).
- Bir doküman tek konuyu anlatır; 1–3 sayfa tavan (GDD dahil). Uzuyorsa bölünür.

## Durum işaretleri (ortak sözlük)
- Hat/iş durumu: 🟢 tamam · 🟡 devam · 🔴 başlamadı · ⛔ insan kapısı bekliyor
- Görevler: ⬜ TODO · ⏳ IN_PROGRESS · ✅ DONE
- Doküman/şema durumu: Taslak · Aktif · Kilitli · Arşiv

## Tasarım-kod senkronu
Oyun repolarındaki 04–10 dokümanları (kodu tüketen M3/M4 çıktıları) "Kod Senkron
Durumu" rozeti ve "Değişiklik Geçmişi" tablosu taşır; kodu zaten yazılmış bir
bölüm değişince bu iz zorunludur, henüz kodlanmamış taslak serbesttir. Detay ve
gerekçe: [ADR-0006](../decisions/ADR-0006-tasarim-degisim-yonetimi.md).

## Veri dokümanları
- Analytics event'leri snake_case ve [schemas/event-schema.md](../../schemas/event-schema.md) standardına tabidir.
- Şema versiyonu dosya adında (`.v1`); kırıcı değişiklik yeni versiyon açar.
- YAML/JSON bloklarında yorum satırlarıyla doldurma talimatı verilir (şablonlarda olduğu gibi).
