# ADR-0005 — Şablon Tabanlı Oyun Dokümantasyonu

**Tarih:** 2026-07-12 · **Durum:** Taslak (Nazım onayı bekliyor) · **Karar sahibi:** Nazım

## Bağlam
Toy Pile için 16 dosyalık numaralı doküman seti (00–15) sıfırdan yazıldı ve iyi çalıştı
(analiz: [02-toy-pile-dokuman-analizi](../strategy/02-toy-pile-dokuman-analizi.md)).
Ancak set tekrarlanabilir değildi: yapı Toy Pile'a gömülü, sonraki oyun yine sıfırdan yazacaktı.

## Seçenekler
1. Her oyun kendi dokümanını serbest yazar — − standart erozyonu, ajan çıktıları karşılaştırılamaz.
2. **Toy Pile setini şablonlaştır (templates/game-docs/00–15); her oyun kopyalayıp doldurur.**

## Karar
Seçenek 2. Numaralama ve makine eşlemesi Toy Pile setinden aynen korunur
(00-DEVFLOW … 15-RELEASE_CHECKLIST); şablonlar oyundan bağımsız iskelet + doldurma
talimatı içerir. Yeni oyun açılışında set oyun reposuna kopyalanır.

## Gerekçe
"Onlarca oyun aynı standartla" hedefinin somut mekanizması. Ajanlar için de kritik:
A3/A4/A5 çıktı formatını şablondan alır; sonraki aşama şablona karşı doğrular.

## Sonuçlar
- Şablon değişikliği = standart değişikliği → ADR gerekir; oyun içi sapmalar oyun
  reposunda "bilinçli sapma" notuyla kayıt edilir.
- Oyun repolarında biriken iyi pratikler A9 tarafından şablonlara geri işlenir
  (fabrika öğrenir).
