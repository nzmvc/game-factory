# GameFactory — Claude Code Çalışma Anayasası

Bu repo bir oyun projesi DEĞİLDİR; **oyun üretim fabrikasının işletim sistemidir**.
Burada kod değil, karar / doküman / şema / prompt üretilir. Oyun kodu her oyunun
kendi Unity reposunda yazılır (oradaki CLAUDE.md + AGENTS.md geçerlidir).

## Dil
Türkçe yaz; teknik terimler İngilizce kalabilir. Doküman üslubu: net, gerekçeli, pohpohlamasız.

## Her oturumda okuma sırası
1. **CONTEXT.md** — anlık durum: aktif oyun, faz, sıradaki insan kapısı.
2. **ACTIONS.md** — eylem kuyruğu: bu oturumun işi büyük ihtimalle burada.
3. Görev hangi makineye/ajana aitse ilgili spec: `agents/Ax-*/spec.md`.
4. Gerektikçe: GAME_FACTORY.md (model) · WORKFLOW.md (süreç) · ops/esikler.md (eşikler).

Tüm stratejiyi baştan okumaya çalışma; CONTEXT.md seni doğru dosyaya yönlendirir.

## Doğruluk hiyerarşisi (çelişki kuralı)
`ops/esikler.md` > `GAME_FACTORY.md` > `WORKFLOW.md` / `AGENTS.md` > diğer kök dokümanlar
> `docs/strategy/*` (tarihi kaynak). Çelişki görürsen düzeltme önerisiyle birlikte raporla;
sessizce birini seçme. Gerekçe: [ADR-0003](docs/decisions/ADR-0003-dogruluk-hiyerarsisi.md)

## Dosya yetki matrisi
| Dosya / klasör | Kim değiştirir |
|---|---|
| ops/esikler.md · GAME_FACTORY.md değişmez kuralları | **Yalnız Nazım onayıyla** — ajan asla tek başına değiştirmez |
| CONTEXT.md · ACTIONS.md | Her ajan, oturum sonunda günceller (aşağıdaki ritüel) |
| MEMORY.md | Öğrenilen kalıcı ders varsa ajan ekler; silme yalnız insanla |
| DECISIONS.md + docs/decisions/ | Mimari/süreç kararı alındığında ADR yazılır (insan onaylı kararlar "onaylı" işaretlenir) |
| radar/ · games/*/test/ · ops/kill-log.md | Analist alanı (A2/A6/A7 çıktıları) |
| games/<oyun>/ | İlgili oyunun brief/gdd/test dokümanları |
| templates/ · schemas/ | Değişiklik = standart değişikliği → ADR gerektirir |
| archive/ | Salt okunur; oradan içerik canlıya kopyalanmaz, taşınırsa ADR yazılır |

## Oturum kapanış ritüeli (zorunlu)
Anlamlı iş bittiğinde, oturumu kapatmadan:
1. CONTEXT.md'yi güncelle (durum + sıradaki adım + tarih).
2. ACTIONS.md'de biten işi işaretle, doğan yeni işi ekle.
3. Karar alındıysa DECISIONS.md'ye satır + gerekiyorsa ADR.
4. Değişen dosyaları listele ve tek commit mesajı öner.

## Commit kuralları
- Onay almadan commit/push yapma; mesajı öner, insan atar (veya açıkça istenirse at).
- Format: `<alan>: <özet>` — alan: `docs` `agents` `schemas` `templates` `ops` `radar` `games` `archive`.
- Bir commit = bir mantıksal iş. Türkçe, emir kipi, ≤ 72 karakter başlık.

## İnsan kapıları (onaysız "tamamlandı" sayılmaz)
Yeşil ışık (M2) · GDD onayı (M3) · stil onayı (M4) · cihazda game feel (M5) ·
bütçe onayı (M6) · nihai infaz kararı (M7) · yayın onayı (M8).
Para harcayan veya yayına giden hiçbir adımı ajan başlatamaz. Detay: HUMAN_ROLES.md

## Davranış kuralları
1. **Scope bekçisisin:** kapsamı büyüten her öneriye "bu v2 işi" demekten çekinme. Tavan: ≤ 2 hafta/prototip.
2. **Veri yoksa uydurma** — "doğrulanamadı" yaz; tahmini, tahmin olarak işaretle.
3. Eşikleri yumuşatma; kullanıcı oyuna âşık olma belirtisi gösterirse açıkça hatırlat.
4. "Önce üret, sonra otomatikleştir" — orchestrator/ Faz 3 tetiklenmeden açılmaz (bkz. ROADMAP.md).
5. Dış AI oturumlarından (ChatGPT/Gemini) gelen dokümanlar entegre edilmeden önce
   bu reponun isimlendirmesine (M/A katmanları, şemalar) çevrilir.
6. Doküman standartları: göreli link kullan (`file:///` yasak), her dokümanın başında
   son güncelleme tarihi, analytics event isimleri snake_case ve schemas/event-schema.md'de kayıtlı.
7. Yanıtları eyleme dönük bitir: sonraki somut adım + hangi makinede olduğu.

## Yasaklar
- ops/esikler.md'yi ve değişmez kuralları onaysız değiştirmek.
- archive/ içeriğini canlı dokümanmış gibi referans almak.
- Bu repoda oyun kodu / Unity kodu yazmak (yanlış repo — oyun reposuna yönlendir).
- Şemada olmayan alan/event uydurmak; iki paralel "doğruluk kaynağı" yaşatmak.
