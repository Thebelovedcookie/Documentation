# Docker UNDER THE HOOD

## Introduction

J'ai commencé à travailler sur Docker lors de mon projet 42, Inception, qui avait pour but de déployer un site WordPress via trois conteneurs différents, avec le même réseau.

Au cours de mes recherches de documentation, j'ai vu beaucoup d'articles, de tutoriels, qui parlaient de ce que Docker est, et de comment l'utiliser.

Mais rien sur ce qu'il se passait vraiment à la création d'un conteneur. L'idée ici est de comprendre comment la technologie fonctionne.

--------

### Docker THE ORIGIN

Docker est une plateforme permettant de lancer certaines applications dans des conteneurs logiciels, lancée en 2013.

#### C'est quoi Docker ?

Docker est un outil qui peut empaqueter une application et ses dépendances dans un conteneur isolé, qui pourra être exécuté sur n'importe quel serveur.

Il ne s'agit pas de virtualisation mais de conteneurisation, une forme plus légère qui s'appuie sur certaines parties de la machine hôte pour son fonctionnement. Source : [Wikipedia](https://fr.wikipedia.org/wiki/Docker_(logiciel))

#### D'accord mais... Comment ça fonctionne?

##### Sommaire

1. La containerization
    1.1 [Les namespaces](./Containerization/Linux_Kernel/Namespaces/Namespaces.md)
    1.2 [Cgroups](./Containerization/Linux_Kernel/Cgroups.md)
