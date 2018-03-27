# Installation

[guide d'installation docker](https://www.docker.com/community-edition)

```
docker -v
> Docker version 17.12.0-ce, build c97c6d6
```

# TP découverte

```
# Lancer votre premier conteneur
docker run hello-world
```

```
# Lister les images
docker images 
```

```
# Lister les process docker actifs (conteneur)
docker ps 
```

```
# Lister tous les process docker
docker ps -a
```

```
# Lancer votre deuxième conteneur
docker run ubuntu:latest /bin/echo 'Hello World!'
```

```
# Rentrer en mode intéractif
docker run -it ubuntu:latest /bin/bash
```
--> vous êtes sous ubuntu!

# Dockerfile
## TP 1 : PHP
Nous allons ici déployer un site php dans un conteneur docker.

Dans un répertoire de travail, docker-tp1 par exemple, créer un fichier nommé ''Dockerfile'' contenant les lignes suivantes:
```
FROM php:7.2-apache
COPY ./myapp /var/www/html/
```

Créer également un fichier index.php situer dans le répertoire ./myapp
L'arborscence obtenue est la suivante:


| Dockerfile
| myapp/
       | index.php
       

construire l'image docker
```
docker build -t php-image .
```

Executer le conteneur
```
docker run -d --rm --name php-app -p 8081:80 php-image
```
* -d indique que le conteneur est en mode démon.
* --rm indique que si le conteneur est arrêté (docker stop...), alors on supprime toutes ses datas.
* --name indique le nom que l'on souhaite donner au conteneur. chaque conteneur doit avoir un nom unique.
* -p 8081:80 indique qu'une requête lancée sur le port 8081 de la machine hôte sera redirigée vers le port 80 du conteneur docker.


se rendre sur localhost:8080
> attention, avec la toolbox l'ip n'est pas locahost. Faire un `docker-machine ip` pour connaitre la bonne ip.

## TP Docker-Compose  
 ### créer un service REST (api) avec les outils de votre choix
 Le service doit exposer au moins une URL et répondre au format text ou JSON
 
 ```
 http://localhost:8080/hello (répond Hello!)

 ```
 
 ### Dockerfile
 Une fois le service REST créé et testé, créer un Dockerfile afin de pouvoir exécuter ce service dans un conteneur

---
Build de l'image

```
 docker build -t monService .  
```
---
Lancement du conteneur à partir de l'image précédemment créée
``` 
 docker run -p 7000:8080 
```

## Docker Compose
### Deuxième service REST
Créer un deuxième service REST qui expose au moins une URL.
Lorsque l'on appel ce service, il appelle à son tour le premier service REST. Il y a donc un client REST à créer, c'est à
dire un client capable d'appeler une URL et de récupérer le resultat.
Ensuite : 
 * lancer le premier service  (Ex. localhost:8080)
 * lancer le deuxième service  (Ex. localhost:8081)
 * appeler le deuxième service et vérifier qu'il appelle bien le premier service

### docker-compose.yml

 * créer un fichier docker-compose qui associe ces 2 services
 
Exemple d'arborescence : 
 * service1/
   * src/
   * Dockefile
 * service2/
   * src/
   * Dockerfile
 * docker-compose.yml
 






