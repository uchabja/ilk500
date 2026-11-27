# Ekran bazlı ürün gereksinimleri

Referans boyutu 390×844, telefon portre. Uzun içerik kaydırılır. Alt navigasyon ana ve alan listelerinde sabit; detayda geri ok ve ilgili alan bağlamı korunur. Her ekran gerçek veriden beslenir. Mockup numaraları ile eşleşir.

| No | Ekran | İçerik ve etkileşim |
|---|---|---|
| 01 | Ana Sayfa | Tarih, ayarlar, bugün soru/sayfa/deneme, D/Y/B, günlük hedef varsa progress, hızlı soru/deneme butonları, üç alanın kaynak sayıları ve ayrı sayfa/deneme ilerlemeleri, aylık takvim, son çalışılanlar, favoriler. Alan kartına dokun → alan. Son kitaba dokun → detay. Hızlı giriş → kaynak seçici. |
| 02 | Alan / Soru Bankası | Başlık ve +; üç alt sekme, anlık kitap/yayınevi araması, ders chip'leri ve filtre paneli, sıralama, görünen kitap sayısı. Dikey gerçek kapak, başlık, yayınevi, ders, kaynak türü, benzersiz sayfa x/y, yüzde ve progress bar, favori. Bilinmeyen toplamda “Sayfa sayısını gir”. Tümü/başlanmamış/devam eden/tamamlanmış; yayınevi/kaynak türü/favori/arşiv. Sıralama isim, arşiv sırası, ilerleme, kalan sayfa, son çalışma, yanlış oranı. |
| 03 | Alan / Deneme | Aynı liste ve filtre davranışı; progress tamamlanan farklı deneme/toplam, varsa D/Y/B ve son çalışma. + deneme kitabı ekler. |
| 04 | Kitap detay / Konular | Kapak, kitap adı, ders, yayınevi, favori, düzenle menüsü, benzersiz sayfa x/y ve yüzde, D/Y/B, yeni çalışma CTA. Konular/Sayfalar/Geçmiş sekmeleri. Konu satırında ad, aralık, progress, kalan sayfa. Dokununca aralıkla kayıt formu açılabilir. Modüllü kitapta modül seçici. |
| 05 | Kitap detay / Sayfalar | Sayfa haritası (sayfa başına hücre, tamamlanmış/kısmi/çalışılmamış), aralık seçme, sayfaya dokunup durum ve geçmiş görüntüleme, sayfa atla. Konumsuz kayıt varsa uyarı ve eşleştirme butonu. Büyük kitaplarda sayfa grupları ve sanallaştırma. |
| 06 | Hızlı çalışma kaydı | Kaynak seçili veya seçilebilir, tarih (bugün), aralık/ayrık aralık/adet/sayfa bazında mod; konum ve adet, otomatik hesap, tamamlandı veya kısmi, D/Y/B opsiyonel, süre/not opsiyonel, kaydet. Toplam soru otomatik. Konu çakışmaları gösterilir. Kaydet sonrası geri al ve son kayda git. |
| 07 | Deneme kitabı detay | Kapak, x/y tamamlandı, yüzdelik, numaralı denemeler (tamamlandı işareti), son deneme kayıtları, sıradakine devam, favori, düzenle. Numara seçilince sonuç girişine geç. Eski denemede geçmiş + tekrar çöz. |
| 08 | Deneme kayıt ekranı | Deneme numarası, tarih, tamamlandı; Toplam/Ders Bazlı toggle, D/Y/B, isteğe bağlı süre/not. Sadece tamamlandı olarak kaydet mümkün. Ders bazlı modda satır ekle/çıkar, toplam otomatik ve salt okunur. Önceden kayıtlı sonuç düzenle veya tekrar olarak kaydet seçenekleri. |
| 09 | Alan / İstatistik | Tarih filtresi, ders/kaynak türü filtreleri, sayfa çalışma hacmi, benzersiz sayfa, soru, deneme girişleri, doğru-yanlış-boş ve oranlar, günlük grafik, ders karşılaştırması, yanlış oranı kitap sıralaması (varsayılan en az 20 tam sonuçlu soru, düzenlenebilir), kaynak envanteri; konu bazlı ilerleme kitaplara göre. Kartlar ilgili filtreli listeye gider. |
| 10 | Takvim / Gün detay | Ay değiştir, gün hücresi soru sayısı ve yoğunluk; gün seç, toplamları ve kayıt listesini aç, + geçmiş tarihli giriş. Boş gün ile sonuçsuz çalışma ayrımı. Geçmişteki kaydı düzenle/sil. |
| 11 | Kitap ekle/düzenle | Ad, alan, ders (Genel dahil), tür, yayınevi, basım yılı, kapak, toplam sayfa veya deneme adedi; konu liste editörü (başlangıç/bitiş, ekle/düzenle/sil), modül editörü yalnız ilgili kaynaklarda. Toplam azaltma kayıtları aşarsa önce kullanıcı çözüm seçsin; otomatik veri silme yok. Arşivle, geri yükle, sil. |
| 12 | Ayarlar / Yedek | Tema sistem/açık/koyu, günlük soru veya sayfa hedefi isteğe bağlı, yedek oluştur, dosyadan geri yükle önizleme ve onay, arşivlenen kaynaklar, çalışma geçmişi, veri özeti. Yedek tüm kullanıcı verisini ve özel kapakları içerir. |
| 13 | Kaynak seçici | Alan, soru bankası/deneme, arama, ders filtresi, favori ve son çalışılanlar üstte, gerçek kaynak listesi. Seçim formu önceden doldurur. Yeni kitap ekleme bağlantısı. |
| 14 | Çalışma geçmişi | Tarih filtreli kronolojik kayıtlar; kitap, tür, aralık/adet veya deneme numarası, varsa D/Y/B, tekrar etiketi. Düzenle, sil ve geri alma. Alan/kitap detayından kapsamlı açılabilir. |

## Durumlar ve UI detayları
- İlk açılış: tüm kitaplar mevcut, ilerlemeler 0 veya bilinmiyor; takvim boş. “İlk çalışmanı ekle” CTA. Geçmiş/istatistik boş olduğunda veri uydurma.
- Form: yalnız sayfa adedi (kitapta) zorunlu; tarih otomatik, kitap bağlamdan seçili; boş D/Y/B alanları isteğe bağlı. Adet modu sayfa konumu olmadan kayıt alır. Kaydet butonu geçerli kayıtla aktif. Sayı alanları tamsayı, negatif yok; süre pozitif dakika. Kaydedilmeyen değişikliklerde geri uyarısı.
- Filtre paneli: seçimler birlikte uygulanır; sıfırla, sonuç sayısı ve uygula. Tümü ders filtresi ile Genel dersi farklıdır. Türkçe karakterlerle arama; İ/i ve I/ı normalizasyonu, aksan toleransı önerilir. Bilinmeyen oranlar sıralamada en sona.
- Kısmi sayfa bitmiş sayılmaz; çalışma hacmine girer. Tekrar çözümde mevcut sayfa durumunu otomatik geriye düşürme. Hatalı tamamlamayı düzenle/sil ile geri al.
- Grafiklerde boş veri “Henüz sonuç yok”, eksi/NaN/sonsuz yok; ekran okuyucu açıklaması ve metinsel etiket. Renk tek başına durum taşımaz. 44–48 dp dokunma hedefleri, kontrast, klavye üstünde kaydet.
- Günlük hedef isteğe bağlı ve varsayılan kapalı; ardışık gün serisi, o gün en az bir geçerli çalışma kaydı ile artar. Favori arşivlenen kaynak ana hızlı listede görünmez.
