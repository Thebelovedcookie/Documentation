# Processus

Concrètement, un processus est une structure :

```
struct task_struct {
    pid_t pid;                       // PID du processus
    pid_t tgid;                      // ID du groupe de threads
    struct mm_struct *mm;            // Espace mémoire (pile, heap, code)
    struct files_struct *files;      // Descripteurs de fichiers ouverts
    struct nsproxy *nsproxy;         // Pointeurs vers les namespaces
    struct cred *cred;               // UID, GID, permissions
    struct signal_struct *signal;    // Gestion des signaux
    struct sched_entity se;          // Infos pour l’ordonnanceur CPU
    ...
};
```

Quand on utilise `fork()` ou `clone()`, ces fonctions vont :

- allouer une nouvelle structure `task_struct` (dans l'espace mémoire du noyau via `kmem_cache_alloc()`),
- copier ou référencer une partie des informations du parent (selon les flags de `clone()`),
- initialiser des champs (nouveau PID, compteurs, liens vers les [namespaces](./Linux_Kernel/Namespaces/Namespaces.md), etc),
- ajouter le nouveau processus à la liste globale des tâches (tasklist).

Ce nouveau processus a ses propres pointeurs :

| Élément         | Partage         |
|-----------------|----------------|
| pid             | Nouveau        |
| mm_struct       | Copie ou partage |
| files_struct    | Copie ou partage |
| nsproxy         | Copie ou partage |
| cred (UID, GID) | Copie          |
| signal_struct   | Partagé entre threads du même groupe |

Le noyau ne "voit" ton processus que via `task_struct`.

Quand tu fais :

- un `kill(pid, SIGTERM)` -> le noyau cherche la `task_struct` qui a ce pid,
- un `ps` -> L'outil lit /proc, qui est généré à partir des `task_struct`,
- quand un processus meurt :
  - sa `task_struct` est retirée de la liste des tâches,
  - libérée (retournée au cache),
  - et les structures associées (`mm_struct`, `files_struct`, etc.) sont libérées aussi.

---

# Process

A process is, concretely, a structure:

```
struct task_struct {
    pid_t pid;                       // Process PID
    pid_t tgid;                      // Thread group ID
    struct mm_struct *mm;            // Memory space (stack, heap, code)
    struct files_struct *files;      // Open file descriptors
    struct nsproxy *nsproxy;         // Pointers to namespaces
    struct cred *cred;               // UID, GID, permissions
    struct signal_struct *signal;    // Signal management
    struct sched_entity se;          // CPU scheduler info
    ...
};
```

When you use `fork()` or `clone()`, these functions will:

- allocate a new `task_struct` (in kernel memory via `kmem_cache_alloc()`),
- copy or reference some information from the parent (depending on `clone()` flags),
- initialize fields (new PID, counters, links to [namespaces](./Linux_Kernel/Namespaces/Namespaces.md), etc),
- add the new process to the global task list (tasklist).

This new process has its own pointers:

| Element         | Sharing         |
|-----------------|----------------|
| pid             | New            |
| mm_struct       | Copy or share  |
| files_struct    | Copy or share  |
| nsproxy         | Copy or share  |
| cred (UID, GID) | Copy           |
| signal_struct   | Shared between threads in the same group |

The kernel only "sees" your process via `task_struct`.

When you do:

- a `kill(pid, SIGTERM)` -> the kernel looks for the `task_struct` with that pid,
- a `ps` -> The tool reads /proc, which is generated from `task_struct`,
- when a process dies:
  - its `task_struct` is removed from the task list,
  - freed (returned to the cache),
  - and associated structures (`mm_struct`, `files_struct`, etc.) are freed as well.
