# Manus Talimatı — Web Araştırma Görevleri (M1 / M6 destek)

**Son güncelleme:** 2026-07-14 · Eşik damgası: [ops/esikler.md](../../ops/esikler.md) 2026-07-12 sürümü
**Şema:** [schemas/aday-karti.v1.yaml](../../schemas/aday-karti.v1.yaml) · **Ajan spec'leri:** [A2 Radar](../A2-radar/spec.md) · [A6 Test](../A6-test/spec.md)

Manus otonom çalışır: görevi baştan eksiksiz ver, ara yönlendirme bekleme.
Kullanım alanı **yalnız araştırmadır** — M1 radar taraması, rakip kreatif analizi,
kısıt/politika doğrulaması. Karar, skorlama onayı, kampanya kurulumu, store işlemi
Manus'a verilmez (para ve karar insan kapısındadır).

Kullanım: aşağıdaki görev şablonlarından birini doldur, sonuna ORTAK KURALLAR
bloğunu ekle, tek mesaj olarak gönder.

## ORTAK KURALLAR (her görevin sonuna eklenir)

```
KURALLAR — ihlali çıktıyı geçersiz kılar:
1. Her iddiaya kaynak: URL + erişim tarihi. Kaynak bulamadığın alana
   "doğrulanamadı" yaz; asla tahminle doldurma. Tahmin veriyorsan
   "tahmin" etiketi koy.
2. Hesap açmak, giriş yapmak, form doldurmak, satın almak, deneme
   aboneliği başlatmak, herhangi biriyle iletişime geçmek YASAK.
   Ücretsiz/anonim erişimle görünen veriyle yetin; görünmüyorsa
   "doğrulanamadı" yaz.
3. Site kullanım koşullarını ihlal eden scraping yapma.
4. Karar verme: puan alanların 1–5 önerisi yalnızca öneridir; seçim ve
   skor onayı insan işidir. "Şunu seçmeliyiz" deme, veriyi sun.
5. Çıktı dili Türkçe (oyun/şirket adları ve teknik terimler İngilizce
   kalır). Çıktı tek bir markdown dosyasıdır; başında
   "Son güncelleme: YYYY-AA-GG" satırı bulunur; sonunda tüm kaynakların
   listesi yer alır.
```

## Görev şablonu A — Haftalık radar taraması (M1 · A2 işi)

```
GÖREV: Hyper/hybrid-casual mobil oyun pazarında haftalık radar taraması
yap ve en fazla 10 aday kartı üret.

ARANAN PROFİL: tek parmakla, portre modda, düşünmeden oynanan,
"satisfying" mekanikler (sand sort, screw puzzle, goods sorting tarzı).

ELEME — listeye hiç girmez: match-3 / meta-ağırlıklı türler · multiplayer ·
hikâye tabanlı · elle yoğun içerik üretimi gerektiren · lisanslı IP
gerektiren konseptler.

KAYNAKLAR: Google Play + App Store top charts (US ve TR) · Meta Ad
Library · TikTok Creative Center · AppMagic (ücretsiz tier) ·
PocketGamer.biz · Deconstructor of Fun. Takip publisher'ları: Voodoo,
Rollic, SayGames, Homa, Supersonic, Azur Games, Kwalee, Lion Studios.

HER ADAY KARTINDA ŞU ALANLAR (aday-karti.v1 şeması):
id (R-YYYY-AA-GG-01…) · tarih · origin: radar · mekanik_adi ·
referans_oyunlar (1–3 oyun) · kanit (chart pozisyonu / reklam yoğunluğu /
indirme tahmini + KAYNAK URL + erişim tarihi) · kontrol_semasi
(tap/drag/swipe/hold) · icerik_uretimi (algoritmik / yarı-elle / elle) ·
uc_sn_okunabilirlik (1–5) · gelistirme_maliyeti (1–5, ucuz=5) ·
juice_potansiyeli (1–5) · reklam_izlenebilirlik (1–5) ·
rekabet_yogunlugu (düşük/orta/yüksek) · trend_ivmesi
(yükseliyor/plato/düşüşte) · twist_fikri (kanıtlanmış mekaniğe 1 fark) ·
notlar.

KALİTE: kanit alanı boş veya kaynaksız olan kart geçersizdir. 10 sağlam
kart bulamıyorsan daha az teslim et — kart doldurmak için kalite düşürme;
sıfır aday da geçerli bir sonuçtur.

ÇIKTI: "radar-taramasi-YYYY-Www.md" adında tek markdown dosyası:
1) 5 maddelik yönetici özeti · 2) aday kartları · 3) kaynak listesi.
```

## Görev şablonu B — Rakip kreatif analizi (M6 hazırlığı · A6 işi)

```
GÖREV: Şu oyunların reklam kreatiflerini analiz et: <oyun listesi — örn.
Zen Match, Triple Match 3D, Match Factory!, Tile Busters>.

İNCELE: Meta Ad Library ve TikTok Creative Center'da her oyun için
bulabildiğin aktif kreatifler. Oyun başına en çok tekrarlanan 3–5
kreatif kalıbını çıkar.

HER KALIP İÇİN: hook türü (fail / satisfying / challenge / …) · ilk 3
saniyede ekranda ne var · süre ve format (9:16 video? gerçek oynanış mı
render mı?) · metin/ses kullanımı · kaç varyantını gördüğün + kaynak
linkleri.

SONUÇ BÖLÜMÜ: kalıpların karşılaştırma tablosu + "<aktif oyun> için bu
kalıplardan hangileri uyarlanabilir" bölümü (öneri etiketiyle; seçim
insanın).

ÇIKTI: "rakip-kreatif-analizi-YYYY-AA-GG.md" adında tek markdown dosyası.
```

## Teslim alındığında (insan + Claude Code denetimi)

1. Kanıt linklerinden 2–3 tanesini rastgele aç, iddiayla tutarlılığını kontrol et
   (halüsinasyon taraması) — tutmayan kart iade edilir.
2. Terminoloji/şema denetiminden geçir ([AGENTS.md](../../AGENTS.md) §4) ve Claude Code
   oturumuyla `radar/taramalar/` veya `games/<oyun>/test/` altına işle.
3. Skorlama (M2 cetveli) burada değil, [ops/esikler.md](../../ops/esikler.md) cetveliyle
   A1/Nazım oturumunda yapılır.
