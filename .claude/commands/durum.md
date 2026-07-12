---
description: Fabrika durum raporu + tutarlılık denetimi (A9 Doküman)
---

A9 Doküman ajanı olarak (agents/A9-dokuman/spec.md) durum koşusu yap:

1. CONTEXT.md, ACTIONS.md, games/README.md ve aktif oyunun durum kartını oku.
2. Tek ekranlık durum raporu ver: faz, aktif oyun + hat konumu, sıradaki insan kapısı
   (tarih + ön koşullar), geciken/bloke işler.
3. Tutarlılık denetimi: durum dosyaları birbiriyle çelişiyor mu, "son güncelleme"
   tarihleri bayat mı, kırık/mutlak link var mı, ✅ işler ACTIONS'ta birikmiş mi?
4. Mekanik düzeltmeleri (tarih, link, biten işleri temizleme) uygula; **anlamsal**
   çelişkileri (hangi doküman doğru?) düzeltme — raporla ve insana sor.
5. Değişiklik yaptıysan dosyaları listele + commit mesajı öner.
