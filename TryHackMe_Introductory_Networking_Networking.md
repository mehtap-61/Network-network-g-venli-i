**GİRİŞ AĞ OLUŞTURMA**

*Görev 1-Giriş*

Bu odanın amacı, ağ kurmanın temel prensiplerine yeni başlayanlar için bir giriş sağlamaktır. 
Ağ kurma çok büyük bir konudur, bu nedenle bu aslında sadece kısa bir genel bakış olacaktır; 
ancak, umarım size konu hakkında kendiniz için üzerine inşa edebileceğiniz bazı temel bilgiler verir.

Bu odada ele alınacak konular şunlardır:

•	OSI Modeli
•	TCP/IP Modeli
•	Bu modellerin pratikte nasıl olduğu
•	Temel ağ araçlarına giriş

OSI (Açık Sistemler Bağlantısı) Modeli, bilgisayar ağlarının arkasındaki teoriyi göstermek için kullandığımız standartlaştırılmış bir modeldir. 
Uygulamada, gerçek dünya ağlarının dayandığı aslında daha kompakt TCP/IP modelidir; 
ancak OSI modeli, birçok yönden, ilk anlayışı edinmek için daha kolaydır.

OSI modeli yedi katmandan oluşur:

![OSI_model](https://github.com/user-attachments/assets/a9a5875e-e9ef-4634-af11-109f4b7cea00)

OSI modelinin katmanlarını öğrenmenize yardımcı olacak birçok ezber tekniği var -- beğendiğinizi bulana kadar araştırın.
Bunların her birine sırayla kısaca bir göz atalım:

Katman 7 -- Uygulama:
OSI modelinin uygulama katmanı esasen bir bilgisayarda çalışan programlara ağ seçenekleri sağlar.
Neredeyse yalnızca uygulamalarla çalışır ve verileri iletmek için kullanabilecekleri bir arayüz sağlar. 
Veriler uygulama katmanına verildiğinde, sunum katmanına aktarılır.

Katman 6 -- Sunum:
Sunum katmanı, uygulama katmanından veri alır. Bu veriler genellikle uygulamanın anlayabileceği bir biçimdedir, ancak alıcı bilgisayardaki uygulama katmanı tarafından anlaşılabilecek standart bir biçimde olmayabilir. Sunum katmanı, verileri standart bir biçime çevirir ve ayrıca verilere yönelik herhangi bir şifreleme, sıkıştırma veya diğer dönüşümleri gerçekleştirir. Bu tamamlandığında, veriler oturum katmanına aktarılır.

Katman 5 -- Oturum:
Oturum katmanı sunum katmanından doğru biçimlendirilmiş verileri aldığında, ağ üzerinden diğer bilgisayarla bir bağlantı kurup kuramayacağını görmek ister. 
Kuramazsa bir hata gönderir ve işlem daha ileri gitmez. Bir oturum kurulabiliyorsa, oturum katmanının görevi onu sürdürmek ve iletişimleri senkronize etmek için uzak bilgisayarın oturum katmanıyla işbirliği yapmaktır.
Oturum katmanı özellikle önemlidir çünkü oluşturduğu oturum söz konusu iletişime özgüdür. Bu, tüm veriler karışmadan aynı anda farklı uç noktalara birden fazla istekte bulunmanızı sağlar (bir web tarayıcısında aynı anda iki sekme açmayı düşünün)! 
Oturum katmanı ana bilgisayar ile uzak bilgisayar arasında bir bağlantıyı başarıyla kaydettiğinde, veriler Katman 4'e, yani taşıma katmanına aktarılır.

Katman 4 -- Taşıma:
Taşıma katmanı, çok sayıda önemli işlevi yerine getiren çok ilginç bir katmandır.
İlk amacı, verilerin iletileceği protokolü seçmektir. 
Taşıma katmanındaki en yaygın iki protokol TCP (İletim Kontrol Protokolü) ve UDP'dir (Kullanıcı Datagram Protokolü); TCP ile iletim bağlantı tabanlıdır, 
yani bilgisayarlar arasında bir bağlantı kurulur ve istek süresince bu bağlantı sürdürülür.
Bu, bağlantının tüm paketlerin doğru yere ulaşmasını sağlamak için kullanılabilmesi nedeniyle güvenilir bir iletim sağlar. 
Bir TCP bağlantısı, iki bilgisayarın sürekli iletişim halinde kalmasını sağlayarak verilerin kabul edilebilir bir hızda gönderilmesini ve kaybolan verilerin yeniden gönderilmesini sağlar.
UDP ile ise tam tersi geçerlidir; veri paketleri esasen alıcı bilgisayara atılır -- eğer yetişemiyorsa bu onun sorunudur (bu yüzden bağlantı kötüyse Skype gibi bir şey üzerinden yapılan bir video iletimi pikselleştirilebilir). 
Bunun anlamı, TCP'nin genellikle doğruluğun hızdan daha önemli olduğu durumlarda (örneğin dosya aktarımı veya bir web sayfasının yüklenmesi) seçileceği ve UDP'nin hızın daha önemli olduğu durumlarda (örneğin video akışı) kullanılacağıdır.
Bir protokol seçildiğinde, taşıma katmanı iletimi küçük parçalara böler (TCP üzerinden bunlara segmentler, UDP üzerinden bunlara datagramlar denir), bu da mesajın başarılı bir şekilde iletilmesini kolaylaştırır.

Katman 3 -- Ağ:
Ağ katmanı, isteğinizin hedefini bulmaktan sorumludur. Örneğin, İnternet çok büyük bir ağdır; bir web sayfasından bilgi istemek istediğinizde, sayfanın IP adresini alan ve izlenecek en iyi yolu bulan ağ katmanıdır. Bu aşamada, hala yazılım tarafından kontrol edilen Mantıksal adresleme (yani IP adresleri) olarak adlandırılan şeyle çalışıyoruz. Mantıksal adresler, ağlara düzen sağlamak, onları kategorilere ayırmak ve düzgün bir şekilde sıralamamızı sağlamak için kullanılır. Şu anda mantıksal adreslemenin en yaygın biçimi, muhtemelen zaten aşina olduğunuz IPV4 biçimidir (yani 192.168.1.1, bir ev yönlendiricisi için yaygın bir adrestir).

Katman 2 -- Veri Bağlantısı:
Veri bağlantı katmanı, iletim için fiziksel adreslemeye odaklanır. 
Ağ katmanından (uzak bilgisayarın IP adresini içeren) bir paket alır ve alıcı uç noktanın fiziksel (MAC) adresini ekler.
Ağa bağlı her bilgisayarın içinde, onu tanımlamak için benzersiz bir MAC (Ortam Erişim Kontrolü) adresiyle gelen bir Ağ Arabirim Kartı (NIC) bulunur.
MAC adresleri üretici tarafından ayarlanır ve kelimenin tam anlamıyla karta yazılır; değiştirilemezler -- ancak sahte olabilirler. 
Bilgi bir ağ üzerinden gönderildiğinde, aslında bilginin tam olarak nereye gönderileceğini tanımlamak için kullanılan fiziksel adrestir.
Ayrıca, veriyi iletim için uygun bir biçimde sunmak da veri bağlantı katmanının işidir.
Veri bağlantı katmanı, veri aldığında önemli bir işlev de görür, çünkü alınan bilgilerin iletim sırasında bozulmadığından emin olmak için kontrol eder; bu, veriler katman 1: fiziksel katman tarafından iletildiğinde çok iyi olabilir.
Katman 1 -- Fiziksel:
Fiziksel katman, bilgisayarın donanımına kadar uzanır.
Bir ağ üzerinden veri aktarımını oluşturan elektrik darbelerinin gönderildiği ve alındığı yer burasıdır. 
Fiziksel katmanın görevi, iletimdeki ikili verileri sinyallere dönüştürmek ve bunları ağ üzerinden iletmek, ayrıca gelen sinyalleri almak ve bunları tekrar ikili verilere dönüştürmektir.

*Aşağıdaki "Hangi Katman" Soruları için, katman numarasını (1-7) kullanarak cevaplayın.*

**Hangi katman veriyi TCP veya UDP üzerinden göndermeyi seçer?**
**Cevap:** 4-Transportation(Taşıma)

**Alınan bilgilerin bozulmadığından emin olmak için hangi katman kontrol eder?**
**Cevap:** 2-Data link(Veri bağlantısı)

**Veriler iletim için hangi katmanda biçimlendirilir?**
**Cevap:** 2-Data link(Veri bağlantısı)

**Hangi katman veriyi iletir ve alır?**
**Cevap:** 1-Physical(Fiziksel)

**Başlangıç verilerini standart bir formata kavuşturmak için hangi katman şifreler, sıkıştırır veya başka şekilde dönüştürür?**
**Cevap:** 6- Presentation (Sunum)

**Ana bilgisayar ile alıcı bilgisayarlar arasındaki iletişimi hangi katman izler?**
**Cevap:** 5- Session (oturum)

**Uygulamalardan gelen iletişim isteklerini hangi katman kabul eder?**
**Cevap:** 7- Application(Uygulama)

**Mantıksal adreslemeyi hangi katman gerçekleştirir?**
**Cevap:** 3- Network(Ağ)

**TCP üzerinden veri gönderirken, "bir lokma büyüklüğündeki" veri parçalarına ne ad verirsiniz?**
**Cevap:** Segments

**FTP protokolü hangi katmanla haberleşecektir?**
**Cevap:** 7- Application(Uygulama)

**Canlı bir videoyu iletmek için hangi taşıma katmanı protokolü en uygundur?**
**Cevap:** UDP

*Görev 3-Kapsülleme*

Veriler modelin her katmanından aşağı doğru iletildikçe, söz konusu katmana özgü ayrıntıları içeren daha fazla bilgi iletim başlangıcına eklenir.
Örneğin, Ağ Katmanı tarafından eklenen başlık, kaynak ve hedef IP adresleri gibi şeyleri içerir ve 
Taşıma Katmanı tarafından eklenen başlık (diğer şeylerin yanı sıra) kullanılan protokole özgü bilgileri içerir. 
Veri bağlantı katmanı ayrıca iletim sonuna, verilerin iletim sırasında bozulmadığını doğrulamak için kullanılan bir parça ekler; 
bu, verilerin fragmanı bozmadan kesilemeyeceği ve kurcalanamayacağı için artan güvenlik gibi ek bir avantaja da sahiptir.
Tüm bu sürece kapsülleme denir; verilerin bir bilgisayardan diğerine gönderilebildiği işlem.

![kapsulleme_sureci](https://github.com/user-attachments/assets/a88cd586-999a-47c4-a4de-0d94f5c15a0c)

Kapsüllenmiş verilere, sürecin farklı adımlarında farklı adlar verildiğine dikkat edin. 
7, 6 ve 5. katmanlarda, veriler basitçe veri olarak adlandırılır. 
Taşıma katmanında, kapsüllenmiş veriler bir segment veya bir veri paketi olarak adlandırılır(iletim protokolü olarak TCP veya UDP'nin seçilip seçilmediğine bağlı olarak). 
Ağ Katmanında, veriler bir paket olarak adlandırılır. 
Paket Veri Bağlantısı katmanına iletildiğinde bir çerçeve haline gelir ve bir ağ üzerinden iletildiğinde çerçeve bitlere bölünmüş olur.
Mesaj ikinci bilgisayar tarafından alındığında, süreç tersine döner -- fiziksel katmandan başlayarak uygulama katmanına ulaşana kadar çalışır ve ilerledikçe eklenen bilgileri sıyırır. 
Buna kapsülden çıkarma denir. 
Bu şekilde, OSI modelinin katmanlarını ağ yeteneklerine sahip her bilgisayarın içinde var olduğunu düşünebilirsiniz.
Uygulamada aslında bu kadar net olmasa da, bilgisayarlar veri göndermek için aynı kapsülleme ve veriyi aldıktan sonra kapsüllemeyi kaldırma sürecini takip eder.

En azından pratik kullanımları nedeniyle değil, aynı zamanda bize veri göndermek için standart bir yöntem sağladıkları için Kapsülleme ve kapsüllemeyi kaldırma süreçleri çok önemlidir.
Bu, tüm iletimlerin tutarlı bir şekilde (aynı üreticiden olmalarına, aynı işletim sistemini kullanmalarına veya başka herhangi bir faktöre bakılmaksızın) aynı metodolojiyi takip edeceği ve ağ etkinleştirilmiş herhangi bir cihazın herhangi bir erişilebilir cihaza bir istek göndermesine ve bunun anlaşılacağından emin olmasına olanak tanıyacağı anlamına gelir .

**Kapsülleme sürecinin 2. katmanındaki verilere (OSI modeliyle) nasıl atıfta bulunursunuz?**
**Cevap:** Frames (Çerçeveler)

**UDP protokolü seçilmişse, kapsülleme sürecinin 4. katmanındaki verilere (OSI modeliyle) nasıl atıfta bulunursunuz?
**Cevap:** Datagrams

**Alınan mesaj üzerinde bilgisayar hangi işlemi gerçekleştirir?**
**Cevap:** De-encapsulation

**OSI modelinin kapsülleme sırasında fragman ekleyen tek katmanı hangisidir?**
**Cevap:** Data link

**Kapsülleme ekstra bir güvenlik katmanı sağlar mı (Evet/Hayır)?**
**Cevap:** Evet

**Görev 4-TCP/IP Model**

TCP/IP modeli birçok yönden OSI modeline çok benzer.
Birkaç yıl daha eskidir ve gerçek dünya ağlarının temelini oluşturur.
TCP/IP modeli dört katmandan oluşur: Uygulama, Taşıma, İnternet ve Ağ Arayüzü.
Bunlar, aralarında OSI Modelinin yedi katmanıyla aynı işlev aralığını kapsar.

![TCP_IP](https://github.com/user-attachments/assets/e4330bde-3615-41e9-b492-564f47c67812)

Not: Bazı yeni kaynaklar TCP/IP modelini beş katmana böldü
-- Ağ Arayüzü katmanını Veri Bağlantısı ve Fiziksel katmanlara ayırdı (OSI modelinde olduğu gibi). 
Bu kabul görmüş ve iyi bilinen bir durumdur; ancak resmi olarak tanımlanmamıştır (RFC1122'de tanımlanan orijinal dört katmanın aksine). 
Hangi sürümü kullanacağınız size kalmış 
-- ikisi de genellikle geçerli kabul edilir.
Gerçek dünyada hiçbir şey için kullanılmıyorsa neden OSI modeliyle uğraştığımızı sormakta haklısınız.
Bu sorunun cevabı oldukça basit bir şekilde OSI modelinin (TCP/IP modelinden daha az yoğun ve daha katı olması nedeniyle) ağ kurmanın ilk teorisini öğrenmek için daha kolay olma eğiliminde olmasıdır.

İki model aşağıdaki gibi denk gelmektedir:

![OSI_ve_TCP_IP](https://github.com/user-attachments/assets/0ab0e86c-4f0a-4579-a59b-0d47db8ebebe)

Kapsülleme ve kapsülden çıkarma işlemleri, TCP/IP modeliyle OSI modeliyle aynı şekilde çalışır. 
TCP/IP modelinin her katmanına, kapsülleme sırasında bir başlık eklenir ve kapsülden çıkarma sırasında kaldırılır.

Şimdi işin pratik tarafına geçelim.

Katmanlı bir model görsel bir yardımcı olarak harikadır -- bize verilerin bir ağ üzerinden nasıl kapsüllenip gönderilebileceğine dair genel süreci gösterir, ancak bu aslında nasıl gerçekleşir?

TCP/IP'den bahsettiğimizde, içinde dört katman bulunan bir tabloyu düşünmek güzel ve iyidir, ancak aslında bir protokol paketinden -- bir eylemin nasıl gerçekleştirileceğini tanımlayan kurallar kümesinden -- bahsediyoruz.
TCP/IP adını bunlardan en önemli ikisinden alır: İki uç nokta arasındaki veri akışını kontrol eden İletim Kontrol Protokolü (daha önce OSI modelinde değindiğimiz) ve paketlerin nasıl adreslenip gönderileceğini kontrol eden İnternet Protokolü. 
TCP/IP paketini oluşturan daha birçok protokol vardır; bunlardan bazılarını daha sonraki görevlerde ele alacağız. Ancak şimdilik TCP'den bahsedelim.
Daha önce de belirtildiği gibi, TCP bağlantı tabanlı bir protokoldür. 
Başka bir deyişle, TCP üzerinden herhangi bir veri göndermeden önce, iki bilgisayar arasında kararlı bir bağlantı kurmalısınız. 
Bu bağlantıyı kurma sürecine üçlü el sıkışma denir.
Bir bağlantı kurmaya çalıştığınızda, bilgisayarınız önce uzak sunucuya bir bağlantı başlatmak istediğini belirten özel bir istek gönderir.
Bu istek, esasen bağlantı sürecini başlatmada ilk teması kuran SYN (eş zamanlamanın kısaltması) biti adı verilen bir şey içerir. 
Sunucu daha sonra SYN bitini ve ACK adı verilen başka bir "onay" bitini içeren bir paketle yanıt verecektir. 
Son olarak, bilgisayarınız bağlantının başarıyla kurulduğunu doğrulayan ACK bitini içeren bir paket gönderecektir. 
Üçlü el sıkışma başarıyla tamamlandığında, veriler iki bilgisayar arasında güvenilir bir şekilde iletilebilir. 
İletim sırasında kaybolan veya bozulan veriler yeniden gönderilir, böylece kayıpsız gibi görünen bir bağlantı oluşur.

![client_Server](https://github.com/user-attachments/assets/826415c1-ec64-496e-b27a-f2154dfbad3c)

Tarihçe:
TCP/IP ve OSI modellerinin başlangıçta neden yaratıldığını tam olarak anlamak önemlidir. 
Başlangıçta bir standardizasyon yoktu -- farklı üreticiler kendi metodolojilerini izlediler ve sonuç olarak farklı üreticiler tarafından üretilen sistemler ağ oluşturma konusunda tamamen uyumsuzdu.
TCP/IP modeli, tüm farklı üreticilerin takip edebileceği bir standart sağlamak için 1982'de Amerikan DoD tarafından tanıtıldı. 
Bu, tutarsızlık sorunlarını çözdü. Daha sonra OSI modeli de Uluslararası Standardizasyon Örgütü (ISO) tarafından tanıtıldı; ancak, TCP/IP modeli hala modern ağ oluşturmanın dayandığı standart olduğundan, esas olarak öğrenme için daha kapsamlı bir kılavuz olarak kullanılıyor.

**Hangi model ilk olarak tanıtıldı; OSI mi, TCP/IP mi?**
**Cevap:** TCP/IP

**TCP/IP modelinin hangi katmanı OSI modelinin Taşıma katmanının işlevselliğini kapsar (Tam Adı)?**
**Cevap:** Transport

**TCP/IP modelinin hangi katmanı OSI modelinin (Tam Adı) Oturum katmanının işlevselliğini kapsar?**
**Cevap:** Application

**TCP/IP modelinin Ağ Arayüzü katmanı, OSI modelindeki iki katmanın işlevselliğini kapsar. Bu katmanlar Veri Bağlantısı ve?.. (Tam Ad)?**
**Cevap:** Physical

**TCP/IP modelinin hangi katmanı OSI ağ katmanının işlevselliğini ele alır?**
**Cevap:**Internet

**TCP ne tür bir protokoldür?**
**Cevap:** Connection-based

**SYN neyin kısaltmasıdır?**
**Cevap:** Synchronise

**Üçlü el sıkışmanın ikinci adımı nedir?**
**Cevap:** SYN/ACK

**Üçlü el sıkışmadaki "Teşekkür" bölümünün kısa adı nedir?**
**Cevap:** ACK

**Görev 5- Network tool-ping**

Bu aşamada, umarım tüm teori mantıklı gelmiştir ve artık bilgisayar ağlarının ardındaki temel modelleri anlamışsınızdır.
Odanın geri kalanında, pratik uygulamalarda kullanabileceğimiz bazı komut satırı ağ araçlarına bakacağız.
Bu araçların çoğu diğer işletim sistemlerinde de çalışır, ancak basitlik adına, bu odanın geri kalanında Linux kullandığınızı varsayacağım. 
İnceleyeceğimiz ilk araç ping komutu olacak.
ping komutu, uzak bir kaynağa bağlantının mümkün olup olmadığını test etmek istediğimizde kullanılır. 
Genellikle bu, internetteki bir web sitesi olacaktır, ancak doğru şekilde yapılandırılıp yapılandırılmadığını kontrol etmek istiyorsanız ev ağınızdaki bir bilgisayar için de olabilir.
Ping, daha önce bahsedilen biraz daha az bilinen TCP/IP protokollerinden biri olan ICMP protokolünü kullanarak çalışır. 
ICMP protokolü, OSI Modelinin Ağ katmanında ve dolayısıyla TCP/IP modelinin İnternet katmanında çalışır.
Ping için temel sözdizimi ping <hedef>'tir.
Bu örnekte, Google'a bir ağ bağlantısının mümkün olup olmadığını test etmek için ping kullanıyoruz:

![ping](https://github.com/user-attachments/assets/bbe22da2-834e-4111-b8cb-3cc523f5cb88)

Ping komutunun aslında talep edilen URL yerine bağlandığı Google sunucusunun IP adresini döndürdüğüne dikkat edin. 
Bu, bir web sitesini barındıran sunucunun IP adresini belirlemek için kullanılabildiğinden, ping için kullanışlı bir ikincil uygulamadır. 
Ping'in en büyük avantajlarından biri, hemen hemen her ağ etkin cihazda bulunmasıdır. Tüm işletim sistemleri bunu kutudan çıktığı haliyle destekler ve hatta çoğu gömülü cihaz bile ping'i kullanabilir!
Aşağıdaki soruları deneyin. Sözdizimi ile ilgili tüm sorular, ping için man sayfasını (Linux'ta man ping) kullanarak yanıtlanabilir.

**bbc.co.uk sitesine ping atmak için hangi komutu kullanırsınız?**
**Cevap:** ping bbc.co.uk
**ping muirlandoracle.co.uk
IPV4 adresi nedir?**
**Cevap:**
![ping_2](https://github.com/user-attachments/assets/ce9936e9-a497-4e91-b4fb-9de1781b8af8)

**Gönderilen ping isteklerinin aralığını değiştirmenizi sağlayan anahtar hangisidir?**
**Cevap:** -i
**Hangi anahtar istekleri IPv4 ile sınırlamanıza olanak tanır?**
**Cevap:** -4
**Hangi anahtar size daha ayrıntılı bir çıktı verir?**
**Cevap:** -v
**Görev 6-Traceoute**
Ping komutunun mantıksal devamı 'traceroute'tur.
Traceroute, isteğinizin hedef makineye giderken izlediği yolu haritalamak için kullanılabilir.
İnternet, birbirine bağlı birçok farklı sunucu ve uç noktadan oluşur. 
Bu, gerçekten istediğiniz içeriğe ulaşmak için önce bir sürü başka sunucudan geçmeniz gerektiği anlamına gelir. 

Traceroute, bu bağlantıların her birini görmenizi sağlar -- bilgisayarınız ile istediğiniz kaynak arasındaki her ara adımı görmenizi sağlar. Linux'ta traceroute için temel sözdizimi şudur: traceroute <hedef>
Varsayılan olarak, Windows traceroute yardımcı programı (tracert), ping'in kullandığı aynı ICMP protokolünü kullanarak çalışır ve Unix eşdeğeri UDP üzerinden çalışır. Bu, her iki durumda da anahtarlarla değiştirilebilir.

![traceoute](https://github.com/user-attachments/assets/f64d5ed2-885d-43a6-8b71-dc6c80c6a6ea)

Yönlendiricimden (_gateway) 216.58.205.46 adresindeki Google sunucusuna gitmenin 13 atlama aldığını görebilirsiniz
Şimdi sıra sizde. Daha önce olduğu gibi, anahtarlarla ilgili tüm sorular traceroute için man sayfasıyla cevaplanabilir (man traceroute).

![traceoute_answer](https://github.com/user-attachments/assets/3ee37c04-d8fb-48d5-a73a-0a7c0ec96c95)

Traceroute kullanırken bir arayüzü belirtmek için hangi anahtarı kullanırsınız?
Cevap: -i

Rotayı izlerken TCP SYN isteklerini kullanmak isterseniz hangi anahtarı kullanırsınız?
Cevap: -t

**Traceroute varsayılan olarak TCP/IP modelinin hangi katmanında çalışır (Windows)?**
**Cevap:** Internet

**Görev7 -Network Tools-WHOIS**

Alan Adları -- internetin bilinmeyen kurtarıcıları.
Ziyaret etmek istediğiniz her web sitesinin IP adresini hatırlamanın nasıl bir his olduğunu hayal edebiliyor musunuz? Korkunç bir düşünce.
Neyse ki alan adlarımız var.
Bir sonraki görevde bunun nasıl çalıştığı hakkında biraz daha konuşacağız, ancak şimdilik bir alan adının bir IP adresine dönüştüğünü ve onu hatırlamamıza gerek kalmadığını bilmeniz yeterli (örneğin TryHackMe IP adresi yerine tryhackme.com yazabilirsiniz). Alan adları Alan Adı Kayıt Kuruluşları adı verilen şirketler tarafından kiralanır. Bir alan adı istiyorsanız, gidip bir kayıt kuruluşuna kayıt yaptırırsınız, ardından alanı belirli bir süre için kiralarsınız.
Whois girin.

Whois temelde bir alan adının kime kayıtlı olduğunu sorgulamanıza olanak tanır. Avrupa'da kişisel bilgiler sansürlenir; ancak başka yerlerde bir whois aramasından potansiyel olarak çok sayıda bilgi edinebilirsiniz.
AttackBox kullanan Ücretsiz Kullanıcılar için whois aracının bir web sürümü bulunmaktadır.
(Not: Kullanmadan önce whois'i yüklemeniz gerekebilir. Debian tabanlı sistemlerde bu, sudo apt update && sudo apt-get install whois ile yapılabilir)
Whois aramaları gerçekleştirmek çok kolaydır. Alan adı kaydı hakkında mevcut bilgilerin bir listesini almak için whois <domain> kullanmanız yeterlidir:

![whois_bbc co uk](https://github.com/user-attachments/assets/97598916-bf0f-4617-92ea-464ffeca31f0)

Bu, genellikle bulunabilecek kadar küçük bir bilgi miktarıdır. 
Alan adını, alan adını kaydeden şirketi, son yenilemeyi ve bir sonraki yenilemenin ne zaman yapılacağını ve ad sunucuları hakkında bir sürü bilgiyi (bir sonraki görevde inceleyeceğiz) aldığımızı fark edin.

![noanswer](https://github.com/user-attachments/assets/bbd02eac-9c47-4dbf-992d-f86f15b63933)
**facebook.com için kayıtlı kişinin posta kodu nedir?**
**Cevap:** 94025
![facebook](https://github.com/user-attachments/assets/878b593d-a964-42b0-9f30-6ac54deacd76)

**facebook.com domaini ilk ne zaman kaydedildi (Format: GG/AA/YYYY)?**
**Cevap:** 29/03/1997

![microsoft com_bos](https://github.com/user-attachments/assets/0cb65306-02ea-4228-8d3a-c0f1f9bbc13b)

**Kayıt sahibi hangi şehirde bulunuyor?**   
**Cevap:** Redmond

![microsoft soft_location](https://github.com/user-attachments/assets/7bd8e6ae-1cda-4212-bba1-1993c4a7e273)

**[OSINT] microsoft.com'un kayıtlı adresinin yakınındaki golf sahasının adı nedir?**
**Cevap:** Bellevue Golf Course

**microsoft.com için kayıtlı teknik e-posta nedir?**
**Cevap:** msnhst@microsoft.com

**Görev9: [Networking Tools] Dig**
Önceki görevde alan adlarından bahsetmiştik -- şimdi bunların nasıl çalıştığından bahsedelim.
Bir URL'nin bilgisayarınızın anlayabileceği bir IP adresine nasıl dönüştürüldüğünü hiç merak ettiniz mi? 
Cevap, DNS (Alan Adı Sistemi) adı verilen bir TCP/IP protokolüdür. En temel düzeyde, DNS bize erişmeye çalıştığımız web sitesinin IP adresini bize vermesi için özel bir sunucudan istekte bulunmamızı sağlar. 
Örneğin, www.google.com'a bir istekte bulunursak, bilgisayarımız önce özel bir DNS sunucusuna (bilgisayarınızın nasıl bulacağını zaten bildiği) bir istek gönderir. 
Sunucu daha sonra Google için IP adresini arar ve bize geri gönderir. Bilgisayarımız daha sonra isteği Google sunucusunun IP adresine gönderebilir.

Bunu biraz parçalayalım.
Bir web sitesine bir istekte bulunursunuz.
Bilgisayarınızın yaptığı ilk şey, açık bir IP->Alan adı eşlemesinin oluşturulup oluşturulmadığını görmek için yerel "Ana Bilgisayar Dosyası"nı kontrol etmektir. 
Bu, DNS'den daha eski bir sistemdir ve modern ortamlarda çok daha az kullanılır; ancak, yine de çoğu işletim sisteminin arama sıralamasında önceliklidir.
Manuel olarak hiçbir eşleme oluşturulmamışsa, bilgisayar daha sonra web sitesi için depolanmış bir IP adresi olup olmadığını görmek için yerel DNS önbelleğini kontrol eder; varsa, harika. Yoksa, işlemin bir sonraki aşamasına geçer.
Adresin henüz bulunmadığını varsayarak, bilgisayarınız daha sonra özyinelemeli DNS sunucusu olarak bilinen bir şeye bir istek gönderecektir. 
Bunlar ağınızdaki yönlendirici tarafından otomatik olarak bilinecektir. Birçok İnternet Servis Sağlayıcısı (İSS) kendi özyinelemeli sunucularını korur, ancak Google ve OpenDNS gibi şirketler de özyinelemeli sunucuları kontrol eder.
Bilgisayarınızın bilgi isteğini nereye göndereceğini otomatik olarak bilmesi bu şekildedir: yinelemeli bir DNS sunucusunun ayrıntıları yönlendiricinizde veya bilgisayarınızda saklanır.
Bu sunucu ayrıca popüler alan adları için bir sonuç önbelleği tutar; ancak, talep ettiğiniz web sitesi önbellekte saklanmamışsa, yinelemeli sunucu isteği bir kök ad sunucusuna iletir.
2004'ten önce dünyada tam olarak 13 kök ad DNS sunucusu vardı. Günümüzde çok daha fazlası var; ancak, orijinal sunuculara atanan aynı 13 IP adresini kullanarak erişilebilirler (bir istekte bulunduğunuzda en yakın sunucuyu alabilmeniz için dengelenmiştir). Kök ad sunucuları esasen bir sonraki seviyedeki DNS sunucularını takip eder ve isteğinizi yönlendirmek için uygun olanı seçer. Bu alt seviye sunuculara Üst Seviye Alan Adı sunucuları denir.
Üst Düzey Alan Adı (TLD) sunucuları uzantılara ayrılır.
Örneğin, tryhackme.com'u arıyorsanız isteğiniz .com alan adlarını işleyen bir TLD sunucusuna yönlendirilir.
bbc.co.uk'u arıyorsanız isteğiniz .co.uk alan adlarını işleyen bir TLD sunucusuna yönlendirilir.
Kök ad sunucularında olduğu gibi TLD sunucuları bir sonraki seviyeyi takip eder: Yetkili ad sunucuları.
Bir TLD sunucusu bilgi isteğinizi aldığında, sunucu bunu uygun bir Yetkili ad sunucusuna iletir.
Yetkili ad sunucuları, alan adları için DNS kayıtlarını doğrudan depolamak için kullanılır. 
Başka bir deyişle, dünyadaki her alan adının DNS kayıtları bir yerlerde Yetkili bir ad sunucusunda depolanır; bunlar bilginin kaynağıdır.
İsteğiniz sorguladığınız alan adının yetkili ad sunucusuna ulaştığında, ilgili bilgileri size geri göndererek bilgisayarınızın talep ettiğiniz alan adının arkasındaki IP adresine bağlanmasını sağlar.
Web tarayıcınızda bir web sitesini ziyaret ettiğinizde bunların hepsi otomatik olarak gerçekleşir, ancak bunu dig adlı bir araçla manuel olarak da yapabiliriz. 
Ping ve traceroute gibi, dig de Linux sistemlerine otomatik olarak yüklenmelidir.
dig, etki alanları hakkında bilgi için seçtiğimiz yinelemeli DNS sunucularını manuel olarak sorgulamamızı sağlar:
dig <domain> @<dns-server-ip>
Ağ sorun giderme için çok kullanışlı bir araçtır.

![dig](https://github.com/user-attachments/assets/1c9d2b47-0d0f-4474-9737-a2b0e0a7e510)

Özetle, bu bilgi bize bir sorgu gönderdiğimizi ve başarılı bir şekilde (yani Hata Yok) tam bir yanıt aldığımızı söylüyor -- ki bu, beklendiği gibi, sorguladığımız alan adının IP adresini içeriyor.
dig'in bize verdiği bir diğer ilginç bilgi de sorgulanan DNS kaydının TTL'sidir (Yaşam Süresi). Daha önce belirtildiği gibi, bilgisayarınız bir alan adını sorguladığında, sonuçları yerel önbelleğinde depolar.
Kaydın TTL'si, bilgisayarınıza kaydı geçerli olarak değerlendirmeyi ne zaman bırakacağını söyler -- yani, önbelleğe alınmış kopyaya güvenmek yerine verileri tekrar istemesi gereken zamanı.
TTL, yanıt bölümünün ikinci sütununda bulunabilir:

![TTL](https://github.com/user-attachments/assets/53e79a71-c9d2-406c-a78f-ccf09b0f08b9)

TTL'nin (DNS önbelleğe alma bağlamında) saniyelerle ölçüldüğünü hatırlamak önemlidir, bu nedenle örnekteki kayıt iki dakika otuz yedi saniyede sona erecektir.

**DNS neyin kısaltmasıdır?**
Cevap: DNS-Domain Name System

**Bir alan adı aradığınızda bilgisayarınızın sorgulayacağı ilk DNS sunucusu türü nedir?**
**Cevap:** Recursive (Tekrarlayan)

**Alan adı uzantılarına özgü kayıtları (yani .com, .co.uk*, vb.)* içeren DNS sunucusu türü hangisidir? Adın uzun versiyonunu kullanın.**
**Cevap:** Top-level Domain

**Bilgisayarınızın bir alan adının IP adresini bulmak için ilk bakacağı yer neresidir?**
**Cevap:**  host file

**Google iki adet genel DNS sunucusu çalıştırıyor. Bunlardan biri 8.8.8.8 IP ile sorgulanabilir, diğerinin IP adresi nedir?**
**Cevap:**    8.8.4.4

**Bir DNS sorgusunun TTL'si 24 saat ise, kazı sorgusu hangi sayıyı gösterir?**
**Cevap:**   86400

**Görev9 - Daha fazla okuma**

Bu, ağ temelleri hakkında fırtına gibi geçen turumuzu tamamladı. 
Umarım bilgilendirici bulmuşsunuzdur.
Ağ, öğrenmeniz gereken şeylerden biridir. En temelleri ele aldık, ancak kendi başınıza öğrenmeye devam etmeniz çok iyi bir fikir olacaktır.
Daha fazla bilgi açısından, bu odanın içeriğiyle ilgili herhangi bir yardıma ihtiyacınız varsa TryHackMe Discord'da bize ulaşmaktan çekinmeyin. 
Ayrıca, ağ teorisi hakkındaki bilginizi genişletmek istiyorsanız, Steve McQuerry'nin CISCO Self Study Guide'ı çalışmak için harika bir kaynaktır. 
Daha güncel bir sürümü mevcut olabilir; ancak, bu sürüm ucuz, kolayca bulunabilen ve en önemlisi, hala çok alakalı.
CCNA sınavı için bir çalışma kılavuzu olarak tasarlanmış olsa da, bu kitap ağ ilkelerine çok yönlü bir giriş olarak da aynı derecede iyi hizmet ediyor.

![son_answer](https://github.com/user-attachments/assets/30e33dbd-143c-4105-962b-9c488cbe920f)
