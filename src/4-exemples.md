# Exemples

## Exemple 1

Obtindre informació sobre la ruta.

::: tabs
== Java

```java
package UF10_Exemple01;
import java.io.File;
/**
* UF10 Exemple 01: Obtindre informació sobre la ruta
*/
public class UF10_Exemple01 {
 
    public static void main(String[] args) {

        // Dues rutes absolutes
        File carpetaAbs = new File("/home/lionel/fotos");
        File arxiuAbs = new File("/home/lionel/fotos/albania1.jpg");

        // Dues rutes relatives
        File carpetaRel = new File("treballs");
        File fitxerRel = new File("treballs/document.txt");

        // Mostrem les seues rutes
        mostrarRutes(carpetaAbs);
        mostrarRutes(arxiuAbs);
        mostrarRutes(carpetaRel);
        mostrarRutes(fitxerRel);
    }
    public static void mostrarRutes(File f) {
        System.out.println("getParent() : " + f.getParent());
        System.out.println("getName() : " + f.getName());
        System.out.println("getAbsolutePath(): " + f.getAbsolutePath() + "\n");
    }
} 
```

:::

## Exemple 2

Obtindre informació sobre l'estat.

::: tabs
== Java

```java
package UF10_Exemple02;
import java.io.File;
/**
* UF10 Exemple 02: Obtindre informació sobre l'estat
*/
public class UF10_Exemple02 {
 
    public static void main(String[] args) {

        String rutabase="src/main/java/UF10_Exemple02";

        File temp = new File(rutabase + "/Temp");
        File fotos = new File(rutabase + "/Temp/Fotos");
        File document = new File(rutabase + "/Temp/Document.txt");

        System.out.println(temp.getAbsolutePath() + " existeix? " + temp.exists());
        mostrarEstat(fotos);
        mostrarEstat(document);
    }

    public static void mostrarEstat(File f) {
        System.out.println(f.getAbsolutePath() + " arxiu? "+f.isFile());
        System.out.println(f.getAbsolutePath() + " carpeta? "+f.isDirectory());
    }
}
```

:::

## Exemple 3

Obtindre informació sobre l'estat.

::: tabs
== Java

```java
package UF10_Exemple03;
import java.io.File;
import java.util.Date;
/**
* UF10 Exemple 03: Obtindre informació sobre les propietats de fitxers
*/
public class UF10_Exemple03 {
 
    public static void main(String[] args) {

        File document = new File("src/main/java/UF10_Exemple03/Document.txt");
        System.out.println(document.getAbsolutePath());
        long milisegons = document.lastModified();
        Date data = new Date(milisegons);

        System.out.println("Última modificació (ms) : " + milisegons);
        System.out.println("Última modificació (data): " + data);
        System.out.println("Grandària de l'arxiu: " + document.length());
    }
}
```

:::

## Exemple 4

Creació i eliminació de carpetes i arxius.

::: tabs
== Java

```java
package UF10_Exemple04;
import java.io.File;
import java.io.IOException;
/**
* UF10 Exemple 04: Creació i eliminació de carpetes i arxius
* - En la primera execució crea carpeta i dins arxiu.
* - En la segona esborra arxiu (la carpeta no perquè té contingut).
* - En la tercera esborra carpeta (que ja està buida).
*/
public class UF10_Exemple04 {
 
    public static void main(String[] args) {

        String rutaBase="src/main/java/UF10_Exemple04";

        File carpeta = new File(rutaBase + "/Carpeta");
        File arxiu = new File(rutaBase + "/Carpeta/Arxiu.txt");

        boolean creaDir = carpeta.mkdir();
        // Crea el directori si no existeix.
        if (creaDir) {
            System.out.println("Creat directori " + carpeta.getName() + " en la ruta " + carpeta.getParent() + "? " + creaDir);
            // Sols esborra el directori si no conté arxius.
        } else {
            if (!arxiu.exists()) {
                boolean delDir = carpeta.delete();
                System.out.println("Esborrat directori " + carpeta.getName() + " en la ruta " + carpeta.getParent() + "? " + delDir);
            }
        }
        try {
            boolean creaArx=arxiu.createNewFile();
            if (creaArx) {
                System.out.println("Creat arxiu " + arxiu.getName() + " en la ruta " + arxiu.getParent() + "? " + creaArx);
                // Si no ha creat l'arxiu és perquè ja existia i per tant l'esborra. 
            } else {
                boolean delArx = arxiu.delete();
                if (delArx) {
                    System.out.println("Esborrat arxiu " + arxiu.getName() + " en la ruta " + arxiu.getParent() + "? " + delArx);
                }
            }
        } catch (IOException ioe){
        System.out.println("Error en tractament d'arxiu.");
        }
    }
}
```

:::

## Exemple 5

Creació i eliminació de carpetes i arxius.

::: tabs
== Java

```java
package UF10_Exemple05;
import java.io.IOException;
import java.io.File;
/**
* UF10 Exemple 05: Creació i eliminació de carpetes i arxius
*/
public class UF10_Exemple05 {
    public static void main(String[] args) {

        String rutaBase="src/main/java/UF10Exemple05";
        File carpeta = new File(rutaBase + "/Carpeta");
        File arxiu = new File(rutaBase + "/Carpeta/Arxiu.txt");
        creaEstructura (carpeta, arxiu);
        File carpetaNova = new File(rutaBase + "/CarpetaNova");
        File arxiuInt = new File(rutaBase + "/CarpetaNova/Arxiu.txt");
        File arxiuNou = new File(rutaBase + "/CarpetaNova/ArxiuNou.txt");
        boolean renCar = carpeta.renameTo(carpetaNova);
        System.out.println("S'ha mogut i canviat de nom la carpeta? " + renCar);
        boolean renArx = arxiuInt.renameTo(arxiuNou);
        System.out.println("S'ha mogut el document? " + renArx);
    }

    public static void creaEstructura (File carpeta, File arxiu) { 

        boolean creaDir = carpeta.mkdir();
        // Crea el directori si no existeix.
        if (creaDir) {
            System.out.println("Creat directori " + carpeta.getName() + " en la ruta " + carpeta.getParent() + "? " + creaDir);
            // Sols esborra el directori si no conté arxius.
        } else {
            if (!arxiu.exists()) {
                boolean delDir = carpeta.delete();
                System.out.println("Esborrat directori " + carpeta.getName() + " en la ruta " + carpeta.getParent() + "? " + delDir);
            }
        }
        try {
            boolean creaArx=arxiu.createNewFile();
            if (creaArx) {
                System.out.println("Creat arxiu " + arxiu.getName() + " en la ruta " + arxiu.getParent() + "? " + creaArx);
                // Si no ha creat l'arxiu és perquè ja existia i per tant l'esborra. 
            } else {
                boolean delArx = arxiu.delete();
                if (delArx) {
                    System.out.println("Esborrat arxiu " + arxiu.getName() + " en la ruta " + carpeta.getParent() + "? " + delArx);
                }
            }
        } catch (IOException ioe){
        System.out.println("Error en tractament d'arxiu.");
        }
    }
}
```

:::

## Exemple 6

Llistat de carpetes i arxius continguts en una carpeta.

::: tabs
== Java

```java
package UF10_Exemple06;
import java.io.IOException;
import java.io.File;

/**
 * UF10 Exemple 06: Llistat de carpetes i arxius continguts en una carpeta
 * - Si existeixen carpetes i arxius, els elimina i mostra missatge de carpeta buida.
 * - Si la carpeta està buida, crea carpetes i arxius i ho llista.
 */
public class UF10_Exemple06 {
    public static void main(String[] args) {

        // Creem una carpeta Contingut on es posarà la resta de carpetes i arxius
        String rutaBase = "src/main/java/UF10_Exemple06";
        File carpeta = new File(rutaBase + "/Contingut");
        boolean creaDir = carpeta.mkdir();
        rutaBase += "/Contingut";

        // Omplim o buidem la carpeta Contingut
        creaEstructura(rutaBase);
        // Creem un Array amb els elements que hi ha en la carpeta Contingut
        File dir = new File(rutaBase);
        File[] llista = dir.listFiles();

        System.out.println("Contingut de " + dir.getAbsolutePath() + " :");
        // Si la llista està buida mostrem missatge
        if (llista == null || llista.length == 0) {
            System.out.println("La carpeta està buida.");
        } else { 
            // Si hi ha elements en la llista, recorrem l'Array i es va mostrant el nom de cada element
            for (int i = 0; i < llista.length; i++) {
                File f = llista[i];
                if (f.isDirectory()) {
                    System.out.println("[DIR] " + f.getName());
                } else {
                    System.out.println("[ARX] " + f.getName());
                }
            }
        }
    }

    // Si la carpeta Contingut té carpetes i arxius, els esborrem; si està buida, es creen
    public static void creaEstructura(String rutaBase) {

        // Creació o esborrat de 5 arxius
        for (int i = 1; i <= 5; i++) {
            File arxiu = new File(rutaBase + "/Arxiu" + i + ".txt");
            try {
                boolean creaArx = arxiu.createNewFile();
                if (creaArx) {
                    System.out.println("Creat arxiu " + arxiu.getName() + " en la ruta " + arxiu.getParent() + "? " + creaArx);
                } else {
                    System.out.println("L'arxiu " + arxiu.getName() + " ja existia, s'esborra.");
                    arxiu.delete();
                }
            } catch (IOException e) {
                System.out.println("Error en crear l'arxiu: " + arxiu.getName());
            }
        }

        // Creació o esborrat de 3 carpetes
        for (int i = 1; i <= 3; i++) {
            File subCarpeta = new File(rutaBase + "/Carpeta" + i);
            if (subCarpeta.exists()) {
                System.out.println("La carpeta " + subCarpeta.getName() + " ja existia, s'esborra.");
                eliminarCarpeta(subCarpeta);
            } else {
                boolean creaDir = subCarpeta.mkdir();
                System.out.println("Creada carpeta " + subCarpeta.getName() + "? " + creaDir);
            }
        }
    }

    // Funció auxiliar per eliminar una carpeta i el seu contingut recursivament
    private static void eliminarCarpeta(File carpeta) {
        File[] fitxers = carpeta.listFiles();
        if (fitxers != null) {
            for (File fitxer : fitxers) {
                if (fitxer.isDirectory()) {
                    eliminarCarpeta(fitxer);
                } else {
                    fitxer.delete();
                }
            }
        }
        carpeta.delete();
    }
}
```

:::

## Exemple 7

Llegir valors enters d'un arxiu anomenat "Enters.txt".

Es provocarà diversos errors: arxiu no existeix, arxiu amb dades no numèriques, llegir desprès d'haver arribat al EOF, llig després de tancar l'arxiu.

::: tabs
== Java

```java
package UF10_Exemple07;

import java.io.*;

/**
 * UF10 Exemple 07: Llegir valors enters d'un arxiu anomenat "Enters.txt"
 * Es provocarà diversos errors: arxiu no existeix, arxiu amb dades no numèriques,
 * llegir després d'haver arribat al EOF, llegir després de tancar l'arxiu.
 */
public class UF10_Exemple07 {

    public static void main(String[] args) {
        String ruta = "src/main/java/UF10_Exemple07/Enters.txt";
        int valor;

        try (BufferedReader lector = new BufferedReader(new FileReader(ruta))) {
            String linia;
            // Bucle de lectura fins arribar al final del fitxer
            while ((linia = lector.readLine()) != null) {
                try {
                    valor = Integer.parseInt(linia.trim()); // Convertim la línia a enter
                    System.out.println("El valor llegit és: " + valor);
                } catch (NumberFormatException im) {
                    System.out.println("Error 2: Dada no numèrica -> " + linia);
                    im.printStackTrace();
                }
            }

            // Provocar un error de lectura després de tancar el fitxer
            // lector.readLine(); // Això donaria un error

        } catch (FileNotFoundException nf) {
            System.out.println("Error 1: El fitxer no existeix.");
            nf.printStackTrace();
        } catch (IOException e) {
            System.out.println("Error 5: Error d'E/S.");
            e.printStackTrace();
        }
    }
}
```

:::

## Exemple 8

S'escriuen 20 valors enters , començant per l'1 i cada vegada el doble de l'anterior.

- Si l'arxiu no existeix el crea.
- Si existeix el sobreescriu.

Després obrim de nou l'arxiu i afegim dades, en aquest el creem de forma que no sobreescriga el que ja hi havia.

::: tabs
== Java

```java
package UF10_Exemple08;

import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

/**
 * UF10 Exemple 08: S'escriuen 20 valors enters, començant per l'1 i cada vegada el
 * doble de l'anterior. Després obrim de nou l'arxiu i afegim dades, en aquest cas
 * el creem de forma que no sobreescriga el que ja hi havia.
 */
public class UF10_Exemple08 {

    public static void main(String[] args) {

        // Escriptura inicial. Si no existeix l'arxiu el crea, si existeix el sobreescriu.
        try {
            File f = new File("src/main/java/UF10_Exemple08/Enters.txt");
            BufferedWriter escriptor = new BufferedWriter(new FileWriter(f));

            int valor = 1;
            for (int i = 1; i <= 20; i++) {
                escriptor.write(Integer.toString(valor)); // Escriure valor com a String
                escriptor.write(" "); // Espai en blanc
                valor *= 2; // Calculem pròxim valor
            }
            escriptor.newLine(); // Escriure nova línia
            escriptor.write(Integer.toString(65)); // Escrivim el valor 65 com a text
            escriptor.newLine();
            
            escriptor.close(); // Tanquem el BufferedWriter
            System.out.println("Fitxer escrit correctament");
        } catch (IOException e) {
            System.out.println("Error 1: " + e);
        }

        // Es torna a obrir l'arxiu i s'afig informació sense sobreescriure
        try {
            File f = new File("src/main/java/UF10_Exemple08/Enters.txt");
            BufferedWriter escriptor = new BufferedWriter(new FileWriter(f, true));

            escriptor.newLine(); // Escriure nova línia
            int valor = 65;
            for (int i = 0; i < 20; i++) {
                escriptor.write(Integer.toString(valor + i)); // Escriure valor com a String
                escriptor.write(" "); // Espai en blanc
            }
            escriptor.newLine(); // Escriure nova línia
            
            escriptor.close(); // Tanquem el BufferedWriter
            System.out.println("Fitxer escrit correctament");
        } catch (IOException e) {
            System.out.println("Error 2: " + e);
        }
    }
}
```

:::
