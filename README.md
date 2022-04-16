**Genel Notlar** :

ping -containerIsmi- : Çalışan bir containera ping atma, bu pingi durdukmak için ctrl + C yapmamız lazım

Herhangi bir containerı stop yada exit edip durdurmadan çıkmak istiyorsak ctrl P + ctrl Q basmalıyız(read escape sequence)

İşletim Sistemi : Donanımların(Monitor,Ram,Ekran Kartı vs) uygulamaları çalışmasına aracılık eden yazılım.

Kernel : Üstteki işi yapan en temel işletim sistemi parçası.

NOT: Pc'de işletim sistemi olmasada uygulama çalıştırabiliriz. Ama o çalıştıracağımız uygulamaların hangi donanımı kullanması gerektiğini kodlarla bilmesi gerekli

### Sanallaştırma (VM) : 
Öncelikle sunucunun çalışma mantığını kısaca hatırlayalım. Sunucuyu bir bilgisayar gibi düşün, ve bunun içine bir işletim sistemi
bu işletim sisteminin üzerine uygulama kurulurdu. Daha sonra bu sunucuya bağlanmak isteyenlere de uzaktan gerekli konfigürasyonlar yapılır, bağlanırdı.
2000 lerin başında IT şirketleri fiziksel sunucular kullanırlardı(BARE METAL), mesela 5 tane uygulamam var, 5 tane fiziksel sunucu satın alırlardı,Ve bu 5 uygulamayı 
bu sunuculara koyarlardı, Günümüzde ise sanallaştırma dediğimiz olay ile işler yürüyor sanallaştırma dediğimiz olay ise şudur. Bir sunucu içerisinde
5 tane işletim sistemi kuruyoruz ve bu işletim sistemlerine çalıştırmak istediğimiz 5 uygulamayı kuruyoruz. Artık eski zamanlardaki gibi sunucu sipariş et,
gelmesini bekle, kurulumunu yap gibi zaman ve maddi maliyetler ortadan kalkıyor.

### Docker :
Docker şudur, yukarıda sanallaştırma işini yapıyor fakat sanallaştırmada her bir işletim sistemi kendi temel işlerinide görmek için fazlaca alan ve çaba 
harcıyorlar, docker ise tek bir işletim sistemi üzerinde birden fazla sunucu çalıştırmamıza olanak sağlıyor ve 5 işletim sisteminin temel işleri için harcayacağı
eforları yerine artık tek bir işletim sistemi efor harcıyor.Ayrıca diyelim ki sanal makinanız içindeki uygulamayı başka bir yere taşımak istediniz bu çok yorucu 
ve zahmetli bir iştir.Fakat docker kullanırsanız, taşımak istediğiniz pc'de docker olması yeterlidir. Ayrıca containerlar VM'e göre çok daha hızlıdırlar.

<img src="https://user-images.githubusercontent.com/54666839/162386446-774bf897-d254-4a45-b277-ff3e301a16b4.png" width="625"/> 

Docker Engine 3 componentten oluşur :
- Docker Daemon : Volumes,İmage,Container,Network yaratmamızı ve yönetmemizi sağlar.
- Docker Rest API : Dockerın diğer uygulamalarla haberleşmesini sağlar.
- Docker CLI : Docker komut satırı ara yüzü.

### Container ve Image :
Bir sunucunun içerdiği tüm componentlerin bir şablonudur. Örnekle bir sunucu içerisinde bir işletim sistemi, bir uygulama ve bu uygulamayı çalıştırmak 
için bir jre var, image bunların hepsinin tutulduğu bir alandır fakat sunucudan tek farkı imageler içinde çekirdek yani kernel bulunmaz, containerın bulunduğu işletim 
sisteminin kernelini kullanır. Container ise bu imagenin çalışır halidir. Biz imageleri pull eder çalıştırarak container oluştururuz.

<img src="https://user-images.githubusercontent.com/54666839/162386304-e333d2b8-d115-4f2b-b811-900abbdb2b5b.png" width="625"/> 

### Docker Registry :
Docker imagelarının tutulduğu repository. En meşhuru ve en çok kullanılanı docker hub'tır. Docker dünyasının githubı olarak düşünebiliriz.

### Commands :
**docker** : Dockerı ait bütün komutları listeler. Options, Management Commands ve Commands adında 3 başlığı vardır. 
- Options altındaki komutlar docker deamon'a bağlanırken kullanabileceğimiz komutlar var.
- Management Commands altında docker komutlarını nerede çalıştıracağımızı söyleyen komutlar var, Örnekle, 2016 yılından önce dockerda bir iş yapmak istiyorsak mesela 
hello-world app'ini çalıştırmak istiyorsak docker run hello-world yazınca iş bitiyor container çalışıyordu, fakat 2016'dan sonra docker karmaşıklaşınca şöyle bi çözüm
getirdiler artık hello-world appini çalıştırmak istediğimizde -docker çalıştırmakİstediğimizAlan komut- yani docker container run hello-world sistemini getirdi, işte 
docker management commands altında bu container gibi çalışma alanlarımız mevcut.
- Commands dockera ait diğer tüm komutlar

<img src="https://user-images.githubusercontent.com/54666839/162386573-6379fcc4-f23f-478d-b0a9-b5dec0d4cbac.png" width="625"/> 

<img src="https://user-images.githubusercontent.com/54666839/162387597-b25c3157-45e8-4fa7-8693-01ba58619d1b.png" width="425"/> 


**docker image --help** , **docker container --help** : Herhangi bir management commands yazdık ama devamında ne yapacağımızı unuttuk --help yazarak o management commandsta hangi komutları kullanabileceğimizi görürüz. Yazacağımız herhangi bir komutun sonuna --help koymak o komutu nasıl kullancağımızı da anlatır.

**docker version** : Versiyon bilgilerini gösterir.

**docker info** : Aktif olarak kaç container çalışıyor,kaç image var gibi bilgileri gösteren komut

**docker container ls (docker ps'de aynı işi görüyor)** : Aktif olarak çalışan containerları gösterir.

**docker container ls -a (docker ps -a'da aynı işi görüyor)** : Aktif ve pasif tüm containerları gösterir.

**docker image ls** : Aktif olarak çalışan imageleri gösterir.

**docker image ls -a** : Aktif ve pasif tüm imageleri gösterir.

**docker container create -imageID or imageName-** : Belirtilen image'den container oluşturur fakat çalıştırmaz.

**docker container start -containerID or containerName-** : Belirtilen containerı çalıştırır.

**docker container stop -containerID or containerName-** : Belirtilen containerı durdurur.

**docker container run -imageID or imageName-** : Belirtilen image'den hem container oluşturur hem o containerı çalıştırır. Image localimizde yoksa bile docker registry'den(dockerHub) gider alır.

**docker container run --rm -imageID or imageName-** : Belirtilen image'den hem container oluşturur hem o containerı çalıştırır fakat container durduğu anda containera siler.

**docker container rm -containerID or containerName-** : Belirtilen containerı siler. (Containerlar UP durumda silinmez!).
**docker image rm -imageID or imageName-**

**docker container rm -f -containerID or containerName-** : Belirtilen containerı silmeye zorlar. Kesin sileceğimiz containerlar silerken sıkıntı çıkartırsa bunu kullanabiliriz.
**docker image rm -f -imageID or imageName-**

**attach mode , detach mode** : Containerı başlatırken, o cantainerın arkada planda mı yoksa bizim localimizde mi çalışacağını belirtiriz. Eğer Detach mode ile kullanırsak **docker run -d imageID** şeklinde komut yazmamız lazım ve localimizdeki cmd yine bize aittir, çalıştırdığımız containera gitmez. Fakat bu -d yi yazmasaydık attach mode ile devam etmiş olurduk ve cmd de yazacağımız komutlar containerımızın komutları olurdu.

**docker container exec -it -containerID or containerName- -sh/bash/powershell-** : Bu exec komutu ile "detach modda" çalıştırdığımız("çalışan containera") yani arka planda çalıştırdığımız yani komut satırına ulaşamadığımız containerın komut satırına ulaşmak için kullanıyoruz. Burada exec komutu bize bu işlemi yaptırıyor ve komutun sonundaki sh/bash/powerhell kısmı ise o containerın kurulu olduğu işletim sisteminin komut satırına ulaşmak için yazdığımız kod.(sh:alphine, bash:ubuntu) Örnek: Diyelim ki localimizdeki işletim sistemi Windows ve containarın içerisinde ubuntu var, O zaman o containerı exec yani execute ettikten sonra artık ubuntu komutlarını yazmalıyız.Buradaki --it aslında --interactive --tty komutlarının birleşimi ve belirtilen container ile bir terminal bağlantısı kur demek. 

**NOT** : exit ile stop arasındaki fark, exit ile çalışan container içindeyken o containerdan çıkarız ve kendi komut satırımıza döneriz ama container çalışmaya devam eder, stop ile containerın çalışmasını durdururuz.

**docker container prune** : Çalışmayan* bütün containerları siler, Silmeden onay ister.

**docker image prune -a** : Bütün imageleri siler, Silmeden onay ister.


### Volume :
Varsayalım ki aynı imageden 3 tane container oluşturduk ve içerisinde farklı farklı işlemler yaptık, günün sonunda o işlemler hiç bir zaman birbirine karışmaz. Her bir containerın içerisinde yaptığımız işlemler o containera özel olur. Fakat bazı durumlar vardır ki biz o containerda yaptığımız işlemleri,değişiklikleri başka containerda da görebilelim. Bunu git teki dev branchine benzetebilirsin. İşte Volumeler aslında dev branchi oluyor, biz devden branch koparır localimizde değişiklik yaparız daha sonra merge edilince değişikliğimiz dev'de görülürüz. Volumelerinde mantığı aslında budur.

docker volume --help diyerek bir çok şeyi inceleyebilirsin.

**docker volume create -volumeName-** : Yeni bir volume oluşturma.

ls, rm, prune ve inspect gibi image ile containerlardaki aynı komutları volumeler içinde kullanabiliriz.

<img src="https://user-images.githubusercontent.com/54666839/162627720-637e60e9-d203-4def-ac5f-22546e04226c.png" width="925"/> 

docker run -it -v ilkVolume:/App:ro centos sh : Buradaki "ro" Read only demek, bu container içerisinde gezinebiliriz ama değişiklik yapamayız.



**Bind Mounts** : Bilgisayarımızdaki herhangi bir dosyayı,klasörü vs. container içerisine atmaya denir.
Üstteki görseldeki gibi bind mounts yapabiliriz tek fark volume adının yerine localimizdeki bağlamak istediğimiz klasörü yazıyoruz.

--> **docker container run -d -p 80:80 -v C:\Users\samet.cavur\Desktop\deneme:/usr/share/nginx/html/ nginx**


### Docker Networks :
Bu konunun mantığı şöyledir. Diyelim ki birden fazla containerımız var yada containerımızı third party bir container ile haberleştireceğiz işte bu Docker Network türleri ile containerların birbirleriyle haberleşmesini sağlıyoruz. Docker engine kurulu makinada bridge,host ve none network objeleri otomatik kurulur.
Network Türleri:
- **Bridge** : Adından da anlaşılacağı üzere iki container arasında köprü kurar ve haberleşmelerini sağlar. Eğer bir containerı network tanımlaması yapmaz isek bu network türünü default olarak kullanır.
- **Host** : Bridge gibi iki container arasında köprü kurmak yerine belli bir host belirler ve tüm containerları o hosta bağlar.
- **Macvlan** : Bu network ile oluşturulan ağ objelerine bağlı containerlara bir mac adresi atar ve containerları fiziksel bir cihaz gibi görür. (MAC Adresi : Bir bilgisayar ağında, bir cihazın ağ donanımını tanımaya yarar)
- **None** : Bu network türünce containerın herhangi bir ağ bağlantısı networkü olmadığı varsayılır.
- **Overlay** : Kümeleme gibi düşünebiliriz. Haberleşmesini istediğimiz containerları bir küme haline getiriyoruz ve hepsinin tek bir ağ bağlantısı olduğunu varsayıyoruz.

**docker network inspect -none,bridge,host-** : Bu komut ile belirtilen networkün tüm özelliklerini görebiliriz. Bu networke bağlı containerları da aynı zamanda görebiliriz.

Docker bize default olarak bridge networkü verse de zaman zaman kendi customer bridge networklerimizi yaratmak isteyebiliriz. Onu da şöyle yaparız:

**docker network create --driver=host deneme2** : deneme2 adında host networkü  yaratma(fakat local makine yalnızca 1 tane host networke izin verir)

**docker network create customerBridge** : Default olarak tanımlanan networkten(Bridgeden) customerBridge adında bir network yarat.

**Örnek**

* 2 tane container yaratacağız ve aynı network üzerinde tanımlayarak birbirleriyle haberleşmelerini sağlayacağız. 

1. Öncelikle network yaratalım : 
-> docker network create kopru1
2. 2 tane container yaratalım ve networklerinin kopru1 olduğunu tanımlayalım : 
-> docker container run -d -it --name cont1 --net kopru1 sametcavur/image
-> docker container run -d -it --name cont2 --net kopru1 sametcavur/image
3. Herhangi bir containera girelim ve diğerine ping atalım.
-> docker container exec -it cont2 sh
-> ping con1
4. Burada artık cont2 nin cont1 e ping attığını göreceğiz.Pingi durdurmak için ctrl+C bas, Containerı durdumadan containerdan çıkmak için ctrl+P+Q bas.

**Not** : Eğer 2 tane containerı aynı network üzerinde yaratmazsak birbirlerine container isimleri ile ping atamazlar, containerlara inspect ile girip ip adreslerini almamız lazım, ip adresleri üzerinden ping atabiliriz.

**NOT** : Subneti,Gateway,İprange i de custom olsun diyorsak alttaki gibi daha da özel networkler yaratabiliriz.
 
docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 CustomKopru

**NOT** : Default bridge yerine custom bridge kullanmak daha iyidir. Çünkü default bridge network altında tanımlanmış çalışan bir containerın bağlantısını kesemez yada başka networke bağlayamazsınız. Fakat custom oluşturuluşmuş bridge network altındaki containerın bağlantısını kesip birden fazla networke bağlayabilirsiniz. Bu işlemide şöyle bir komut satırı ile yapabilirsin.

docker network connect -networkIsmi- -container- : Bu containerı bu networke bağla demek.

docker network disconnect -networkIsmi- -container- : Bu contarinerın bu network ile bağlantısını kes demek.

**NOT** : Bir network rm ile sileceğimiz zaman altında hiç bir container olmamalı.


** **
**Port Publish** : Bu konuyu şöyle açıklayabiliriz. Üstteki networks konusunda gördüğümüz host network'ü kullanarak containerların haberleşmesini sağladığımızı varsayalım. Fakat Bu containerlara third party bir erişim olmasını istediğimizde bizim bu containerlarını out'a publish etmiş olmamız lazım. Bunu ise şöyle yapıyoruz.

-p yada --publish komutlarını kullanıyoruz.

Örnek : docker container run -d -p 8080:80 -imagemiz-   --> İşte buradaki [-p 8080:80] port publish etme işlemi oluyor ve ilk 8080 yazdığımız host portumuz ikinci yazdığımız 80 ise container portumuz.

NOT: Tek komutta birden fazla port publish edilebilir.














