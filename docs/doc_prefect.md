# PROJET S10 - Prefect

## Description

Prefect est un outil d'orchestration de workflow pour construire, observer et réagir aux pipelines de données.

Il permet de transformer n'importe quel fonction python en une unité de travail qui peut être observé et orchestré, à l'aide de décorateurs.

Il est possible de l'utiliser en CLI, et de se connecter soit avec l'interface Web ou une clé API.

Il permet de gérer des flows multiple simultanées et permet de visualiser un dashboard (interface web) montrant les informations des flows d'exécutions.

### Utilisation de `Work-pool`, `Deployment`, `Flow` et `Task`

Les Flows peuvent être divisés en Tasks. Mais les Tasks sont éxécutées de manière séquentielle, ce qui les rends trop différentes des jobs parralélisables. De plus, une task ne peut appeler une autre task.
Les flows sont parralélisables, et nous pouvons invoquer de multiples flows à partir d'un flow dit Master. Il est possible d'invoquer un flow avec des paramètres.

Les flows "Master" sont contenus dans des déploiements, qui sont eux-même contenus dans un work-pool.

![Structure dans Prefect](./img/orga_prefect.png)

Les "work pools" et les "workers" servent de lien entre l'environnement d'orchestration de Prefect et l'environnement d'exécution. Lorsqu'un déploiement déclenche l'exécution d'un flow, celui-ci est assigné à un "work pool" spécifique pour la planification. 

Un "worker" opérant dans l'environnement d'exécution peut alors interroger son "work pool" désigné pour rechercher de nouveaux flux à exécuter.

### Planification (Schedules)

Il permet d'automatiser la création de nouveaux flow d'exécution pour les déploiements. (Schedules utilise l'API)

### Automatisations

Possibilité de configurer des actions que Prefect exécutera automatiquement en se basant sur les événements. (event-basis triggering)

### Déploiement

#### Local

On peut déployer Prefect sur notre machine.

Il donne un contrôle total sur l'environnement d'exécution, mais nous devenons responsable de la maintenance du support.

#### Distant

Possibilité d'utiliser des services cloud comme AWS, Azure et même Prefect Cloud.

#### Docker

Possibilité de mettre des workflow dans des conteneurs Docker pour les déployer facilement sur les plateforme prenant en charge Docker.

## Équivalence avec CiGri

Nous avons vu précédemment que nous pouvons exécuter des programmes python et les faire apparaître dans l'interface web de Prefect.

Maintenant, nous voulons savoir si Prefect pourrait remplacer CiGri, du moins pour certaines fonctionnalités. Pour cela, nous allons voir si il existe des équivants pour les commandes `grid`, puis nous allons voir pour les types de jobs.

### Commandes grid
 
#### gridevent

Utilisation des [Automations](https://docs.prefect.io/latest/concepts/automations/) de Prefect pour configurer des triggers pour des événements de plusieurs natures:
- Changement d'état d'un flow run.
- L'état du work pool
- L'état du déploiement
- Des seuils de métrique comme la durée moyenne, la latence et la progression de l'exécution.
- Des événements customisables.

Et pour chaque événement déclenché, il est possible d'associer une action à réaliser. 

#### gridnotify

Dans les Automations de Prefect, Prefect utilise le service [Sendgrid](https://sendgrid.com/en-us/pricing) pour les notifications sur Discord, Email, Slack, Teams, ...

#### gridstat

Il est possible d'obtenir des informations sur un flow précis avec la commande `prefect flow-run inspect <ID>`.

De même pour le deploiement, avec la commande `prefect deployment inspect <NAME>`.

De même pour un work-pool, `prefect work-pool inspect <NAME>`.

#### griddel

En ligne de commande, il est possible d'exécuter, annuler et supprimer un flow avec la commande `prefect flow-run` + {`execute`;`cancel`;`delete`} + `<ID>`.

Nous pouvons même supprimer des flows déjà terminés (gridclean), mais pour l'instant, nous n'avons pas la notion de base de données.

De plus, pour les deploiement, nous pouvons supprimer, et modifier le deploiement avec la commande `prefect deployment` + {`apply`;`delete`}

Pour les work-pools, nous pouvons les créer, mettre à jour, supprimer, mettre en pause et les reprendre. `prefect work-pool` + {`create`;`update`;`delete`;`pause`;`resume`} + `<NAME>`

#### gridsub

Nous pouvons scheduler un flow avec `prefect deployment run '<name-flow>/<name-deployment>'`.

Et pour le lancer, `python <file.py>`.

Ou tout faire avec une seule commande: `prefect flow-run run <ID>`.

#### gridcluster

_Pas de piste interessante_

## Campagnes et Jobs

### Propositions d'équivalence

TODO: Pros & Cons

Pour trouver les équivalents des campagnes et des jobs dans prefect, nous avons dresser un tableau de proposition:

| CiGri    | Prefect P1 | Prefect P2 | Prefect P3 | Prefect P4 |
| -------- | ---------- | ---------- | ---------- | ---------- |
| Campagne | Flow       | Flow       | Deployment | Work-pool  |
| Job      | Task       | (sub)Flow  | Flow       | Deployment |

Maintenant, il faut peser le pour et le contre.
    
**Prefect P1**
- Inconvénients:
    - Impossible d'intéragir avec la task de façon individuelle

**Prefect P2**
- Avantages:
    - Permet d'utiliser les tasks pour avoir une décomposition plus fine
- Inconvénients:
    - Impossible de rajouter des flows (ce sont des subflows) dans un flow

**Prefect P3**
- Avantages:
    - Possibilité d'ajouter des exécutions de flows 
- Inconvénients:
    - Impossible de mettre en pause un déploiement

**Prefect P4**
- Avantages:
    - Possibilité de supprimer, mettre en pause et reprendre un work-pool

### Choix

Après beaucoup de discussions, nous avons fait des choix: Utiliser Prefect comme historique et un outil de notification, c'est-à-dire, pour chaque changement d'état sur OAR, Prefect sera informé par CiGri V4 en créant un flow dans un déploiement representant un état, dans un work-pool associé à la campagne.

Donc, nous avons choisi d'utiliser les work-pools comme campagne, les flows comme job et utiliser les déploiements représentants les états du job sur OAR.

## Fonctionnalités

TODO: fonctionnalité
