importance: 4

---

# Filtreleme ve yeni dizi dönme

`filterRange(arr, a, b)` adında bir fonksiyon yazın. `arr` argümanı alsın, `a` ile `b` arasını alsın ve döndersin.

Fonksiyon diziyi modifiye etmemeli. Yeni bir dizi döndürmeli.

Örneğin:

```js
let arr = [5, 3, 8, 1];

let filtered = filterRange(arr, 1, 4); 

alert( filtered ); // 3,1 (eşleşen değerler)

alert( arr ); // 5,3,8,1 (modifiye edilmedi)
```