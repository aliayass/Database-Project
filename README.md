# Sanat Eserleri ve Müzeler Veritabanı Projesi

Bu proje, müzelerde sergilenen sanat eserlerini, müze bilgilerini, ziyaretçilerin etkileşimlerini, etkinlikleri, koleksiyonları ve müze içi yönetimi detaylı bir şekilde yönetmek amacıyla oluşturulmuş bir veritabanı sistemidir. Proje, sanat eserleri ve koleksiyonlar ile müze içi görevler ve ziyaretçi etkileşimleri gibi birçok bileşeni kapsamaktadır.

## İçindekiler

- [Proje Özeti](#proje-özeti)
- [Veritabanı Yapısı](#veritabanı-yapısı)
  - [Varlıklar ve Nitelikleri](#varlıklar-ve-nitelikleri)
  - [İlişkiler](#ilişkiler)
  - [Yorumlama ve Puanlama İlişkisi](#yorumlama-ve-puanlama-ilişkisi)
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

12. **Puan ve Yorum**(İlişkisel Tablo)
- **puanlama_id**: Puanlamanın benzersiz kimlik numarası (PK).         
- **eser_id**: Puanlanan sanat eserinin kimlik numarası (FK).       
- **ziyaretci_id**: Puan veren ziyaretçinin kimlik numarası (FK).       
- **puan**: Verilen puan (örneğin, 1-5 arasında bir değer). 

### İlişkiler

1. **Müze - Sanat Eseri**: Her müze birden fazla sanat eseri sergileyebilir (**1:N**).
2. **Sanatçı - Sanat Eseri**: Her sanatçı birden fazla eser yaratabilir (**1:N**).
3. **Sanat Eseri - Eser Türü**: Her sanat eseri bir türe aittir (**1:N**).
4. **Müze - Koleksiyon**: Her müze birden fazla koleksiyon içerebilir (**1:N**).
5. **Koleksiyon - Sanat Eseri**: Her koleksiyon birden fazla sanat eseri içerebilir (**1:N**).
6. **Müze - Etkinlik**: Her müze birden fazla etkinliğe ev sahipliği yapabilir (**1:N**).
7. **Etkinlik - Sanat Eseri**: Her etkinlik birden fazla sanat eserini sergileyebilir (**1:N**).
8. **Sanat Eseri - Puanlama**: Her sanat eseri birden fazla puan alabilir (**1:N**).
9. **Sanat Eseri - Yorum**: Her sanat eseri birden fazla yorum alabilir (**1:N**).
10. **Müze - Bilet**: Her müze için birden fazla bilet satılabilir (**1:N**).
11. **Müze - Sponsorluk**: Her müze birden fazla sponsorluk anlaşmasına sahip olabilir (**N:N**).
12. **Ziyaretçi - Sanat Eseri**: Her ziyaretçi birden fazla sanat eserine puan verebilir ve yorum yapabilir(**N:M**).


![image](https://github.com/user-attachments/assets/51dea352-7d98-487b-b512-a3690b141e5a)

