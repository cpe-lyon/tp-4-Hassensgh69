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

## Exercice 7. Installation d’un logiciel à partir du code source

1. Commencez par cloner le dépôt git suivant :
git clone https://gitlab.com/jallbrit/cbonsai
          
          root@LAPTOP-C8JV71L4:~# git clone https://gitlab.com/jallbrit/cbonsai
          Clonage dans 'cbonsai'...
          warning: redirection vers https://gitlab.com/jallbrit/cbonsai.git/
          remote: Enumerating objects: 383, done.
          remote: Counting objects: 100% (216/216), done.
          remote: Compressing objects: 100% (103/103), done.
          remote: Total 383 (delta 122), reused 199 (delta 111), pack-reused 167
          Réception d'objets: 100% (383/383), 91.03 Kio | 13.00 Mio/s, fait.
          Résolution des deltas: 100% (193/193), fait.
          
2. Rendez vous dans le dossier cbonsai. Un fichier README.md) est livré avec les sources, et vous explique comment compiler le programme (vous pouvez installer un lecteur de Markdown pour Bash, commemdless pour vous faciliter la lecture de ce type de fichiers).
          
![image](https://user-images.githubusercontent.com/80455696/192954574-fcdd9aa9-7306-4d3e-809f-6ca8be25f625.png)



## Exercice 8. Création de dépôt personnalisé

1. Dans le dossier scripts créé lors du TP 2, créez un sous-dossier origine-commande où vous créerez un
sous-dossier DEBIAN, ainsi que l’arborescence usr/local/bin où vous placerez le script écrit à l’exercice 2


![image](https://user-images.githubusercontent.com/80455696/192957060-29eb921b-ee45-4829-bbc0-644239966a5b.png)

3. Revenez dans le dossier parent de origine-commande (normalement, c’est votre $HOME) et tapez la
commande suivante pour construire le paquet :


![image](https://user-images.githubusercontent.com/80455696/192963975-372d9464-faf9-4b92-af3f-2d32b78c6712.png)

### Création du dépôt personnel avec reprepro

1. Dans votre dossier personnel, commencez par créer un dossier repo-cpe. Ce sera la racine de votre
dépôt

![image](https://user-images.githubusercontent.com/80455696/192964578-9e2b710c-fcf7-4ebd-b665-7180f6a0c526.png)

2. Ajoutez-y deux sous-dossiers : conf (qui contiendra la configuration du dépôt) et packages (qui contiendra nos paquets)

![image](https://user-images.githubusercontent.com/80455696/192966147-550373c6-0474-4a81-92b1-d4460c330a70.png)


3. Dans conf, créez le fichier distributions suivant :

![image](https://user-images.githubusercontent.com/80455696/193002223-3a999e6f-a172-4146-a17a-4f6596cee9ff.png)

4. Dans le dossier repo-cpe, générez l’arborescence du dépôt avec la commande
reprepro -b . export

![image](https://user-images.githubusercontent.com/80455696/192968476-b294ac74-58e8-4cda-940e-bb5dba718d7e.png)

5.Copiez le paquet origine-commande.deb créé précédemment dans le dossier packages du dépôt, puis,
à la racine du dépôt, exécutez la commande

![image](https://user-images.githubusercontent.com/80455696/193017703-cd147dab-1e74-44bb-b735-06fa888fc713.png)

6. Il faut à présent indiquer à apt qu’il existe un nouveau dépôt dans lequel il peut trouver des logiciels.
Pour cela, créez (avec sudo) dans le dossier /etc/apt/sources.list.d le fichier repo-cpe.list
contenant : deb file:/home/VOTRE_NOM/repo-cpe cosmic multiverse

![image](https://user-images.githubusercontent.com/80455696/193017922-8003fbb4-3510-4ec0-a212-b7e99694be94.png)

## Signature du dépôt avec GPG

Apres avoir la mis a jour avec apt update on peut voir que notre dépôt est désormais pris en compte
![image](https://user-images.githubusercontent.com/80455696/193000772-d91670e7-1bea-4e97-b34f-ec22792f6156.png)
