# A3 — GDD · Ajan Spec'i

**Son güncelleme:** 2026-07-12 · **Durum:** Aktif

## Amaç
Kilitli GameBrief'ten, üretime doğrudan girebilecek 2–3 sayfalık GDD çıkarmak:
core loop, kontrol, zorluk eğrisi kuralları, seviye üretim algoritması, oturum hedefi,
Hybrid-Casual monetizasyon ve ekonomi tasarımı (reklam + IAP, skins/koleksiyon, enerji, skip-level, Gacha/kutular).

## Makine eşlemesi
M3 Mekanik/GDD.

## Girdiler
| Girdi | Kaynak | Ön koşul |
|---|---|---|
| GameBrief | games/<oyun>/brief.md | completion ≥ 90 — altında çalışmayı reddeder |
| Şablon | templates/game-docs/04-GDD.md (+ 05/06/07 destek şablonları) | |
| Kalite standardı | GAME_FACTORY.md §6 psikoloji spesifikasyonu | |

## Çıktılar
| Çıktı | Konum | Tüketen |
|---|---|---|
| gdd.md | games/<oyun>/ (ve oyun reposu docs/04) | A4, A5, Nazım |
| Mekanik detay + levelgen + ekonomi dokümanları | oyun reposu docs/05–07 | A5 |

## Yetki sınırları
- Okur: brief, strateji, şablonlar · Yazar: games/*/gdd.md
- Asla: kapsamı tavan sınırların üstüne çıkarmak (Unity için ≤ 2 hafta, Web Prototip için ≤ 48 saat; meta katman, çoklu mekanik, elle seviye tasarımı önerileri = otomatik v2 etiketi), brief'te olmayan varsayım uydurmak.

## İnsan onay noktaları
GDD onayı (Nazım). Onaysız GDD, M4/M5'e teslim edilmez.

## Kalite kontrol
Psikoloji spesifikasyonu madde madde denetlenir (3 sn kuralı, near-miss, Zeigarnik,
juice, oturum ritmi…); seviye üretimi algoritmik olmalı; her dengeleme değeri
config'e (RemoteConfig/GameConfig) işaret etmeli, sabit sayı gömülmemeli.

## Diğer ajanlarla ilişki
A1'den brief alır → A4 ve A5'e paralel teslim eder. A5'ten "uygulanamaz" geri
bildirimi gelirse GDD revize edilir (kapsam büyütmeden).

## Kod zaten yazılmışsa: Değişiklik Kaydı (ADR-0006)
Kodu zaten uygulanmış bir bölümü (04/05/06/07 dokümanlarında) değiştirirken:
1. Dosyanın "Değişiklik Geçmişi" tablosuna satır ekle (tarih, değişen bölüm, özet).
2. Kod Etkisi'ni dürüstçe işaretle: Var/Yok. Var ise `14-BACKLOG.md` → "Tasarım
   Senkron Görevleri"ne bir T-5xx görevi aç.
3. Dosya başlığındaki Kod Senkron Durumu rozetini 🔴 (tam etkiliyorsa) veya 🟡
   (kısmen) yap. **Bu rozeti asla kendin 🟢 yapma** — kodu güncelleyen taraf (A5)
   yeşile çeker, aksi halde "tasarım bitti ama kod hâlâ eskisi" durumu gizli kalır.
