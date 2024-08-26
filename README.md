# Docker Project - Softy Pinko

## Contexte

Docker est une plateforme permettant de containeriser vos applications, c'est-à-dire de les empaqueter dans des environnements portables et autonomes pouvant être exécutés n'importe où. Cela vous permet de déplacer rapidement votre application d'un environnement à un autre, par exemple de votre ordinateur local à un serveur, sans vous soucier des dépendances ou des problèmes de configuration. Docker utilise des conteneurs, qui sont des environnements isolés contenant tout ce dont une application a besoin pour fonctionner (bibliothèques, dépendances, configurations). Les conteneurs Docker sont légers et peuvent être démarrés et arrêtés rapidement, ce qui les rend idéaux pour le développement et le déploiement de logiciels modernes.

Dans ce projet, vous allez créer une infrastructure pour une application qui utilise un proxy inverse, un répartiteur de charge, deux serveurs d'application et un serveur front-end.

## Design de Haut Niveau

Le design se compose d'un seul serveur qui sert de point d'entrée pour votre application. Ce serveur agit en tant que serveur proxy inverse, qui route le trafic vers les serveurs d'API ou le serveur de contenu statique front-end, et en tant que répartiteur de charge pour équilibrer le trafic entre les deux serveurs d'API. Le trafic est distribué à l'aide de l'algorithme de répartition en boucle (Round Robin).

## Prérequis

Avant de commencer, assurez-vous d'avoir :

- Installé Docker Desktop sur votre ordinateur local. [Télécharger Docker](https://www.docker.com/)
- Vous êtes familiarisé avec Docker. [Tutoriel Docker](https://docs.docker.com/get-started/)

## Tâches

<details>
<summary>1. Créez votre première image Docker</summary>

Dans cette tâche, vous allez créer une image Docker à partir d'un Dockerfile basé sur la dernière version d'Ubuntu. L'image mettra à jour et mettra à niveau les paquets, puis affichera "Hello, World!" lorsque le conteneur sera exécuté.

**Étapes :**
- Créez un `Dockerfile` basé sur `ubuntu:latest`.
- Exécutez `apt-get update` et `apt-get upgrade -y`.
- Faites en sorte que le conteneur affiche "Hello, World!" lors de l'exécution.

</details>

<details>
<summary>2. Back-end</summary>

Créez un serveur Flask simple qui renvoie "Hello, World!" via une API. Vous installerez `python3`, `pip3` et `flask` dans l'image Docker.

**Étapes :**
- Installez `python3`, `python3-pip`, et `flask` dans l'image Docker.
- Créez un fichier `api.py` avec un point d'entrée Flask qui retourne "Hello, World!".
- Exécutez le serveur Flask sur le port 5252.

</details>

<details>
<summary>3. Front-end</summary>

Configurez un serveur web Nginx pour héberger le front-end de l'application. Le contenu statique sera servi via un Dockerfile personnalisé pour Nginx.

**Étapes :**
- Créez un `Dockerfile` basé sur `nginx:latest`.
- Copiez les fichiers front-end dans `/var/www/html/softy-pinko-front-end`.
- Configurez Nginx pour servir le contenu statique sur le port 9000.

</details>

<details>
<summary>4. Connexion du Front-end et Back-end</summary>

Connectez le front-end au back-end en utilisant des requêtes AJAX. Configurez CORS dans Flask pour permettre les requêtes entre domaines.

**Étapes :**
- Ajoutez du JavaScript à `index.html` pour charger les données dynamiques depuis le back-end.
- Modifiez le `Dockerfile` du back-end pour installer `flask-cors` et permettre les requêtes cross-origin.

</details>

<details>
<summary>5. Simplification avec Docker Compose</summary>

Utilisez Docker Compose pour orchestrer l'exécution simultanée des services front-end et back-end. Un fichier `docker-compose.yml` sera créé pour gérer le déploiement des services.

**Étapes :**
- Créez un fichier `docker-compose.yml` pour définir les services front-end et back-end.
- Utilisez `docker-compose build` pour construire les images et `docker-compose up` pour les exécuter.

</details>

<details>
<summary>6. Serveur Proxy</summary>

Ajoutez un serveur proxy Nginx pour router les requêtes vers le front-end ou le back-end selon l'URL demandée. Le serveur proxy simplifie la gestion des services en masquant les détails d'implémentation des clients.

**Étapes :**
- Créez un `Dockerfile` pour un serveur proxy basé sur Nginx.
- Configurez un fichier `proxy.conf` pour router les requêtes vers les services appropriés.
- Mettez à jour `docker-compose.yml` pour inclure le service proxy.

</details>

<details>
<summary>7. Mise à l'échelle horizontale</summary>

Ajoutez un deuxième serveur API pour gérer les pics de trafic. Configurez le répartiteur de charge Nginx pour équilibrer les requêtes entre plusieurs serveurs API en utilisant l'algorithme Round Robin.

**Étapes :**
- Modifiez `docker-compose.yml` pour créer plusieurs instances du service back-end.
- Utilisez `docker-compose up --scale back-end=2` pour démarrer plusieurs serveurs API.
- Vérifiez que le répartiteur de charge balance les requêtes entre les serveurs API.

</details>

## Structure du Répertoire

- **task0** : Création de l'image Docker initiale.
- **task1** : Implémentation du back-end avec Flask.
- **task2** : Configuration du serveur front-end avec Nginx.
- **task3** : Connexion front-end et back-end.
- **task4** : Gestion des services avec Docker Compose.
- **task5** : Ajout du serveur proxy Nginx.
- **task6** : Mise à l'échelle horizontale avec plusieurs serveurs API.

## Repository GitHub

Vous pouvez trouver le code source de ce projet sur GitHub : [holbertonschool-softy-pinko-docker](https://github.com/holbertonschool-softy-pinko-docker).
