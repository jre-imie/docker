# docker

## TP découverte

Lancer votre premier conteneur
```
docker run hello-world
```

Lister les images
```
docker images 
```

Lister les process docker actifs (conteneur)
```
docker ps 
```

Lister tous les process docker
```
docker ps -a
```

Lancer votre deuxième conteneur
```
docker run ubuntu:latest /bin/echo 'Hello World!'
```

Rentrer en mode intéractif
```
docker run -t -i ubuntu:latest /bin/bash
```
--> vous êtes sous ubuntu!

## TP rest  
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
 






