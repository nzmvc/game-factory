---
description: Yeşil ışık almış aday için yeni oyun kaydı açar (WORKFLOW.md §3 prosedürü)
argument-hint: <oyun-adi>
---

Yeni oyun başlatma prosedürünü uygula. Oyun adı: $ARGUMENTS

Ön koşul kontrolü (sağlanmıyorsa DURDUR ve eksiği raporla):
1. Bu oyun için yeşil ışık kararı var mı? DECISIONS.md'de kayıt ara; yoksa insan
   onayı olmadan devam etme (değişmez kural 3–4).

Adımlar:
1. `games/<oyun-adi>/` klasörünü aç: `README.md` (durum kartı — games/toy-pile/README.md
   formatında), `brief.md` (schemas/gamebrief.v1.json şemasına uygun iskelet; bilinen
   alanları aday kartından doldur, bilinmeyenlere "TBD" yaz ve completion score'u dürüst hesapla).
2. `games/README.md` kayıt defterine satır ekle.
3. CONTEXT.md'yi güncelle (aktif oyun / hat konumu) ve ACTIONS.md'ye açılış işlerini ekle
   (GDD üretimi, Unity repo kurulumu, şablon kopyalama).
4. Unity reposu için insan görevlerini listele: repo oluşturma (`game-<oyun-adi>`),
   templates/game-docs/ + game-repo-CLAUDE.md/AGENTS.md kopyalama talimatı.
5. Değişen dosyaları listele, commit mesajı öner. Sonraki somut adımı ve hangi
   makinede olduğunu söyle (normalde: M3 — A3 GDD üretimi, GDD onay kapısına hazırlık).
