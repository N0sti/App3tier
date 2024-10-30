# Base de données PostgreSQL pour une application 3-tiers

Ce guide explique comment configurer et déployer une base de données PostgreSQL à l'aide de Docker dans le cadre d'une architecture d'application 3-tiers.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants installés sur votre machine :

- Docker

## Structure de fichiers

Voici l'architecture du projet pour la base de données PostgreSQL :

```sh
my_3tier_app/
├── db/
│   └── Dockerfile
└── documentation.md


Étapes de configuration
1. Créer la structure de fichiers
mkdir my_3tier_app
cd my_3tier_app
mkdir db
cd db

2. Créer le Dockerfile
Dans le dossier db, créez un fichier nommé Dockerfile avec le contenu suivant :
FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
    POSTGRES_USER=usr \
    POSTGRES_PASSWORD=pwd

3. Construire l'image Docker
Retournez au dossier principal et construisez l'image Docker pour la base de données :

cd ..
docker build -t my_postgres_db -f db/Dockerfile db


4. Lancer le conteneur Docker
Lancez un conteneur à partir de l'image que vous venez de créer :


docker run -d --name my_postgres_container -p 5432:5432 my_postgres_db
5. Vérifier que la base de données fonctionne
Connectez-vous à la base de données pour vérifier qu'elle fonctionne correctement :


docker exec -it my_postgres_container psql -U usr -d db
Une fois connecté, vous pouvez exécuter des commandes SQL pour vérifier que tout fonctionne. Par exemple :


SELECT 1;
Pour quitter la session psql, tapez simplement \q ou exit.

6. Documentation
Assurez-vous de documenter toutes les étapes que vous avez suivies dans un fichier documentation.md.

Commandes utiles
Arrêter le conteneur

docker stop my_postgres_container
Redémarrer le conteneur

docker start my_postgres_container
Supprimer le conteneur

docker rm my_postgres_container
Recréer le conteneur

docker run -d --name my_postgres_container -p 5432:5432 my_postgres_db


docker run \ --name my-my_postgres_container \  --net app-network \ -e POSTGRES_DB=db \  -e POSTGRES_USER=usr / -e POSTGRES_PASSWORD=pwd \ -d \ postgres:14.1-alpine

Nom de l'image Docker
Image Docker : my_postgres_db
Nom du conteneur Docker
Conteneur Docker : my_postgres_container