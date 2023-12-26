# Döngü-tabanlı Çözüm

Döngü tabanlı çözüm aşağıdaki gibidir:

```js run
let list = {
  deger: 1,
  sonraki: {
    deger: 2,
    sonraki: {
      deger: 3,
      sonraki: {
        deger: 4,
        sonraki: null
      }
    }
  }
};

function listeYaz(list) {
  let tmp = list;

  while (tmp) {
    alert(tmp.deger);
    tmp = tmp.sonraki;
  }

}

listeYaz(list);
```
Dikkat ederseniz `tmp` adında geçici bir değişken tutarak listeni üzerinden geçildi. Bunun yerine `list` fonksiyon parametresi de kullanılabilir:

```js
function listeYaz(list) {

  while(*!*list*/!*) {
    alert(list.deger);
    list = list.sonraki;
  }

}
```
... Fakat çok akıllıca bir yöntem değil. İleride fonksiyonu genişletmek gerekebilir. Liste ile bir şeyler yapmak gerekebilir. Eğer `list` değişirse bu gerekliliklerin hiçbiri yerine getirilemez.

Değişken isimlerinden konuşmak gerekirse `list` burada liste'nin kendisidir, `ilk` elemanıdır ve öyle kalmalıdır. Temiz ve güvenilir.

Diğer taraftan `tmp` liste için aynı `i`'nin `for` için gerekliliği gibidir.

# Öz çağrı çözümü

`listeYaz(list)`'in öz çağrı çözümü şu mantığa dayanır: Liste'nin çıktısını almak için o anki `list` elemanının çıktısı basılmalıdır. Sonra diğer `list.sonraki` elemanlarının yapılmalıdır.

```js run
let list = {
  deger: 1,
  sonraki: {
    deger: 2,
    sonraki: {
      deger: 3,
      sonraki: {
        deger: 4,
        sonraki: null
      }
    }
  }
};

function listeYaz(list) {

  alert(list.deger); // elemanın çıktısını bas

  if (list.sonraki) {
    listeYaz(list.sonraki); // listenin geri kalan elemanları için de aynısını yap
  }

}

listeYaz(list);
```

Hangisi daha iyi?

Teknik olarak döngü versiyonu daha etkilidir. İki yöntem de aynı işi yapar, fakat döngü versiyonu iç içe fonksiyonlar için kaynak harcamaz.

Diğer taraftan özçağrı versiyonu daha kısa ve bazen anlaşılması daha kolaydır.
