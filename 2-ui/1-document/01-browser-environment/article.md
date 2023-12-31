# Tarayıcı Ortamı, Özellikleri

Javascript dili başlangıçta internet tarayıcıları için oluşturuldu. O zamandan beri geliştirildi ve birçok kullanımı ve platformu ile bir dil haline geldi.


Bir platform tarayıcı, bir web sunucusu, bir çamaşır makinesi veya başka bir sunucu olabilir. Bunların her biri platforma özgü fonksiyonlar sağlar. JavaScript özelliklerinde bunu bir sunucu ortamı olarak adlandırılır.

Bir sunucu ortamı dil çekirdeğine ek olarak platforma özgü nesneler ve fonksiyonlar sağlar. İnternet tarayıcıları internet sayfalarını kontrol etmek için bir yol sunar. Node.js sunucu tarafı özellikleri vb. 


İşte javascriptin internet tarayıcısında çalıştığında elimizde ne olduğunu gösteren bir kuş bakışı.

![](windowObjects.png)

`window` denilen bir "kök" nesnesi var. İki rolü vardır.

1. Birincisi, Javascript kodu için evrensel bir nesnedir. bölümde açıklandığı gibi info:global-object
2. İkincisi, "tarayıcı penceresini" temsil eder ve kontrol etmek için yöntemler sağlar. 

Örneğin, burada `window`u evrensel bir nesne olarak kullandık.

```js run
function selamSoyle() {
  alert("Selam");
}

// evrensel değişkenler `window` özellikleri olarak erişilebilir.
window.selamSoyle();
```

Ve burada `window`u pencerenin yüksekliğini görmek için tarayıcı penceresi olarak kullandık: 

```js run
alert(window.innerHeight); // İç pencere yüksekliği
```

Daha fazla `window`a özgü yöntemler ve özellikler var, bunlardan daha sonra bahsedeceğiz.

## Document Object Model (DOM) (Belge Nesneli Modeli)

`document` nesnesi sayfa içeriğine erişimi sağlar. Sayfada herhangi bir şeyi değiştirebilir ya da oluşturabiliriz.

Örneğin:
```js run
// arka plan rengini kırmızı olarak değiştirelim.
document.body.style.background = 'red';

// 1 saniye sonra tekrar değiştirelim
setTimeout(() => document.body.style.background = '', 1000);
```

Burada `document.body.style` kullandık fakat daha fazla parametreler var. Özellikleri ve yöntemleri tanımlamada açıklanmıştır. Tesadüf ki, bunu geliştiren iki grup vardır. 

DOM standartları : <https://dom.spec.whatwg.org>

Eskiden hiçbir standart yoktu. -- her tarayıcı her ne istiyorsa onu uyguladı. Bu yüzden farklı tarayıcıların aynı şeyler için farklı metotları ve özellikleri vardı. Geliştiriciler her bir tarayıcı için farklı kodlar yazmak zorunda kalıyordu. Karanlık dağınık zamanlar.

Şimdi bile bazen tarayıcılara özgü özellikleri kullanan ve uyumsuzluklar etrafında çalışan eski kodlarla çalışabiliriz ama bu derste modern şeyler kullanacağız: Onlara ihtiyacın olana kadar eski şeyler öğrenmeye gerek yok (şansın yüksek değil). 

Daha sonra herkesi ortak noktada toplamak için DOM standartı belirlendi. İlk versiyon "DOM Level 1" idi, sonra DOM Level 2 tarafından genişletildi, sonra DOM Level 3 ve şimdi DOM Level 4. WhatWG grubundan insanlar sürümden sıkıldılar ve numara olmadan sadece DOM olarak adlandırdılar. Öyleyse biz yapacağız.

```smart header="DOM yalnızca tarayıcı için değildir."
DOM özelliği bir belgenin yapısını açıklar ve onu işlemek için nesne sağlar. Onu kullanan tarayıcı olmayan araçlarda var.

Örneğin, HTML sayfalarını indiren ve işleyen sunucu-taraflı araçlar. Ancak DOM özellikleri sadece bir bölümü destekleyebilir.
```

```smart header="Stil için CSSOM"
CSS kuralları ve stil sayfaları HTML yapısına benzemez. Bu yüzden nesneler olarak nasıl temsil edildiklerini ve nasıl okunup yazılacağını açıklayan bir tanımlama vardır. [CSSOM](https://www.w3.org/TR/cssom-1/)

CSSOM, belgi için stil kurallarını değiştirdiğimizde DOM ile birlikte kullanılıyor. Pratikte olsa CSSOM nadiren gereklidir. Çünkü genelde CSS kuralları statiktir. Javascript'e CSS kuralları ekleme/çıkarma nadiren ihtiyacımız var. Bu yüzden onu kapatmayız.
```

## BOM (Tarayıcı Nesne Modeli) 

HTML'in bir parçası (BOM), belge dışında her şey ile çalışmak için tarayıcı (sunucu ortamı) tarafından sağlanan ek nesnelerdir.

Örneğin:

- [navigator](mdn:api/Window/navigator) nesnesi tarayıcı ve işletim sistemi hakkında arkaplan bilgisi sağlar. Birçok özelliği var, fakat en çok bilinen ikisi şunlardır: `navigator.userAgent` -- mevcut tarayıcı hakkında, ve `navigator.platform` -- platform hakkında (Windows/Linux/Mac arasında farklılık olacağından yardım gerekebilir). 
- [location](mdn:api/Window/location) nesnesi geçerli adresi okumayı ve tarayıcıyı yenisine yönlendirmeyi sağlar

`location` nesnesini bu şekilde kullanabiliriz: 

```js run
alert(location.href); // Geçerli URL'yi gösterir
if (confirm("wikipedia'ya git?")) {
  location.href = 'https://tr.wikipedia.org'; // Tarayıcı başka bir URL'ye yönlendirir.
}
```

`alert/confirm/prompt` fonksiyonları da BOM'un bir parçasıdır: Bunlar doğrudan belge ile ilgili değildir ancak kullanıcı ile tarayıcının saf iletişim kurmasını temsil eder. 

```smart header="HTML specification"
BOM genel kısmıdır[HTML specification](https://html.spec.whatwg.org).

Evet, doğru duydun. <https://html.spec.whatwg.org>'deki HTML özelliği yalnızca "HTML dili" (etiketler, nitelikler) ile ilgili değil, aynı zamanda birçok nesne, yöntem ve tarayıca özgü DOM uzantılarını da kapsar. Bu "geniş anlamda HTML"dir.
```

## Özet

Standar hakkında konuşurken:

DOM tanımlaması
: belge yapısını, manipülasyonları, olayları açıklar, Bkz <https://dom.spec.whatwg.org>.

CSSOM tanımlaması
: stil sayfaları ve stil kurallarını açıklar, bunlarla yapılan manipülasyonları ve belge bağlanmalarını sağlar, Bkz <https://www.w3.org/TR/cssom-1/>.

HTML tanımlaması
: HTML dilini (etiketler vs.) ve ayrıca BOM (tarayıcı nesne modeli) -- çeşitli tarayıcı fonksiyonlar: `setTimeout`, `alert`, `location` vb açıklar, Bkz <https://html.spec.whatwg.org>. DOM özelliğini alır ve birçok ek özellik ve yöntemle geliştirir.

Lütfen yukarıdaki bağlantıları kontrol edin. Çünkü öğrenecek birçok şey var. Her şeyi hatırlamak imkansızdır.

Bir özellik ve yöntem hakkında okumak istediğinizde -- Mozilla kılavuzu <https://developer.mozilla.org/en-US/search> güzel kılavuzlardan bir tanesidir, ancak ilgili özelliklerin okunması daha iyi olabilir: daha karmaşık ve okunması uzun fakat temel bilginiz eksiksiz ve sağlam hale gelecektir.

Şimdi DOM öğrenmeye başlayacağız. Çünkü belge, kullanıcı arayüzünde önemli bir rol oynuyor, ayrıca onunla çalışmak en karmaşık kısımdır.
