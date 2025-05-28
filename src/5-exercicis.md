# Exercicis

## Exercicis (A) - Gestió de fitxers

Per a provar aquests exercicis cal utilitzar l'arxiu *Documents.zip*. Descarrega-ho de l'aula virtual i descomprimeix-ho en la carpeta de cada projecte que crees.

## Exercici A1 - Mostrar informació de fitxers

Implementa un programa que demane a l'usuari introduir per teclat una ruta del sistema d'arxius (per exemple, "C:/Windows" o "Documents") i mostre informació sobre aquesta ruta (veure funció més a baix). El procés es repetirà una vegada i una altra fins que l'usuari introduïsca una ruta buida (tecla intro). Haurà de manejar les possibles excepcions.

Necessitaràs crear la funció `void mostraInfoRuta(File ruta)` que donada una ruta de tipus `File` faça el següent:

- Si és un arxiu, mostrarà per pantalla el nom de l'arxiu.
- Si és un directori, mostrarà per pantalla la llista de directoris i arxius que conté (els seus noms). Haurà de mostrar primer els directoris i després els arxius.
- En qualsevol cas, afig davant del nom l'etiqueta **[D]** o **[A]** per a indicar si és un directori o un arxiu respectivament.
- Si el path no existeix llançarà un `FileNotFoundException`.

## Exercici A2 - Mostrar informació de fitxers (v2)

Partint d'una còpia del programa anterior, modifica la funció `mostraInfoRuta`:

- En el cas d'un directori, mostrarà la llista de directoris i arxius en ordre alfabètic. És a dir, primer els directoris en ordre alfabètic i després els arxius en ordre alfabètic. Et serà útil `Arrays.sort()`.
- Afig un segon argument `boolean info` que quan siga `true` mostrarà, al costat de la informació de cada directori o arxiu, la seua grandària en bytes i la data de l'última modificació. Quan **info** siga `false` mostrarà la informació com en l'exercici anterior.

## Exercici A3 - Canviant de nom directoris i fitxers

Implementa un programa que faça el següent:

- Canviar el nom de la carpeta **Documents** a **DOCS**, el de la carpeta **Fotografias** a **FOTOS** i el de la carpeta **Libros** a **LECTURAS**.
- Canviar el nom de tots els arxius de les carpetes **FOTOS** i **LECTURES** llevant-li l'extensió. Per exemple, astronauta.jpg passarà a dir-se astronauta.

## Exercici A4 - Creant (i movent) carpetes

Implementa un programa que cree, dins de **Documents**, dues noves carpetes: **Les meues Coses** i **Alfabet**. Mou les carpetes **Fotografias** i **Libros** dins de **Les meues Coses**. Després crea dins de **Alfabet** una carpeta per cada lletra de l'alfabet (en majúscules): **A**, **B**, **C**... **Z**. Et seran d'ajuda els codis numèrics ASCII: [https://elcodigoascii.com.ar](https://elcodigoascii.com.ar).

## Exercici A5 - Esborrant arxius

Implementa un programa amb una funció `boolean esborraTot(File f)` que esborre `f`:  

- Si no existeix llançarà una excepció.  
- Si és un arxiu l'esborrarà.  
- Si és un directori, esborrarà primer els seus arxius i després el propi directori (recorda que per a poder esborrar un directori ha d'estar buit).  
- Retornarà `true` si va poder esborrar el `File f` (`false` si no ha sigut possible).  

Prova la funció esborrant les carpetes:

- `Documents/Fotografias`  
- `Documents/Libros`  
- `Documents`  

(és a dir, tres anomenades a la funció, en aqueix ordre).

**Super extra challenge:** Aquesta funció, tal com està definida, no esborrarà les subcarpetes que estiguen dins d'una carpeta (per a això caldria esborrar primer el contingut d'aquestes subcarpetes). Se t'ocorre com podria fer-se? Intenta-ho si t'animes ;-)

---

## Cas pràctic A - MiniTerminal & MiniFileManager

Implementa un programa que funcione com una xicoteta terminal Linux amb alguns comandos (simplificats) que permeten a l'usuari realitzar diferents operacions de gestió d'arxius.  

Els comandos que l'usuari podrà executar són:  

- `pwd`: Mostra com és la carpeta actual.
- `cd <DIR>`: Canvia la carpeta actual a **DIR**. Amb `..` canvia a la carpeta superior.
- `ls`: Mostra la llista de directoris i arxius de la carpeta actual (primer directoris, després arxius, tots dos ordenats alfabèticament).
- `ll`: Com `ls` però mostra també la grandària i la data d'última modificació.
- `mkdir <DIR>`: Crea el directori **DIR** en la carpeta actual.
- `rm <FILE>`: Esborra **FILE**. Si és una carpeta, esborrarà primer els seus arxius i després la carpeta. Si té subcarpetes, les deixarà intactes i mostrarà un avís a l'usuari.
- `mv <FILE1> <FILE2>`: Mou o canvia el nom a **FILE1** a **FILE2**.
- `help`: Mostra una breu ajuda amb els comandos disponibles.
- `exit`: Acaba el programa.

### Classe MiniTerminal

Classe principal (amb funció `main`) que s'encarregarà d'interactuar amb l'usuari i interpretar els comandos (quin comando es demana, arguments, etc.). Utilitzarà la segona classe per a realitzar les operacions de gestió d'arxius. Manejarà totes les possibles excepcions.  

### Classe MiniFileManager

Tindrà els atributs i mètodes que necessites per a realitzar les diferents operacions relacionades amb la gestió d'arxius. Necessitaràs almenys un mètode per cada operació. Es llançarà una excepció si es produeix un error o l'operació sol·licitada no és possible.  

Alguns exemples que podries implementar:  

- `String getPWD()`: Retorna una cadena de text amb la carpeta actual.  
- `boolean changeDir(String dir)`: Canvia la carpeta actual a **dir**. Retorna `true` si va ser possible.  
- `void printList(boolean info)`: Mostra una llista amb els directoris i arxius de la carpeta actual. Si **info** és `true` mostrarà també la seua grandària i data de modificació.  
- etc.  

## Exercicis (B) - Lectura i escriptura de fitxers

Per a provar aquests exercicis cal utilitzar l'arxiu *Documents.zip*.

## Exercici B1 - Màxim i mínim

Implementa un programa que mostre per pantalla els valors màxims i mínims de l'arxiu *numeros.txt*.

## Exercici B2 - Notes d'alumnes

L'arxiu *alumnes_notes.txt* conté una llista de 10 alumnes i les notes que han obtingut en cada assignatura. El nombre d'assignatures de cada alumne és variable. Implementa un programa que mostre per pantalla la nota mitjana de cada alumne al costat del seu nom i cognom, ordenat per nota mitjana de major a menor.

## Exercici B3 - Ordenant arxius

Implementa un programa que demane a l'usuari un nom d'arxiu A per a lectura i un altre nom d'arxiu B per a escriptura. Llegirà el contingut de l'arxiu A (per exemple ‘usa_persones.txt’) i ho escriurà ordenat alfabèticament en B (per exemple ‘usa_persones_sorted.txt’).

## Exercici B4 - Nom i cognoms

Implementa un programa que genere aleatòriament noms de persona (combinant noms i cognoms de ‘usa_noms.txt’ i ‘usa_cognoms.txt’). Se li demanarà a l'usuari quants noms de persona desitja generar i a quin arxiu afegir-los (per exemple ‘usa_persones.txt’).

## Exercici B5 - Diccionari

Implementa un programa que cree la carpeta ‘Diccionari’ amb tants arxius com lletres de l'abecedari (A.txt, B.txt… Z.txt). Introduirà en cada arxiu les paraules de ‘diccionari.txt’ que comencen per aquesta lletra.

## Exercici B6 - Cerca en PI

Implementa un programa que demane a l'usuari un número de qualsevol longitud, com per exemple “1234”, i li diga a l'usuari si aquest número apareix en el primer milió de decimals del número pi (estan en l'arxiu *pi-million.txt*). No està permés utilitzar cap llibreria ni classe ni mètode que realitze la cerca. Has d'implementar l'algorisme de cerca tu mateix.

## Exercici B7 - Estadístiques

Implementa un programa que llija un document de text i mostre per pantalla algunes dades estadístiques: nombre de línies, nombre de paraules, nombre de caràcters i quines són les 10 paraules més comunes (i quantes vegades apareixen). Prova el programa amb els arxius de la carpeta *Llibres*.