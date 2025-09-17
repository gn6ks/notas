---
titulo: Desarrollo de Interfaces
autor: gn6ks
creado: 10-09-2025
profesor/a: mviel@florida-uni.es
---

## Javascript

### Funciones de tipo flecha (arrow functions)

Funciones de tipo Flecha '=>', como si fuera un F(x).

```javascript
const array = [1, 2, 3, 4];
const sumadosArr = [];
const suma = (elem) => elem + 1;

const maxElement = (a, b, c) => Math.max(a, b, c);

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

#### Metodos javascript para arrays

El metódo `.map()` sirve para crear un array en el que los componentes se han modificado o transformado.
Sintaxis básica:

```javascript
array.map(function(elemento, indice, array)) {
  //funciones para cada elemento
});
```

Los parametros que devuelven el `.map()` siempre es un array

```javascript
const nums = [10, 9, 7];
const numerosMult = nums.map((elem) => elem * 2);
console.log(numerosMult);

const nums = [5, 10, 15];
const divididos = nums.map((elem) => elem / 5);
console.log(divididos);

const noms = ["Anna", "Joan", "Maria"];
const addExcl = noms.map((elem) => elem + "!");
console.log(addExcl);

const nums2 = [2, 4, 6, 8];
const cuadrados = nums2.map((elem) => elem * elem);
console.log(cuadrados);
```

El metódo `.filter()`se utiliza para seleccionar elementos dentro de un array que cumplen unos requisitos.
Sintaxis básica:

```javascript
array.filter(function(elemento, indice, array)) {
  //retornar condicion;
});
```

Ejemplos de funcionamiento de `.filter()`

```javascript
const numeros = [2, 7, 4, 10];
const imparesPos = numeros.filter((elem, indice) => indice % 2 === 1);
console.log(imparesPos);
```

El metódo `.forEach()` se utiliza para recorrere cada elemento de un array y ejecutar una función con cada uno, no devuelve un array nuevo.
Sintaxis básica: 

```javascript
array.forEach((elemento, indice, array)) {
  //instrucciones
});
```
