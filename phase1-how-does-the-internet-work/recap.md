# İnternetin Arka Planındaki Gizli Düzen: Dijital Dünyayı Şekillendiren 6 Şaşırtıcı Gerçek

#### Giriş
Günlük hayatta bir web tarayıcısının adres çubuğuna bir adresi yazıp "Enter" tuşuna bastığınızda, saniyeden çok daha kısa bir sürede ekranınıza zengin, renkli ve etkileşimli bir sayfa yüklenir. Çoğumuz için bu durum sıradan ve çaba gerektirmeyen bir kullanıcı deneyiminden ibarettir. Ancak bu basit tetiklemenin arka planında; milisaniyeler seviyesinde senkronize çalışan, hataya yer bırakmayan görünmez protokoller, katmanlı ağ mimarileri ve katı tarayıcı derleme kuralları bulunur. 

Web teknolojilerini oluşturan bu devasa altyapı, küresel veri iletiminden ekrandaki tek bir pikselin çizilmesine kadar her aşamada sıkı standartlara dayanır. Yazılımcılardan sistem mimarlarına kadar sektörde çalışan birçok uzmanın dahi zaman zaman karıştırdığı bu mekanizmalar, aslında internetin işletim sistemini oluşturur. Bu makalede, web standartlarının ve ağ iletişiminin arka planında yer alan, doğru bilinen yanlışları ortadan kaldıracak 6 temel teknik gerçeği sistem mimarisi perspektifiyle inceliyoruz.

---

### 1. Her URL Bir URI'dir, Ama Her URI Bir URL Değildir
Yazılımcılar ve ağ uzmanları günlük dilde URI ve URL kavramlarını sıklıkla birbirinin yerine kullansa da, teknik standartlar açısından bu iki terim arasında belirgin bir kavramsal hiyerarşi ve mantıksal fark bulunur.

* **URI (Uniform Resource Identifier):** İnternet ortamındaki soyut veya fiziksel bir kaynağı tanımlamaya yarayan en üst şemsiye standarttır. Bir kaynağı konuma, ada (URN) veya her ikisine göre tanımlayabilir.
* **URL (Uniform Resource Locator):** URI standartlarının özel bir alt kümesidir. Bir kaynağı yalnızca tanımlamakla kalmaz; o kaynağın internet üzerinde nerede bulunduğunu ve ona hangi protokol aracılığıyla (HTTP, HTTPS, FTP vb.) erişileceğini açıkça belirtir.

**Analitik Değerlendirme:** Aradaki temel fark "tanımlama" (identification) ile "konumlandırma" (location) arasındaki mimari ayrıma dayanır. Bir kaynağın adını veya kimliğini belirtmek onu tanımlar (URI); ancak o kaynağa nasıl ve nereden ulaşılacağını tarif etmek onu bir konum belirleyici (URL) yapar. Örneğin, bir e-posta adresi biçimi (`mailto:bilgi@example.com`) veya bir kitabın ISBN numarası (`urn:isbn:0451450523`) kaynağı tanımlayan bir URI örneğiyken; bir web sayfasının tam adresi (`https://example.com/index.html`) hem konumu hem de erişim protokolünü bildirdiği için bir URL'dir. 

> *"Her URL bir URI'dir, ancak her URI bir URL değildir. URI genel bir tanımlama aracıdır; URL ise bir kaynağın internet üzerindeki kesin konumunu ve ona nasıl erişileceğini belirten özel bir alt kümedir."*

---

### 2. Ağ İletişiminin 7 Katmanlı Anayasası: OSI Modeli ve Veri Sarmalama
İnternet ortamında farklı donanım ve yazılımlara sahip cihazların birbiriyle sorunsuz haberleşebilmesi, ISO bünyesindeki TC 97 komitesi tarafından geliştirilen ve 1984 yılında son şeklini alan 7 katmanlı **OSI (Open Systems Interconnection)** referans modeline dayanır. 

OSI modeli öncesinde sistemler üreticiye bağımlı kapalı yapılar (IBM SNA vb.) üzerinden haberleşmekteydi. OSI, her biri belirli bir Protokol Veri Birimi (PDU) ile çalışan 7 katmanlı bağımsız bir standart getirmiştir:

* **7. Uygulama Katmanı** ---> PDU: Veri (Data) *[HTTP, FTP, SMTP]*
* **6. Sunum Katmanı** ---> PDU: Veri (Data) *[Sözdizim, Şifreleme, JPEG, SSL]*
* **5. Oturum Katmanı** ---> PDU: Veri (Data) *[Oturum Kurma, Yönetme, Sonlandırma]*
* **4. Taşıma Katmanı** ---> PDU: Bölüt (Segment) *[Akış & Hata Kontrolü, TCP/UDP]*
* **3. Ağ Katmanı** ---> PDU: Paket (Datagram) *[Yönlendirme / Routing, IP, ICMP]*
* **2. Veri Bağlantısı** ---> PDU: Çerçeve (Frame) *[MAC Adresleme, Ethernet, Switch]*
* **1. Fiziksel Katman** ---> PDU: Bit *[Sinyaller, Kablolama, Fiber Optik]*

**Veri Sarmalama ve Sökme (Encapsulation / Decapsulation):** Veri gönderilirken 7. katmandan 1. katmana doğru ilerler. Her aşamada veriye o katmanın görevini temsil eden ayrı bir başlık (header) eklenir. Karşı cihazda ise bu işlem tersine işler; ham bit dizisi üst katmanlara çıkarken başlıklar sırayla sökülür ve ham veri hedefe teslim edilir.

> *"Günümüzde TCP/IP modeli daha yaygın kullanılsa da, OSI referans modeli veri iletimindeki her aşamanın mantıksal haritasını çıkaran teorik bir anayasa olmayı sürdürmektedir."*

---

### 3. Ekrandaki Tek Bir Kare İçin Çalışan "Kritik Oluşturma Yolu" (Critical Rendering Path)
Sunucudan tarayıcıya ulaşan ilk veriler anlamsız bayt dizilerinden ibarettir. Bu ham verinin ekrandaki renkli, düzenli ve etkileşimli piksellere dönüşmesi sürecine **Kritik Oluşturma Yolu** (CRP) denir. Süreç şu 6 katı adımda gerçekleşir:

1. **HTML Okuma ve DOM İnşası:** Tarayıcı ham baytları karakterlere dönüştürür. Karakterler HTML standartlarına göre jetonlara (tokens) ayrılır. Jetonlar düğümlere (nodes) dönüştürülerek DOM ağacı elde edilir.
2. **CSSOM Ağacı Oluşturma:** Karşılaşılan CSS kuralları ayrıştırılarak stillerin hiyerarşik haritasının tutulduğu CSSOM ağacı inşa edilir.
3. **Render Tree Birleşimi:** DOM ve CSSOM birleştirilir. Render Tree sadece ekranda *fiilen görünecek* öğeleri içerir (`display: none` olanlar ağaca alınmaz, ancak `visibility: hidden` olanlar alan kapladıkları için alınır).
4. **Layout (Yerleşim / Reflow):** Viewport (ekran) genişliği baz alınarak, nesnelerin kutu modelindeki kesin piksel koordinatları hesaplanır.
5. **Paint (Çizim):** Metinler, renkler, gölgeler, kenarlıklar ve görseller pikseller halinde rasterize edilerek ekrana boyanır.
6. **Compositing (Birleştirme):** z-index, 3D dönüşümler veya saydamlık gibi katmanlı yapılar doğru sırayla üst üste bindirilerek nihai görüntü ekrana iletilir.

> *"Kullanıcının milisaniyeler içinde gördüğü basit bir web sayfasının arkasında, devasa bir grafik motoru mühendisliği yatar."*

---

### 4. Kodun Akışını Kesen Güç: JavaScript ve Parser-Blocking
Web sayfalarının dinamik çalışmasını sağlayan JavaScript, aynı zamanda tarayıcının oluşturma (rendering) performansındaki en kritik darboğazlardan biridir. Tarayıcı HTML kodunu yukarıdan aşağıya doğru satır satır okurken (parsing) bir `<script>` etiketiyle karşılaştığında, **HTML ayrıştırma işlemini derhal durdurur (Parser-Blocking).**

**Neden Durdurur?**
Çünkü JavaScript kodları, DOM veya CSSOM yapısını manipüle etme potansiyeline sahiptir (örneğin, `document.write()` ile sayfaya yeni bir element eklenebilir). Tarayıcı, inşa ettiği ağacın JavaScript tarafından değiştirilip değiştirilmeyeceğini bilemeyeceği için riske girmez. HTML okumayı durdurur, sunucudan script dosyasını indirir, V8 (Chrome) veya SpiderMonkey (Firefox) gibi motorlarda derler (JIT Compilation) ve çalıştırır. Bütün bu işlemler bitmeden HTML ayrıştırmaya devam etmez.

**Analitik Değerlendirme:** Bu darboğaz "Beyaz Ekran" (White Screen of Death) süresini uzatan temel faktördür. Modern web mimarisinde bu sorunu aşmak için `async` (indirme asenkron, çalışırken bloklar) ve `defer` (indirme asenkron, DOM tamamlanınca çalışır) nitelikleri (attributes) standart hale gelmiştir. 

---

### 5. İlk Milisaniyelerin Kahramanı: DNS ve TCP 3-Yönlü El Sıkışma
Web'in perde arkasındaki en büyük yanılgılardan biri, URL'ye girip Enter'a basıldığı anda sunucuyla anında veri alışverişinin başladığı düşüncesidir. Oysa tek bir byte HTML verisi yola çıkmadan önce devasa bir protokol diplomasisi yaşanır.

1. **DNS Çözümlemesi (İnternetin Telefon Rehberi):** Tarayıcı `example.com`'un hangi IP adresinde olduğunu bilemez. İstek sırasıyla Tarayıcı Önbelleği -> İşletim Sistemi -> Yönlendirici (Router) -> ISP (Servis Sağlayıcı) DNS sunucularına gider. Gerekirse Kök (Root) ve TLD (Top Level Domain) sunucularından IP adresi (örn. `192.0.2.1`) bulunur.
2. **TCP 3-Yönlü El Sıkışma (3-Way Handshake):** IP bulunduktan sonra verilerin kayıpsız iletilmesini sağlayan TCP protokolü devreye girer. İstemci "Bağlanabilir miyim?" (SYN) der, sunucu "Evet, bağlanabilirsin, sen de beni duyuyor musun?" (SYN-ACK) der, istemci "Evet duyuyorum, başlıyoruz" (ACK) der. 
3. **TLS El Sıkışması:** Bağlantı güvenli (HTTPS) ise, TCP'nin üzerine şifreleme anahtarlarının ve sertifikaların paylaşıldığı ek bir kriptografik el sıkışma daha yaşanır.

> *"Web sunucusu size asıl web sayfasını göndermeye başlamadan önce ağ üzerinde okyanuslar aşan, binlerce kilometrelik bu karmaşık tanışma merasimi genellikle 50 ile 200 milisaniye içinde tamamlanır."*

---

### 6. İnternetin Hafıza Kaybı: HTTP'nin Durumsuz Doğası (Stateless)
Her gün kullandığımız web uygulamaları (sepetler, oturumlar, mesajlaşmalar) son derece "kişisel" ve "devamlı" bir deneyim sunsa da, altlarında yatan HTTP protokolü tasarım gereği **durumsuz (stateless)** bir protokoldür. 

HTTP sunucusu amnezik (hafıza kaybı yaşayan) bir resepsiyonist gibidir. Ona gönderdiğiniz ardışık iki istek arasında hiçbir bağ kuramaz. Sayfaya giriş yaptığınızı söyleyen ilk istekle, sepete ürün eklediğiniz ikinci isteği tamamen birbirinden bağımsız iki farklı kişi yapmış gibi değerlendirir.

**Durum (State) Yönetimi Nasıl Sağlanır?**
İşte tam bu noktada sistem mimarları web'in bu açığını yamamak için çeşitli teknolojiler geliştirmiştir:
* **Çerezler (Cookies) ve Session ID:** Sunucu size gizli bir bilet (Session ID) verir ve tarayıcınıza bunu kaydetmesini söyler. Tarayıcı her yeni HTTP isteğinin başlığına (Header) bu bileti zımbalayarak sunucuya "Ben önceki adımdaki aynı kişiyim" der.
* **JSON Web Tokens (JWT):** Modern RESTful API'lerde sunucunun hafıza yükünü azaltmak için, kullanıcının kimlik bilgileri kriptografik olarak imzalanıp bir token halinde istemciye bırakılır.

> *"Bugün deneyimlediğimiz akıcı, kişiselleştirilmiş ve güvenli web deneyimi, doğası gereği hiçbir şeyi hatırlamayan bir protokolün üzerine inşa edilmiş zekice state (durum) yönetimi hilelerine dayanmaktadır."*