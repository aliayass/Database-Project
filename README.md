# Sanat Eserleri ve Müzeler Veritabanı Projesi

Bu proje, müzelerde sergilenen sanat eserlerini, müze bilgilerini, ziyaretçilerin etkileşimlerini, etkinlikleri, koleksiyonları ve müze içi yönetimi detaylı bir şekilde yönetmek amacıyla oluşturulmuş bir veritabanı sistemidir. Proje, sanat eserleri ve koleksiyonlar ile müze içi görevler ve ziyaretçi etkileşimleri gibi birçok bileşeni kapsamaktadır.

## İçindekiler

- [Proje Özeti](#proje-özeti)
- [Veritabanı Yapısı](#veritabanı-yapısı)
  - [Varlıklar ve Nitelikleri](#varlıklar-ve-nitelikleri)
  - [İlişkiler](#ilişkiler)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)

## Proje Özeti

Sanat Eserleri ve Müzeler Veritabanı, aşağıdaki kullanıcı türlerini ve işlevleri destekler:

- **Ziyaretçiler (Sanatseverler)**: Sanat eserlerini görüntüleyebilir, yorum yapabilir, puan verebilir, müzeye ziyaretlerini kaydedebilir ve müze biletlerini satın alabilir.
- **Müze Yöneticileri**: Sanat eserleri, sanatçılar, koleksiyonlar, etkinlikler ve müze çalışanları hakkında bilgi ekleyebilir ve düzenleyebilir.
- **Sanatçılar**: Eser bilgilerini sisteme ekleyebilir ve güncelleyebilir.

Bu veritabanı modeli; müzeler, sanat eserleri, sanatçılar, ziyaretçiler, ziyaretler, koleksiyonlar, etkinlikler ve sponsorluklar gibi birçok varlığı kapsamaktadır.

## Veritabanı Yapısı

### Varlıklar ve Nitelikleri

1. **Müze**
   - **muze_id** (PK): Müzenin benzersiz kimlik numarası.
   - **ad**: Müzenin adı.
   - **adres**: Müzenin bulunduğu adres.
   - **ziyaret_saatleri**: Müzenin ziyaret saatleri.
   - **giris_ucreti**: Müze giriş ücreti.

2. **Sanat Eseri**
   - **eser_id** (PK): Sanat eserinin benzersiz kimlik numarası.
   - **ad**: Eserin adı.
   - **tur_id** (FK): Eserin türünü işaret eden yabancı anahtar.
   - **yaratilis_tarihi**: Eserin yaratılış tarihi.
   - **sanatci_id** (FK): Eserin sanatçısını işaret eden yabancı anahtar.
   - **muze_id** (FK): Eserin sergilendiği müzeyi işaret eden yabancı anahtar.
   - **koleksiyon_id** (FK, Opsiyonel): Eserin bir koleksiyona atanması durumunda koleksiyon kimliği.

3. **Sanatçı**
   - **sanatci_id** (PK): Sanatçının benzersiz kimlik numarası.
   - **ad**: Sanatçının adı.
   - **dogum_tarihi**: Sanatçının doğum tarihi.
   - **biyografi**: Sanatçı hakkında kısa bilgi.

4. **Ziyaretçi**
   - **ziyaretci_id** (PK): Ziyaretçinin benzersiz kimlik numarası.
   - **isim**: Ziyaretçinin adı.
   - **email**: Ziyaretçinin e-posta adresi (tekil ve zorunludur).
   - **parola**: Ziyaretçinin parola bilgisi (şifrelenmiş olarak saklanmalıdır).

5. **Puanlama**
   - **puanlama_id** (PK): Puanlama işleminin benzersiz kimlik numarası.
   - **puan**: Ziyaretçinin esere verdiği puan (1 ile 5 arasında).
   - **ziyaretci_id** (FK): Puanı veren ziyaretçiyi işaret eden yabancı anahtar.
   - **eser_id** (FK): Puan verilen sanat eserini işaret eden yabancı anahtar.

6. **Yorum**
   - **yorum_id** (PK): Yorumun benzersiz kimlik numarası.
   - **icerik**: Yorumun içeriği.
   - **yorum_tarihi**: Yorumun yapıldığı tarih ve saat.
   - **ziyaretci_id** (FK): Yorumu yapan ziyaretçiyi işaret eden yabancı anahtar.
   - **eser_id** (FK): Yorum yapılan sanat eserini işaret eden yabancı anahtar.

7. **Eser Türü**
   - **tur_id** (PK): Eser türünün benzersiz kimlik numarası.
   - **ad**: Eser türünün adı (ör. Resim, Heykel, Fotoğraf, Dijital).

8. **Müze Çalışanı**
   - **calisan_id** (PK): Çalışanın benzersiz kimlik numarası.
   - **ad**: Çalışanın adı.
   - **gorev**: Çalışanın görev tanımı.
   - **muze_id** (FK): Çalışanın görev yaptığı müzeyi işaret eden yabancı anahtar.

9. **Bilet**
   - **bilet_id** (PK): Biletin benzersiz kimlik numarası.
   - **ziyaretci_id** (FK): Bileti alan ziyaretçiyi işaret eden yabancı anahtar.
   - **muze_id** (FK): Biletin geçerli olduğu müzeyi işaret eden yabancı anahtar.
   - **satin_alim_tarihi**: Biletin satın alındığı tarih.

10. **Koleksiyon**
    - **koleksiyon_id** (PK): Koleksiyonun benzersiz kimlik numarası.
    - **ad**: Koleksiyonun adı.
    - **muze_id** (FK): Koleksiyonun ait olduğu müze.
    - **aciklama**: Koleksiyon hakkında kısa bilgi.

11. **Etkinlik**
    - **etkinlik_id** (PK): Etkinliğin benzersiz kimlik numarası.
    - **ad**: Etkinliğin adı.
    - **tarih**: Etkinliğin tarihi.
    - **aciklama**: Etkinliğin açıklaması.
    - **muze_id** (FK): Etkinliğin düzenlendiği müze.

12. **Ziyaret**
    - **ziyaret_id** (PK): Ziyaretin benzersiz kimlik numarası.
    - **ziyaretci_id** (FK): Ziyaretin sahibi ziyaretçi.
    - **muze_id** (FK): Ziyaret edilen müze.
    - **ziyaret_tarihi**: Ziyaretin gerçekleştiği tarih.

13. **Etkinlik Sanat Eseri (Bağlantı Tablosu)**
    - **etkinlik_sanat_eser_id** (PK): İlişkinin benzersiz kimlik numarası.
    - **etkinlik_id** (FK): Etkinliği işaret eden yabancı anahtar.
    - **eser_id** (FK): Sanat eserini işaret eden yabancı anahtar.

### İlişkiler

1. **Müze - Sanat Eseri**: Her müze birden fazla sanat eseri sergileyebilir (**1:N**).
2. **Sanatçı - Sanat Eseri**: Her sanatçı birden fazla eser yaratabilir (**1:N**).
3. **Sanat Eseri - Eser Türü**: Her sanat eseri bir türe aittir (**1:N**).
4. **Müze - Koleksiyon**: Her müze birden fazla koleksiyon içerebilir (**1:N**).
5. **Koleksiyon - Sanat Eseri**: Her koleksiyon birden fazla sanat eseri içerebilir (**1:N**).
6. **Ziyaretçi - Ziyaret**: Her ziyaretçi birden fazla müzeyi ziyaret edebilir (**1:N**).
7. **Müze - Ziyaret**: Her müze birçok kez ziyaret edilebilir (**1:N**).
8. **Müze - Etkinlik**: Her müze birden fazla etkinliğe ev sahipliği yapabilir (**1:N**).
9. **Etkinlik - Sanat Eseri**: Her etkinlik birden fazla sanat eserini sergileyebilir (**N:M**).
10. **Sanat Eseri - Puanlama**: Her sanat eseri birden fazla puan alabilir (**1:N**).
11. **Sanat Eseri - Yorum**: Her sanat eseri birden fazla yorum alabilir (**1:N**).
12. **Müze - Bilet**: Her müze için birden fazla bilet satılabilir (**1:N**).
13. **Müze - Sponsorluk**: Her müze birden fazla sponsorluk
