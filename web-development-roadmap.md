# Kapsamlı Full-Stack Web Developer Yol Haritası

Bu rehber, bir web uygulamasının tarayıcıdaki tıklamadan sunucudaki veritabanına kadar geçen tüm yolculuğunu ve bu ekosistemi ayakta tutan teknolojileri derinlemesine öğrenmek isteyenler için hazırlanmıştır. Hedef, teknolojileri sadece kullanmak değil, "nasıl" ve "neden" çalıştıklarını anlamaktır.

---

## Aşama 1: Temeller – İnternet Nasıl Çalışır?
Her şeyin başladığı yer. Kod yazmaya başlamadan önce, yazdığın kodun üzerinde çalışacağı altyapıyı anlamalısın.

*   **Ağ ve Protokoller (TCP/IP):** Verilerin kablolar üzerinden nasıl paketlere bölünüp hedefe ulaştığını öğren. (IPv4 vs IPv6, Portlar, Router'lar).
    *   *Neden önemli?* Sunucu bağlantı hatalarını ve ağ sorunlarını teşhis edebilmek için.
*   **DNS (Domain Name System):** `www.google.com` yazdığında arka planda IP adresinin nasıl çözümlendiğini anla. Kayıt türlerini (A, CNAME, TXT, MX) incele.
    *   *Neden önemli?* Canlıya aldığın bir projenin domain yönlendirmelerini yaparken hayati öneme sahiptir.
*   **HTTP ve HTTPS:** İstemci (tarayıcı) ve sunucu arasındaki iletişim kuralları. Metotları (GET, POST, PUT, DELETE), Başlıkları (Headers) ve Durum Kodlarını (200 OK, 404 Not Found, 500 Server Error) ezberleme, mantığını kavra.
*   **Tarayıcıların Çalışma Mantığı:** Tarayıcı bir HTML dosyasını nasıl okur, DOM ağacını nasıl oluşturur ve sayfayı nasıl çizer (Rendering)?

---

## Aşama 2: Ön Yüz (Frontend) – Kullanıcının Dünyası
Kullanıcının gördüğü, etkileşime girdiği her şey bu aşamanın konusudur.

*   **HTML5 & CSS3 (Temeller):**
    *   *HTML:* Sadece etiketleri değil, "Semantik HTML" (SEO ve erişilebilirlik için doğru etiket kullanımı) kavramını öğren.
    *   *CSS:* Kutu modeli (Box Model), Flexbox ve CSS Grid ile modern sayfa düzenleri kurabilme. Medya sorguları (Media Queries) ile mobil uyumlu (Responsive) tasarımlar yapma.
*   **JavaScript (Derinlemesine Core JS):** Çerçevelere (framework) geçmeden önce dili çok iyi tanı.
    *   DOM Manipülasyonu, Event Listener'lar.
    *   **Asenkron Programlama:** İnternet yavaştır. Veri beklerken tarayıcının donmaması için Callback'ler, Promises ve `Async/Await` yapılarını yut.
    *   *İleri Seviye:* Event Loop, Closure, Scope, Hoisting kavramlarını mülakat seviyesinde öğren.
*   **Modern Frontend Ekosistemi:**
    *   *Paket Yöneticileri:* npm, yarn veya pnpm.
    *   *Build Araçları:* Vite veya Webpack.
    *   *Framework:* React.js (veya Next.js). Component mimarisi, State yönetimi (Redux veya Context API), Hook'lar.

---

## Aşama 3: Arka Yüz (Backend) – Mantık ve Sunucu
İş kurallarının çalıştığı, verilerin işlendiği ve güvenliğin sağlandığı mutfak kısmı.

*   **Programlama Dili & Çatı (Örn: C# ve .NET Core):** Tip güvenli (Type-safe), nesne yönelimli (OOP) bir dil ile sağlam mimariler kurma.
*   **API Mimarileri (RESTful & Diğerleri):**
    *   *REST:* Kaynak (Resource) odaklı API tasarımı. HTTP metotlarını doğru kullanma.
    *   *GraphQL:* İstemcinin sadece ihtiyacı olan veriyi çekebilmesine olanak tanıyan sorgu dili.
    *   *Gerçek Zamanlı İletişim:* WebSockets ve SignalR ile anlık mesajlaşma/bildirim altyapıları.
*   **Kimlik Doğrulama ve Yetkilendirme (Auth & Authz):**
    *   Session ve Cookie tabanlı sistemler.
    *   **JWT (JSON Web Token):** Modern ve durumsuz (stateless) API güvenliği.
    *   OAuth 2.0 ve OpenID Connect: "Google ile Giriş Yap" mantığı.

---

## Aşama 4: Veritabanları ve Veri Yönetimi
Uygulamanın hafızası. Veriyi nasıl saklayacağın, uygulamanın performansını doğrudan etkiler.

*   **İlişkisel Veritabanları (RDBMS & SQL):** PostgreSQL veya MS SQL Server.
    *   Tablo tasarımları, ilişkiler (Bire-Bir, Bire-Çok, Çoka-Çok).
    *   *Optimizasyon:* İndeksleme (Indexing), Normalizasyon kuralları ve Transaction yönetimi (ACID prensipleri).
*   **NoSQL Veritabanları:** MongoDB. Esnek, doküman tabanlı veri saklama stratejileri. Hangi durumda SQL, hangi durumda NoSQL kullanacağını analiz etme.
*   **Önbellekleme (Caching):** Redis. Sık istenen verileri hızlı okumak için RAM üzerinde tutma mantığı.
*   **ORM (Object-Relational Mapping):** Entity Framework Core. SQL yazmadan kod üzerinden veritabanı sorguları oluşturma (LINQ).

---

## Aşama 5: DevOps, Sistem Yönetimi ve Bulut
Kodunu sadece kendi bilgisayarında değil, tüm dünyaya hizmet verecek sunucularda yönetme sanatı.

*   **Versiyon Kontrolü (Git & GitHub):** Kod geçmişini tutma, dallanma (branch) stratejileri (GitFlow) ve ekip içi kod inceleme (Pull Request) süreçleri.
*   **Linux & Terminal:** Sunucuların %90'ı Linux'tur. Temel Bash komutları, dosya izinleri ve SSH bağlantısı.
*   **Konteynerizasyon (Docker):** "Benim bilgisayarımda çalışıyordu!" bahanesini bitiren teknoloji. Uygulamanı ve tüm bağımlılıklarını izole bir kutuya (container) koyma.
*   **Sürekli Entegrasyon & Dağıtım (CI/CD):** GitHub Actions veya GitLab CI ile, kodu GitHub'a gönderdiğinde otomatik olarak test edilmesi ve sunucuya yüklenmesi (deployment).
*   **Bulut Bilişim (Cloud):** AWS (EC2, S3) veya Azure temelleri.

---

## Aşama 6: Mimari, Güvenlik ve Optimizasyon
Projeler büyüdüğünde kodun spagettiye dönmemesi ve sistemin çökmemesi için gerekenler.

*   **Yazılım Mimarileri:**
    *   Design Patterns (Tasarım Kalıpları): Singleton, Factory, Repository pattern vb.
    *   Clean Architecture, Onion Architecture veya Domain Driven Design (DDD) temelleri. Katmanların birbirinden nasıl izole edileceği.
    *   Monolitik vs. Mikroservis mimarileri arasındaki farklar.
*   **Güvenlik (OWASP Top 10):** Web dünyasındaki en yaygın saldırıları (SQL Injection, XSS, CSRF, DoS) ve bunlardan nasıl korunacağını öğrenme.
*   **Ölçeklenebilirlik (Scalability):** Dikey (Sunucu donanımını artırma) ve Yatay (Sunucu sayısını artırma) ölçekleme. Load Balancer (Yük Dengeleyici) kavramı.
*   **İzleme (Monitoring) & Loglama:** Uygulama çöktüğünde neden çöktüğünü bulmak için yapılandırılmış loglama (Serilog) ve görselleştirme (Kibana, Grafana).

---

## Aşama 7: Yazılım Testleri ve Kalite Güvencesi (QA)
Kodu yazdın, ama çalıştığından "gerçekten" emin misin? Manuel testleri bırakıp otomasyona geçiş.

*   **Unit Testing (Birim Testleri):** En küçük kod parçalarını (fonksiyonları) izole bir şekilde test etme (Örn: C# için xUnit, JS için Jest).
*   **Integration Testing:** Farklı modüllerin (örneğin API ile veritabanının) birlikte doğru çalışıp çalışmadığını test etme.
*   **End-to-End (E2E) Testing:** Kullanıcı gibi davranan botlar yazarak uygulamanın baştan sona test edilmesi (Cypress, Playwright).
*   **TDD (Test Driven Development):** Kodu yazmadan önce testini yazma felsefesi.

---

### Tavsiyeler
*   Bu listeyi baştan sona okuyup bitirilecek bir "kitap" gibi düşünme. Her aşamada ufak projeler yap.
*   Örneğin: Aşama 1 ve 2'yi bitirince bir "Hava Durumu Uygulaması" yap. Aşama 3 ve 4 bitince bunu kendi API'ne ve veritabanına bağla. Aşama 5'te bu projeyi sunucuya yükle. Aşama 6 ve 7'de performansını artırıp testlerini yaz.