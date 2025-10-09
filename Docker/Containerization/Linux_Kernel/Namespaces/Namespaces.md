# Namespaces

Les namespaces sont l'une des principales caractéristiques du noyau Linux.

Ils permettent d'isoler les ressources du noyau.

Ils garantissent qu'un processus ne verra qu'un ensemble spécifié de ressources.



![image](../../../Image/Namespace.png)

Chaque processus individuel ne peut voir ou utiliser que le namespace auquel il est associé.

Ce type de fonctionnalité entre processus et namespace peut être observé à travers les 8 namespaces différents.

En voici quelques-uns :

1. **[Mount](./Mounts.md) (MNT)** : Contrôle les points de montage. Lorsqu’un nouvel espace de noms est créé, les points de montage actuels sont copiés dans ce nouvel espace de noms.

2. **Process ID (PID)** : Fournit aux processus des identifiants de processus (PID) distincts pour chaque namespace.

3. **Interprocess Communication (IPC)** : Empêche les processus appartenant à des espaces de noms différents de partager des mécanismes de communication interprocessus (comme la mémoire partagée SHM).

4. **Network (NET)** : Virtualise la pile réseau.

5. **Unix Time Sharing (UTS)** : Permet à un système d'avoir différents noms d'hôte et de domaine pour différents processus.

