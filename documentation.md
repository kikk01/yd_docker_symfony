# **Démarrage en fonction de la version**
Docker -v pour avoir la version de docker engine

<https://docs.docker.com/compose/compose-file/compose-file-v3/> permet de savoir comment rédiger le fichier composer.yaml. Voir l’exemple sur cette page

La version 20,10 semble être lié à la version de docker compose 3,9

# **docker-compose.yml**
Créer un fichier docker-compose.yml

A l’intérieur j’y met les containers (services) ainsi que les images qu’ils vont instancier :

- Aller sur <https://hub.docker.com/>
- rechercher l’image dont j’ai besoin
- Je vais utiliser docker-compose donc je cherche la config « via docker-compose » qui va m’indiquer les lignes à ajouter dans le docker.compose.yml
## **Apache**
Pour apache on utilise un fichier DockerFile (dans le fichier php + customisation de l’image : choix de yoan, on peut trouver des articles à ce sujet en gogglant : docker image apache custom)

Pour apache on utilise un image mais un build qu’on va appeler dans notre exemple « php », nom du repertoire du dockerFile

Le fichier vhosts est une copie strict de la doc symfony

https://symfony.com/doc/current/setup/web\_server\_configuration.html

**mettre à jour docker à chaque fois fichier docker-compose.yml est modifier**

docker-compose up -d

# **Création du projet**
**Créer le projet symfony dans le container docker**

docker exec [container\_name] composer create-project symfony/website-skeleton [project\_name]

Dans notre exemple c’est  www\_yd\_docker\_symfony

le nom du projet est lié au fichier vhosts.conf => documentRoot et Directory => project

**Devenir propriétaire du projet**

sudo chown -R $USER ./

**config du .env**

DATABASE\_URL="mysql://root:@db\_yd\_docker\_symfony:3306/[db\_name]?serverVersion=5.7"

db\_name is the container name of my bdd set in the composer.yml

**command symfony de création de bdd**

1. Connexion à l’intérieur du container : docker exec -it www\_yd\_docker\_symfony bash

can imagine the container as a server.

Then this command open the shell of the server

2. rentrer dans le répertoire du projet : cd project

From here I can use all the php/bin console command from symfony
3. ## **Envoie de mail**
Création et personnalisation du controleur

**configuration du mailer**

dans le .env :

MAILER\_DSN=smtp://maildev\_yd\_docker\_symfony:25

A partir de la, maildev devient le serveur pour envoyer des mails
