# TP 4 - Gestion des paquets
## Exercice 1. Commandes de base

1. Commencez par mettre à jour votre système avec les commandes vues dans le cours


2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet
alias pour qu’il ne soit pas perdu au prochain redémarrage ?

      root@LAPTOP-C8JV71L4:/home/hassen# alias maj="apt-get update"
      root@LAPTOP-C8JV71L4:/home/hassen# alias maj="apt-get update" >> ~/.bashrc
      root@LAPTOP-C8JV71L4:/home/hassen# source ~/.bashrc
      root@LAPTOP-C8JV71L4:/home/hassen# maj
