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
 
7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.

glances : Il affiche les informations du pc et son utilisation de cpu en temp réel par exemple
          root@LAPTOP-C8JV71L4:/home/hassen# apt install glances

tldr :  C'est un man simplifié 
          root@LAPTOP-C8JV71L4:/home/hassen# apt install tldr
          
hollywood : C'est un petit jeu qui affiche une simulation de hacking
          root@LAPTOP-C8JV71L4:/home/hassen# apt install hollywood

8. Quels paquets proposent de jouer au sudoku ? 

Ce sont les paquets gnome-sudoku ou ksudoku

## Exercice 2.

          hassen@LAPTOP-C8JV71L4:~$ dpkg -S ls | grep "/ls$"
          coreutils: /bin/ls
          klibc-utils: /usr/lib/klibc/bin/ls
          
  Script :
          #!/bin/bash

          echo $(dpkg -S $1 | grep "/$1")

![image](https://user-images.githubusercontent.com/80455696/192234659-dd18dfab-70d2-4714-8c1c-dad7bf0818e1.png)

## Exercice 3.

![image](https://user-images.githubusercontent.com/80455696/192236187-0682fbc7-9630-42e7-96c8-59598e75f942.png)

## Exercice 4.

Lister les programmes livrés avec coreutils. En particulier, on remarque que l’un deux se nomme [. De quoi s’agit-il ?

          root@LAPTOP-C8JV71L4:/home/hassen# dpkg -L coreutils

## Exercice 5. aptitude

emacs est un éditeur de texte
Lynx est un navigateurs web en mode texte

## Exercice 6. Installation d’un paquet par PPA

2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?
          
          root@LAPTOP-C8JV71L4:/etc/apt/sources.list.d# ls
          linuxuprising-ubuntu-java-jammy.list
