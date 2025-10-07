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
};
```

Ejemplos de funcionamiento de `.filter()`

```javascript
const numeros = [2, 7, 4, 10];
const imparesPos = numeros.filter((elem, indice) => indice % 2 === 1);
console.log(imparesPos);

const nums = [1, 2, 3, 4, 5, 6];
const nPares = (nums) => nums.filter((elem) => elem % 2 === 0);
console.log(nPares(nums));

const words = ["sol", "pluja", "mar"];
const words3 = (words) => words.filter((elem) => elem.length > 3);
console.log(words3(words));
```

El metódo `.forEach()` se utiliza para recorrere cada elemento de un array y ejecutar una función con cada uno, no devuelve un array nuevo.
Sintaxis básica:

```javascript
array.forEach((elemento, indice, array)) {
  //instrucciones
};
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
//se hace una constante para guardar los elementos acumulados, el acumulador = 0, se va sumando elemento a elemento
const array1Sumado = (array1) =>
  array1.reduce((accum, elem) => accum + elem, 0);
console.log(array1Sumado(array1));
//45

//A partir d'un array d'strings i numeros, mostra un string que els continga tots
let array2 = ["a", 1, "b", 2, "c", 3];
//para poder concatenar loos elementos, se les pide que se sumen, pero no acumulados en un numero, sino con el elemento '' vacio
const array2Concat = (array2) =>
  array2.reduce((accum, elem) => accum + elem, "");
console.log(array2Concat(array2));
// a1b2c3

// A partir d'un array de dies, em torne un OBJECTE amb tants atributs com dies i la posició de cada dia
// És a dir per a l'array ['dilluns', 'dimarts', 'dimecres']
// torne un objecte {dilluns:0, dimarts:1, dimecres:2}
let dies = ["dilluns", "dimarts", "dimecres"];
//se reduce el array, para que segun el elemento del array se determine su posicion en el indice y se retorne en modo de {} objeto
const diesPos = dies.reduce((accum, elem, indice) => {
  accum[elem] = indice;
  return accum;
}, {});
console.log(diesPos);

//A partir d'un array amb objectes Musics (nom i instrument que toca)
//Que torne un array amb els noms de tots els components
// [ 'Joan', 'Pep', 'Vicent Lloret', 'Ariadna', 'Guillem' ]
let musics = [
  { nom: "Joan", instrument: "vocal" },
  { nom: "Pep", instrument: "guitarra" },
  { nom: "Vicent Lloret", instrument: "guitarra" },
  { nom: "Ariadna", instrument: "bateria" },
  { nom: "Guillem", instrument: "baix" },
];
//tenemos un array de musicos
//que se reduce, sabiendo que es el array y el elemento es musico, entonces hacemos un .push() para que el array guarde solo el elemento del nombre, gracias a las propiedades de javascript, sabe que propiedades globales son dentro de cada objeto.
//se retorna el array de solo los nombres, no de los objetos
const nomsMusics = (musics) =>
  musics.reduce((arryMuscis, musico) => {
    arryMuscis.push(musico.nom);
    return arryMuscis;
  }, []);
console.log(nomsMusics(musics));

//Ara feu-ho utilitzant map()
//con map es aun mas facíl
console.log(musics.map((music) => music.nom));

//Ara que torne un array només amb els noms del musics que toquen la guitarra
//['Pep', 'Vicent Lloret']
//se filtra solo por la propiedad de instrumento, gracias al filter se puede poner una condicion
const filtradosGui = musics.filter((music) => music.instrument === "guitarra");
//para mas adelante hacer un array .map() con solo los nombres
const nombresFilt = filtradosGui.map((music) => music.nom);
console.log(nombresFilt);

//Amb reduce
//['Pep', 'Vicent Lloret']
//con reduce se hace todo dentro de una misma constante
//se usa un array y el elemento, se filtra segun su propiedad, y luego hacemos un push de la propiedad nombre
//asi se restorna el array entero, solo con lo que se ha pusheado
const nomsMusicsGui = (musics) =>
  musics.reduce((arryMuscis, musico) => {
    if (musico.instrument === "guitarra") {
      arryMuscis.push(musico.nom);
    }
    return arryMuscis;
  }, []);
console.log(nomsMusicsGui(musics));

//----------------------------------------------------------------------------------

const users = [
  {
    id: 1,
    name: "Jonathon Haley",
    username: "Monte.Weber2",
    email: "Daphne43@yahoo.com",
    phone: "1-563-675-1857 x11708",
    website: "carmela.net",
    password: "hashed_password",
  },
  {
    id: 2,
    name: "Dean John",
    username: "dd.1",
    email: "deno@google.com",
    phone: "1-123-543-1857 123212",
    website: "dd.net",
    password: "Dean_hashed_password",
  },
];

//Que torne un array d'objectes amb l'email, el tel i la web
[
  {
    email: "Daphne43@yahoo.com",
    website: "carmela.net",
    phone: "1-563-675-1857 x11708",
  },
  {
    email: "deno@google.com",
    website: "dd.net",
    phone: "1-123-543-1857 123212",
  },
];

//hacemos un reduce() en el que acumulamos en un array, los objetos que necesitamos, y de los objetos solo cogemos las propiedades que nos interesan
//en vez de crear un objeto temporal, le metemos en el push el objeto nuevo creado y retornamos el array
const usersContactInfo = users.reduce((array, user) => {
  array.push({
    email: user.email,
    website: user.website,
    phone: user.phone,
  });
  return array;
}, []);

console.log(usersContactInfo);

//-----------------------------------------------------
//A partir d'un arrar de comandes com el proporcionat
let comandes = [
  {
    client: {
      nom: "Manel Viel",
    },
    productes: [
      {
        id: 1,
        nom: "Taronges",
      },
      {
        id: 2,
        nom: "Pomes",
      },
    ],
  },
  {
    client: {
      nom: "Joan Mi",
    },
    productes: [
      {
        id: 3,
        nom: "Peres",
      },
      {
        id: 2,
        nom: "Pomes",
      },
    ],
  },
  {
    client: {
      nom: "Tomas Marin",
    },
    productes: [
      {
        id: 4,
        nom: "Freses",
      },
      {
        id: 2,
        nom: "Peres",
      },
      {
        id: 1,
        nom: "Platans",
      },
    ],
  },
];

// tornar un array anomenat llistat de comandes, on cada element siga un array d'objectes on
// aparega només el client i el producte de la seua comanda.
// Exemple:

//llistatDeComandes => [
//    [
//        { client: 'Manel Viel', productes: 'Taronges' },
//        { client: 'Manel Viel', productes: 'Pomes' }
//    ],
//    [
//        { client: 'Joan Mi', productes: 'Peres' },
//         { client: 'Joan Mi', productes: 'Pomes' }
//     ],
//     [
//         { client: 'Tomas Marin', productes: 'Freses' },
//         { client: 'Tomas Marin', productes: 'Peres' },
//         { client: 'Tomas Marin', productes: 'Platans' }
//     ]
// ]

//este me costó un poco mas de entender
//un map() de las comandas porque es el array de objetos, pero cada objeto tiene 2 objetos dentro, cliente y productes
//entonces ya con la comanda mapeada, mapeas el producto para saber el cliente y el producto
//y como map devuelve siempre un array te quitas 2 de un 1 tiro
const llistatDeComandes = (comandes) =>
  comandes.map((comanda) =>
    comanda.productes.map((producte) => ({
      client: comanda.client.nom,
      productes: producte.nom,
    }))
  );

console.log(llistatDeComandes(comandes));
```

Ejercicios Clase 24-09-2025, Reduce, Filter, Map, JSON:

```javascript
const dadesUsuaris = [
  {
    id: 1,
    name: "Leanne Graham",
    username: "Bret",
    email: "Sincere@april.biz",
    address: {
      street: "Kulas Light",
      suite: "Apt. 556",
      city: "Gwenborough",
      zipcode: "92998-3874",
      geo: {
        lat: "-37.3159",
        lng: "81.1496",
      },
    },
    phone: "1-770-736-8031 x56442",
    website: "hildegard.org",
    company: {
      name: "Romaguera-Crona",
      catchPhrase: "Multi-layered client-server neural-net",
      bs: "harness real-time e-markets",
    },
  },
  {
    id: 2,
    name: "Ervin Howell",
    username: "Antonette",
    email: "Shanna@melissa.tv",
    address: {
      street: "Victor Plains",
      suite: "Suite 879",
      city: "Wisokyburgh",
      zipcode: "90566-7771",
      geo: {
        lat: "-43.9509",
        lng: "-34.4618",
      },
    },
    phone: "010-692-6593 x09125",
    website: "",
    company: {
      name: "Deckow-Crist",
      catchPhrase: "Proactive didactic contingency",
      bs: "synergize scalable supply-chains",
    },
  },
  {
    id: 3,
    name: "Clementine Bauch",
    username: "Samantha",
    email: "Nathan@yesenia.net",
    address: {
      street: "Douglas Extension",
      suite: "Suite 847",
      city: "McKenziehaven",
      zipcode: "59590-4157",
      geo: {
        lat: "-68.6102",
        lng: "-47.0653",
      },
    },
    phone: "1-463-123-4447",
    website: "ramiro.info",
    company: {
      name: "Romaguera-Jacobson",
      catchPhrase: "Face to face bifurcated interface",
      bs: "e-enable strategic applications",
    },
  },
  {
    id: 4,
    name: "Patricia Lebsack",
    username: "Karianne",
    email: "Julianne.OConner@kory.org",
    address: {
      street: "Hoeger Mall",
      suite: "Apt. 692",
      city: "South Elvis",
      zipcode: "53919-4257",
      geo: {
        lat: "29.4572",
        lng: "-164.2990",
      },
    },
    phone: "493-170-9623 x156",
    website: "kale.biz",
    company: {
      name: "Robel-Corkery",
      catchPhrase: "Multi-tiered zero tolerance productivity",
      bs: "transition cutting-edge web services",
    },
  },
  {
    id: 5,
    name: "Chelsey Dietrich",
    username: "Kamren",
    email: "Lucio_Hettinger@annie.ca",
    address: {
      street: "Skiles Walks",
      suite: "Suite 351",
      city: "Roscoeview",
      zipcode: "33263",
      geo: {
        lat: "-31.8129",
        lng: "62.5342",
      },
    },
    phone: "(254)954-1289",
    website: "",
    company: {
      name: "Keebler LLC",
      catchPhrase: "User-centric fault-tolerant solution",
      bs: "revolutionize end-to-end systems",
    },
  },
];

//Crear una funció que es diga llistat_Id_Nom_Email() que ens torne un array
// d'objectes amb l'id, nom i email dels usuaris
/* [
    { id: 1, name: 'Leanne Graham', email: 'Sincere@april.biz' },
    { id: 2, name: 'Ervin Howell', email: 'Shanna@melissa.tv' },
    { id: 3, name: 'Clementine Bauch', email: 'Nathan@yesenia.net' },
...
] */
//fer-ho amb map
//array de objetos que cada objeto tiene 2 objetos dentro
//gracias a javascript y sus propiedades globales, se hace un map() en el que solo quieres que devuelva los id, name y email
//y el map() devuelve dicho array
const llistat_Id_Nom_Email = (dadesUsuaris) =>
  dadesUsuaris.map(({ id, name, email }) => ({ id, name, email }));
console.log(llistat_Id_Nom_Email(dadesUsuaris));

//fer-ho amb reduce (canvieu-li el nom a la funció per llistat_Id_Nom_Email_reduce())
//en vez de hacer un objeto temporal, se hace el push de las propiedades del elemento User que le dictamos
//los coge, los pushea y retorna el array reducido con los objetos que queremos
const llistat_Id_Nom_Email_reduce = (dadesUsuaris) =>
  dadesUsuaris.reduce((arrUsuarios, User) => {
    arrUsuarios.push({
      id: User.id,
      name: User.name,
      email: User.email,
    });
    return arrUsuarios;
  }, []);
console.log(llistat_Id_Nom_Email_reduce(dadesUsuaris));

//Crear una funció llistaAmbAddress() que ens torne un llistat d'objectes que contenen
// els atributs id, name, email, i address, PERÒ address serà un string que concatenarà els atributs
// street suite i zipcode city
//Exemple:
/* {
    id: 1,
    name: 'Leanne Graham',
    email: 'Sincere@april.biz',
    address: 'Kulas Light Apt. 556\n        92998-3874 Gwenborough'
   },
   {
    id: 2,
    name: 'Ervin Howell',
    email: 'Shanna@melissa.tv',
    address: 'Victor Plains Suite 879\n        90566-7771 Wisokyburgh'
    } */

//exactamente la misma estructura que el ejercicio map primero, retornamos lo que queremos gracias a las propiedades globales, y conseguimos coger lo que necesitamos de address, concatenandolo con cadenas vacias " "
//retornamos el array nuevo en el map()
const llistatAmbAddress = (dadesUsuaris) =>
  dadesUsuaris.map(({ id, name, email, address }) => ({
    id,
    name,
    email,
    address:
      address.street +
      " " +
      address.suite +
      " " +
      address.zipcode +
      " " +
      address.city,
  }));

console.log(llistatAmbAddress(dadesUsuaris));

//Crea una funció llistaIds_EmpresesSenseWebsite() que torne un array amb els id d'aquelles empreses que no tenen website
//[ { id: 2 }, { id: 5 } ]
//este no lo sabia que se podia hacer, estaba haciendo dos funciones diferentes
//se filtra segun el parametro de que si su propiedad website esta vacia, entonces al filtrarlo se hace un .map() sobre la misma funcion para solo coger el parametro de los objetos
//y este retorna el array de objetos
const llistaIds_EmpresesSenseWebsite = (dadesUsuaris) =>
  dadesUsuaris.filter((usu) => usu.website === "").map((usu) => usu.id);
console.log(llistaIds_EmpresesSenseWebsite(dadesUsuaris));

//Crear una funció esWebsiteBuit(usuari) que donat un objecte usuari, em diga si la website esta buida o no
//ni map ni nada, if ternario y si esta vacio lo esta
//en vez de pasar el array entero pasas solo el elemento que necesitas comprobar
const esWebsiteBuit = (usuario) => {
  return usuario.website === "" ? "esta buit" : "no esta buit";
};
console.log(esWebsiteBuit(dadesUsuaris[0]));
console.log(esWebsiteBuit(dadesUsuaris[1]));

//Crear una funció tornaId(usuari) que donat un usuari em torne un objecte id
//exactamente lo mismo pero solo retornas el id del usuario si o si, pasandole el usuario del array
const tornaId = (usuario) => {
  return usuario.id;
};
console.log(tornaId(dadesUsuaris[0]));

//Creeu una funció (POSEU-LI vosaltres un nom descriptiu) que amb un reduce/filter, torne un array amb els id d'aquelles empreses que no tenen website
//[{ id: 2 }, { id: 5 }]
//se usa un reduce para acumular todo en un array de objetos y el elemento se llama user, de tal manera que si su website esta vacia esta hace un push de su id y devuelve el array de los objetos
const EmpresaIdReduce = (dadesUsuaris) =>
  dadesUsuaris.reduce((array, user) => {
    if (user.website === "") {
      array.push(user.id);
    }
    return array;
  }, []);
console.log(EmpresaIdReduce(dadesUsuaris));

//reduce en una sola línia
// [ { id: 2 }, { id: 5 } ]
//se reduce todo solo si la website esta vacia, en caso correcto se hace un concat del id del usu, sino nada, y devuelve el array de objetos
console.log(
  dadesUsuaris.reduce(
    (arr, usu) => (usu.website === "" ? arr.concat({ id: usu.id }) : arr),
    []
  )
);
```

Ejercicios de repaso 6-10-2025

```javascript
const usuarios = [
  {
    id: 1,
    name: "Leanne Graham",
    email: "Sincere@april.biz",
    address: { city: "Gwenborough", zipcode: "92998-3874" },
    company: { name: "Romaguera-Crona" },
    posts: [
      { id: 1, title: "Post 1", likes: 10 },
      { id: 2, title: "Post 2", likes: 20 },
    ],
  },
  {
    id: 2,
    name: "Ervin Howell",
    email: "Shanna@melissa.tv",
    address: { city: "Wisokyburgh", zipcode: "90566-7771" },
    company: { name: "Deckow-Crist" },
    posts: [
      { id: 3, title: "Post 3", likes: 5 },
      { id: 4, title: "Post 4", likes: 15 },
    ],
  },
];
//solo las ciudades
const ciudadesUnicas = (usuarios) =>
  usuarios.reduce((arrayCiudades, usu) => {
    arrayCiudades.push({
      city: usu.address.city,
    });
    return arrayCiudades;
  }, []);
console.log(ciudadesUnicas(usuarios));

//total de likes en posts de cada usuario
const totalLikesUser = (usuarios) =>
  usuarios.map((usuario) => ({
    name: usuario.name,
    totalLikes: usuario.posts.reduce((accum, num) => (accum += num.likes), 0),
  }));
console.log(totalLikesUser(usuarios));

//saber post con mas likes
const postMasPopular = (usuarios) => {
  let postMaxLikes = usuarios[0].posts[0];
  usuarios.forEach((usuario) => {
    usuario.posts.forEach((post) => {
      if (post.likes > postMaxLikes.likes) {
        postMaxLikes = post;
      }
    });
  });
  return postMaxLikes;
};
console.log(postMasPopular(usuarios));

//agregar posts a cada usuario dicho por codigo
const agregarPostUsuario = (usuarios, userId, post) => {
  usuarios.forEach((usuario) => {
    if (usuario.id === userId) {
      usuario.posts.push(post);
    }
  });
  return usuarios;
};
// console.log(agregarPostUsuario(usuarios, 1, { id: 5, title: "post 5", likes: 100 }));
console.log(
  JSON.stringify(
    agregarPostUsuario(usuarios, 2, { id: 5, title: "post 5", likes: 100 }),
    null,
    2
  )
);

//listar array de usuarios con mas de N posts
const listarMasNPost = (usuarios, numero) => {
  return usuarios.filter((usu) => usu.posts.length > numero);
};
console.log(listarMasNPost(usuarios, 2));
```
