---
titulo: Desarrollo de Interfaces
autor: gn6ks
creado: 10-09-2025
profesor/a: mviel@florida-uni.es
---

Funciones de tipo Flecha '=>', como si fuera un F(x).
```javascriptconst 
const array = [1, 2, 3, 4];
const sumadosArr = [];
const suma = (elem) => elem + 1;

const maxElement = (a, b, c) => Math.max(a, b, c)

function recorrer(arr) {
  for (let i = 0; i < arr.length; i++) {
    sumadosArr[i] = suma(arr[i]);
  }
  console.log(sumadosArr);
}

recorrer(array);


console.log(maxElement(-9, 90, 2));

const saluda = () => console.log("hola");
saluda();
```
