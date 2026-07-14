# GameFactory Değerlendirme ve Geliştirme Yol Haritası (V1)

**Son güncelleme:** 2026-07-14 · **Hazırlayan:** Manus · **Durum:** Taslak (Nazım onayı bekliyor)

Bu doküman, mevcut `GameFactory` altyapısının `game-dev` becerileriyle entegrasyonunu, üretim hattındaki darboğazların giderilmesini ve 2026 mobil oyun pazarı trendlerine (Hybrid-Casual) uyumunu hedefler.

---

## 1. Mevcut Durum Analizi (Audit)

### Güçlü Yanlar
- **Disiplinli Metrik Kültürü:** `ops/esikler.md` ile tanımlanan deterministik karar yapısı, Hyper-Casual (HC) üretimindeki en büyük risk olan "oyuna aşık olma" hatasını engelliyor.
- **Modüler Mimari:** M0–M8 makine hattı ve A1–A9 ajan katmanı, otomasyona çok uygun bir temel sunuyor.
- **Açık Sorumluluklar:** İnsan ve ajan rollerinin net ayrımı, ölçeklenebilirlik için kritik.

### Gelişim Alanları (Darboğazlar)
- **Unity Bağımlılığı ve Hız:** Mevcut şasi Unity tabanlıdır. Prototip aşamasında (M5-M6) Unity build süreçleri ve store onayları, pazar testlerini (CPI/CTR) yavaşlatabilir. Bu durum, hızlı iterasyon gerektiren HC pazarında bir dezavantaj oluşturmaktadır [1].
- **Monetizasyon Derinliği:** `Toy Pile` örneğinde görüldüğü üzere, monetizasyon "v2 işi" olarak görülüyor. 2026 pazarında Hybrid-Casual başarısı, monetizasyonun mekanikle en baştan (M3 aşamasında) iç içe geçmesini gerektirmektedir [2]. Hybrid-casual oyunlar, uygulama içi satın almalardan (IAP) %20'ye varan gelir artışı göstermiştir [3].
- **Ajan Otomasyonu:** Ajanlar şu an "prompt bazlı manuel" çalışıyor. `game-dev` becerisinin sunduğu uçtan uca üretim (Babylon.js) hattı henüz tam olarak kullanılmamaktadır.

---

## 2. Geliştirme Önerileri

### A. "Web-First" Prototipleme Hattı (M5 & M6 Entegrasyonu)
Unity yerine, **Babylon.js** tabanlı bir "Hızlı Test Hattı" eklenmelidir.
- **Neden:** Web tabanlı oyunlar (Playable Ads veya Instant Games), store onayı beklemeden doğrudan reklam ağlarında (Meta/TikTok) test edilebilir. Bu yaklaşım, pazar testlerini hızlandırarak maliyetleri düşürür ve daha fazla oyun fikrinin doğrulanmasına olanak tanır [1].
- **Aksiyon:** `game-dev` becerisini kullanarak M5 (Kod) aşamasını 48 saatlik web prototiplerine indirmek. Eğer CPI < $0.40 gelirse, Unity (M0) şasisine geçiş yapılır.

### B. Hybrid-Casual Monetizasyon Stratejisi (M3 & M7)
Monetizasyon sadece reklam izletmek değil, bir ekonomi tasarımıdır. Hybrid-casual oyunlar için hem reklam hem de IAP gelir modellerinin dengeli bir şekilde kullanılması önerilmektedir [4].
- **IAP Katmanı:** "Remove Ads" dışında, koleksiyon (skins), enerji sistemi ve "Skip Level" paketleri GDD'ye (M3) dahil edilmelidir. IAP, reklam gelirlerine kıyasla önemli ölçüde daha fazla gelir potansiyeli sunmaktadır [5].
- **Değişken Ödül (Variable Reward):** `Toy Pile`'daki şok dalgası gibi mekanikler, "Gacha" benzeri kutu açılışları veya nadir obje toplama sistemleriyle desteklenmelidir.
- **Metrik Güncelleme:** `ops/esikler.md` dosyasına LTV (Lifetime Value) ve ARPU (Average Revenue Per User) hedefleri eklenmelidir.

### C. Ajan Hattı Otomasyonu (Faz 3 Hazırlığı)
Ajanların (özellikle A3 GDD ve A5 Kod) `game-dev` becerisiyle senkronize edilmesi, üretim verimliliğini artıracaktır.
- **A5 (Kod) Güncellemesi:** A5 artık sadece Unity promptu yazan değil, `game-dev` pipeline'ını (Babylon.js + React) kullanarak çalışan bir "Web Game Developer" haline getirilebilir.
- **A4 (Görsel) Güncellemesi:** Manus'un dahili görsel üretim yetenekleri, asset listesini otomatik olarak `/manus-storage/` üzerinden oyuna bağlamalıdır.

---

## 3. Stratejik Yol Haritası (Aksiyon Listesi)

| Öncelik | Aksiyon | İlgili Makine | Hedef Çıktı |
|---|---|---|---|
| **P1** | **Babylon.js Entegrasyonu:** `game-dev` skill'ini M5 prototip hattına dahil et. | M5 | 48 saatte web-playable prototip. |
| **P1** | **Monetizasyon Revizyonu:** `Toy Pile` GDD'sini gerçek bir Hybrid-Casual ekonomisiyle güncelle. | M3 | IAP + Economy Design dokümanı. |
| **P2** | **Radar v2 (A2):** TikTok ve Meta Ad Library taramalarını `webpage_extract` ile otomatize et. | M1 | Haftalık otomatik aday kartı üretimi. |
| **P2** | **Eşik Güncellemesi:** 2026 pazar verilerine göre IAP ve LTV eşiklerini ekle. | ops/esikler.md | Yeni Hybrid-Casual cetveli. |
| **P3** | **Orkestrasyon (Faz 3):** Ajanlar arası dosya transferini (GameBrief -> GDD -> Code) otomatikleştir. | orchestrator/ | Sıfır manuel müdahale ile prototip. |

---

## 4. Sonuç ve Öneri

`GameFactory`, bir "Oyun Fabrikası" olma yolunda çok sağlam bir temele sahip. Ancak 2026'nın hızlı değişen pazarında **hız (web-first)** ve **derinlik (hybrid-monetization)** eksik kalıyor. 

**Önerim:** `Toy Pile` oyununun M6 testini yaparken, paralel olarak `game-dev` skill'i ile bir **Web-Playable** versiyonunu üretelim. Bu sayede hem Unity'nin hantallığından kurtuluruz hem de gerçek kullanıcı verisini (CPI/CTR) günler içinde toplarız.

---

**Onay:** Nazım Avcı (Producer) [ ] 
**Uygulama:** Manus (A1/A9)

## Referanslar

[1] Converge.ai. (2026, June 22). *Game Dev Pipeline Guide 2026: Design to Production Workflow*. [https://combos.converge.ai/blog/game-pipeline](https://combos.converge.ai/blog/game-pipeline)
[2] GameGrowthAdvisor. (2026, April 16). *Hybrid Casual Games 2026: Market Size, Trends ...*. [https://gamegrowthadvisor.com/blog/2026-04-16-hybrid-casual-game-design-strategy-2026/](https://gamegrowthadvisor.com/blog/2026-04-16-hybrid-casual-game-design-strategy-2026/)
[3] Cinevva. *Casual Games Trends in 2026 (What the Data Actually Says)*. [https://app.cinevva.com/guides/casual-games-trends-2026](https://app.cinevva.com/guides/casual-games-trends-2026)
[4] Adjoe. *Hybrid-casual Games: Users, Features, Monetization*. [https://adjoe.io/glossary/what-are-hybridcasual-games/](https://adjoe.io/glossary/what-are-hybridcasual-games/)
[5] Unity. (2026, June 22). *Game Monetization: Models, Strategies & How to Choose*. [https://unity.com/resources/mobile-game-monetization-guide](https://unity.com/resources/mobile-game-monetization-guide)
