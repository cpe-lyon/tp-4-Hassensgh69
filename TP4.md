# TP 4 - Gestion des paquets
## Exercice 1. Commandes de base

1. Commencez par mettre à jour votre système avec les commandes vues dans le cours


2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet
alias pour qu’il ne soit pas perdu au prochain redémarrage ?

                  root@LAPTOP-C8JV71L4:/home/hassen# alias maj="apt-get update"
      
                  root@LAPTOP-C8JV71L4:/home/hassen# alias maj="apt-get update" >> ~/.bashrc
      
                  root@LAPTOP-C8JV71L4:/home/hassen# source ~/.bashrc
      
                  root@LAPTOP-C8JV71L4:/home/hassen# maj

3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.

                  root@LAPTOP-C8JV71L4:/home/hassen# grep installed /var/log/dpkg.log | tail -n5
                  2022-09-23 09:13:21 status installed man-db:amd64 2.10.2-1
                  2022-09-23 09:13:21 status installed hicolor-icon-theme:all 0.17-2
                  2022-09-23 09:13:21 status installed tilix:amd64 1.9.4-2build1
                  2022-09-23 09:13:21 status installed libglib2.0-0:amd64 2.72.1-1
                  2022-09-23 09:13:21 status installed libc-bin:amd64 2.35-0ubuntu3.1
                  

4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install

           root@LAPTOP-C8JV71L4:/home/hassen# grep "apt install" /var/log/apt/history.log |tail -n5
           Commandline: /usr/bin/apt install -y language-pack-fr wfrench
           Commandline: apt install npm


5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de paquets installés sur la machine (ne pas hésiter à consulter le manuel !). Comment explique-t-on la(petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?
          
          root@LAPTOP-C8JV71L4:/home/hassen# dpkg -l | grep "ii" | wc -l
          1096
          
 6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ?
 
          root@LAPTOP-C8JV71L4:/home/hassen# apt list | wc -l

          WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

          68953
 
