# ADR-0004 — Önce Prompt, Sonra SDK (Orchestrator Faz 3 Kilidi)

**Tarih:** 2026-07-12 · **Durum:** Taslak (main_analysis §1.1 karar 5'te özü onaylı) · **Karar sahibi:** Nazım

## Bağlam
Elde çalışır görünen bir orchestrator var (archive/aos-gemini/AOS_ORCHESTRATOR.py) ama
simüle veriyle karar veriyor ve onaylı cetvelle çelişiyor. SDK inşası oyun çıkarmaktan
tatlıdır; "fabrika tuzağı" en büyük risk olarak kayıtlı.

## Seçenekler
1. Orchestrator'ı şimdi düzeltip kullan — − hattın darboğazı otomasyon değil üretim;
   efor yanlış makineye akar.
2. **Ajanlar Faz 1–2'de prompt/spec olarak yaşar; SDK orkestrasyonu tetik koşuluna bağlanır.**

## Karar
Her ajan önce `agents/Ax/spec.md` + prompt olarak tanımlanır ve elle işletilir.
`orchestrator/` klasörü kilitlidir; açılma tetiği: **≥ 2 prototip hattan geçti VE
(radar 3 hafta elle aksadı VEYA ayda 2+ prototip hedefi).**

## Gerekçe
"Önce üret, sonra otomatikleştir" değişmez kuralının yapısal uygulaması. Spec'ler
araçtan bağımsız yazıldığı için Faz 3'te sıfır çeviri maliyetiyle SDK'ya taşınır.

## Sonuçlar
- Faz 3'te bile insan kapıları koda gömülür (auto-spend yok) ve model adları
  hardcode edilmez.
- Tetik gelmeden orchestrator PR'ı açan her ajan/oturum bu ADR'yi ihlal eder.
