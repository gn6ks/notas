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

const nums = [1, 2, 3, 4, 5, 6];
const nPares = (nums) => (nums.filter(elem => elem % 2 === 0));
console.log(nPares(nums));

const words = ["sol", "pluja", "mar"];
const words3 = (words) => (words.filter(elem => elem.length > 3));
console.log(words3(words));
```

El metódo `.forEach()` se utiliza para recorrere cada elemento de un array y ejecutar una función con cada uno, no devuelve un array nuevo.
Sintaxis básica:

```javascript
array.forEach((elemento, indice, array)) {
  //instrucciones
});
```

El método `.reduce()` se utiliza para reducir todo un array a un solo valor, por ejemplo para sumar, restar o inclusive concatenar.
Sintaxis básica:

```javascript
array.reduce(function (accumulador, element, index, array) {
  return novaCosa;
}, valorInicial);
```

Ejemplo en uso:

```javascript
const numeros = [1, 2, 3, 4];
const suma = numeros.reduce((acc, num) => acc + num, 0);
console.log(suma); // 10

const nums2 = [2, 3, 4];
const numsMult = nums2.reduce((accum, elem) => accum * elem, 1);
console.log(numsMult);

const palabras = ["hola", "mon"];
const palabrasJuntas = palabras.reduce((accum, elem) => accum + elem, "");
console.log(palabrasJuntas);
```

Ejercicios Clase 18-09-2025, Reduce, Filter, Map:

```javascript
//A partir d'un array de numeros, mostra la suma de tots ells
let array1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const array1Sumado = (array1) => (array1.reduce((accum , elem) => accum + elem, 0));
console.log(array1Sumado(array1));
//45

//A partir d'un array d'strings i numeros, mostra un string que els continga tots
let array2 = ['a', 1, 'b', 2, 'c', 3];
const array2Concat = (array2) => (array2.reduce((accum, elem) => accum + elem, ""));
console.log(array2Concat(array2));
// a1b2c3

// A partir d'un array de dies, em torne un OBJECTE amb tants atributs com dies i la posició de cada dia
// És a dir per a l'array ['dilluns', 'dimarts', 'dimecres'] 
// torne un objecte {dilluns:0, dimarts:1, dimecres:2}
let dies = ['dilluns', 'dimarts', 'dimecres'];
const diesPos = dies.reduce((accum, elem, indice) => {
    accum[elem] = indice;
    return accum;
}, {});
console.log(diesPos);


//A partir d'un array amb objectes Musics (nom i instrument que toca)
//Que torne un array amb els noms de tots els components
// [ 'Joan', 'Pep', 'Vicent Lloret', 'Ariadna', 'Guillem' ]
let musics = [
    {'nom': 'Joan', 'instrument': 'vocal'},
    {'nom': 'Pep', 'instrument': 'guitarra'},
    {'nom': 'Vicent Lloret', 'instrument': 'guitarra'},
    {'nom': 'Ariadna', 'instrument': 'bateria'},
    {'nom': 'Guillem', 'instrument': 'baix'}
]
const nomsMusics = (musics) => (musics.reduce((arryMuscis, musico) => {
    arryMuscis.push(musico.nom);
    return arryMuscis;
}, []));
console.log(nomsMusics(musics));

//Ara feu-ho utilitzant map()
console.log(musics.map((music) => music.nom));

//Ara que torne un array només amb els noms del musics que toquen la guitarra
//['Pep', 'Vicent Lloret']
const filtradosGui = musics.filter((music) => music.instrument === "guitarra");
const nombresFilt = filtradosGui.map((music) => music.nom);
console.log(nombresFilt);

//Amb reduce
//['Pep', 'Vicent Lloret']
const nomsMusicsGui = (musics) => (musics.reduce((arryMuscis, musico) => {
    if (musico.instrument === "guitarra") {
        arryMuscis.push(musico.nom);
    }
    return arryMuscis;
}, []));
console.log(nomsMusicsGui(musics));
```