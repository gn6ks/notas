---
titulo: Acceso a Datos
autor: gn6ks
creado: 11-09-2025
profesor: rsanz@florida-uni.es
---

## Ejercicios de clase dia 18-09-2025
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

## Apuntes Tema 1 Ficheros
### Teoria Tema 1
![ClassFile](assets/seccionFile.png)
> metodos de la clase File

![FileReader_BufferedReader](assets/frbr.png)
> para la lectura de caracteres (16 bits)

![FileWriter_BufferedWriter](assets/fwbw.png)
> para la escritura de caracteres (16 bits)

#### Sección 1 Tema 1

```java
package Tema1Ejercicios1;

import java.io.File;

public class Seccion1ejecs1to5 {
    public static void main(String[] args) {
        //ejec1 - Realitza un programa que reba com a paràmetre d’entrada un string amb un directori i
        //mostre el string per pantalla.
        File directorio = new File("."); //clase File, el directorio es el que se le pasa por new File
        System.out.println(directorio); //print de la ruta

        //ejec2 - Ampliar el programa anterior (crea una altra aplicació) per tal que mostre totes les
        //característiques d’interés del directori, prenent com a referència la informació que
        //proporciona la classe File
        System.out.println(directorio.getName()); //nombre
        System.out.println(directorio.getPath()); //ruta
        System.out.println(directorio.getAbsolutePath()); //ruta absoluta
        System.out.println(directorio.canRead()); //permisos de lectura
        System.out.println(directorio.canWrite()); // ** de escritura
        System.out.println(directorio.isFile()); //si es archivo .isDirectory si es directorio
        System.out.println(directorio.length()); //tamaño

        //ejec3 - Introduir una comprovació en el programa anterior (crea una altra aplicació) per determinar
        //si el directori existeix.
        System.out.println(directorio.exists());

        //ejec4 - Realitzar un programa que donat un directori, comprove si existeix i torne un missatge de
        //confirmació si existeix o una alerta en cas contrari.
        if (directorio.exists()) {
            System.out.println("directorio existe");
        } else {
            System.out.println("directorio no existe");
        }

        //ejec5 - Realitza un programa que reba com a paràmetres d’entrada un directori i una extensió de
        //fitxer (per exemple .txt) i torne per pantalla tots els fitxers del directori que complisquen el
        //criteri.
        String strdir = args[0];
        System.out.println(strdir);
        File dir = new File(strdir);
        FiltroExtension extension = new FiltroExtension(".txt");
        String[] listaArchivos = dir.list(extension);
        for (int i = 0; i < listaArchivos.length; i++) {
            System.out.println(listaArchivos[i]);
        }
    }
}
```

```java
package Tema1Ejercicios1;

import java.io.File;
import java.util.Scanner;

public class Seccion1ejec6 {
    public static void main(String[] args) {
        //ejec 6 - Modifica el programa anterior (crea una altra aplicació) per que tinga en compte que si no
        //se li passa ninguna extensió com a paràmetre, mostre tot el contingut del directori.
        String direc = args[0]; //se pasa la ruta del directorio por parametro
        File dir = new File(direc); //y se crea un nuevo manejador de archivo de ese directorio (manejador NO creador)
        String extension = ""; //se llama a la extension
        if (args.length > 1) { //comprobamos a traves de los argumentos si le hemos pasado mas de 1 argumento por parametro
            extension = args[1]; //en caso true, asignamos el nuevo argumento
            System.out.println("Listando archivos con extensión '" + extension + "':");
        } else {
            //en caso false listamos todo
            System.out.println("Listando archivos con extensión por defecto:");
        }

        FiltroExtension filtro = new FiltroExtension(extension); //clase externa
        String[] listaArchivos = dir.list(filtro); //array de strings que son el contenido de dir
        if (listaArchivos != null && listaArchivos.length > 0) {
            for (String archivo : listaArchivos) {
                System.out.println(archivo); //por cada string archivo en la listaArchivos, se printean en la terminal
            }
        } else {
            System.out.println("No se encontraron archivos con la extensión especificada o el directorio está vacío.");
        }
    }
}
```

```java
package Tema1Ejercicios1;

import java.io.File;
import java.util.Arrays;
import java.util.Scanner;

public class Seccion1ejec7 {
    public static void main(String[] args) {
        //ejec 7 - Modifica el programa anterior (crea una altra aplicació) per tal que admeta com a
        //paràmetres d’entrada un nombre qualsevol d’extensions, tornant després per pantalla tots
        //els fitxers del directori que tinguen alguna de les extensions indicades.
        String direc = args[0]; 
        File dir = new File(direc);
        String extension = "";
        if (args.length > 1) {
            for (int i = 1; i < args.length; i++) { //la unica diferencia con el anterior es que como sabemos que le vamos pasando extensiones
                extension = args[i];                //estos se van creando a medida que veamos los que le hemos pasado
                System.out.println("Listando archivos con extensión '" + extension + "':");
                ListarArchivos(dir, extension);
            }
        } else {
            System.out.println("Listando archivos con extensión por defecto:");
            ListarArchivos(dir, extension);
        }
    }

    //lo convertimos en una funcion ya que lo usamos varias veces, pasandole directorio y extensiones/extension
    public static void ListarArchivos(File dir, String extension) {
        FiltroExtension filtro = new FiltroExtension(extension);
        String[] listaArchivos = dir.list(filtro);
        if (listaArchivos != null && listaArchivos.length > 0) {
            for (String archivo : listaArchivos) {
                System.out.println(archivo);
            }
        } else {
            System.out.println("No se encontraron archivos con la extensión especificada o el directorio está vacío.");
        }
    }
}
```

```java
package Tema1Ejercicios1;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;

public class Seccion1ejec8 {
    public static void main(String[] args) {
        //ejec 8 - Desenvolupa un programa que donat un fitxer, realitze una còpia del mateix (en el mateix
        //directori i canviant-li el nom) i el borre després. Mostra una traça per pantalla de les accions
        //per a veure que es realitzen.
        String fich = args[0]; //fichero por parametro
        File fichero = new File(fich); //manejador de fichero
        File ficheroRenombrado = new File(fich + "Renombrado"); //manejador de nuevofichero

        if (fichero.exists()) { //si existe
            System.out.println("Existe el archivo " + fichero); //lo decimos
            System.out.println("copiando en directorio origen " + fichero.getParent()); //y lo copiamos en el mismo directorio
            try {
                Files.copy(fichero.toPath(), ficheroRenombrado.toPath()); //copia de origen a destino
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
            if (ficheroRenombrado.renameTo(fichero)) { //cambiar el nombre de fichero a el nombre que ficheroRenombrado tiene con renameTo()
                System.out.println("Fichero renombrado copiado");
                System.out.println("eliminando fichero copiado y renombrado");
                if (ficheroRenombrado.delete()) { //delete() para eliminar
                    System.out.println("Fichero renombrado eliminado");
                } else {
                    System.out.println("Fichero renombrado no eliminado");
                }
            } else {
                System.out.println("Fichero renombrado no copiado");
            }
        } else {
            System.out.println("NO Existe el archivo " + fichero);
        }
    }

    //se queda igual
    public static void ListarArchivos(File dir, String extension) {
        FiltroExtension filtro = new FiltroExtension(extension);
        String[] listaArchivos = dir.list(filtro);
        if (listaArchivos != null && listaArchivos.length > 0) {
            for (String archivo : listaArchivos) {
                System.out.println(archivo);
            }
        } else {
            System.out.println("No se encontraron archivos con la extensión especificada o el directorio está vacío.");
        }
    }
}
```

##### Proyecto de Seccion 1 Tema 1
```java
package Tema1Proyecto;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.attribute.FileTime;
import java.util.Scanner;

public class proyecto {
    public static void main(String[] args) {
        //poner ruta como argumento 0 y hacer un File nuevo
        String ruta = args[0];
        File archivo = new File(ruta);
        //scanner para el menu
        Scanner sc = new Scanner(System.in);
        int opcion;
        do {
            menu();
            System.out.println("Escoga opción");
            opcion = sc.nextInt();
            switch (opcion) {
                case 0:
                    System.out.println("Saliendo del programa :D");
                    break;
                case 1:
                    getInformacion(archivo);
                    break;
                case 2:
                    crearCarpeta(archivo);
                    break;
                case 3:
                    crearFitxer(archivo);
                    break;
                case 4:
                    elimina(archivo);
                    break;
                case 5:
                    renomena(archivo);
                    break;
                default:
                    System.out.println("Opcion no valida");
                    break;
            }
        } while (opcion != 0);
    }

    public static void menu() {
        //display de las opciones
        System.out.println("======Gestor Archivos Albux=====");
        System.out.println("(0). Salir");
        System.out.println("(1). Obtener información");
        System.out.println("(2). Crear Carpeta en ruta");
        System.out.println("(3). Crear fichero en ruta");
        System.out.println("(4). Eliminar fichero/carpeta en ruta");
        System.out.println("(5). Renombrar fichero/carpeta en ruta");
        System.out.println("================================");

    }

    public static void ultimaModificacion(File rutaArchivo) {
        Path pathArchivo = Paths.get(rutaArchivo.getAbsolutePath()); //tener en una clase Path el path absoluto del archivo
        FileTime lastModifiedTime = null; //con FileTime se puede saber el ultimo momento que se modifico el archivo
        try {
            lastModifiedTime = Files.getLastModifiedTime(pathArchivo); //con getLastModifiedTime
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        System.out.println("Ultima modificación: " + lastModifiedTime); //print del tiempo
    }

    public static void getInformacion(File directorio) {
        if (directorio.isFile()) { //si es archivo
            System.out.println("Nombre del archivo: " + directorio.getName());
            System.out.println("Tipo de archivo: fichero");
            System.out.println("Ruta del fichero: " + directorio.getAbsolutePath());
            ultimaModificacion(directorio);
            System.out.println("Esta oculto? " + directorio.isHidden());
            System.out.println("Tamaño en bytes: " + directorio.length());
        } else { //si es directorio
            System.out.println("Nombre del archivo: " + directorio.getName());
            System.out.println("Tipo de archivo: directorio");
            System.out.println("Ruta del fichero: " + directorio.getAbsolutePath());
            ultimaModificacion(directorio);
            System.out.println("Esta oculto? " + directorio.isHidden()); //si esta oculto a la vista del usuario
            System.out.println("Espacio libre: " + directorio.getUsableSpace()); //cuanto de disco usable queda 
            System.out.println("Espacio disponible en partición: " + directorio.getFreeSpace()); //cuanto de espacio libre queda
            System.out.println("Espacio total: " + directorio.getTotalSpace()); //cuanto de espacio total hay
        }
    }

    public static void crearCarpeta(File rutaArchivo) {
        System.out.println("Creando nueva carpeta en: " + rutaArchivo.getParent()); //en el mismo directorio
        File carpetaNueva = new File(rutaArchivo + "Carpeta"); //manejador de carpetaNueva
        if (carpetaNueva.mkdir()) { //y se crea con el nombre de rutaArchivo+Carpeta
            System.out.println("Carpeta creada exitosamente");
        } else {
            System.out.println("Carpeta NO se ha podido crear");
        }
    }

    public static void crearFitxer(File rutaArchivo) {
        //lo mismo que el anterior pero con CreateNewFile(), este necesita un try por que puede dar error
        System.out.println("Creando nuevo fichero en: " + rutaArchivo.getParent());
        File nuevoFichero = new File(rutaArchivo + "Fichero");
        try {
            if (nuevoFichero.createNewFile()) {
                System.out.println("Fichero creada exitosamente");
            } else {
                System.out.println("Fichero NO se ha podido crear");
            }
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

    public static void elimina(File rutaArchivo) {
        System.out.println("Eliminando el fichero/carpeta: " + rutaArchivo.getAbsolutePath());
        if (rutaArchivo.delete()) { //eliminar
            System.out.println("Fichero/carpeta eliminado exitosamente");
        } else {
            System.out.println("Fichero/carpeta NO se ha podido eliminar");
        }
    }

    public static void renomena(File rutaArchivo) {
        System.out.println("Renombrando el fichero/carpeta: " + rutaArchivo.getAbsolutePath());
        File ficheroRenombrado = new File(rutaArchivo + "Renombrado");
        if (rutaArchivo.renameTo(ficheroRenombrado)) { //y para el renombrado es (archivo_a_renombrar.renameTo(nuevo_nombre_archivo))
            System.out.println("Fichero/carpeta renombrado exitosamente");
        } else {
            System.out.println("Fichero/carpeta NO se ha podido renombrar");
        }
    }
}
```

#### Sección 2 Tema 1

```java
/*ejec 1 - Escriu un programa que reba com a paràmetre d’entrada la ruta d’un fitxer, llija el seu
contingut i el mostre per pantalla caràcter a caràcter.*/
package Tema1Ejercicios2;

import java.io.File;
import java.io.FileReader;
import java.nio.charset.StandardCharsets;


public class ejec1 {
    public static void main(String[] args) {
        String rutaArchivo = args[0]; //se pasa la ruta por parametro
        File fitxer = new File(rutaArchivo); //manejador del archivo

        try {
            FileReader archivo = new FileReader(fitxer, StandardCharsets.UTF_8); //para leer caracter a caracter (16 bits)
            int valor = archivo.read(); //cada caracter es un int()
            while (valor != -1) { //mientras haya algo en el valor
                System.out.print((char) valor); //se imprime el valor a character
                valor = archivo.read(); //se machaca el contenido guardado en memoria por el nuevo contenido
                Thread.sleep(50); //tiempo de espera entre caracteres
            }
            archivo.close();
        } catch (Exception error) {
            error.printStackTrace();
        }
    }
}
```

```java
/*ejec 2 - Crea un altre programa, modificació de l’anterior, que admeta un altre paràmetre d’entrada
addicional que permeta especificar la velocitat a la qual es mostren els caràcters.*/
package Tema1Ejercicios2;

import java.io.File;
import java.io.FileReader;
import java.nio.charset.StandardCharsets;


public class ejec2 {
    public static void main(String[] args) {
        String rutaArchivo = args[0]; //parametro del archivo
        String velocidad = args[1]; //parametro de la velocidad
        int milisecons = Integer.parseInt(velocidad); //string a entero
        File fitxer = new File(rutaArchivo); //manejador de archivo

        try {
            FileReader archivo = new FileReader(fitxer, StandardCharsets.UTF_8); //reader para leer caracter a caracter
            int valor = archivo.read();
            while (valor != -1) {
                System.out.print((char) valor);
                valor = archivo.read();
                Thread.sleep(milisecons); //la velocidad es la que dice el usuario por parametro
            }
            archivo.close();
        } catch (Exception error) {
            error.printStackTrace();
        }
    }
}
```

```java
/*ejec 3 - Realitza un altre programa que mostre un nombre determinat de caràcters per pantalla (per
exemple 100), espere a que l’usuari presione alguna tecla, mostre un altre bloc de caràcters,
torne a esperar, i així successivament fins mostrar tot el contingut.*/
//en vez de hacer cada 100 caracteres, simplemente dije que lo hiciera linea a linea para practicar el bufferedreader
//la solución correcta seria hacer un contador, que muestre cada caracter, y hasta que el contador no llegara a 100 se imprimieran
//una vez llegara a 100 que se hiciera un sc.nextLine(), sin necesidad de buffered
package Tema1Ejercicios2;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.nio.charset.StandardCharsets;
import java.util.Scanner;

public class ejec3 {
    public static void main(String[] args) {
        String archivo = args[0];
        File arch = new File(archivo);
        Scanner sc = new Scanner(System.in);

        try {
            FileReader fr = new FileReader(archivo, StandardCharsets.UTF_8);
            BufferedReader br = new BufferedReader(fr); //un buffered es para trabajar con las lineas, es mas rapido y necesita de parametro el filereader
            String linea = br.readLine(); //cada String linea se guarda lo que el br lee
            while (linea != null) { //mientras que la linea no este vacia
                System.out.println(linea); //se imprime en pantalla
                linea = br.readLine(); //se machaca la memoria para entrar la nueva linea
                sc.nextLine(); //cada vez q el usuario pulsa una tecla imprime la siguiente linea
            }
            fr.close(); //cerrar todo es importante porque da error
            br.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

```java
/*ejec 4 - Crea un programa que donat un fitxer de text, llija i mostre el seu contingut línia a línia.*/
//como lo habia hecho de la manera anterior mal este ya lo tenia, es igual al ejec 3 
package Tema1Ejercicios2;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.nio.charset.StandardCharsets;

public class ejec4 {
    public static void main(String[] args) {
        String archivo = args[0];
        File arch = new File(archivo);

        try {
            FileReader fr = new FileReader(archivo, StandardCharsets.UTF_8);
            BufferedReader br = new BufferedReader(fr);
            String linea = br.readLine();
            while (linea != null) {
                System.out.println(linea);
                linea = br.readLine();
            }
            fr.close();
            br.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}

```

```java
/*ejec 5 - Crea un altre programa, modificació de l’anterior, que accepte com a paràmetres d’entrada
un nombre que indique la velocitat a la qual es mostren les línies.*/
//igual que el ejercicio anterior pero pasandole la velocidad por parametro, pasandolo de string a integer
package Tema1Ejercicios2;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.nio.charset.StandardCharsets;

public class ejec5 {
    public static void main(String[] args) {
        String archivo = args[0];
        String velocidad = args[1];
        int velocidadMiliseconds = Integer.parseInt(velocidad);

        try {
            FileReader fr = new FileReader(archivo, StandardCharsets.UTF_8);
            BufferedReader br = new BufferedReader(fr);
            String linea = br.readLine();
            while (linea != null) {
                System.out.println(linea);
                linea = br.readLine();
                Thread.sleep(velocidadMiliseconds);
            }
            fr.close();
            br.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

```java
/*ejec 6 - Crea un altre programa a partir de l’anterior que en comptes de mostrar el contingut per
consola l’escriga en un altre fitxer del mateix directori.*/
package Tema1Ejercicios2;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class ejec6 {
    public static void main(String[] args) {
        //archivos parametros y linea
        String linea;
        String archivo = args[0];
        File f1 = new File(archivo);
        String archivoCopia = args[1];
        File f2 = new File(archivoCopia);

        try {
            //leemos con fr y br el primer archivo donde se encuentra la informacion
            FileReader fr = new FileReader(f1, StandardCharsets.UTF_8);
            BufferedReader br = new BufferedReader(fr);
            //con fw y bw vamos a escribir todo en el segundo archivo
            FileWriter fw = new FileWriter(f2, StandardCharsets.UTF_8);
            BufferedWriter bw = new BufferedWriter(fw);
            while ((linea = br.readLine()) != null) { //mientras que la linea no se encuentre vacia
                bw.write(linea); //se escribe en f2
                bw.newLine(); //con un salto de linea para que todo no se encuentre pegado entre si
                bw.flush(); //sirve para forzar a que se escriba SEA LO QUE SEA
            }
            fr.close(); //cerrar todo
            br.close();
            fw.close();
            bw.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

```java
/*ejec 7 - Realitza un programa que permeta rebre per teclat una sèrie de strings per part de l’usuari
i els vaja escrivint en un fitxer de text. Com a condició de finalització, l’usuari haurà
d’escriure un string que siga “exit”.*/
package Tema1Ejercicios2;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.Scanner;

public class ejec7 {
    public static void main(String[] args) {
        //parametros
        Scanner sc = new Scanner(System.in);
        String linea;
        String archivo = args[0];
        File f1 = new File(archivo);

        try {
            FileWriter fw = new FileWriter(f1, StandardCharsets.UTF_8);
            BufferedWriter bw = new BufferedWriter(fw);
            System.out.println("Lineas a escribir: ");
            linea = sc.nextLine(); //en vez de leer todo con un fr br, lo lee de la consola
            while (!linea.equals("exit") ) {
                bw.write(linea); //se escrie la primera linea
                System.out.println("Lineas a escribir: ");
                linea = sc.nextLine(); //se borra de la memoria la ultima linea asi exit no sale en el fichero
                bw.newLine(); //salto linea
                bw.flush(); //se fuerza
            }
            fw.close(); //todo cerrado
            bw.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

```java
/*ejec 8 - Modifica el programa anterior (o crea un programa nou) per a que el nom del fitxer incloga
la data i l’hora de creació.*/
package Tema1Ejercicios2;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class ejec8 {
    public static void main(String[] args) {
        //parametros
        Date d1 = new Date(); //clase date para que me de la fecha del sistema, como el archivo se crea cuando se ejecuta el programa, te quitas 2 de un 1 tiro
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd_HHmmss"); //formatear porque ":" no se permite en el nombre del archivo, sino renameTo() da false
        Scanner sc = new Scanner(System.in);
        String linea;
        String archivo = args[0];
        File f1 = new File(sdf.format(d1) + ".txt"); //se usa el formato para dar formato al archivo

        //esto es exactamente igual que el ejercicio anterior
        try {
            FileWriter fw = new FileWriter(f1, StandardCharsets.UTF_8);
            BufferedWriter bw = new BufferedWriter(fw);
            System.out.println("Lineas a escribir: ");
            linea = sc.nextLine();
            while (!linea.equals("exit")) {
                bw.write(linea);
                System.out.println("Lineas a escribir: ");
                linea = sc.nextLine();
                bw.newLine();
                bw.flush();
            }
            fw.close();
            bw.close();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```