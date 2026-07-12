# MEMORY — Fabrikanın Kalıcı Hafızası

> Tekrarlanabilirliğin kaynağı: her oyun, test ve hata buraya ders bırakır.
> CONTEXT.md "şu an"ı, DECISIONS.md "neye karar verildiğini", bu dosya
> "**ne öğrenildiğini**" tutar. Öldürülen oyunların ayrıntılı kaydı: [ops/kill-log.md](ops/kill-log.md)

**Son güncelleme:** 2026-07-12

---

## Yazma kuralları

- Bir ders ancak **tekrar kullanılabilir** biçimde yazılır: *durum → gözlem → bundan sonra ne yapılacak*.
- Kaynak göster (test verisi, oturum, tarih). Veri yoksa "izlenim" olarak işaretle.
- Silme yok; geçersizleşen ders üstü çizilerek ~~işaretlenir~~ ve nedeni yazılır.
- Ajanlar ders ekleyebilir; ayıklama (hangileri kural olacak) insan işidir.
  Kurala dönüşen ders ADR'ye/CLAUDE.md'ye taşınır, buradan link verilir.

## Süreç dersleri

| Tarih | Ders | Kaynak |
|---|---|---|
| 2026-07-11 | Dış AI oturumları (ChatGPT/Gemini) kendi isimlendirmesini dayatır ("Machine 0" çakışması); entegrasyondan önce fabrika terminolojisine çeviri zorunlu. | AOS uzlaştırması, [main_analysis](docs/strategy/main_analysis.md) §1.1 |
| 2026-07-11 | Çalışan ama kurgu veriyle karar veren otomasyon, çalışmayan otomasyondan tehlikelidir (AOS_ORCHESTRATOR simüle veri + çelişen cetvel). | [archive/aos-gemini/](archive/aos-gemini/) |
| 2026-07-11 | İki paralel skorlama cetveli fabrikayı ikiye böler; cetvel tek dosyada yaşar, koda gömülmez. | main_analysis §1.1 karar 3 |
| 2026-07-12 | Doküman setinde birden çok "tek doğruluk kaynağı" iddiası birikiyor; hiyerarşi açıkça yazılmalı. | [ADR-0003](docs/decisions/ADR-0003-dogruluk-hiyerarsisi.md) |

## Üretim / teknik dersler

| Tarih | Ders | Kaynak |
|---|---|---|
| 2026-07-12 | Şasi-lite (Dummy/Console stub) CPI testi için yeterli; gerçek SDK yatırımı ancak BÜYÜT kararından sonra. | Toy Pile M0 kararı |
| 2026-07-12 | Mutlak `file:///` linkler repo taşınınca kırılıyor; göreli link standardı. | toy-pile docs analizi |

## Pazar / test dersleri

*(İlk CPI testi sonrası dolacak — F-101/F-102)*

## Kill-log özeti

| Oyun | Karar | Tarih | Bir cümlelik ders |
|---|---|---|---|
| *(henüz yok)* | | | |
