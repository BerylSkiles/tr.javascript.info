Bugün geçen zamanı alabilmek için bugünün 00:00:00'ı için bir `tarih` objesi oluşturup bunu `şimdi`'nin `tarih` objesinden çıkarabilirsiniz. 

Bunun sonucu milisaniye cinsinden olacaktır, bundan dolayı dönen değeri 1000'e bölerseniz saniye alırsınız:

```js run
function bugundenSaniye() {
  let simdi = new Date();

 // o anki gün/ay/yıl'ı kullanarak yeni bir tarih objesi oluşturur.
 let bugun = new Date(simdi.getFullYear(), simdi.getMonth(), simdi.getDate());

  let fark = simdi - bugun; // ms cinsinden
  return Math.round(fark / 1000); // saniyeye çevrildi
}

alert( bugundenSaniye() );
```
Bunun alternatifi, saat/dakika/saniye gibi bilgilerin saniyeye çevrilmesidir:

```js run
function bugundenSaniye() {
  let d = new Date();
  return d.getHours() * 3600 + d.getMinutes() * 60 + d.getSeconds();
};
```
