# ADR-0006 — Tasarım Değişiklik Kaydı ve Kod Senkron Durumu

**Tarih:** 2026-07-13 · **Durum:** Taslak (Nazım onayı bekliyor) · **Karar sahibi:** Nazım

## Bağlam
Toy Pile'da M3 (GDD/mekanik/ekran) dokümanları yazıldı, M5 (kod) onlara göre
yazıldı, oyun cihazda test edildi ve tasarım beğenilmedi. Şimdi tasarım dokümanları
değişecek — ama kod zaten o dokümanların **eski haline** göre yazılmış durumda.
Sorulan soru: bir tasarım dokümanı, onu uygulayan kod zaten varken değişince, (1)
neyin değiştiği, (2) kodun neresini etkilediği, (3) kodun ne zaman yetiştiği nasıl
izlenecek? Şu anda bu iz tamamen kayıp — doküman sessizce güncelleniyor, kod
drift'i fark edilmiyor.

## Seçenekler
1. **Ayrı bir değişiklik veritabanı/CHANGELOG dosyası** (`docs/DESIGN_CHANGELOG.md`)
   — tüm dokümanların değişikliğini tek yerde toplar. Artı: taranması kolay.
   Eksi: içerikten kopar, güncel tutulması ayrı bir disiplin ister, tek doğruluk
   kaynağı ilkesini zedeler (ADR-0003).
2. **Git commit mesajlarına güven** — doküman değişikliği zaten git'te. Artı: sıfır
   ek iş. Eksi: "kod etkisi var mı" analizini commit mesajı garanti etmez; agent'lar
   commit geçmişini taramaz, dokümanı okur.
3. **Doküman içi "Değişiklik Geçmişi" tablosu + kod senkron rozeti, kod-etkili
   girişler backlog'a yansır.** İçerikle birlikte yaşar (tek doğruluk kaynağı
   korunur), agent doküman içinde görür, backlog'da iş olarak takip edilir.

## Karar
Seçenek 3. Kod tarafından tüketilen her tasarım dokümanı (M3/M4 çıktıları:
04-GDD, 05-GAME_MECHANICS, 06-LEVELGEN, 07-SCORING_AND_ECONOMY, 08-SCREEN_FLOW,
09-SCREEN_DESIGN, 10-JUICE_GUIDE) iki şeyi taşır:

1. **Başlıkta kod senkron rozeti:** `**Kod Senkron Durumu:** 🟢 Senkron | 🟡 Kısmi | 🔴 Bekliyor`
2. **Dosya sonunda "Değişiklik Geçmişi" tablosu:**

   | Tarih | Değişen bölüm | Özet | Kod Etkisi | Backlog | Durum |
   |---|---|---|---|---|---|
   | YYYY-AA-GG | §X | ne değişti, tek cümle | Var/Yok (+ dosya/sınıf) | T-xxx (varsa) | 🔴 Bekliyor / 🟢 Uygulandı |

**Tetik kuralı:** Bu tablo yalnız **kodu zaten yazılmış** bir bölüm değiştiğinde
zorunludur — henüz kodlanmamış tasarım taslağı serbestçe düzenlenir, ek yük yok.

**El değiştirme akışı:**
- Tasarımı değiştiren (A3 veya insan) satırı ekler, "Kod Etkisi: Var" ise
  `14-BACKLOG.md`'ye bir görev (T-xxx, "Tasarım Senkron Görevleri" bölümü) açar,
  doküman rozetini 🔴/🟡 yapar.
- Kodu güncelleyen (A5) görevi kapatınca hem backlog satırını hem doküman
  rozetini/tablo durumunu 🟢 yapar. Rozeti yalnız kodu yazan/doğrulayan taraf
  yeşile çeker — tasarımcı kendi değişikliğini "uygulandı" işaretleyemez.

## Gerekçe
- Tek doğruluk kaynağı ilkesi korunur (ADR-0003): iz, içeriğin yanında yaşar,
  ayrı bir dosyada çürümez.
- A3↔A5 el değiştirme sözleşmesi zaten dosya-tabanlı (AGENTS.md §2); bu mekanizma
  aynı modele "durum" ekler, yeni bir haberleşme kanalı açmaz.
- Rozeti yalnız kod tarafının yeşile çekmesi, "tasarımcı yazdı, kimse uygulamadı
  ama sanki bitmiş gibi duruyor" riskini yapısal olarak engeller.
- Her küçük düzenlemede zorunlu olmaması (yalnız kodlanmış bölüm değişince) küçük
  ekibin hızını korur; bürokrasi tasarım taslağı aşamasında değil, drift riski
  gerçekken devreye girer.

## Sonuçlar
- `templates/game-docs/04,05,06,07,08,09,10` şablonlarına rozet + tablo eklenir
  (ADR-0005 kapsamında şablon değişikliği).
- `templates/game-docs/14-BACKLOG.md`'ye "Tasarım Senkron Görevleri" bölümü eklenir.
- `agents/A3-gdd/spec.md` ve `agents/A5-kod/spec.md` bu akışı sorumluluk olarak alır.
- Mevcut oyun repolarında (Toy Pile) geriye dönük uygulanır: dosyalar 🟢 Senkron
  rozetiyle ve boş tabloyla açılır, bundan sonraki her değişiklik buradan işler.
