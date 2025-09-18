---
titulo: Acceso a Datos
autor: gn6ks
creado: 11-09-2025
profesor: rsanz@florida-uni.es
---

Ejercicios de clase dia 18-09-2025
```java
package WorkSpaceDatos;

import java.io.*;

public class Ejemplo1 {
    public static void main(String[] args) {
        File fichero = new File("pitodani.txt");

        System.out.println("nombre fichero: " + fichero.getName());
        System.out.println("ruta: " + fichero.getPath());
        System.out.println("ruta absoluta: " + fichero.getAbsolutePath());
        System.out.println("se puede leer: " + fichero.canRead());
        System.out.println("se puede escribir: " + fichero.canWrite());
        System.out.println("tamaño: " + fichero.length());

        File directorio = new File(".");
        String[] listaArchivos  = directorio.list();
        System.out.println("Lista de directorios: " + directorio.getName());

        for (int i = 0; i < listaArchivos.length; i++) {
            System.out.println(listaArchivos[i]);
        }

        for (String s: listaArchivos) {
            System.out.println(s);
        }

        String strdir = args[0];
        System.out.println(strdir);
        File dir = new File(strdir);
        FiltroExtension extension = new FiltroExtension(".txt");
        String[] listaArchivos2 = dir.list(extension);
        for (int i = 0; i < listaArchivos2.length; i++) {
            System.out.println(listaArchivos2[i]);
        }
    }
}

```
