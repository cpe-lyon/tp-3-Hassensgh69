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
    
    

          usermod -a -G dev alice
          usermod -a -G dev bob 
          usermod -a -G dev dave
          
          
          usermod -a -G dev bob
          usermod -a -G dev charlie 
          usermod -a -G dev dave
          
          
          
          
   4. Donnez deux moyens d’afficher les membres de infra

    
          
          grep infra /etc/group
          
          getent group dinfra
          
  5. Faites de dev le groupe propriétaire des répertoires /home/alice et /home/bob et de infra le groupe
propriétaire de /home/charlie et /home/dave

           sudo chgrp -R dev /home/alice
           sudo chgrp -R dev /home/charlie
           sudo chgrp -R dev /home/dave
           
           
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
