# A7 — İnfaz (Veri & Karar Raporu) · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif

## Amaç
Test verilerini eşik tablosuyla karşılaştırıp gerekçeli **karar paketi** hazırlamak.
Karar önerisi deterministiktir; LLM yalnız "neden" bölümünü yazar.

## Makine eşlemesi
M7 Veri & İnfaz.

## Girdiler
| Girdi | Kaynak |
|---|---|
| CPI/CTR/IPM verileri | games/<oyun>/test/ panosu |
| Retention + playtime | Firebase/analytics (soft launch aşamasında) |
| Eşikler | ops/esikler.md — **tek kaynak, kopyalanmaz** |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| Karar raporu: veri tablosu + eşik karşılaştırması + öneri (ÖLDÜR/DÜZELT/BÜYÜT) + gerekçe | games/<oyun>/test/ | Nazım |
| Kill kaydı (karar ÖLDÜR ise) | ops/kill-log.md | MEMORY.md |
| Kohort takip raporları (post-release) | games/<oyun>/test/ | sürekli iyileştirme |

## Rapor formatı (zorunlu ayrım)
1. **Ham veri** (kaynaklı, tarihli)
2. **Eşik karşılaştırma tablosu** (mekanik: yeşil/kırmızı işaretleme — yorum yok)
3. **Deterministik öneri** (karar mantığı: hepsi yeşil→BÜYÜT · tek zayıf→DÜZELT(1 hak) · çoklu kırmızı→ÖLDÜR)
4. **Yorum/bağlam** (LLM bölümü — açıkça işaretli)

## Yetki sınırları
- İşleten: Analist (**inşa eden infaz etmez** — raportör kod yazan kişi olamaz)
- Asla: eşik yumuşatmak, "bir şans daha" önermek (DÜZELT hakkı 1'dir ve kayıtlıdır),
  veriyi yorumla karıştırmak, nihai karar vermek.

## İnsan onay noktaları
✔ Nihai karar (Nazım). Rapor tartışılır, eşik tartışılmaz.

## Kalite kontrol
Rapordaki her sayı kaynağa link verir; eksik metrik "veri yok" olarak işaretlenir,
tahminle doldurulmaz. Karar sonrası ders MEMORY.md'ye işlenir — ders çıkarılmadan
oyun kapanmaz.
