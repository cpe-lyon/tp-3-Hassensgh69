# TP 3 - Utilisateurs, groupes et permissions
## Exercice 1. Gestion des utilisateurs et des groupe


1.   Utilisez la commande groupadd pour créer deux groupes dev et infra  


          sudo groupadd infra
          sudo groupadd dev

2.   Créez ensuite 4 utilisateurs alice, bob, charlie, dave avec la commande useradd, en demandant la
création de leur dossier personnel et avec bash pour shell
      
     Utilisateur alice :  
     
          sudo useradd -m alice
          sudo usermod --shell /bin/bash alice
          sudo grep alice /etc/passwd
          
          
     Utilisateur bob :
          
          sudo useradd -m bob
          sudo usermod --shell /bin/bash bob
          sudo grep bob /etc/passwd
          
        
     Utilisateur charlie :
          
          sudo useradd -m charlie
          sudo usermod --shell /bin/bash charlie
          sudo grep charlie /etc/passwd     
   
     Utilisateur dave :
          
          sudo useradd -m dave
          sudo usermod --shell /bin/bash dave
          sudo grep dave /etc/passwd      
          
    
  3. Ajoutez les utilisateurs dans les groupes créés :
    
    GROUPE DEV :

          usermod -a -G dev alice
          usermod -a -G dev bob 
          usermod -a -G dev dave
          
    GROUPE INFRA :
    
          usermod -a -G infra bob
          usermod -a -G infra charlie 
          usermod -a -G infra dave
                 
          
   4. Donnez deux moyens d’afficher les membres de infra

    
          grep infra /etc/group
          getent group dinfra
          
  5. Faites de dev le groupe propriétaire des répertoires /home/alice et /home/bob et de infra le groupe
propriétaire de /home/charlie et /home/dave

           sudo chgrp -R dev /home/alice
           sudo chgrp -R dev /home/bob
           sudo chgrp -R infra /home/charlie
           sudo chgrp -R infra /home/dave
           
  6. Remplacez le groupe primaire des utilisateurs :
- dev pour alice et bob
- infra pour charlie et dave
          
   Groupe dev :
   
          sudo usermod alice -g dev
          sudo usermod bob -g dev
          
   Groupe infra:
   
          sudo usermod charlie -g infra
          sudo usermod dave -g infra
          
          
 7.  Créez deux répertoires /home/dev et /home/infra pour le contenu commun aux membres de chaque
groupe, et mettez en place les permissions leur permettant d’écrire dans ces dossiers:


          sudo mkdir /home/dev
          sudo mkdir /home/infra
          
          sudo chgrp -R infra /home/infra
          sudo chgrp -R dev /home/dev
          sudo chmod g+w /home/infra
          sudo chmod g+w /home/dev

8.  Comment faire pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer
ou supprimer ce fichier ? 

          
          sudo chmod 700 " repertoire "
          
          
          
 9.  Pouvez-vous ouvrir une session en tant que alice ? Pourquoi ? 
  
  
  On ne peut pas ouvrir une session avec son compte car son compte n'est pas activé.
  
  
  
 10.   Activez le compte de l’utilisateur alice et vérifiez que vous pouvez désormais vous connecter avec son
compte.

             sudo passwd alice
          
  On peut maintenant se connecter avec le compte d'alice        

          
 11. Comment obtenir l’uid et le gid de alice ?

          id alice
 
 12. Quelle commande permet de retrouver l’utilisateur dont l’uid est 1003 ?

          id 1003
          

13. Quel est l’id du groupe dev ?
         
         grep dev /etc/group
         dev:x:1002:alice,bob,dave
         
14. Quel groupe a pour gid 1002 ? 
    
    C'est le groupe dev
    
15. Retirez l’utilisateur charlie du groupe infra. Que se passe-t-il ? Expliquez.

          sudo gpasswd --delete charlie infra
     
     Apres avoir fait ca l'utilisateur charlie est definitivement supprimer
     
 16. Modifiez le compte de dave de sorte que :
 
 il expire au 1er juin 2021 : 
 
          chage -e 2021-06-01 dave
 
 il faut changer de mot de passe avant 90 jours :
 
          chage -M 90 dave
 
 il faut attendre 5 jours pour modifier un mot de passe :

          chage -m 5 dave

 l’utilisateur est averti 14 jours avant l’expiration de son mot de passe :

          chage -W 14 dave

 le compte sera bloqué 30 jours après expiration du mot de passe : 
                    
           chage -I 30 dave              
           
 
17. Quel est l’interpréteur de commandes (Shell) de l’utilisateur root ?

        

18. Si vous regardez la liste des comptes présents sur la machine, vous verrez qu’il en existe un nommé
nobody. A quoi correspond-il ?

Nobody est le nom conventionnel d'un compte d'utilisateur à qui aucun fichier n'appartient, qui n'est dans aucun groupe qui a des privilèges et dont les seules possibilités sont celles que tous les "autres utilisateurs" ont.

          grep nobody /etc/passwd
          nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
          
          
 19. Par défaut, combien de temps la commande sudo conserve-t-elle votre mot de passe en mémoire ?
Quelle commande permet de forcer sudo à oublier votre mot de passe ? 

La coommande sudo conserve en memoire notre mot de passe pendant 15 minutes

La commande suivante permet de forcer sudo a oublier notre mote de passe :
          
          sudo -k
          
          
## Exercice 2. Gestion des permissions  

1. Dans votre $HOME, créez un dossier test, et dans ce dossier un fichier fichier contenant quelques lignes de texte. Quels sont les droits sur test et fichier ?

![image](https://user-images.githubusercontent.com/80455696/191705801-d84f532d-847d-4901-a0eb-a433f6aef6e3.png)

2. Retirez tous les droits sur ce fichier (même pour vous), puis essayez de le modifier et de l’afficher en tant que root. Conclusion ?

L'utilisateur root peut toujours tout faire car il aura tout le temps tout les droits.

![image](https://user-images.githubusercontent.com/80455696/191706392-c184920f-c170-45aa-9bf4-c9135d7b779e.png)

3. Redonnez vous les droits en écriture et exécution sur fichier puis exécutez la commande echo "echo Hello" > fichier. On a vu lors des TP précédents que cette commande remplace le contenu d’unfichier s’il existe déjà. Que peut-on dire au sujet des droits ?

![image](https://user-images.githubusercontent.com/80455696/191706941-7206a126-8703-4c6e-bf01-9b3c86e21089.png)

On peut modifier le fichier sans avoir besoinde l'utilisateur ROOT.

4. Essayez d’exécuter le fichier. Est-ce que cela fonctionne ? Et avec sudo ? Expliquez.

Oui on peut executer le fichier avec ou sans root car on lui adonner tout les droits avec la commande chmod 777 fichier

5. Placez-vous dans le répertoire test, et retirez-vous le droit en lecture pour ce répertoire. Listez le contenu du répertoire, puis exécutez ou affichez le contenu du fichier fichier. Qu’en déduisez-vous ?Rétablissez le droit en lecture sur test.

On ne peut plus lister le contenu du fichier car nous nous sommes enlever les droits.

6. Créez dans test un fichier nouveau ainsi qu’un répertoire sstest. Retirez au fichier nouveau et au répertoire test le droit en écriture. Tentez de modifier le fichier nouveau. Rétablissez ensuite le droiten écriture au répertoire test. Tentez de modifier le fichier nouveau, puis de le supprimer. Que pouvezvous déduire de toutes ces manipulations ?

En enlevant le droit en ecriture l'user ne peut plus modifie le fichier nouveau ainsi seul root pourra le faire, il faut ainsi obligatoirement le droit en ecriture pour l'user afin qu'il puisse modifier un fichier dans un reperoire.


7. Positionnez vous dans votre répertoire personnel, puis retirez le droit en exécution du répertoire test.
Tentez de créer, supprimer, ou modifier un fichier dans le répertoire test, de vous y déplacer, d’en
lister le contenu, etc…Qu’en déduisez vous quant au sens du droit en exécution pour les répertoires ?

On peut en conclure que sans les droits d'execution on ne peut rien manipuler sur un dossier.


8. Rétablissez le droit en exécution du répertoire test. Positionnez vous dans ce répertoire et retirez lui
à nouveau le droit d’exécution. Essayez de créer, supprimer et modifier un fichier dans le répertoire
test, de vous déplacer dans ssrep, de lister son contenu. Qu’en concluez-vous quant à l’influence des
droits que l’on possède sur le répertoire courant ? Peut-on retourner dans le répertoire parent avec ”cd
..” ? Pouvez-vous donner une explication ?

Les droits d'un fichier sont separés de ceux d'un dossier c'est a dire que les droits d'xecution d'un dossier n'influent pas sur ceux des fichiers qu'ils contient.

9. Rétablissez le droit en exécution du répertoire test. Attribuez au fichier fichier les droits suffisants
pour qu’une autre personne de votre groupe puisse y accéder en lecture, mais pas en écriture.

          chmod 740 fichier
          
10. Définissez un umask très restrictif qui interdit à quiconque à part vous l’accès en lecture ou en écriture,
ainsi que la traversée de vos répertoires. Testez sur un nouveau fichier et un nouveau répertoire.

![image](https://user-images.githubusercontent.com/80455696/191808371-77a6d17f-f13f-4d61-a66b-35f1759b9ec8.png)

11.Définissez un umask très permissif qui autorise tout le monde à lire vos fichiers et traverser vos répertoires, mais n’autorise que vous à écrire. Testez sur un nouveau fichier et un nouveau répertoire.

![image](https://user-images.githubusercontent.com/80455696/191808874-83a24cee-b9d8-4f1c-bc09-3357da0a30cd.png)

12. Définissez un umask équilibré qui vous autorise un accès complet et autorise un accès en lecture aux
membres de votre groupe. Testez sur un nouveau fichier et un nouveau répertoire.

 ![image](https://user-images.githubusercontent.com/80455696/191809303-4fc7f8de-0d40-4433-bc54-7ea068b8199f.png)
                  
13. Transcrivez les commandes suivantes de la notation classique à la notation octale ou vice-versa (vous
pourrez vous aider de la commande stat pour valider vos réponses) :

- chmod 534 fic
- chmod 602 fic
- chmod rw-r-x--wx fic
- chmod 520 fic

14. Affichez les droits sur le programme passwd. Que remarquez-vous ? En affichant les droits du fichier
/etc/passwd, pouvez-vous justifier les permissions sur le programme passwd ?

          ls -l /etc/passwd 

On peut voir que seul root peut executer ce fichier car ce fichier contient des informations sensible très restreintes.
