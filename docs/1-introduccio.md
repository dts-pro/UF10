# 1. Introducció

La principal funció d'una aplicació informàtica és la manipulació i transformació de dades. Aquestes dades poden representar coses molt diferents segons el context del programa: notes d'estudiants, una recopilació de temperatures, les dates d'un calendari, etc. Les possibilitats són il·limitades. Totes aquestes tasques de manipulació i transformació es duen a terme normalment mitjançant l'emmagatzematge de les dades en variables, dins de la memòria de l'ordinador, per la qual cosa es poden aplicar operacions, ja siga mitjançant operadors o la invocació de mètodes.

Desgraciadament, totes aquestes variables només tenen vigència mentre el programa s'està executant. Una vegada el programa finalitza, les dades que contenen desapareixen. Això no és problema per a programes que sempre tracten les mateixes dades, que poden prendre la forma de literals dins del programa, o quan el nombre de dades a tractar és xicotet i es pot preguntar a l'usuari. Ara bé, imagineu-vos haver d'introduir les notes de tots els estudiants cada vegada que s'executa el programa per a gestionar-les. No té cap sentit.

Per tant, en alguns casos, apareix la necessitat de poder registrar les dades en algun suport de memòria externa perquè es mantinguen de manera persistent entre diferents execucions del programa, o fins i tot si s'apaga l'ordinador.

La manera més senzilla d'aconseguir aquest objectiu és emmagatzemar la informació aprofitant el sistema d'arxius que ofereix el sistema operatiu. Mitjançant aquest mecanisme, és possible tindre les dades en un format fàcil de manejar i independent del suport real, ja siga un suport magnètic com un disc dur, una memòria d'estat sòlid com un llapis de memòria USB, un suport òptic, cinta, etc.

En aquesta unitat didàctica s'expliquen diferents classes de Java que ens permeten crear, llegir, escriure i eliminar fitxers i directoris, entre altres operacions. També s'introdueix la serialització d'objectes com a mecanisme de gran utilitat per a emmagatzemar objectes en fitxers i després recuperar-los en temps d'execució.
