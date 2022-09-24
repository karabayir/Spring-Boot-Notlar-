# Spring-Boot-Notlar



 
PAKET YAPISI

controller: api'ların bulunduğu paket yapısı. (Gelen istekleri kontrol et. Aşağı tarafdaki katmanları boşuna yorma , isteklerde hata varsa hemen geriye dön devam etme)

dto       : Controller aracılığıyla göndereceğimiz modellerin ve nesnelerin bulunduğu katman.

exception : Projedeki hataları yakalayıp açıklayan kodların bulunduğu katman.

model     : Entity ve yardımcı ek nesnelerin bulunduğu katman.

repository: Modelleri veritabanına aktaran , veritabanından veriyi alıp modellere çeviren katman.

service   : Controller'dan isteği alıp diğer dış servislerle ilişki kurar ve repository katmanına veriyi iletir ya da repository katmanından veriyi çeken katman.

------------------------------------------------

 DESIGN PATTERN

  FACADE

  Serivice katmanı kenidi Repository'si ile konuşur.
  A Service -> A Repository -> A Model
  A service yalnızca kendisine hizmet eden Repository ile konuşabilir. ( A Repository ).
  
  A Service B Repository ile doğrudan konuşamaz.
  A Service -> B Repository -> B Model ( YANLIŞ )
  A Service -> B Service -> B Repository -> B Model ( DOĞRU )
 
-------------------------------------------------
 MODEL SINIFLARI
 
  Kotlin Data Class kullanıldı.
  
- EqualsAndHashCode içerir.

- toString içerir.

- immutability data oluşturabilme içerir.

- * getter setter gibi metodlarla uğraşmama içerir.

-------------------------------------------------
 LIST - SET FARKI

 - List yapısında aynı nesne bir çok defa eklenebilir.
  
 - Set yapısında aynı nesneden bir ikincisi daha olmaz. Her nesne farklı olur .

-------------------------------------------------
 Model Sınıflarda Neden Equals ve Hash override edildi ?

-> Hash sayesinde model , hash algoritması ile primitive int değer olarak veri tablosunda tutulur.

-> Set<> yapısı kullandığımız için hash override yaptık.

-> Transaction hash kodu içinde Account tutarsak Account içinde de Transaction olduğu için birbirleini döngüye sokarlar.

-------------------------------------------------
 Neden DTO ?

-Model sınıfları içinde istemediğim yerleri almayabilirim ya da o model sınıfında olmayan bir şey ekleyebilirim.

-DTO , API response'larımıza daha esnek davranabilmemizi ve daha kontrolü elde tutmamızı sağlar.

-DTO kullanımının mutlaka olması önerilir.

- Esneklik , ileriye yönelik açıklık sağlar.
-------------------------------------------------
Neden Protected Kullandık?

->Servisler arasındaki veri transferlerinde Entity kullanılabilir / Entity can use for data transfer where between services.

 -Ancak metodların protected olması önemlidir / But all methods (in service) should have protected method.
 
 -Sadece servislerin kullanabileceği metod olması için protected yapılır. / Using protected because  method only can use by services.

-------------------------------------------------
  Neden Logger Kullandık ?

- Hata durumlarını yazılımcıya bildirme amaçlı yazılır.

- System.out.println(); ile göreceğimden daha fazlasını detaylıca verir.

- Bu sayede herhangi bir hata veya bilgi mesajının nereden üretildiğini Log'a bakarak bulabiliyorum.
--------------------------------------------------
  PathVariable ile RequestBody Farkı Nedir ?

 - PatVariable bilgiyi URL'den alır.
 
 - RequestBody bilgiyi JSON'dan alır.
--------------------------------------------------
 Optional ve Stream Özellikleri

- Optional if-else yapısından kurtarır.
- Stream for döngüsünden kurtarır.
--------------------------------------------------

## @Service  @Component Farkı Nedir ?

-Bulunduğum sınıftan başka bir katmana erişmek istersem @Service (Başka katmanlara gider) Başka bir katmandan bulunduğum sınıfa erişmek için @Component (Katmanlardan buraya gelir) 

-@Componet , @Service gibi inject edilebilir. @Service ile aynı özellikleri taşır.

--------------------------------------------------

### CI ( Continuous Integration )

Birden fazla kişinin ya da aynı kişinin yapmış olduğu geliştirmeleri bir yerde kayıt altında tutmasıdır (github ,gitlab , bitbucket).

### CD ( Continuous Deployment )

Geliştirmeler paket haline getirilip belli süreçler sonucunda kullanıma sunulmasıdır.
