# ADR-0002 — Makine (M) ve Ajan (A) Katman Ayrımı ve İsimlendirme

**Tarih:** 2026-07-12 · **Durum:** Taslak (main_analysis §1.1'de özü onaylı) · **Karar sahibi:** Nazım

## Bağlam
Dış AI oturumları (ChatGPT/Gemini AOS) "Machine 0 = Studio Architect ajanı" gibi
tanımlarla geldi; onaylı fabrikada Makine 0 = Unity şasisi. Aynı isim iki katmanda
iki farklı şeyi işaret edince doküman seti bölündü.

## Seçenekler
1. AOS isimlendirmesine geç — − onaylı hattın tüm dokümanları kırılır.
2. **İki katmanı ayır: M-öneki üretim adımları (fiziksel hat), A-öneki ajanlar
   (otomasyon kabuğu)** — + çakışma yapısal olarak imkânsızlaşır.

## Karar
Makine numaraları **M0–M8 fiziksel hatta aittir, değişmez**. Ajanlar **A-öneki** alır;
bir ajan bir makinenin otomasyon kabuğudur. AOS'un "Studio Architect"i = A1.
Makine eşlemesi olmayan yatay ajanlar A9'dan itibaren numara alır.

## Gerekçe
main_analysis §1.1 karar 1'in genelleştirilmesi. Katman ayrımı ayrıca doğru soyutlama:
süreç (makine) araçtan (ajan) bağımsız yaşar; Faz 3'te işletim değişse de hat değişmez.

## Sonuçlar
- Dış oturumdan gelen her doküman entegrasyondan önce bu isimlendirmeye çevrilir
  (denetim: A9). Çevrilmeden repoya giremez.
- Yeni ajan ekleme prosedürü AGENTS.md §5'te; numara çakışması yasak.
