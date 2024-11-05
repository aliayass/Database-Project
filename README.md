# Database-Project
# Sanat Eserleri ve Müzeler Veritabanı Projesi

Bu proje, müzelerde sergilenen sanat eserleri, müze bilgileri ve ziyaretçilerin bu eserlerle olan etkileşimlerinin yönetilmesini sağlayan bir veri tabanı sistemidir. Sistem; sanat eserlerinin, sanatçıların ve müze bilgilerinin kaydedilmesini, sanat eserlerinin müzelerde sergilenmesini ve ziyaretçilerin bu eserlerle etkileşime geçmesini sağlar.

## Proje Özeti

Sanat Eserleri ve Müzeler Veritabanı, aşağıdaki kullanıcı türlerini ve işlevleri destekler:
- **Ziyaretçiler (Sanatseverler)**: Sanat eserlerini görüntüleyebilir, yorum yapabilir ve puan verebilir.
- **Müze Yöneticileri**: Sanat eserleri ve sanatçılar hakkında bilgi ekleyebilir, güncelleyebilir.
- **Sanatçılar**: Eser bilgilerini sisteme ekleyebilir ve güncelleyebilir.

Proje; müzeler, sanat eserleri, sanatçılar ve ziyaretçi etkileşimlerini (puanlama ve yorumlar) içeren bir veri tabanı modeli oluşturur.

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
- **tur**: Eserin türü (resim, heykel, vb.).
- **yaratilis_tarihi**: Eserin yaratılış tarihi.
- **sanatci_id** (FK): Eserin sanatçısını işaret eden yabancı anahtar.
- **muze_id** (FK): Eserin sergilendiği müzeyi işaret eden yabancı anahtar.

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

### Varlık-İlişki Diyagramı (ERD)

Projeye ait veritabanı modelinin ER diyagramını `docs/ERD.png` dosyasına ekledik. Bu diyagram, tablolar arasındaki ilişkileri görsel olarak göstermektedir.

## İlişkiler ve Kısıtlamalar

- **Müze - Sanat Eseri İlişkisi**: Her müzede birden fazla sanat eseri sergilenebilir (1:N).
- **Sanatçı - Sanat Eseri İlişkisi**: Her sanatçı birden fazla eser yaratabilir, ancak her eser yalnızca bir sanatçıya ait olur (1:N).
- **Sanat Eseri - Puanlama İlişkisi**: Bir sanat eseri birçok ziyaretçi tarafından puanlanabilir, her ziyaretçi de birden fazla eseri puanlayabilir (N:M).
- **Sanat Eseri - Yorum İlişkisi**: Bir sanat eseri birçok ziyaretçi tarafından yorumlanabilir, her ziyaretçi de birden fazla eser hakkında yorum yapabilir (N:M).

