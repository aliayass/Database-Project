# Sanat Eserleri ve Müzeler Veritabanı Projesi

Bu proje, müzelerde sergilenen sanat eserlerini, müze bilgilerini, ziyaretçilerin etkileşimlerini, etkinlikleri, koleksiyonları ve müze içi yönetimi detaylı bir şekilde yönetmek için oluşturulmuş bir veritabanı sistemidir. Sistem, sanat eserleri ve koleksiyonlar ile müze içi görevler ve ziyaretçi etkileşimleri gibi birçok bileşeni kapsamaktadır.

## Proje Özeti

Sanat Eserleri ve Müzeler Veritabanı, aşağıdaki kullanıcı türlerini ve işlevleri destekler:
- **Ziyaretçiler (Sanatseverler)**: Sanat eserlerini görüntüleyebilir, yorum yapabilir, puan verebilir, müzeye ziyaretlerini kaydedebilir ve müze biletlerini satın alabilir.
- **Müze Yöneticileri**: Sanat eserleri, sanatçılar, koleksiyonlar, etkinlikler, eğitim programları ve müze çalışanları hakkında bilgi ekleyebilir, düzenleyebilir.
- **Sanatçılar**: Eser bilgilerini sisteme ekleyebilir ve güncelleyebilir.

Bu veri tabanı modeli; müzeler, sanat eserleri, sanatçılar, ziyaretçiler, ziyaretler, koleksiyonlar, etkinlikler, eğitim programları, sponsorluklar ve oda bilgileri gibi birçok varlığı kapsar.

## Veritabanı Yapısı

### Varlıklar (Tablolar) ve Nitelikleri

#### 1. Müze
- **muze_id** (PK): Müzenin benzersiz kimlik numarası.
- **ad**: Müzenin adı.
- **adres**: Müzenin bulunduğu adres.
- **ziyaret_saatleri**: Müzenin ziyaret saatleri.
- **giris_ucreti**: Müze giriş ücreti.

#### 2. Sanat Eseri
- **eser_id** (PK): Sanat eserinin benzersiz kimlik numarası.
- **ad**: Eserin adı.
- **tur_id** (FK): Eserin türünü işaret eden yabancı anahtar.
- **yaratilis_tarihi**: Eserin yaratılış tarihi.
- **sanatci_id** (FK): Eserin sanatçısını işaret eden yabancı anahtar.
- **muze_id** (FK): Eserin sergilendiği müzeyi işaret eden yabancı anahtar.
- **koleksiyon_id** (FK, Opsiyonel): Eserin bir koleksiyona atanması durumunda koleksiyon kimliği.
- **oda_id** (FK): Eserin sergilendiği odayı işaret eden yabancı anahtar.

#### 3. Sanatçı
- **sanatci_id** (PK): Sanatçının benzersiz kimlik numarası.
- **ad**: Sanatçının adı.
- **dogum_tarihi**: Sanatçının doğum tarihi.
- **biyografi**: Sanatçı hakkında kısa bilgi.

#### 4. Ziyaretçi
- **ziyaretci_id** (PK): Ziyaretçinin benzersiz kimlik numarası.
- **isim**: Ziyaretçinin adı.
- **email**: Ziyaretçinin e-posta adresi (tekil ve zorunludur).
- **parola**: Ziyaretçinin parola bilgisi (şifrelenmiş olarak saklanmalıdır).

#### 5. Puanlama
- **puanlama_id** (PK): Puanlama işleminin benzersiz kimlik numarası.
- **puan**: Ziyaretçinin esere verdiği puan (1 ile 5 arasında olmalıdır).
- **ziyaretci_id** (FK): Puanı veren ziyaretçiyi işaret eden yabancı anahtar.
- **eser_id** (FK): Puan verilen sanat eserini işaret eden yabancı anahtar.

#### 6. Yorum
- **yorum_id** (PK): Yorumun benzersiz kimlik numarası.
- **icerik**: Yorumun içeriği.
- **yorum_tarihi**: Yorumun yapıldığı tarih ve saat.
- **ziyaretci_id** (FK): Yorumu yapan ziyaretçiyi işaret eden yabancı anahtar.
- **eser_id** (FK): Yorum yapılan sanat eserini işaret eden yabancı anahtar.

#### 7. Eser Türü
- **tur_id** (PK): Eser türünün benzersiz kimlik numarası.
- **ad**: Eser türünün adı (ör. Resim, Heykel, Fotoğraf, Dijital).

#### 8. Müze Çalışanı
- **calisan_id** (PK): Çalışanın benzersiz kimlik numarası.
- **ad**: Çalışanın adı.
- **gorev**: Çalışanın görev tanımı.
- **muze_id** (FK): Çalışanın görev yaptığı müzeyi işaret eden yabancı anahtar.

#### 9. Bilet
- **bilet_id** (PK): Biletin benzersiz kimlik numarası.
- **ziyaretci_id** (FK): Bileti alan ziyaretçiyi işaret eden yabancı anahtar.
- **muze_id** (FK): Biletin geçerli olduğu müzeyi işaret eden yabancı anahtar.
- **satın_alim_tarihi**: Biletin satın alındığı tarih.

#### 10. Eğitim Programı
- **program_id** (PK): Eğitim programının benzersiz kimlik numarası.
- **ad**: Programın adı.
- **tarih**: Programın yapılacağı tarih.
- **muze_id** (FK): Programın yapılacağı müzeyi işaret eden yabancı anahtar.

#### 11. Sponsor
- **sponsor_id** (PK): Sponsorun benzersiz kimlik numarası.
- **ad**: Sponsorun adı.
- **iletisim**: Sponsorun iletişim bilgileri.

#### 12. Sponsorluk
- **sponsorluk_id** (PK): Sponsorluğun benzersiz kimlik numarası.
- **sponsor_id** (FK): Sponsorun kimliği.
- **muze_id** (FK): Sponsorluk yapılan müzenin kimliği.
- **destek_miktari**: Sponsor tarafından sağlanan destek miktarı.

#### 13. Oda
- **oda_id** (PK): Odanın benzersiz kimlik numarası.
- **ad**: Odanın adı.
- **kat**: Odanın bulunduğu kat.
- **muze_id** (FK): Odanın bağlı olduğu müzeyi işaret eden yabancı anahtar.

### İlişkiler

1. **Müze - Sanat Eseri**: Her müze birden fazla sanat eseri sergileyebilir (**1:N**).
2. **Sanatçı - Sanat Eseri**: Her sanatçı birden fazla eser yaratabilir (**1:N**).
3. **Sanat Eseri - Oda**: Her oda birden fazla eser içerebilir (**1:N**).
4. **Sanat Eseri - Eser Türü**: Her sanat eseri bir türe aittir (**1:N**).
5. **Müze - Koleksiyon**: Her müze birden fazla koleksiyon içerebilir (**1:N**).
6. **Koleksiyon - Sanat Eseri**: Her koleksiyon birden fazla sanat eseri içerebilir (**1:N**).
7. **Ziyaretçi - Ziyaret**: Her ziyaretçi birden fazla kez müzeyi ziyaret edebilir (**1:N**).
8. **Müze - Ziyaret**: Her müze birçok kez ziyaret edilebilir (**1:N**).
9. **Müze - Etkinlik**: Her müze birden fazla etkinliğe ev sahipliği yapabilir (**1:N**).
10. **Etkinlik - Sanat Eseri**: Her etkinlik birden fazla sanat eserini sergileyebilir (**N:M**).
11. **Sanat Eseri - Puanlama**: Bir sanat eseri birçok ziyaretçi tarafından puanlanabilir (**N:M**).
12. **Sanat Eseri - Yorum**: Bir sanat eseri birçok ziyaretçi tarafından yorumlanabilir (**N:M**).
13. **Bilet - Müze**: Her bilet yalnızca bir müzede geçerli olur (**1:N**).
14. **Müze Çalışanı - Müze**: Her çalışan yalnızca bir müzeye atanır (**1:N**).
15. **Sponsor - Müze**: Her sponsor, birden fazla müzeye destek olabilir (**N:M**).
16. **Müze - Eğitim Programı**: Her müze birden fazla eğitim programına sahip olabilir (**1:N**).


