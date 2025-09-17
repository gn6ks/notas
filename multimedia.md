---
titulo: Programación Multimedia y Dispositivos moviles
autor: gn6ks
creado: 12-09-2025
profesor: fsegura@florida-uni.es
---

## React Native

### Eventos React

React Native funciona mediante la orientación de eventos, es decir que se modifican mediante eventos y no mediante objetos.
Manejadores de eventos "handler" funcion que maneja el evento.
La sintaxis en general de react-native consiste en camelCase.

```javascript
onNombreEvento();
```

Para que la aplicación reaccione a un evento, es necesario
asociarle una lógica que se ejecutará cuando se produzca el
evento -> Manejadores de eventos.

```javascript
handlerOnPress();
```

ejemplo de handlerOnPress() detallado:

```javascript
export default function App() {
  function handleOnPress() {
    alert("Hola");
  }
  return (
    <View style={styles.container}>
      <Pressable onPress={handleOnPress}>
        <Text style={styles.text}>Púlsame!</Text>
      </Pressable>
    </View>
  );
}
```

### Hooks React

Utilidades ya implementadas en el propio React sin las cuales no es posible hacer ciertas acciones.

En React Native no actualizamos las variables
propias de un componente, lo que hacemos es actualizar su
estado.

```javascript
import { View, Pressable, Text, StyleSheet } from "react-native";
import { useState } from "react";
export default function App() {
  const [color, setColor] = useState("yellow");
  function handleOnPress() {
    setColor("green");
    alert("Ahora sí que va");
  }
  return (
    <View style={[styles.container, { backgroundColor: color }]}>
      <Pressable onPress={handleOnPress}>
        <Text style={styles.text}>Púlsame!</Text>
      </Pressable>
    </View>
  );
}
```
A continuación se muestra una vista previa de la sintaxis de `useState`:

![Sintaxis de useState](/home/gn6ks/Escritorio/_estudios/_dam2/_notas/sintaxisUseState.png)
