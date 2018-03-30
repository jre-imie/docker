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

```
`# supprimer tous les conteneurs actifs / inactifs
docker rm $(docker ps -a -q)
```
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


* Dockerfile
* myapp/
  * index.php
       

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

# TP Docker-Compose  

> L'objectif de ce TP est de créer deux services REST, dont l'un appel le second.
> On créerea un Dockerfile pour chacun de ces services
> Ensuite nous écrirons un docker-compose.yml afin de faire communiquer ces services entres eux.

L'arborescence obtenue sera la suivante :
 
Exemple d'arborescence : 
 * service1/
   * src/
   * Dockefile
 * service2/
   * src/
   * Dockerfile
 * docker-compose.yml
 
 ## créer un service REST "count" avec les outils de votre choix
Le service expose une url, count, qui fait +1 à chaque appel.
Ex:
* au premier appel, répond 1
* au deuxième appel : répond 2
* ...
 
 ```
 http://localhost:8080/count 

 ```
 
 ### Dockerfile
 Une fois le service REST créé et testé, créer un Dockerfile afin de pouvoir exécuter ce service dans un conteneur

---
Faire un build de l'image

```
 docker build -t monService .  
```
---
lancer le conteneur à partir de l'image précédemment créée
``` 
 docker run -p 7000:8080 
```
## Créer un deuxième service REST, "showcount"
* Créer un deuxième service REST qui expose au moins une URL.
Lorsque l'on appel ce service, il appelle à son tour le premier service REST. Il y a donc un client REST à créer, c'est à
dire un client capable d'appeler une URL et de récupérer le resultat.
* Créer un Dockerfile pour ce service

## docker-compose.yml

 * créer un fichier docker-compose qui associe ces 2 services
 * faire en sorte que le service "showcount" appelle le service "count" et affiche le résultat à l'ecran
 



# Docker usual commands

[doc Dockerfile](https://docs.docker.com/engine/reference/builder/)
[doc Compose file](https://docs.docker.com/compose/compose-file/)
[doc Reference](https://docs.docker.com/reference/)




