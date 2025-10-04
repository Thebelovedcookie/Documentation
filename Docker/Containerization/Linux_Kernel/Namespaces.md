# Namespaces

Les namespaces sont l'une des principales caractéristiques du noyau Linux.

Ils permettent d'isoler les ressources du noyau.

Ils s'assurent qu'un processus ne verra qu'un ensemble spécifié de ressources.

Les exemples de ressources sont les IDs des processus, les noms d'hôte (hostnames), les fichiers, les noms d'utilisateur, les accès réseau et les communications inter-processus.

Le terme "namespaces" fait référence au type de namespace ainsi qu'à l'espace de noms spécifié.

![image](../../Image/Namespace.png)

Chaque processus individuel ne peut voir ou utiliser que le namespace auquel il est associé.

Ce type de fonctionnalité entre processus et namespace peut être observé à travers les 8 namespaces différents.

1. Mount (MNT) : Contrôle les points de montage. Lorsqu’un nouvel espace de noms est créé, les points de montage actuels sont copiés dans ce nouvel espace de noms.

2. Process ID (PID) : Fournit aux processus des identifiants de processus (PID) distincts pour chaque namespace.

3. Interprocess Communication (IPC) : Empêche les processus appartenant à des espaces de noms différents de partager des mécanismes de communication interprocessus (comme la mémoire partagée SHM).

4. Network (NET) : Virtualise la pile réseau.

5. Unix Time Sharing (UTS) : Permet à un système d'avoir différents noms d'hôte et de domaine pour différents processus.

### Euh.. Mais encore ? 

Un namespace dans linux, c'est comme une boite fermee ou on a ranger un aspect du systeme (processus, reseau, fichiers, etc).

Chaque boites est isolees des autres, donc ce qu'il y a dedans ne peux pas "voir" ce qu'il y a dans les autres.

#### En pratique

Un namespace, c'est donc un mecanismes d'isolation fourni par linux qui donne a un processus l'illusion qu'il est seul a utiliser une ressources alors qu'en realite il partage le noyau avec d'autres.

Un namespace applique a un ou plusieurs processus va faire effet de loupe deformantes qui va en changer sa visions du systemes.

Par exemple, un conteneur (qui est un seul processus) n'est pas associe a un seul namespace mais a plusieurs en meme temps. 

![container](../../Image/Containeur.png)