# DOCKER

Docker permet la mise en œuvre de conteneurs s'exécutant en isolation, via une API de haut-niveau. Construit sur des capacités du noyau Linux (surtout les cgroups et espaces de nommage), un conteneur Docker, à l'opposé de machines virtuelles traditionnelles, ne requiert aucun système d'exploitation séparé et n'en fournit aucun. Il s'appuie plutôt sur les fonctionnalités du noyau et utilise l'isolation de ressources (comme le processeur, la mémoire, les entrées et sorties et les connexions réseau) ainsi que des espaces de noms séparés pour isoler le système d'exploitation tel que vu par l'application. Docker accède aux capacités de virtualisation du noyau Linux, soit directement à travers la bibliothèque runc (disponible depuis Docker 0.9), soit indirectement via libvirt, LXC (Linux Containers) ou systemd-nspawn. 

## INTRODUCTION

La plateforme de conteneurisation repose sur sept composants principaux. Le Docker Engine est un outil client-serveur sur lequel repose la technologie de container pour prendre en charge les tâches de création d’applications basées container. Le moteur crée un processus daemon server-side permettant d’héberger les images, les containers, les réseaux et les volumes de stockage. Ce daemon fournit aussi une interface SLI client-side permettant aux utilisateurs d’interagir avec le daemon via l’API de la plateforme.

Les containers créés sont appelés Dockerfiles. Le composant Docker Compose permet de définir la composition des composants au sein d’un container dédié. Le Docker Hub est un outil SaaS permettant aux utilisateurs de publier et de partager des applications basées container via une bibliothèque commune.

Les containers sont donc proches des machines virtuelles, mais présentent un avantage important. Alors que la virtualisation consiste à exécuter de nombreux systèmes d’exploitation sur un seul et même système, les containers se partagent le même noyau de système d’exploitation et isolent les processus de l’application du reste du système.

Pour faire simple, plutôt que de virtualiser le hardware comme l’hyperviseur, le container virtualise le système d’exploitation. Il est donc nettement plus efficient qu’un hyperviseur en termes de consommation des ressources système. Concrètement, il est possible d’exécuter près de 4 à 6 fois plus d’instances d’applications avec un container qu’avec des machines virtuelles comme Xen ou KVM sur le même hardware.

Le mode Docker Swarm du Docker Engine prend en charge l’équilibrage des charges des clusters . Ainsi, les ressources de plusieurs hôtes peuvent être rassemblées pour agir comme une seul ensemble. Ainsi, les utilisateurs peuvent rapidement échelonner le déploiement de containers.

## DOCKER HUB

Docker Hub is the world's easiest way to create, manage, and deliver your teams' container applications. [Dockerhub](https://hub.docker.com/)

## INSTALLATION

[Installation docker](https://docs.docker.com/get-docker/)

[VSCode extension docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

## COMMANDS

### PULL DOCKER IMAGE

``` bash
docker pull <image>
```

::: tip Remarque
Le conteneur est un environnement d'exécution pour une image. Lorsque nous le faisons docker pull "image", le conteneur n'est pas encore démarré ni créé.
:::

### CREATE & START CONTAINER

``` bash
$ docker create -t ​​-i fedora bash
...
dff32a272ad4c94cd51419ee4f53c371e3c3a8cfb448a469634d4420e139d118
```

``` bash
$ docker start -a -i dff32a272ad4c
...
[racine@dff32a272ad4 /]# 
```

- i : interactif, garde STDIN ouvert même s'il n'est pas attaché
- t : alloue un pseudo-TTY
- a : attache les STDOUT et STDERR du conteneur et transmet tous les signaux au processus.

### RENAME CONTAINER

``` bash
$ docker renommer my_container my_new_container
```

### DOCKER RUN

Crée et démarre un conteneur en une seule opération.

``` bash
$ docker run -it ubuntu-ssh-k /bin/bash
```

### REMOVE CONTAINER
``` bash
$ docker rm myfedora
```

### DOCKER UPDATE

Met à jour les limites de ressources d'un conteneur. Exemple : mise à jour de plusieurs configurations de ressources pour plusieurs conteneurs :

``` bash
$ docker update --cpu-shares 512 -m 300M dff32a272ad4 happy_kare
...
dff32a272ad4
happy_kare
```

### DOCKER INFORMATIONS
``` bash
$ docker ps
$ docker ps -a
...
COMMANDE D'IMAGE D'ID DE CONTENEUR ÉTAT CRÉÉ NOMS DE PORTS
e2481c1bad5d ubuntu-ssh-k:latest "/bin/bash" il y a 10 heures Jusqu'à 10 heures hopeful_carson 
```

### DOCKER LOGS

Obtient les journaux du conteneur. (Nous pouvons utiliser un pilote de journal personnalisé, mais les journaux ne sont disponibles que pour json-file et journald dans 1.10)

``` bash
$ docker logs 839f66a78983
```

### DOCKER INSPECT CONTAINER

Examine toutes les informations sur un conteneur (y compris l'adresse IP).
Pour obtenir l'adresse IP d'un conteneur en cours d'exécution :

``` bash
$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' $(docker ps -q)
...
172.17.0.5
```

### OTHER CONTAINER INFORMATIONS

``` bash
$ docker events // obtient les événements du conteneur.
$ le port docker // montre le port du conteneur faisant face au public.
$ docker top // montre les processus en cours dans le conteneur.
$ docker stats // affiche les statistiques d'utilisation des ressources des conteneurs.
$ docker diff // affiche les fichiers modifiés dans le FS du conteneur.
```

### OTHER COMMANDS DOCKER CONTAINER
``` bash
$ docker start // démarre un conteneur afin qu'il soit en cours d'exécution.
$ docker stop // arrête un conteneur en cours d'exécution.
$ docker restart //arrête et démarre un conteneur.
$ docker pause // met en pause un conteneur en cours d'exécution, le "congelant" en place.
$ docker unpause // réactivera un conteneur en cours d'exécution.
$ docker wait // bloque jusqu'à ce que le conteneur en cours d'exécution s'arrête.
$ docker kill // envoie un SIGKILL à un conteneur en cours d'exécution.
$ docker attach //se connectera à un conteneur en cours d'exécution.
Ou nous pouvons utiliser ce qui suit pour obtenir tty :
$ docker exec -i -t mon-nginx-1 /bin/bash
```


### IMAGE
``` bash
$ docker images // affiche toutes les images.
$ docker images -a
$ docker import // crée une image à partir d'une archive tar.
$ docker build // crée une image à partir de Dockerfile.
$ docker commit // crée une image à partir d'un conteneur, par défaut, le conteneur en cours de validation et ses processus seront mis en pause pendant que l'image est validée.
$ docker rmi // supprime (et dé -balise) une image du nœud hôte
$ docker load // charge une image à partir d'une archive tar en tant que STDIN, y compris les images et les balises
$ docker save // enregistre une image dans un flux d'archive tar sur STDOUT avec tous les calques, balises et versions parents
$ docker history // montre l'historique de l'image
$ docker tag // balise une image avec un nom
$ docker images purge // Purge de images
```

### VOLUMES
``` bash
$ docker volume ls // Liste les volumes
$ docker volume prune // Remove volume non utilisé
```

### OTHER
``` bash
$ docker system prune // Clean images, container, volumes & network not associated
$ docker system prune -a // Clean images, container, volumes & network
```
