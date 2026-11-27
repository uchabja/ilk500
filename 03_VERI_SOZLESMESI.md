# Veri sözleşmesi ve hesaplama kuralları

## A. Kaynak dosyaları (gerçek seed)

İki JSON dosyasının kökü dizidir. UTF-8. ID'ler string, eşsiz, değişmez. `ders_grubu` geriye uyum için tutulur ve `alan` ile eşit; filtre ve navigasyon için yalnız `alan` kullanılır. Alan enum: `AGS`, `EĞİTİM`, `ÖABT`. `ders` serbest Türkçe metin; `Genel` gerçek ders etiketi, “Tümü” UI filtresi. `baski_yili` nullable integer. `kapak` basename, `arsiv/kapaklar/{kapak}` yolu. Yayınevi ve ad ayrı alanlardır. `sira_no` kaynak dizisi içindeki özgün sıra. `kaynak_turu`: `soru_bankasi`, `cikmis_sorular`, `konu_anlatimi`, `yaprak_test`. Deneme türü ayrı dosyadan anlaşılır. Alan değişikliklerinde ID ve kapak adı aynı kalır.

### kitaplar.json — gerçek örnek (konu dizisi kısaltılmış)


```json
[
  {
    "id": "kitap-1",
    "sira_no": 1,
    "yayinevi": "Dizgi Kitapevi",
    "kitap_adi": "Çıkmış Sorular",
    "alan": "EĞİTİM",
    "ders_grubu": "EĞİTİM",
    "ders": "Genel",
    "baski_yili": null,
    "kapak": "kitap-1.png",
    "kaynak_turu": "cikmis_sorular",
    "sayfa_sayisi": 431,
    "icindekiler": [
      {
        "id": "kitap-1-konu-1",
        "konu": "Eğitimin Temel Kavramları",
        "baslangic_sayfasi": 5,
        "bitis_sayfasi": 60
      }
    ],
    "sayfa_sayisi_kaynagi": "arsiv"
  }
]
```

### denemeler.json — gerçek örnek
```json
[
  {
    "id": "deneme-1",
    "sira_no": 1,
    "yayinevi": "Yargı Yayınevi",
    "kitap_adi": "10’suz Olmaz",
    "alan": "EĞİTİM",
    "ders_grubu": "EĞİTİM",
    "ders": "Genel",
    "baski_yili": 2021,
    "kapak": "deneme-1.png",
    "deneme_sayisi": 10
  }
]
```

`icindekiler`: id, konu, baslangic_sayfasi (pozitif int), bitis_sayfasi (pozitif int veya null), opsiyonel modul_id. Aralıklar dahilî. Son konu bitişi null ise etkili bitiş = ilgili kitap/modül toplamı; toplam bilinmiyorsa konu yüzdesi bilinmiyor. Orijinal null'u sıfıra çevirmeyin. Diğer konuların sınırlarını koruyun. `sayfa_sayisi` int veya null; `sayfa_sayisi_kaynagi` = `arsiv` (mevcut değer), `icindekiler_tahmini` (en büyük başlangıç/bitiş), `bilinmiyor`, uygulamada kullanıcı düzenlerse `kullanici`. Tahmini toplamı küçük bir etiketle belirtin. Cevap anahtarı, kaynakça, çözümler dahil; otomatik çıkarma yok. Sayfa sayısı bilinmeyen kitap-6, kullanıcı sayfa toplamı girene kadar adet/konum kaydı alabilir ancak yüzdesi gösterilmez.

**Kitap-3 özel durum:** 512 toplam sayfa orijinal arşivden; üç modülde numaralar tekrar 3'ten başlıyor. `moduller` dizisi `{id,ad,sayfa_sayisi,sayfa_sayisi_kaynagi}`. Konularda `modul_id` eklendi. Modül tahmini minimumları 163,177,139; toplam 479, fiziksel kitap toplamı 512. Bu 33 sayfanın dağılımı bilinmiyor. Kullanıcı modül toplamlarını doğrular/düzenler; toplam 512 ile uyum kontrolü yap, uyumsuzlukta açıklama göster ve nihai toplam/modül değerlerini düzenlemeye yönlendir. Sayfa anahtarı (kitap_id, modul_id, sayfa_no); birbirinin aynısı sayılmaz. Genel kitap ilerlemesi 512 üzerinden ancak açıkça geçici gösterilir; modül dağılımı kesinleşmeden %100 varsayılmaz. Her modüle kendi sayfa haritası. Tahmini sınırın ötesindeki kayıtta önce modül toplamını düzenleme sun. Diğer kitaplarda modül yok (null).

## B. Kullanıcı kayıtları (mantıksal sözleşme, teknolojiden bağımsız)

Aşağıdaki örnekler gerçek kullanıcı verisi değildir. Alan isimlerini veya eşdeğer mantığı koruyun. Her kayıt benzersiz ID, yerel çalışma tarihi `YYYY-MM-DD`, oluşturma/güncelleme zamanı ISO-8601. Tarih filtreleri cihazın yerel takvim gününe göre, UTC'ye kaydırmayın. İlişkiler ID bazlı. Kaynak türü ve alan güncel kaynak meta verisinden okunur; düzenleme istatistikleri de günceller. Arşivleme geçmişi yok etmez.

```json
{
  "id": "ornek-calisma-1",
  "kitap_id": "kitap-37",
  "tarih": "2026-11-27",
  "modul_id": null,
  "sayfa_adedi": 6,
  "araliklar": [{"baslangic":81,"bitis":86,"durum":"tamamlandi"}],
  "dogru":24,"yanlis":5,"bos":1,
  "sure_dakika":null,"not":null,
  "konu_id":null,
  "olusturma_zamani":"2026-11-27T10:00:00+03:00",
  "guncelleme_zamani":"2026-11-27T10:00:00+03:00"
}
```

- Adet modunda `araliklar=[]`, `sayfa_adedi>0`, kullanıcı sonradan kesin aralık eşleştirebilir. Eşleştirme aynı kaydı günceller, yeni çalışma yaratmaz. Aralık modunda sayfa_adedi = aralık birleşiminin kardinalitesi; farklı aralıklar örtüşemez veya birleştirilir. `durum` = `tamamlandi` veya `kismi`. Tekrar çalışılan sayfalarda aynı kayıt içi tekrar değil, yeni kayıt olarak eklenir. Modül varsa her kayıt bir modüle ait; modüller arası çalışmayı ayrı kaydet.
- D/Y/B nullable nonnegative integer; üçü de boş olabilir; elle 0 ayrı anlamlı. Sadece toplam sayı isteyen kullanıcı için opsiyonel `toplam_soru` alanı açılabilir; D/Y/B tam ise toplam otomatik, kısmi ise elle toplam >= bilinen bileşenler. Sayfa bazlı ayrıntı modu: her sayfa için aynı tip sonuç içeren çocuk satırlar, ana sonuç bunlardan hesaplanır ve tekrar toplanmaz. Konu ataması isteğe bağlı; otomatik konu sonucu yalnız kesin tek konuya düşen konumlu kayıt ya da ayrı konu ayrıntısı ile mümkündür. Birden fazla konuya ait toplam D/Y/B'yi sayfa sayısına göre dağıtma.

```json
{
  "id":"ornek-deneme-kaydi-1","deneme_kitabi_id":"deneme-4",
  "deneme_no":1,"tarih":"2026-11-27","tamamlandi":true,
  "sonuc_modu":"toplam","dogru":16,"yanlis":3,"bos":1,
  "ders_sonuclari":[],"sure_dakika":null,"not":null,
  "olusturma_zamani":"2026-11-27T10:00:00+03:00",
  "guncelleme_zamani":"2026-11-27T10:00:00+03:00"
}
```

Ders bazlı modda `sonuc_modu=ders_bazli`, `ders_sonuclari=[{"ders":"Tarih","dogru":16,"yanlis":3,"bos":1}]`; üst D/Y/B null veya türetilmiş salt okunur, yalnız çocuk sonuçları sayılır. Ders isimleri seçilebilir/eklenebilir, aynı kayıt içinde tekrar ders yok. Deneme numarası 1..deneme_sayisi, tekrarlar ayrı kayıt ID. Deneme soru adetleri arşivde mevcut değil; otomatik 20/80 vb. varsaymayın. Deneme tamamlandı işareti sonuç yokken de geçerlidir. Deneme toplamını azaltırken kayıtlı deneme numaraları aşılırsa düzenleme engellenir veya kullanıcı çözüm seçer. Kullanıcı metadata: favori, arsivlendi, özel kapak ve kullanıcı kaynakları; ayarlar: tema, hedef türü/değeri. Yedek şema sürümü, kaynaklar (kullanıcı düzenlemeleri dahil), çalışma kayıtları, deneme kayıtları, ayarlar, özel kapaklar. Geri yükleme öncesi şema/ilişki doğrula, önizleme ve onay al, tek atomik işlem; başarısızsa eskisini koru. Kayıtlar, ayarlar ve seed için kalıcı depolama şart.

## C. Türetilmiş metrikler (tek hesaplama katmanı)

- Kitap ilerleme = benzersiz tamamlanmış sayfa anahtarları / toplam sayfa ×100; bilinmeyen toplamda null. Kısmi durum, aynı sayfanın tamamlanmış kaydı varsa tamamlanmış kabul edilir. Silme/düzenleme sonrası tekrar hesapla. Kitap kalan = toplam − benzersiz tamamlanan. Konu = tamamlanmış sayfaların etkili konu aralığı ile kesişimi / aralık uzunluğu. Konu sonuçları birden fazla konuya tahmini dağıtılmaz.
- Deneme ilerleme = en az bir tamamlandı kaydı olan benzersiz deneme no / toplam deneme ×100. Tekrar hacmi artırır, ilerlemeyi artırmaz.
- Çalışılan sayfa hacmi = seçili tarihlerdeki kayıtların sayfa_adedi toplamı (tekrar dahil). Benzersiz tamamlanan sayfa ayrı metriktir. Konumsuz kayıt sadece hacim. Deneme adedi = tamamlanmış deneme oturumları; benzersiz deneme ilerlemesi ayrı.
- Toplam soru: D/Y/B tam girilmişse toplamları; yalnız toplam biliniyorsa onu; eksik bileşen varsa ve toplam yoksa kesin toplam bilinmiyor. Bilinen toplamların toplamını göster ve “X kaydın soru sayısı eksik” belirt. D/Y/B sayıları bilinen bileşenlerin toplamıdır, eksik kapsam etiketi ile. Oranlar yalnız D/Y/B üçü de bilinen kayıtlar üzerinden, ağırlıklı: doğru = ΣD/Σ(D+Y+B); yanlış = ΣY/Σ(D+Y+B); boş = ΣB/Σ(D+Y+B). Payda 0 => null, — göster. Ders bazlı satırları atomik kapsam olarak kullan; toplam-only Genel kayıtlar başka derse atanmaz. Tarih/ders/alan filtreleri birlikte uygulanır. Yanlış oranı sıralaması varsayılan en az 20 tam sonuçlu soru, ayarlanabilir; soru sayısı yanında.
- Ana alan kartı ayrı iki oran: toplam bilinen sayfalarda tamamlanan / toplam bilinen sayfa (bilinmeyen toplamı olan kitapları kapsam dışı bırak ve bildir), tamamlanan deneme / toplam deneme. Farklı birimleri tek ortalamaya katma. Arşivlenenler aktif envanter/ilerleme dışında; tarihsel hacim ve sonuçlar varsayılan dahil, filtreyle hariç tutulabilir.
- Takvimde günlük bilinen soru toplamı; hiç kayıt yok => boş, kayıt var toplam bilinmiyor => nokta/“?”; bilinen toplam 0 => 0. Bir günde karışık veri varsa toplam ve eksik kayıt etiketi. Seride geçerli kayıt olan her takvim günü bir gün. Günlük hedef yalnız tanımlıysa göster.
