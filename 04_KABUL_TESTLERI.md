# Kabul testleri

Testleri gerçek çalışan uygulamada uygula. Her satır geçer/kalır, kanıtı ve varsa kısıtla raporlanır.

| ID | Test | Beklenen |
|---|---|---|
| T01 | İlk kurulum | 37 kitap, 16 deneme kitabı, 53 kapak; 1200 konu ve 248 deneme; hiçbir örnek çalışma kaydı yok. |
| T02 | Alan filtreleri | AGS 14/3; EĞİTİM 14/2; ÖABT 9/11. Eğitim kaynakları AGS altında görünmez. Genel etiketi ayrı ders filtresi. |
| T03 | Yeniden başlat | Kaynak düzenleme, favori ve çalışma kaydı korunur, seed tekrarlanmaz. |
| T04 | Arama/sıralama | Türkçe kitap adı ve yayınevi, ders + durum birlikte filtrelenir; geri dönünce seçim korunur. |
| T05 | Sayfa kaydı | 10–15 aralığı 6 sayfa, D/Y/B boşken kaydedilir; konu ve kitap ilerlemesi güncellenir. |
| T06 | Tekrar | 10–15 sonra 14–19: hacim 12, benzersiz tamamlanan 10. |
| T07 | Adet modu | 5 sayfa, konumsuz: hacim +5, benzersiz değişmez. Sonradan aralık eşleştirildiğinde hacim yeniden artmaz. |
| T08 | Kısmi | 20–22 kısmi: 3 hacim, 0 tamamlanmış. Sonra tamamla: 3 benzersiz; önceki tamamlamayı tekrar kısmi kaydı düşürmez. |
| T09 | Düzenle/sil | Örtüşen kayıt silinince diğer kayıtlardaki tamamlanan sayfalar korunur. Geri alma çalışır. |
| T10 | Eksik toplam | kitap-6 yüzde yok; toplam girilince hesaplanır; geçersiz küçültme veri silmez. |
| T11 | Tahmini son konu | Son konu bitişi null ise toplamı etkili bitiş olarak kullan; toplam değişince aralık da değişir. |
| T12 | Modüller | kitap-3 modül 1 sayfa 5 ve modül 2 sayfa 5 iki ayrı sayfa. 512 toplam korunur, tahmini modül sınırı uyarısı görünür. |
| T13 | Deneme | deneme-4 no 1 sadece tamamlandı; 1/30. Tekrar kaydet: 1/30, 2 oturum. Silme sonrası kalan kayıtla durum güncellenir. |
| T14 | Deneme ders modu | 10/2/1 + 8/1/0 = 22 toplam soru; üst toplam tekrar sayılmaz. |
| T15 | Oran ağırlığı | 10/0/0 ve 10/80/0: 20 doğru /100 = %20; eksik D/Y/B kayıtları oran hesabına katılmaz. |
| T16 | Konu çakışması | Bir kayıt iki konuyu kapsıyorsa sayfa ilerlemesi ikisinde doğru; D/Y/B tahmini bölünmez. |
| T17 | Takvim | Geçmiş tarihli kayıt o güne gider. Boş gün, soru sayısı bilinmeyen kayıt ve 0 farklı görünür. Ay değişimi çalışır. |
| T18 | İstatistik kapsamı | Gün/hafta/ay/tümü, alan ve ders filtreleri; hacim ile benzersiz ilerleme farklı; yanlış oranı minimum soru filtresi çalışır. |
| T19 | QoL | Favori, son çalışılan, devam et, günlük hedef, seri, tema, arşivle/geri getir çalışır. |
| T20 | Yedek | Düzenlenen kaynaklar ve yeni özel kapaklar dahil yedek al, boş kurulumda geri yükle; aynı sonuçlar. Bozuk dosya eski veriyi değiştirmez. |
| T21 | Offline | İlk kurulum tamamlandıktan sonra uçak modunda aç, kapaklar, arama, kayıt, istatistik, yeniden açma çalışır. |
| T22 | Telefon | Dar ekran, sayı klavyesi, kaydırma, geri navigasyon, erişilebilirlik, koyu tema; kırpılma/taşma yok. |
