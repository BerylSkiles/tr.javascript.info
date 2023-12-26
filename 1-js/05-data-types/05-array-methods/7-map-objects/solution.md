
```js run no-beautify
let ahmet = { adi: "Ahmet", soyadi: "Doğtaş", id: 1 };
let mehmet = { adi: "Mehmet", soyadi: "İstikbal", id: 2 };
let muzaffer = { adi: "Muzaffer", soyadi: "Bellona", id: 3 };

let kullanicilar = [ ahmet, mehmet, muzaffer ];

*!*
let kullaniciMapped = kullanicilar.map(kullanici => ({
  adi_soyadi: `${kullanici.adi} ${kullanici.soyadi}`,
  id: kullanici.id
}));
*/!*

/*
kullaniciMapped = [
  { adi_soyadi: "Ahmet Doğtaş", id: 1 },
  { adi_soyadi: "Mehmet İstikbal", id: 2 },
  { adi_soyadi: "Muzaffer Bellona", id: 3 }
]
*/

alert( kullaniciMapped[0].id ) // 1
alert( kullaniciMapped[0].adi_soyadi ) // Ahmet Doğtaş
```
Dikkat ederseniz ok fonksiyonunda süslü parantez kullanmamız gerekti.

Aşağıdaki gibi yazılamaz:
```js
let kullaniciMapped = kullanicilar.map(kullanici => *!*{*/!*
  adi_soyadi: `${kullanici.adi} ${kullanici.soyadi}`,
  id: kullanici.id
});
```

Hatırlayacağınız üzere iki türlü ok fonksiyonu bulunmaktadır: Gövdesi olmadan `deger => ifade` veya gövdeli `deger => {...}`

Bizim kullandığımız şekliyle JavaScript `{`'i fonksiyon başlangıcı olarak kabul etmektedir. Objenin başlangıcı değil. Halbuki biz obje olmasını istiyoruz. Bu durumda bunları "normal" parantez içine almamız gerekmekte.

```js
let kullaniciMapped = kullanicilar.map(kullanici => *!*({*/!*
  adi_soyadi: `${kullanici.adi} ${kullanici.soyadi}`,
  id: kullanici.id
}));
```

Şimdi çalışır.


