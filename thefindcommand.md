<a href="tryhackme.com/room/thefindcommand">GO TO PLAY THE ROOM</a></br>
<img src="find.jpg" width="50px">
## TASK #2
_____________
1-Find all files whose name ends with **.xml**
Dans cette partie on vous demande de retrouver tous les fichiers qui se terminent par .xml alors
le mieux est d'utiliser les options telles que
- type : pour les types ( fichiers(f) ou dossiers(d)) 
    qui est suivi de l'argument soit f ou d
- name : pour le nom fichiers ou dossiers
    qui est suivi de l'argument qui est le nom et a noter que sur linux il les termes qu'on appelle joker { * = tous, ?= n'importe, ...}
 pour cette 1ere partie vous allez fournir
``` 
find / -type <argument> -name "<joker>.<extensionArechercher>"
``` 
2-Find all files in the /home directory (recursive) whose name is **user.txt** (case insensitive)
Cet partie cet presque la même avec seule différence qu'on demande de travailler avec le répertoire
/home de trouver le fichier user.txt mais insensible à la casse.
on a pour argument -iname : le nom est insensible à la casse.
```
find /<directoryAchercher> -type <f or d> -iname "nomDuFichier.extension"
```
3-Find all directories whose name contains the word **exploits**
```
find / -type <f or d> -name "<joker>MotArechercher<joker>"
```

## TASK #3
___________
1-Find all files owned by the user **kittycat**
Dans cette partie on discute a propos du proprietaire des fichiers et avec find on peut connaitre
le propriétaire d'un fichier avec l'option -user alors la réponse sera:
```
find / -type < f or d > -user <NomDuProprietaire>
```
2- Find all files that are exactly 150 bytes in size
Faut savoir que pour préciser la taille d'un fichier il suffit d'ajouter l'option
-size mais pour savoir la taille en byte il faut ajouter l'argument c suivi de la taille alors la
réponse sera :
```
find / -type <f or d > -size <tailleDuFichier>c
```
3-Find all files in the /home directory (recursive) with size less than 2 KiB’s and extension **.txt**
POUR trouver la taille d'un fichier en KiB's on se sert de l'argument k alors la réponse sera :
```
find /<directory> -type <f or d> -size -<tailleDuFichier>k -name "<joker>.<extension>"
```
4-Find all files that are exactly readable and writeable by the owner, and readable by everyone else (use octal format)
Le format octal c'est le format avec les chiffres exemple 1 jusqu'à 9. la notion de permission sous linux
a été le tourment de chaque utilisateur car c'est compliqué mais je vais résumé pour vous:
___________________________________
Numéro en octal | permission       |
-----------------------------------
1               |   read (r)       |
2               |  written(w)      |
4               |   execute(x)     |

et aussi vous devez savoir que il ya la notion
|rwx|rwx|rwx|
|---|---|---|
|U  | G | E |

- (U)ser; (G)roup ; (E)veryone

et bien c'est ainsi qu'on concluera que pour trouver les droites que ce soit
du User et autres il faut faire l'addition et la soustraction des nombres octal, exemple
4 + 2 = 6, et bien on dira que quelqu'un a le droit wx. si je disais trouver
le fichier dont le User a le droit de read, le group de written et les autres execute alors ce sera en octal
ainsi : 124
Pour le faire avec find on a trois manieres avec l'option -perm qui sera suivi soit du
- ou /
- : quand l'utilisateur doit avoir au moins le droit spécifié
/ : quand l'utilisateur a l'une des droits spécifiés

ainsi la réponse sera 
```
find / -type < f or d> -perm 644
```
où 644 : wx x x

5-Find all files that are only readable by anyone (use octal format)
```
find / -type <f or d> -perm /444
```
où 644 : r r r

6- Find all files with write permission for the group **others**, regardless of any other permissions, with extension **.sh** (use symbolic format)
le format symbolic c'est un format particulier dans l'affichage des droits, exemple
u pour USER, g pour Group et o pour les autres, avec + pour ajouter et - pour enlever et = pour soumettre
des droits a un group ouu user et ignorer les autres
```
find / -type <f or d> -o=w -name "<joker>.sh"
```
7- Find all files in the /usr/bin directory (recursive) that are owned by root and have at least the SUID permission (use symbolic format)
SUID = s 
```
find /usr/bin -type f -user <proprietaire> -permission -u=<SUIDvalue>
```
8-Find all files that were not accessed in the last 10 days with extension **.png**
avoir acces a un fichier est représenté par l'option -a mais pour préciser le temps dans lequel
il faut ajouter l'argument time ainsi on aura -atime
```
find / -type f -atime +<numberOfDays> -name "<joker>.<extension>"
```
9-Find all files in the /usr/bin directory (recursive) that have been modified within the last 2 hours
pour voir les fichiers modifier depuis un temps il faut l'option -m mais pour dire qu'il a été modifié depuis un temps durée il faut préciser l'argument min( minute) et on sait que 1 heure vaut 60 minutes ainsi la réponse sera:

```
find /usr/bin -type <f or d> -mmin -<TempsModifierEnMinute>
```


## FIN
