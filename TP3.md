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
          
