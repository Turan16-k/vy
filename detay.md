İki videoda (Kayhan Ayar tarafından anlatılan **Veri Yapıları 1. Ödevi**) bahsedilen tüm mimari kurallar, ekran tasarımları, menü akışları, dosya formatı ve öğrenciden ek olarak istenen tüm detaylar aşağıda baştan sona eksiksiz şekilde sıralanmıştır.

---

## 1. Veri Yapısı ve Bellek Mimarisi

* **İki Ayrı Bağlı Liste (Linked List) Kullanımı:**
* **Matris Bağlı Listesi:** Her bir matrisin içindeki her bir sayı ayrı bir düğüm (node) olarak tutulur ve bağlı liste yapısıyla birbirine bağlanır. Matrisin kaç satır ve kaç sütundan oluştuğu bilgisi de bu bağlı liste yapısının içinde bir şekilde saklanmalıdır.
* **Ana Bağlı Liste (Üst Liste):** Her bir düğümünde bir matrisi (matris bağlı listesini) tutan ikinci bir bağlı listedir.


* **Düğüm Sayısında Sınır Olmaması:** Sol panelde tek seferde 5 düğüm gösterilse de ana listedeki toplam düğüm sayısında bir üst sınır (5, 10, 20, 100 vb.) olmamalıdır.
* **Nesne Tabanlı Programlama (OOP) ve Heap Kullanımı:** Tüm yapılar nesneye dayalı programlama teknikleriyle geliştirilmeli ve dinamik olarak oluşturulan her yerde sürekli **heap** belleği kullanılmalıdır.

---

## 2. Konsol Arayüzü ve Görsel Düzen

Ekran üç ana bölümden oluşur:

1. **Sol Panel (Ana Liste Düğümleri):** Düğümler yukarıdan aşağıya **5'erli gruplar** halinde çizilir. Seçili olan düğümün sağ tarafında bir ok/işaretçi (`<---` gibi) bulunur.
2. **Orta Panel (Seçili Matris):** Sol panelde seçili olan düğümün içindeki matrisin elemanları tablo düzeninde gösterilir.
3. **Sağ Panel (Aktif Menü):** O an içinde bulunulan menüye ait tuş yönergeleri bir kutu içinde listelenir.

### Düğüm Kutularının İçeriği ve Sıralama Kuralı

Sol paneldeki her bir düğüm kutusu üç satırdan oluşur:

* **Üst satır:** Düğümün kendi bellek adresi (ör. `0x21b85225ba80`).
* **Orta satır (Öğrenciden istenen ekleme):** Videodaki örnekte boş bırakılmıştır; buraya o düğümdeki **matrisin aritmetik ortalaması** yazdırılmalıdır.
* **Alt satır:** Bir sonraki düğümün bellek adresi. Listenin son elemanında bir sonraki düğüm olmadığı için bu değer **`0`** (`0x0` / `nullptr`) olarak görünür.
* **Sıralama Kuralı (Öğrenciden istenen ekleme):** Ana listedeki düğümler, içerdikleri matrislerin **aritmetik ortalamalarına göre küçükten büyüğe doğru** sıralı olmalıdır.

---

## 3. Ana Menü (Düğüm Gezinimi) ve İşlemleri (1. Video)

Program açıldığında ilk olarak **"Dugum gezinimi aktif"** menüsü görünür. Komutlar ilgili tuşa basılıp **Enter** yapılarak çalıştırılır:

| Tuş | Ekrandaki Açıklama / İşlev | Detaylı Davranış |
| --- | --- | --- |
| `W` / `S` | *w/s tuslari ile gezebilirsiniz* | `S` bir alt düğüme, `W` bir üst düğüme geçer. |
| `Q` | *q tusu ile one dugum ekle* | Seçili düğümün **önüne** rastgele bir matris düğümü ekler. |
| `E` | *e tusu ile arkaya dugum ekle* | Seçili düğümün **sonrasına** rastgele bir matris düğümü ekler. |
| `F` | *f tusu ile dugum secilebilir* | Seçili düğümün **Matris İşlem Menüsünü** açar. |
| `X` | *(Öğrenciden istenen ekleme)* | Uygulamadan çıkar ve güncel listeyi dosyaya kaydeder. |

### Sayfalama (5'erli Gezinme) Kuralları

* En alttaki 5. düğümdeyken `S` tuşuna basıldığında, devamında düğüm varsa **bir sonraki 5'li grup** ekrana gelir. Son grupta 5'ten az eleman varsa (örneğin 2 tane) sadece mevcut olanlar gösterilir.
* Bir grubun en üstündeki düğümdeyken `W` tuşuna basıldığında, üstte başka düğümler varsa **bir önceki 5'li gruba** geçilir.
* Listenin en başındaki (ilk) düğümdeyken `W` tuşuna basıldığında üstte başka düğüm olmadığı için seçim orada sabit kalır.

### Rastgele Matris Oluşturma Kuralları (`Q` ve `E` Tuşları)

* `Q` (öne ekleme) veya `E` (sonrasına ekleme) yapıldığında, yeni düğümün içindeki matrisin **genişliği, yüksekliği ve sayıları rastgele** oluşturulur.
* Matristeki sayılar **en fazla iki basamaklı (`0` ile `99` arası)** olmalıdır.
* Aynı matris içindeki sayılar **kesinlikle tekrar etmemelidir**. (Örneğin `10×10` boyutunda 100 elemanlı bir matriste `0`'dan `99`'a kadar tüm sayılar yalnızca birer kez bulunmalıdır.)

---

## 4. Dosya Okuma ve Kaydetme (`Sayilar.txt`)

* **Dosya Formatı:** `Sayilar.txt` dosyasındaki **her bir satır bir matrisi** temsil eder.
* Satırın **ilk iki sayısı** matrisin boyutunu (satır ve sütun / genişlik ve yükseklik) belirtir.
* Devamındaki sayılar satır satır matris elemanlarını verir. (Videodaki ilk satır örneği: `9 9 ...` — 9 satır, 9 sütun ve ardından her biri 9 elemandan oluşan satırlar.)


* **Program Açılışında Okuma:** Uygulama çalıştığında ilk olarak bu dosyayı okur, her satırdan ilgili matrisi oluşturur ve bunları ana bağlı listenin düğümlerine tek tek yerleştirir.
* **Program Kapanışında Kaydetme (`X` Tuşu):**
* Ana menüye `X` seçeneği eklenmelidir.
* Kullanıcı `X`'e bastığında uygulama kapanır; ekleme ve çıkarma işlemleri sonucunda oluşan güncel liste, **dosyanın eski içeriği tamamen silinerek sıfırdan** aynı formatta dosyaya yazılır (eski verinin üzerine ekleme/append yapılmamalıdır).



---

## 5. Matris İşlem Menüsü (2. Video)

Ana menüde bir düğüm seçiliyken `F` tuşuna basıldığında **"Dugum islemleri aktif"** menüsü açılır.

### Menü Seçenekleri

1. **`1` — Satır Sil (`1 tusu ile satir silin`)**
2. **`2` — Sütun Sil (`2 tusu ile sutun silin`)**
3. **`3` — Satır ve Sütun Değiştir *(Öğrenciden istenen ekleme)***
4. **`X` — Geri Dön (`x tusu ile dugum gezinime gidin`)**

### Alt İşlemlerin Detayları

* **Satır Silme (`1` — "Satir silme aktif"):**
* Seçili satır, matrisin solunda bir ok (`>`) ile gösterilir.
* `W` / `S` tuşlarıyla satırlar arasında yukarı/aşağı gezinilir.
* `D` tuşuna basıldığında seçili satır silinir (silme sonrası seçim imleci yukarı doğru kayar).
* `X` tuşuna basıldığında ana menüye (düğüm gezinimine) dönülür.


* **Sütun Silme (`2` — "Sutun silme aktif"):**
* `A` / `D` tuşlarıyla sütunlar arasında sola/sağa gezinilir.
* `F` tuşuna basıldığında seçili sütun silinir.
* `X` tuşuna basıldığında ana menüye dönülür.


* **Satır ve Sütun Değiştirme (`3` — Öğrenciden istenen ekleme):**
* `3` tuşuna basıldığında yeni bir alt menü açılmasına gerek yoktur; aynı menü ekranında kalınır.
* Kullanıcıdan sırasıyla **sütun numarası** ve **satır numarası** istenir.
* Girilen satır ile sütunun yerleri değiştirilir ve ardından **ana menüye geri dönülür**.
* Bu işlem matrisin elemanlarını değiştirmediği için aritmetik ortalama değişmez, dolayısıyla ana listenin sıralaması da etkilenmez.



### Silme İşlemlerine Dair Kritik Kurallar

* **Gecikmeli Yeniden Sıralama:** Satır veya sütun silindiğinde matrisin aritmetik ortalaması değişir. Ancak kullanıcı silme işlemi yaparken seçili düğümün yeri anlık olarak değişip ekrandan kaymamalıdır. Bu nedenle **yeniden sıralama işlemi silme anında değil, `X` tuşuna basılıp ana menüye dönüldüğünde** yapılmalıdır.
* **Boş Kalan Düğümün Silinmesi:** Satır veya sütun silme işlemleri sonucunda bir matriste hiç eleman kalmazsa, o matrisi barındıran ana düğüm de **ana bağlı listeden tamamen silinmeli** ve önceki-sonraki düğümler arasındaki bağlantı (pointer) yeniden kurulmalıdır.

İki videonun tamamını baştan sona tekrar kontrol ettim; **videolarda anlatılan tüm zorunlu özellikler, tuş kontrolleri, dosya formatı ve bellek/OOP kuralları önceki listede eksiksiz olarak yer alıyor.**

Unutulan bir kural yok; ancak kodlamaya geçmeden önce videolarda satır arasında geçen **iki küçük detayı** not etmenizde fayda var:

* **Yazılı Ödev Dokümanı Uyarısı (2. Video Sonu):** Hoca, videonun sonunda OOP ve heap kurallarının zaten dokümanda yazdığını ve **videoda bahsedilmeyen olası ek kuralların da yazılı ödev dokümanında belirtileceğini** söylüyor. Videoların yanında verilen PDF/dokümanı da mutlaka kontrol edin.
* **Kodlamada Karşılaşacağınız İki Kritik Uç Durum:**
1. **`Q`/`E` Ekleme ve Sıralama:** Videodaki demoda aritmetik ortalamaya göre sıralama henüz eklenmediği için `Q` seçili düğümün tam önüne, `E` tam sonrasına ekliyor. Ödevde liste küçükten büyüğe sıralı olacağından, ekleme sonrası listenin sıralanıp sıralanmayacağını yazılı dokümandan teyit etmek iyi olur.
2. **Kare Olmayan Matriste Satır–Sütun Değiştirme (`3`):** Videoda sadece "sütun numarası ve satır numarası istesin, yerlerini değiştirsin" deniyor. Satır ve sütun sayısı birbirine eşit olmayan (örneğin `4×6`) bir matriste bu işlemin nasıl davranacağı (sadece ortak elemanların mı değişeceği yoksa uyarı mı verileceği) yine yazılı dokümanda netleştirilmiş olabilir.
