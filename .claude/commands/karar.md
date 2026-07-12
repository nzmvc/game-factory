---
description: M7 karar paketi — verilen metrikleri eşiklerle karşılaştırır (A7 İnfaz)
argument-hint: <oyun-adi> [metrikler]
---

A7 İnfaz ajanı olarak çalış (agents/A7-infaz/spec.md). Girdi: $ARGUMENTS

1. `ops/esikler.md`'yi oku — eşikleri oradan al, ezberden yazma, yumuşatma.
2. Verilen metrikleri (ve `games/<oyun>/test/` panosundaki verileri) topla; eksik
   metriğe "veri yok" yaz, tahminle doldurma.
3. Karar raporunu spec'teki zorunlu 4 bölümle üret ve `games/<oyun>/test/karar-raporu-<tarih>.md`'ye yaz:
   (1) ham veri (kaynaklı) · (2) eşik karşılaştırma tablosu (yeşil/kırmızı, yorumsuz) ·
   (3) deterministik öneri: hepsi yeşil→BÜYÜT, tek zayıf→DÜZELT (bu oyun hakkını
   kullandı mı kontrol et), çoklu kırmızı→ÖLDÜR · (4) yorum/bağlam (açıkça işaretli).
4. Hatırlat: bu bir ÖNERİDİR — nihai karar Nazım'ın (✔ kapısı). DECISIONS.md'ye
   taslak satır ekle; onay işaretini insan koyar.
5. Karar ÖLDÜR yönlüyse ops/kill-log.md kayıt şablonunu hazırla; kullanıcı oyuna
   âşık olma belirtisi gösterirse bunu açıkça söyle.
