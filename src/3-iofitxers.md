# 3. Lectura i escriptura de fitxers

Normalment les aplicacions que utilitzen arxius no estan centrades en la gestió del sistema d'arxius del seu ordinador. L'objectiu principal d'usar fitxers és poder emmagatzemar dades de manera que entre diferents execucions del programa, fins i tot en diferents equips, siga possible recuperar-les. El cas més típic és un editor de documents, que mentre s'executa s'encarrega de gestionar les dades relatives al text que està escrivint, però en qualsevol moment pot guardar-lo en un arxiu per a poder recuperar aquest text en qualsevol moment posterior, i afegir altres nous si fos necessari. El fitxer amb les dades del document el pot obrir tant en l'editor del seu ordinador com en el d'un altre company o companya.

Per a saber com tractar les dades d'un fitxer en un programa, cal tenir molt clar com s'estructuren. Dins d'un arxiu es poden emmagatzemar tot tipus de valors de qualsevol mena de dades. La part més important és que aquests valors s'emmagatzemen en forma de seqüència, un darrere l'altre. Per tant, com aviat veureu, la forma més habitual de tractar fitxers és seqüencialment, de manera semblant a com es fa per a llegir-les del teclat, mostrar-les per pantalla o recórrer les posicions d'un array.

::: warning ATENCIÓ
Es denomina **accés seqüencial** al processament d'un conjunt d'elements de manera que només és possible accedir a ells d'acord amb la seva ordre d'aparició. Per a processar un element és necessari processar primer tots els elements anteriors.

:::

Java, juntament amb altres llenguatges de programació, diferencia entre dos tipus d'arxius segons com es representen els valors emmagatzemats en un arxiu.

::: warning ATENCIÓ
En els **fitxers orientats a caràcter**, les dades es representen com una seqüència de cadenes de text, on cada valor es diferencia de l'altre mitjançant un delimitador. En canvi, en els **fitxers orientats a byte**, les dades es representen directament d'acord amb el seu format binari, sense cap separació.
:::

En aquesta unitat didàctica només veurem el processament de fitxers orientats a caràcter.

## 3.1. Fitxers orientats a caràcter

Un fitxer orientat a caràcter no és més que un document de text, com el que es podria generar amb qualsevol editor de text simple. Els valors estan emmagatzemats segons la seva representació en cadena de text, exactament en el mateix format que s'ha utilitzat fins ara per a introduir dades des del teclat. De la mateixa manera, els diferents valors es distingeixen en estar separats entre ells amb un delimitador, que per defecte és qualsevol conjunt d'espais en blanc o salts de línia. Encara que aquests valors es puguin distribuir en línies de text diferents, conceptualment, es pot considerar que estan organitzats un darrere l'altre, seqüencialment, com les paraules en la pàgina d'un llibre.

El següent podria ser el contingut d'un fitxer orientat a caràcter on hi ha deu valors de tipus real, 7 en la primera línia i 3 en la segona:

```plaintext
1.5 0.75 -2.35 18 9.4 3.1416 -15.785  
-200.4 2.56 9.3785  
```

I aquest el d'un fitxer amb 4 valors de tipus String ("Hi", "havia", "una" i "vegada..."):

```plaintext
Hi havia una vegada...  
```

**En un fitxer orientat a caràcter és possible emmagatzemar qualsevol combinació de dades de qualsevol tipus** (int, double, boolean, String, etc.).

```plaintext
7 10 20.5 16.99  
Hi havia una vegada...  
true false 2020 0.1234  
```

El principal avantatge d'un fitxer d'aquest tipus és que resulta molt senzill inspeccionar el seu contingut i generar-lo d'acord amb les nostres necessitats.  

Per al cas dels fitxers orientats a caràcter, cal utilitzar dues classes diferents segons si el que es vol és llegir o escriure dades en un arxiu. Normalment això no és molt problemàtic, ja que **en un bloc de codi donat, només es duran a terme operacions de lectura o d'escriptura sobre un mateix arxiu, però no els dos tipus d'operació alhora**.  

::: warning ATENCIÓ
Per a tractar de manera senzilla fitxers orientats a caràcter, Java proporciona les classes **BufferedReader** (per a lectura) i **BufferedWriter** (per a escriptura) del package **java.io**.
:::

## 3.2. Lectura de fitxer (classe BufferedReader)

**Una manera eficient de llegir dades des d'un fitxer orientat a caràcter és utilitzant la classe BufferedReader.** Aquesta classe permet llegir el contingut d'un arxiu línia per línia de manera eficient, ja que emmagatzema en memòria un conjunt de caràcters per reduir el nombre d'accessos al disc.

Per a processar dades des d'un arxiu, **BufferedReader es crea a partir d'un objecte FileReader**, que especifica la ruta a l'arxiu.

Per exemple, per a crear un objecte de tipus **BufferedReader** de manera que permeta llegir dades des de l'arxiu situat en la ruta "C:\Programes\Unitat10\Document.txt", caldria fer:

::: tabs
== Java

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
...
BufferedReader lectorArxiu = new BufferedReader(new FileReader("C:/Programes/Unitat10/Document.txt"));
...
```

:::

Una vegada instanciat l'objecte **BufferedReader**, podem utilitzar els seus mètodes per llegir el contingut de l'arxiu. El mètode més habitual és **readLine()**, que permet llegir una línia completa del fitxer i avança automàticament a la següent.

És important entendre que **BufferedReader gestiona internament un apuntador que indica sobre quin valor actuarà la següent operació de lectura**. Inicialment, l'apuntador es troba a la primera línia de l'arxiu. **Cada vegada que es crida readLine(), l'apuntador avança fins a la següent línia.**

**És important recordar que readLine() retorna una cadena de text**, que pot necessitar ser convertida al tipus de dada corresponent. Per exemple, per convertir una línia a un número enter, es pot utilitzar **Integer.parseInt()**:

::: tabs
== Java

```java
String linia = lectorArxiu.readLine();
int valor = Integer.parseInt(linia);
```

:::

**Una vegada s'ha finalitzat la lectura de l'arxiu**, ja siga tota o només una part, **és imprescindible executar el mètode close()**. Aquest mètode indica al sistema operatiu que l'arxiu ja no està sent utilitzat pel programa. Si no es crida a **close()**, el sistema operatiu pot mantenir el fitxer bloquejat durant un temps.

::: warning ATENCIÓ
**Sempre cal tancar els arxius amb close() quan s'ha acabat de llegir o escriure en ells.**
:::

Quan es crea un **BufferedReader**, cal tenir en compte que **es pot llançar una excepció de tipus IOException si el fitxer no existeix o si hi ha algun problema en la lectura.** Per tant, és necessari manejar aquesta excepció amb un bloqueig **try-catch**.

El programa següent mostra un exemple de com llegir deu valors enters d'un arxiu anomenat "Enters.txt" situat en la carpeta de treball (hauria de ser la carpeta del projecte NetBeans). Per a provar-ho, crea l'arxiu i introdueix exactament 10 valors enters, un per línia.

::: tabs
== Java

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ProvesFitxers {
    public static final int NUM_VALORS = 10;

    public static void main(String[] args) {
        try {
            // Obrim el fitxer
            BufferedReader lector = new BufferedReader(new FileReader("Enters.txt"));
            
            // Llegim línia per línia
            for (int i = 0; i < NUM_VALORS; i++) {
                String linia = lector.readLine();
                if (linia != null) {
                    int valor = Integer.parseInt(linia);
                    System.out.println("El valor llegit és: " + valor);
                } else {
                    System.out.println("Error: L'arxiu no té suficients línies.");
                    break;
                }
            }
            
            // Cal tancar el fitxer!
            lector.close();
        } catch (IOException e) {
            // En cas d'excepció mostrar l'error
            System.out.println("Error: " + e.getMessage());
            e.printStackTrace();
        } catch (NumberFormatException e) {
            System.out.println("Error: El fitxer conté un format incorrecte.");
        }
    }
}
```

:::

Una diferència important a l'hora de tractar amb arxius respecte a llegir dades del teclat és que les operacions de lectura no són producte d'una interacció directa amb l'usuari, que és qui escriu les dades. Només es pot treballar amb les dades que hi ha en l'arxiu i res més. Això té dos efectes sobre el procés de lectura:

1. **Tipus de dades esperats**: **Quan es duu a terme el procés de lectura d'una seqüència de valors, sempre cal anar amb compte d'usar el mètode adequat per a interpretar el tipus de dada correcte.** Per exemple, si esperem números enters, cal utilitzar **Integer.parseInt()** per convertir el text a un nombre. Cal anar amb compte, ja que si el fitxer té un format incorrecte, es llançarà una excepció **NumberFormatException**.

2. **Comprovació de la disponibilitat de valors**: **També és necessari controlar que mai es llegisquen més valors dels que hi ha disponibles per a llegir.** Intentar llegir una línia quan l'arxiu ja s'ha acabat retorna **null**. Per evitar errors, es pot utilitzar una estructura com un **while**, comprovant si la línia llegida és **null** abans de processar-la.

Per a veure-ho, intenta executar l'exemple anterior modificant l'arxiu de manera que algun dels valors no siguin de tipus sencer, o hi hagi menys de 10 línies.

## 3.3. Escriptura en fitxer (classe BufferedWriter)

Per a escriure dades a un fitxer, anem a usar `BufferedWriter`. Per a instanciar un objecte d'esta classe, primer cal crear un objecte de la classe **FileWriter**, la qual té quatre constructors importants:

- **public FileWriter(File file)**
- **public FileWriter(File file, boolean append)**
- **public FileWriter(String fileName)**
- **public FileWriter(String fileName, boolean append)**

Els primers dos constructors accepten un objecte `File`, mentre que els altres dos permeten passar la ruta directament com a `String`.

Si el fitxer no existeix, es crearà automàticament. Però si ja existeix, el seu contingut s'esborrarà completament, deixant el fitxer amb grandària igual a 0, tret que s'use el mode "append".

::: tabs
== Java

```java
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class ExempleEscriptura {
    public static void main(String[] args) {
        File fitxer = new File("C:/Programes/Unitat11/Document.txt");

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fitxer, true))) {
            writer.write("Aquesta és una nova línia de text.");
            writer.newLine(); // Afegim un salt de línia
            writer.write("Escrivint amb BufferedWriter és més eficient!");
            writer.newLine();
        } catch (IOException e) {
            System.out.println("Error d'escriptura: " + e.getMessage());
        }
    }
}

```

:::

::: warning ATENCIÓ
Tant el constructor de `FileWriter`, com el de `BufferedWriter`, com el mètode `write()` poden llançar una excepció `IOException`.
:::

### 3.3.1. Conversió de valors a String

El mètode `write(int c)` escriu el caràcter Unicode associat al codi passat per paràmetre. Per exemple:

::: tabs
== Java

```java
writer.write("8"); // Escriu el caràcter '8'
writer.write(65); // Escriu 'A' (codi ASCII/Unicode 65)
```

:::

Si es volen escriure nombres o altres tipus de dades, cal convertir-los a `String`, per exemple:

::: tabs
== Java

```java
int edat = 35;
writer.write("" + edat); // Escriu "35"
```

:::

### 3.3.2. Necessitat de close() i try-with-resources

L'escriptura en fitxers pot realitzar-se de manera diferida pel sistema operatiu. Per a garantir que les dades es guarden correctament, és essencial cridar `close()` al final. A més, `close()` allibera el fitxer perquè altres programes puguen accedir-hi.

Un enfocament més segur és usar `try-with-resources`, que tanca automàticament el `FileWriter`:

::: tabs
== Java

```java
try (FileWriter fw = new FileWriter("Enters.txt")) {
    fw.write("Hola món!");
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
```

:::

### 3.3.3. Exemple complet

El següent programa escriu un fitxer anomenat `Enters.txt` amb 20 nombres enters, començant per 1 i doblant cada vegada el valor anterior.

::: tabs
== Java

```java
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class EscriureFitxer {
    public static void main(String[] args) {
        try {
            File f = new File("Enters.txt");
            FileWriter fw = new FileWriter(f, true); // Mode append activat
            BufferedWriter bw = new BufferedWriter(fw); // Afegim BufferedWriter

            int valor = 1;
            for (int i = 1; i <= 20; i++) {
                bw.write(valor + " ");
                valor *= 2;
            }
            bw.newLine(); // Escriu un salt de línia correcte segons el sistema operatiu

            // Important: Tanquem BufferedWriter (tanca també FileWriter)
            bw.close();
            
            System.out.println("Fitxer escrit correctament");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

:::

D'esta manera, el programa aniria afegint 20 nous nombres al final del fitxer en cada execució.
