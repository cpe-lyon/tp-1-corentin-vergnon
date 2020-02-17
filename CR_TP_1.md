# Administration Système Linux - TP n°1

## Manuel

1. A l'aide du manuel, identifiez le rôle de la commande which.

which [-a] nom_de_fichier

Renvoie le chemin des fichiers (ou liens) qui seraient exécutés dans l'environnement courant si ses arguments avaient été donnés comme commandes dans un interpréteur de commandes strictement conforme à POSIX. Pour ce faire, which cherche dans la variable PATH les fichiers exécutables correspondant aux noms des arguments. Which ne normalise pas les chemins.

Code de retour : 
- 0 si toutes les commandes spécifiées sont trouvées et exécutables.
- 1 si une (ou plusieurs) commande spécifiée n'existe pas ou n'est pas exécutable.
- 2 si une option non valable est spécifiée.


2. Quand on consulte une page du manuel, comment peut-on rechercher un terme (par exemple, chercher le terme option dans la page de manuel de which?

man which permet de rentrer dans le manuel de la commande which.
Il suffit ensuite de taper "/option", ce qui va surligner toutes les occurrences de "option" dans le manuel.

3. Comment quitte-t-on le manuel ?

Il suffit d'utiliser la touche "q".

4. Chaque section du manuel a une première page, qui présente le contenu de la section. Afficher la première page de la section 6 : de quoi parle cette section ?

Commande : man 6 intro
intro est le nom de la première page.

## Navigation dans l'arborescence des fichiers

1. Allez dans le dossier /var/log

Commande : cd var/log

2. Remontez dans le dossier parent (/var) en utilisant un chemin relatif.

Rappel : Un chemin relatif identifie une ressource à partir du répertoire courant. Il dépend donc du répertoire courant et n’est pas valide partout.

Commande : cd ..

Permet de retourner dans le dossier parent.

3. Retournez dans le dossier personnel.

Commande : cd ../home/corentin_vergnon/

4. Revenez au dossier précédent (/var) sans utiliser de chemin.

Commande : cd -

Permet de revenir au dossier précédent.

5. Essayez d'accéder au dossier /root : que se passe-t-il ?

Nous avons le message d'erreur suivant : 
-bash: cd: root: Permission denied

6. Essayez la commande sudo cd /root : que se passe-t-il ? Expliquez.

Nous avons le message d'erreur suivant.
sudo: cd: commande not found

C'est un résultat assez étrange. La commande sudo devrait normalement nous donner les droits d'accéder au dossier root.


7. A partir de votre dossier personnel, créez une arborescence de dossiers.

On se positionne d'abord dans notre dossier personnel.
cd home/corentin.vergnon

On crée ensuite les deux dossiers.
mkdir dossier1
mkdir dossier2

On rajoute un fichier dans le dossier1.
touch dossier1/fichier1

On crée deux autres dossiers dans le dossier2.
mkdir dossier2/dossier2.1
mkdir dossier2/dossier2.2

Enfin, on crée deux autres fichiers dans le dossier 2.2
touch dossier2/dossier2.2/fichier2
touch dossier2/dossier2.2/fichier3

8. Revenez dans le dossier personnel : à l'aide de la commande rm, essayez de supprimer Fichier1, puis Dossier1 : que se passe-t-il ?

On supprime le fichier1 avec la commande suivante : 
rm dossier1/fichier1
Le fichier est supprimé.

On essaye ensuite de supprimer le dossier1 avec la commande suivante : 
rm dossier1
Le dossier n'est pas supprimé, et on obtient le message d'erreur suivant : 
rm: cannot remove 'dossier_1' : Is a directory.

9. Quelle commande permet de supprimer un dossier ?

La commande qui permet de supprimer un dossier est "rmdir".

10. Que se passe-t-il quand on applique cette commande à Dossier2 ?

On obtient le message d'erreur suivant : 
rmdir : failed to remove 'dossier2': Directory not empty

Le dossier2 contient des dossiers qui contiennent eux-mêmes des fichiers. Il est donc impossible de le supprimer avec cette commande.

11. Comment supprimer en une seule commande Dossier2 et son contenu ? 

rm -rf dossier
L'argument -rf permet de supprimer le dossier ainsi que son contenu.

## Commandes importantes

1. Quelle commande permet d'afficher l'heure ? A quoi sert la commande time ?

Commande : date +%R

date permet d'afficher l'heure du système.
L'argument + permet de définir le format qu'on souhaite obtenir.
%R permet de récupérer uniquement l'heure de la date.

Description de la commande time :
La fonction time lance le programme représenté par la commande indiquée, avec les arguments fournis. Lorsque la commande se termine, time affiche un message sur la sortie d'erreur contenant des statistiques sur l'exécution du programme. Ces statistiques contiennent 
- le temps écoulé entre l'invocation et la fin de la commande
- le temps CPU écoulé en mode utilisateur (la somme des valeurs tms_utime et tms_cutime de la structure struct tms fournie par l'appel système times(2))
- le temps CPU passé en mode système (la somme des champs tms_stime et tms_cstime de la struct tms fournie par l'appel système times(2)). 


2. Dans votre dossier personnel, tapez successivement les commandes ls puis la : que peut-on déduire sur les fichiers commençant par un point.

La commande ls n'affiche rien.
La commande la affiche plusieurs fichiers/dossiers commençant par un point.

On peut en déduire que ces fichiers et dossiers sont des fichiers systèmes qui sont cachés par défaut.

Rappel : 
La commande ls lite tous les fichiers d'un dossier.
L'argument -a liste aussi les fichiers cachés.
L'argument -l affiche les détails.

3. Où se situe le programme ls ?

On utilise la commande which ls. 
On obtient ceci : /usr/bin/ls


4. Essayez la commande ll. Existe-t-il une entrée de manuel pour cette commande ? Utilisez les commandes alias ou alias pour en savoir plus sur la nature de cette commande.

La commande man ll nous renvoie le message suivant : 
"No manuel entry for ll". 
Il n'y a donc pas de manuel pour cette commande.

La commande alias ll nous renvoie ceci :
alias ll='ls -alF'

On peut en déduire que alias permet de créer des raccourcis de commande, et que ll permet d'utiliser la commande ls avec les arguments -alF.

5. Quelle commande permet d'afficher les fichiers contenus dans le dossier /bin ?

La commande qui permet d'afficher les fichiers contenus dans le fichier est ls /bin.

6. Que fait la commande ls .. ?

Cette commande permet d'afficher les fichiers du dossier parent.

7. Quelle commande donne le chemin complet du dossier courant ?

La commande pwd permet de connaître le chemin complet du dossier courant.

8. Que fait la commande echo 'yo' > plop exécutée 2 fois ?

Cette commande va créer un fichier nommé plop et va écrire "yo" dans ce fichier.
Le fait d'éxecuter cette commande deux fois ne change rien, puisque la deuxième commande va simplement supprimer le fichier plop existant pour le refaire à l'identique.

En résumé : > permet d'écraser un fichier et son contenu.

9. Que fait la commande echo 'yo' >> plop exécutée 2 fois ?

Cette commande va créer un fichier nommé plop et va écrire "yo" dans ce fichier.
Lors de la deuxième exécution de la commande, "yo" va être rajouté à la fin du fichier plop créé précédemment.

En résumé : >> permet d'écrire à la fin d'un fichier sans en écraser le contenu.

10. A quoi sert la commande file ? Essayez la sur des fichiers de types différents.

La commande file permet de déterminer le type d'un fichier indépendamment de son extension.


11. Créez un fichier toto qui contient la chaîne "Hello Toto !". Créer ensuite un lien titi vers ce fichier avec la commande ln toto titi. Modifiez à présent le contenu de toto et affichez le contenu de titi. Qu'observe-t-on ? Supprimez le fichier toto : quelle conséquence cela a-t-il sur titi ?

On crée tout d'abord le fichier avec son contenu en utilisant la commande echo "Hello Toto !" > toto.
On utilise la commande ln toto titi. Elle permet de créer un fichier qui est un lien vers le fichier toto. En utilisant cat titi, on obtient "Hello Toto !".

On modifie le contenu de toto en utilisant la commande 
echo "ModificationToto" >> toto.

On réaffiche le contenu de titi avec cat titi, et on obtient :
Hello Toto !
ModificationToto

On observe que fichier titi a bien été modifié à la suite de la modification du fichier principal. 

On supprime le fichier toto avec rm toto, puis on réaffiche le contenu de titi. On obtient :
Hello Toto !
ModificationToto

Il n'y a pas de conséquence. Toto et titi étaient deux références différentes qui pointaient vers le même fichier. Titi peut exister sans toto.

12. Créez à présent un lien symbolique tutu sur titi avec la commande ln -s titi tutu. Modifiez le contenu de titi. Quelle conséquence pour tutu ? Et inversement ? Supprimez le fichier titi. Quelle conséquence cela a-t-il sur tutu ?

On modifie le contenu de titi avec la commande 
echo "Modif2" >> titi

En utilisant cat pour afficher le contenu des deux fichiers, on obtient le même résultat :
Hello Toto !
ModificationToto
Modif2

On modifit cette fois-ci le contenu de tutu avec la commande
echo "Modif3" >> tutu

Encore une fois, en utilisant cat pour afficher le contenu des deux fichiers, on obtient le même résultat :
Hello Toto !
ModificationToto
Modif2
Modif3

On supprime cette fois-ci le fichier titi avec la commande rm titi.
En utilisant cat tutu, on obtient le message suivant :
cat: tutu: No such file or directory

tutu est un raccourci vers titi, et comme titi n'existe plus, on ne trouve plus le fichier.

13. Affichez à l'écran le fichier /var/log/syslog. Quels raccourcis clavier permettent d'interrompre et reprendre le défilement de l'écran ?

Le raccourci Ctrl+Z permet d'interrompre le défilement à l'écran.
Pour reprendre le défilement, il suffit de taper la commande fg.

14. Affichez les 5 premières lignes du fichier /var/log/syslog, puis les 15 dernières, puis seulement les lignes 10 à 20.

Pour afficher les 5 premières lignes :
head -5 /var/log/syslog

Pour afficher les 15 premières lignes :
tail -15 /var/log/syslog

Pour afficher les lignes de 10 à 20 :
head -20 /var/log/syslog | tail -10 /var/log/syslog


15. Que fait la commande dmesg | less ?



16. Affichez à l'écran le fichier /etc/passwd. Que contient-il ? Quelle commande permet d'afficher la page de manuel de ce fichier ?

Ce fichier est une base de données textuelle d'informations sur les utilisateurs qui peuvent se connecter au système.

La commande qui permet d'afficher la page de manuel de ce fichier est man passwd.

17. Affichez seulement la première colonne triée par ordre alphabétique inverse.

Tout d'abord, on récupère la première colonne avec la commande suivante :
cut -d":" -f1 /etc/passwd

-d permet de définir le séparateur (ici, :), tandis que -f permet de définir les commandes à récupérer.

Il faut ensuite trier dans l'ordre alphabétique inverse avec la commande sort -r.

On combine les deux avec un | pour obtenir la réponse finale.

cut -d":" -f1 /etc/passwd | sort -r


18. Quelle commande nous donne le nombre d'utilisateurs ayant un compte sur cette machine (pas seulement les utilisateurs connectés) ?

On utilise la commande cut -d":" -f1 /etc/passwd | wc -l

On obtient le résultat 31. 


19. Combien de pages de manuel comportent le mot-clé conversion dans leur description ?

Commande : man -k conversion | wc -l

20. A l'aide de la commande find, recherchez tous les fichiers se nommant passwd présents sur la machine.

Commande : sudo find / -name passwd

On obtient une liste des chemins menant aux fichiers se nommant passwd. 

En utilisant wc -l, on peut voir qu'il existe 21 fichiers ayant pour nom passwd.

21. Modifiez la commande précédente pour que la liste des fichiers trouvés soit enregistrée dans le fichier~/list_passwd_files.txt et que les erreurs soient redirigées vers le fichier spécial /dev/null.

Commande : find / -name passwd 2> /dev/null > ~/list_passwd_files.txt

2> permet de rediriger les éventuelles erreurs dans le fichier à la suite.

22. Dans votre dossier personnel, utilisez la commande grep pour chercher où est défini l’alias ll vu précédemment

23. Utilisez la commande locate pour trouver le fichier history.log.

Commande : locate history.log

On obtient un message d'erreur nous disant d'installer la commande suivante :
sudo apt install mlocate

On réexecute la commande et on obtient :
/var/log/apt/history.log

24. Créer un fichier dans votre dossier personnel puis utilisez locate pour le trouver. Apparaît-il ? Pourquoi ?

On utilise touch pour créer un fichier.
La commande locate n'arrive pas à localiser le fichier.


## Personnalisation du shell

1. Commencez par créer une copie de ce fichier, que vous appellerez .bashrc_bak.

Commande : cp ~/.bashrc ./bashrc_bak


3. Le fichier.bashrcest lu au démarrage du shell; pour le recharger, il faudrait donc se déconnecter puis se reconnecter; mais il existe un autre moyen : la commande source .bashrc. Testez-la, l’invite de commande devrait immédiatement passer en couleurs.

Après avoir modifié le fichier en utilisant nano .bashrc, l'utilisation de la commande source .bashrc passe le texte du shell en vert.












