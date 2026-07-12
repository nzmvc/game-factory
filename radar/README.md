# radar/ — Pazar Radarı Çıktıları (M1)

**Yazma alanı:** Analist (A2 promptlarıyla) · Ritim: haftalık 60–90 dk (Pzt)

## Yapı

```
radar/
└── taramalar/
    └── 2026-W30.md      # ISO hafta numarasıyla haftalık tarama
```

## Haftalık tarama dosya formatı

Her tarama dosyası şunları içerir:

1. **Başlık bloğu:** tarih, tarayan, kullanılan kaynaklar.
2. **10 aday kartı** — [schemas/aday-karti.v1.yaml](../schemas/aday-karti.v1.yaml) formatında,
   kanıtsız kart yazılmaz.
3. **Kapanış paragrafı:** haftanın en güçlü 2 adayı ve nedeni.

Prompt seti: [agents/A2-radar/tarama-promptlari.md](../agents/A2-radar/tarama-promptlari.md)

## Akış

Tarama → Pzt senkronunda sunum → seçilen kartlar M2 skorlamasına (A1) →
yeşil ışık alan kart `games/<oyun>/brief.md`'ye dönüşür. Sıfır aday da geçerli bir sonuçtur.
