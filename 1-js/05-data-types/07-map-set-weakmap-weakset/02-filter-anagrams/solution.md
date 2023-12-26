Tüm anagramları bulmak için öncelikle kelimeleri harflerine ayırıp sonrasında sıralamak gerekmektedir.

Örneğin:

```
aks, ask, kas, sak
alim, amil, ilam, imal, imla, mail, mali 
açlık, akçıl, çakıl, çalık, çalkı, kaçlı, kalıç, lakç
...
```
Harf sıralı tipler map anahtarları olacak şekilde kaydedilir.

```js run
function atemiz(dizi) {
  let map = new Map();

  for(let word of dizi) {
    // kelimeyi harflere ayır, sonrasında birleştir.
*!*
    let sorted = word.toLowerCase().split('').sort().join(''); // (*)
*/!*
    map.set(sorted, word);
  }

  return Array.from(map.values());
}

let arr = ["aks", "alim", "açlık", "ask", "ilam", "çalık"];

alert( atemiz(arr) );
```

Harflerin sıralanması `(*)`'da gösterilen zincirleme çağrılar ile yapılır.

Daha kolay anlaşılabilmesi için bunu satırlara ayıralım:

```js
let sorted = arr[i] // AKS
  .toLowerCase() // aks
  .split('') // ['a','k','s']
  .sort() // ['a','k','s']
  .join(''); // aks
```
İki farklı kelime `'AKS'` ve `'ASK'` sıralandığında ikisi de `'AKS'` olmaktadır.

Bir sonraki satır bu kelimeleri map'e eklemeye yarar:

```js
map.set(sorted, word);
```
Eğer aynı karakterlere sahip kelime ile tekrar karşılaşılırsa, map olduğundan dolayı bir öncekinin üzerine yazılacaktır. Bundan dolayı her zaman bir karakter-form'u için maksimum bir tane kelimeye sahip olacağız.

Sonunda `Array.from(map.values())` bu map değerleri üzerinden döngü yapılmasını sağlar.

Burada `Map` yerine normal obje de kullanılabilirdi. Çünkü anahtarlar karakter dizisi olacak.

Bu durumda çözüm şu şekilde olabilir:

```js run
function atemiz(dizi) {
  let obj = {};

  for (let i = 0; i < dizi.length; i++) {
    let sorted = dizi[i].toLowerCase().split("").sort().join("");
    obj[sorted] = dizi[i];
  }

  return Array.from(Object.values(obj));
}

let arr = ["aks", "alim", "açlık", "ask", "ilam", "çalık"];

alert( atemiz(arr) );
```
