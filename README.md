
İşletim Sistemi : Donanımların(Monitor,Ram,Ekran Kartı vs) uygulamaları çalışmasına aracılık eden yazılım.

Kernel : Üstteki işi yapan en temel işletim sistemi parçası.

NOT: Pc'de işletim sistemi olmasada uygulama çalıştırabiliriz. Ama o çalıştıracağımız uygulamaların hangi donanımı kullanması gerektiğini kodlarla bilmesi gerekli

Sanallaştırma (VM): Öncelikle sunucunun çalışma mantığını kısaca hatırlayalım. Sunucuyu bir bilgisayar gibi düşün, ve bunun içine bir işletim sistemi
bu işletim sisteminin üzerine uygulama kurulurdu. Daha sonra bu sunucuya bağlanmak isteyenlere de uzaktan gerekli konfigürasyonlar yapılır, bağlanırdı.
2000 lerin başında IT şirketleri fiziksel sunucular kullanırlardı(BARE METAL), mesela 5 tane uygulamam var, 5 tane fiziksel sunucu satın alırlardı,Ve bu 5 uygulamayı 
bu sunuculara koyarlardı, Günümüzde ise sanallaştırma dediğimiz olay ile işler yürüyor sanallaştırma dediğimiz olay ise şudur. Bir sunucu içerisinde
5 tane işletim sistemi kuruyoruz ve bu işletim sistemlerine çalıştırmak istediğimiz 5 uygulamayı kuruyoruz. Artık eski zamanlardaki gibi sunucu sipariş et,
gelmesini bekle, kurulumunu yap gibi zaman ve maddi maliyetler ortadan kalkıyor.

Docker : Docker şudur, yukarıda sanallaştırma işini yapıyor fakat sanallaştırmada her bir işletim sistemi kendi temel işlerinide görmek için fazlaca alan ve çaba 
harcıyorlar, docker ise tek bir işletim sistemi üzerinde birden fazla sunucu çalıştırmamıza olanak sağlıyor ve 5 işletim sisteminin temel işleri için harcayacağı
eforları yerine artık tek bir işletim sistemi efor harcıyor.Ayrıca diyelim ki sanal makinanız içindeki uygulamayı başka bir yere taşımak istediniz bu çok yorucu 
ve zahmetli bir iştir.Fakat docker kullanırsanız, taşımak istediğiniz pc'de docker olması yeterlidir. Ayrıca containerlar VM'e göre çok daha hızlıdırlar.

<img src="https://user-images.githubusercontent.com/54666839/162386446-774bf897-d254-4a45-b277-ff3e301a16b4.png"/> 

Docker Engine 3 componentten oluşur :
Docker Daemon : Volumes,İmage,Container,Network yaratmamızı ve yönetmemizi sağlar.
Docker Rest API : Dockerın diğer uygulamalarla haberleşmesini sağlar.
Docker CLI : Docker komut satırı ara yüzü.

Container ve Image : Bir sunucunun içerdiği tüm componentlerin bir şablonudur. Örnekle bir sunucu içerisinde bir işletim sistemi, bir uygulama ve bu uygulamayı çalıştırmak 
için bir jre var, image bunların hepsinin tutulduğu bir alandır fakat sunucudan tek farkı imageler içinde çekirdek yani kernel bulunmaz, containerın bulunduğu işletim 
sisteminin kernelini kullanır. Container ise bu imagenin çalışır halidir. Biz imageleri pull eder çalıştırarak container oluştururuz.

<img src="https://user-images.githubusercontent.com/54666839/162386304-e333d2b8-d115-4f2b-b811-900abbdb2b5b.png" width="425"/> 


Commands :
1.docker : Dockerı ait bütün komutları listeler. Options, Management Commands ve Commands adında 3 başlığı vardır. 
->Options altındaki komutlar docker deamon'a bağlanırken kullanabileceğimiz komutlar var.
->Management Commands altında docker komutlarını nerede çalıştıracağımızı söyleyen komutlar var, Örnekle, 2016 yılından önce dockerda bir iş yapmak istiyorsak mesela 
hello-world app'ini çalıştırmak istiyorsak docker run hello-world yazınca iş bitiyor container çalışıyordu, fakat 2016'dan sonra docker karmaşıklaşınca şöyle bi çözüm
getirdiler artık hello-world appini çalıştırmak istediğimizde -docker çalıştırmakİstediğimizAlan komut- yani docker container run hello-world sistemini getirdi, işte 
docker management commands altında bu container gibi çalışma alanlarımız mevcut.
->Commands dockera ait diğer tüm komutlar

<img src="https://user-images.githubusercontent.com/54666839/162386573-6379fcc4-f23f-478d-b0a9-b5dec0d4cbac.png" width="425"/> 

<img src="https://user-images.githubusercontent.com/54666839/162387597-b25c3157-45e8-4fa7-8693-01ba58619d1b.png" width="425"/> 


2.docker image --help , docker container --help : herhangi bir management commands yazdık ama devamında ne yapacağımızı unuttuk --help yazarak o management commandsta
hangi komutları kullanabileceğimizi görürüz.

2.docker version : Versiyon bilgilerini gösterir.

3.docker info : Aktif olarak kaç container çalışıyor,kaç image var gibi
