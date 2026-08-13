# EnglishLab A1

Türkçe konuşan öğrenciler için A1 seviyesi İngilizce öğrenme ve pratik platformu.
Tek bir HTML dosyası — derleme adımı, bağımlılık ve sunucu gerektirmez.

**Canlı:** _(dağıtımdan sonra buraya adresi yaz)_

---

## İçerik

| | Sayı |
|---|---|
| Kelime | 594 (32 kategori) |
| Düzensiz fiil | 36 |
| Gramer konusu | 19 (114 test sorusu) |
| Okuma parçası | 8 (40 anlama sorusu) |
| Zıt / eş anlam çifti | 74 |
| Yazma konusu | 16 |
| Sınav türü | 6 |

## Bölümler

**Vocabulary** — 7 çalışma modu: Review (aralıklı tekrar), Flashcards, Matching,
Gap Fill, Quiz, Listening, Opposites. Her kelimede görsel, örnek cümle ve
tarayıcının konuşma sentezi ile telaffuz.

**Verbs** — Düzensiz fiillerde 5 mod: V1·V2·V3 yazma, çoktan seçmeli,
eşleştirme, 60 saniyelik hız turu ve tam liste.

**Grammar** — 19 A1 konusu; kural tabloları, sık yapılan hatalar ve konu testleri.

**Reading** — 8 metin. Altı çizili kelimelere dokununca Türkçesi ve telaffuzu
çıkar; sonunda doğru/yanlış ve çoktan seçmeli anlama soruları.

**Writing** — Günlük tutma. Her gün bir konu, hazır cümle başlangıçları,
kelime bankası, otomatik taslak kaydı ve yazıları dışa aktarma.

**Exams** — Süreli sınavlar (kelime, fiil, gramer, okuma, karma, seviye belirleme).
Soru haritası, "sonra dön" işareti, cevap anahtarı ve geçmiş sonuçlar.

**Progress** — Günlük hedef, çalışma serisi, kategori bazlı ilerleme, tekrar
kutularının dağılımı, sınav ortalaması.

## Aralıklı tekrar (spaced repetition)

Her kelimenin bir kutusu vardır. Doğru bilirsen kutu yükselir ve kelime daha geç
sorulur; yanlış yaparsan kutu sıfırlanır ve aynı oturumda tekrar çıkar.

| Kutu | Sonraki tekrar | Soru biçimi |
|---|---|---|
| 0 | aynı gün | çoktan seçmeli |
| 1 | 1 gün | çoktan seçmeli |
| 2 | 2 gün | yazma |
| 3 | 4 gün | yazma |
| 4 | 1 hafta | yazma |
| 5 | 2 hafta | yazma |
| 6 | 1 ay — ustalaşıldı | yazma |

Günde en fazla 10 yeni kelime tanıtılır, oturum 20 kartla sınırlıdır.

## Çalıştırma

```bash
# En basiti: dosyaya çift tıkla.
# Telefondan test için yerel sunucu:
python -m http.server 8000
# Telefonun tarayıcısında: http://<bilgisayarın-IP-adresi>:8000
```

## İçerik ekleme

Tüm veriler `index.html` içinde, düz JavaScript dizileri hâlinde durur.
Arayüz sayaçları, sınav havuzları ve ilerleme çubukları eklediğin içeriği
otomatik kapsar — başka hiçbir yeri değiştirmen gerekmez.

**Kelime**

```js
CATEGORIES.push({
  id:"benzersiz-ad", name:"Category Name", tr:"Türkçe Adı",
  icon:"🙂", group:"Daily Life",
  words:[
    { en:"word", tr:"kelime", e:"🙂",
      s:"An English example sentence with the word.",
      st:"Cümlenin Türkçesi." }
  ]
});
```

`s` alanındaki cümle `en` kelimesini içermelidir — boşluk doldurma soruları
oradan üretilir. Çoğul ve üçüncü tekil çekimleri (`words`, `has`, `goes`)
otomatik tanınır.

**Gramer konusu**

```js
GRAMMAR.push({
  id:"benzersiz-ad", icon:"📐", title:"Topic", sub:"Kısa açıklama",
  html:`<p>Anlatım…</p>`,
  ex:[{ en:"Example sentence.", tr:"Türkçesi." }],
  quiz:[{ q:"Soru", o:["A","B","C","D"], a:0, ex:"Neden doğru olduğu" }]
});
```

Sonra `GRAMMAR_ORDER` dizisine `id`'yi istediğin sıraya ekle.

**Okuma parçası** — `READINGS` dizisine ekle. Metinde `[word|türkçesi]`
biçiminde işaretlediğin kelimeler tıklanabilir sözlük balonuna dönüşür.

## Veri ve gizlilik

- Tüm ilerleme **yalnızca tarayıcının `localStorage` alanında** tutulur.
- Uygulama hiçbir ağ isteği yapmaz: `fetch`, `XMLHttpRequest`, WebSocket ve
  dış kaynak (CDN, font, görsel) yoktur. Yazdığın günlükler dâhil hiçbir veri
  cihazından çıkmaz.
- Aynı bilgisayarı birden fazla kişi kullanıyorsa "Profil" düğmesinden isim
  girerek ilerlemeler ayrılabilir.
- "Yedeği indir" ile veriler JSON olarak alınabilir; geri yüklerken dosya
  doğrulamadan geçirilir (tür zorlaması, uzunluk sınırı, bilinmeyen alanların
  atılması).
- Sunucu ve hesap olmadığı için ilerleme cihaza özeldir; telefon ve bilgisayar
  ayrı ayrı ilerleme tutar.

## Dağıtım

Statik dosya olduğu için herhangi bir statik barındırma servisi çalışır.
Vercel için depoyu bağlaman yeterli — ayar gerekmez. `vercel.json` içinde
güvenlik başlıkları (CSP, `X-Frame-Options`, `Referrer-Policy`,
`Permissions-Policy`) tanımlıdır. `connect-src 'none'` sayesinde sayfa
tarayıcı düzeyinde de hiçbir yere veri gönderemez.

İleride mikrofon gerektiren bir özellik (konuşma tanıma) eklersen
`vercel.json` içindeki `Permissions-Policy` satırından `microphone=()`
kısıtını kaldırman gerekir.

## Tarayıcı desteği

Chrome, Edge, Firefox ve Safari'nin güncel sürümlerinde çalışır.
Sesli okuma tarayıcının konuşma sentezi motorunu kullanır; Chrome ve Edge'de
en iyi sonucu verir, bazı Firefox kurulumlarında İngilizce ses paketi
yüklü olmayabilir.

## Teknik

Tek dosya, sıfır bağımlılık, derleme adımı yok. Yaklaşık 294 KB.
Açık ve koyu tema; tema seçilmediğinde cihazın sistem ayarını izler.
Mobil ve masaüstü için ayrı düzenler.
