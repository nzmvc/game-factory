# AGENTS — Ajan Mimarisi

**Son güncelleme:** 2026-07-12 · Rol kartları: [AGENT_ROLES.md](AGENT_ROLES.md) · Spec'ler: [agents/](agents/)

Bu dosya ajanların **nasıl çalıştığını** tanımlar: organizasyon, haberleşme, yetki
sınırları, doğrulama. Kim olduklarını AGENT_ROLES.md tanımlar.

> **Claude dışı bir kod ajanı bu repoda çalışıyorsa:** bu dosya senin giriş noktan.
> Operasyonel kurallar (okuma sırası, dosya yetkileri, kapanış ritüeli, yasaklar)
> [CLAUDE.md](CLAUDE.md)'de tanımlıdır ve araçtan bağımsız geçerlidir — onu da uygula.

---

## 1. Temel ilkeler

1. **Ajan = makinenin otomasyon kabuğu.** Her ajan M0–M8 hattındaki bir adımı işletir;
   süreci değiştirmez. Süreç değişikliği = ADR + insan onayı.
2. **Önce prompt, sonra kod.** Faz 1–2'de her ajan bir talimat dosyasıdır
   (`agents/Ax-*/spec.md` + promptlar); insan onu bir LLM oturumunda elle işletir.
   Faz 3'te aynı spec'ler SDK orkestrasyonuna taşınır — spec değişmez, işletim değişir.
3. **İnsanla konuşan tek ajan A1 Producer'dır** (otomasyon fazında geçerli kural;
   bugün her oturum fiilen A1 şapkasıyla açılır).
4. **Karar ajanı yoktur.** Ajanlar rapor, öneri ve skor üretir; ✔ kapılarında karar insanındır.
   M7'de karar mantığı deterministik eşik tablosudur — LLM yalnız "neden" raporu yazar.

## 2. Haberleşme: dosya-tabanlı sözleşmeler

Ajanlar birbirine mesaj atmaz; **repo üzerinden, şemalı dosyalarla** konuşur.
Git = mesaj kuyruğu, dosya = mesaj, şema = protokol.

```
A2 Radar ──aday kartı (schemas/aday-karti.v1.yaml)──▶ radar/taramalar/
                                                          │
A1 Producer ──GameBrief (schemas/gamebrief.v1.json)──▶ games/<oyun>/brief.md
                                                          │
A3 GDD ──gdd.md (templates/game-docs/04-GDD.md)──▶ games/<oyun>/
                                                          │
A4 Görsel ──stil + asset listesi──▶ games/<oyun>/   A5 Kod ──build──▶ oyun reposu
                                                          │
A6 Test ──kreatif brief + kampanya sonuçları──▶ games/<oyun>/test/
                                                          │
A7 İnfaz ──karar raporu──▶ games/<oyun>/test/ + ops/kill-log.md
                                                          │
A8 ASO ──store paketi──▶ games/<oyun>/aso/
```

Kural: bir ajanın çıktısı, sonraki ajanın **girdi şemasına** uymuyorsa hat durur;
uymayan çıktı "tamamlandı" sayılmaz.

## 3. Yetki sınırları (okuma/yazma matrisi)

| Ajan | Okur | Yazar | Asla yapamaz |
|---|---|---|---|
| A1 Producer | Tüm repo | games/*/brief.md · DECISIONS.md taslağı · CONTEXT/ACTIONS | Karar vermek; eşik değiştirmek |
| A2 Radar | ops/esikler.md · schemas/ | radar/taramalar/ | Aday kartına kanıtsız veri yazmak |
| A3 GDD | brief + strateji + templates | games/*/gdd.md | Kapsamı 2 hafta tavanının üstüne çıkarmak |
| A4 Görsel | gdd.md | games/*/stil-rehberi.md, asset listesi | Store asset'ine CPI testinden önce efor |
| A5 Kod | gdd + şablon promptlar | **Oyun reposu** (bu repoda yalnız prompt dosyaları) | Bu repoda oyun kodu yazmak; şasiyi oyuna göre değiştirmek |
| A6 Test | gdd + kreatif analiz | games/*/test/ | Kampanyayı bütçe onayı olmadan başlatmak |
| A7 İnfaz | test verileri + ops/esikler.md | karar raporu · ops/kill-log.md | Eşik yumuşatmak; karar vermek |
| A8 ASO | oyun + karar raporu | games/*/aso/ | Yayın onayı olmadan store işlemi |
| A9 Doküman | Tüm repo | CONTEXT/ACTIONS/MEMORY · docs/ · link/şema bakımı | İçerik kararı almak; eşik/kural değiştirmek |

Ortak sınır: `ops/esikler.md`, `GAME_FACTORY.md` değişmez kuralları ve `schemas/`
yalnız insan onaylı ADR ile değişir.

## 4. Çapraz doğrulama

- **Şema kontrolü:** Her teslimde alıcı ajan, girdiyi şemaya karşı doğrular
  (GameBrief completion ≥ 90 olmadan A3 çalışmaz).
- **Eşik bekçisi:** A7 raporu her zaman ham veri + eşik tablosu karşılaştırması içerir;
  yorum ve veri ayrı bölümlerde yazılır (kaynağı karışmaz).
- **Kalite denetimi:** A3/A4 çıktıları GAME_FACTORY.md §6 psikoloji spesifikasyonuna
  karşı madde madde denetlenir; A9 doküman tutarlılığını (link, tarih, şema) denetler.
- **Dış oturum kuralı:** ChatGPT/Gemini oturumlarından gelen her doküman entegre
  edilmeden önce bu reponun isimlendirmesine çevrilir (denetim: A9).

## 5. Yeni ajan ekleme

1. `agents/_sablon/spec.md` kopyalanır → `agents/A<n>-<isim>/spec.md` doldurulur.
2. Hangi makineye hizmet ettiği, girdi/çıktı şemaları ve yetki satırı (bu dosya §3) tanımlanır.
3. AGENT_ROLES.md'ye rol kartı özeti eklenir; ADR yazılır (yeni ajan = mimari karar).
4. İnsan onayı → CONTEXT.md güncellenir. Numara çakışması yasak; makine eşlemesi
   olmayan ajanlar A9'dan sonra numara alır.

## 6. Claude Code entegrasyonu

- Bu repoda oturum açan Claude Code, [CLAUDE.md](CLAUDE.md) anayasasına tabidir ve
  görev hangi ajana aitse o spec'i yükler.
- `.claude/commands/` sık akışları kısayola bağlar (`/new-game`, `/radar`, `/durum`).
- `.claude/agents/` bazı ajanların Claude Code subagent tanımlarını içerir
  (ör. A2 radar taraması arka planda ayrı bağlamda koşabilir).
- Faz 3'te orkestrasyon SDK'sı seçilir (bkz. ROADMAP.md); ajan spec'leri aynen taşınır.
