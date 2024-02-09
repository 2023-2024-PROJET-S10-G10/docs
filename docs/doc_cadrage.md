# **Document de cadrage - Groupe 10**

## **I. Cahier des charges**

### **1. Contexte et Enjeux**

Dans un contexte de recherche scientifique, il peut être nécessaire d'utiliser des calculateurs pour réaliser des simulations, analyser des données et autres.
CiGri est utilisé dans ce contexte pour permettre aux scientifiques d'empreinter des ressource de calcul afin de réaliser ces tâches.
Cet intergiciel est destiné à être utilisé par les labos de la région grenobloise mais pourraient être étendu à la région lyonnaise.
Il existe déjà une version de CiGri en place actuellement. Les fonctionnalités sont donc déjà définies. Mais nous souhaitons mettre le logiciel à jour vers un langage plus récent afin de le maintenir plus facilement.
Le problème à résoudre est de définir correctement l'architecture et les fonctionnalités afin de pouvoir commencer le développement en Python en ayant une vision globale du projet.
Pour les utilisiteurs, rien de très important ne devrait changer, l'avantage sera la facilité pour les développeurs chargé de maintenir le projet et de le faire évoluer.


### **2. Objectifs (et Exigences fonctionnelles)**

L'objectif est de livrer un projet fonctionnel permettant de faire tout ce que permet de faire CiGri3 mais codé en python au lieu de Ruby. Nous souhaitons aussi fournir une documentation complète pour les développeurs et les utlilisateurs afin de permettre une reprise simple de l'évolution du projet.


### **3. Processus de validation**

Pour valider la réussite de ce projet, nous nous attendons à réaliser le portage complet et fonctionnel de l'application CiGri3, incluant toutes les fonctionnalités présentes actuellement.


## **II. organisation projet**

### **1. Demarche & Planning**

Dans l'application des méthodes agiles, nous avons des routines comme les daily-meeting du matin, d'une durée de 5-10 minutes selon l'ordre du jour et qui sont résumés dans des rapports présents dans notre dépôt dédié à la documentation. Nous avons aussi un logbook mise à jour au fur et à mesure. Mais également la planification des sprints à travers un diagramme de Gantt.

(voir diagramme de Gantt)

Cependant, les fonctionnalités n'ayant pas encore été définies, nous ne pouvons pas planifier plus que ça.


### **2. Ressources**

En ce qui concerne l'équipement et le matériel, nous avons besoin de nos ordinations avec une configuration adaptée. 

Nous n'avons pas de budget prévisionnel.

Au niveau humain, nous sommes un groupe de quatre futurs ingénieurs, ayant des compétences en python, en structure de base de données, et des _softskills_. De plus, nos encadrants sont des chercheurs en Informatique qui ont utilisé et travaillé sur sur les versions précédentes de l'outil, CiGri.


### **3. organisation du projet et communication**

Notre équipe est composé de:

| Nom                       | Rôle                             |
|:------------------------- |:-------------------------------- |
| Killian GRICOURT          | **Chef de projet** / Développeur |
| Antoine BONFILS           | **Scrum Master** / Développeur   |
| Diego CORREIA DE OLIVEIRA | **Tech lead** / Développeur      |
| Tanguy DELAS              | **Communication** / Développeur  |

Nous avons rédigé une charte de règle et valeurs: 

```markdown
# Règles et Valeurs Communes pour le Groupe 10 du PROJET S10

Rédigé le: 29/01/2024

En tant que membre du groupe 10 du Projet S10, nous nous engageons à respecter un ensemble de **règles** et de **valeurs communes** (**en plus** de ceux et celles imposés par les enseignants) pour garantir une collaboration **efficace**, **harmonieuse** et **productive**, ainsi qu'éviter le maximum de **conflits inutiles** et **non-productifs**.

1. ***Communication ouverte et respectueuse***: Nous nous engageons à maintenir une communication **ouverte** et **respectueuse** entre tous les membres du groupe. Nous nous efforcerons de donner notre avis de manière **constructive**, d'**écouter attentivement** les autres et de résoudre les désaccords de manière **respectueuse**.

2. ***Engagement et participation***: Chaque membre du groupe s'engage à **participer activement** aux réunions, aux tâches assignées et aux discussions liées au projet. Nous considérons que l'engagement de chacun est essentiel pour atteindre nos objectifs.

3. ***Répartition équitable des tâches***: Nous nous efforcerons de répartir **équitablement** les tâches et les responsabilités au sein du groupe. Chacun devra contribuer de manière équilibrée en fonction de ses compétences et de son emploi du temps.

4. ***Résolution constructive des conflits***: Si des conflits surgissent, nous nous engageons à les aborder de manière **constructive** et à chercher des solutions **mutuellement acceptables**.

5. ***Respect des horaires de travail***: Nous tiendrons compte des horaires de travail convenus et respecterons les besoins de chacun en matière de disponibilité lors de la planification des réunions et des échéances en dehors des heures inscrites sur ADE.

6. ***Partage de connaissances***: Nous encourageons **le partage des connaissances** et des **compétences** au sein du groupe, afin de favoriser la croissance **personnelle** de chacun et le succès **collectif**.

7. ***Responsabilité personnelle***: Chaque membre est responsable de **son propre comportement** et de **sa contribution** au groupe. Nous nous efforçons de maintenir une attitude **professionnelle** et **respectueuse** en tout temps.

Nous acceptons collectivement ces règles et valeurs communes et nous nous engageons à les respecter. Le non-respect de ces règles entraînera des actions appropriées, y compris des discussions au sein du groupe pour résoudre les problèmes.

Nous sommes convaincus que le respect de ces règles et de ces valeurs communes contribuera à renforcer notre groupe et à mener à bien notre projet avec succès.
```

Tout au long du projet, nous mettons à jour nos documentation (rapports des daily-meetings, logbook ,évolution du diagramme de Gantt) et nous tenons au courant nos encadrants (M. BZEZNIK et M. RICHARD).

Pour l'équipe étendue, nos encadrants sont des chercheurs en Informatique qui ont utilisé et travaillé sur les versions précédentes de CiGri. M. BZEZNIK est créé les trois premières versions de CiGri, et M. RICHARD a travaillé sur des projets en lien avec CiGri. Ils nous apportent une expertise précise sur nos réflexions et nos travaux.

Pour la validation des étapes du projet, nous n'avons pas une planification précise; nous pensions faire une revue de projet après ces étapes:

- Définition des fonctionnalités présentes dans la version 3 de CiGri, et de celles à ajouter dans la version 4, et la rédaction du cahier des charges (documentation précise).

- Implémentation de la solution et des programmes en python (toujours avec une documentation fidèle).

- Mise en place des différents services associés à CiGri.

Les principales méthodes de communication avec le maître d'ouvrage sont: les discussions sur `Slack` et les divers réunions réalisées à la demande des membres du groupe, et / ou de celle d'un encadrant.


### **4. Risques**

#### **SWOT**

(S)trength : Les membres du groupe se connaissent bien. La communication est fluide, directe, et efficace. Ils ont l'habitude de travailler ensemble ce qui permet de répartir plus efficacement les tâches. Confiance.

(W)eaknesses : Les membres du groupe se connaissent bien. Il arrive que les membres se dissipent. Aucun de nous ne connais le ruby.

(O)pportunities : Nous pouvons discuter de sujet très techniques avec nos encadrants. ils ont créer le logiciel à migrer et peuvent répondre à toutes nos questions.

(T)hreats : Deadline courte. Documentation technique incomplète. Difficulté d'obtenir un environnement de tests fonctionnels.

#### **Plan de mitigation des risques**

| Intitulé                                                            | Probabilité d'occurrence | Gravité | Criticité | Action préventive                                                                        | Action correctives                  |
| ------------------------------------------------------------------- | ------------------------ | ------- | --------- | ---------------------------------------------------------------------------------------- |:----------------------------------- |
| Dissipation d'intension                                             | 3                        | 2       | Modéré    | Charte des règles et des valeurs communes                                                | Scrum master met le hola            |
| Deadline courte (pas le temps de faire tout ce qu'on voulait faire) | 3                        | 3       | Forte     | Planification (diagramme de Gantt), daily meeting, revue de projet                       | Justification du travail non achevé |
| Difficulté d'obtenir un environnement de tests fonctionnels         | 4                        | 1       | Faible    | Avoir fini les tâches précédentes, obtenir un nixos-compose qui contient l'environnement | Explication des difficultés         |

Correspondances des coefficients pour la probabilité d'occurrence et la gravité:

| Probabilité d'occurrence | Coefficient |     | Gravité          | Coefficient |
| ------------------------ | ----------- | --- | ---------------- | ----------- |
| De 0% à 25%              | 1           |     | Peu importante   | 1           |
| De 25% à 50%             | 2           |     | Importante       | 2           |
| De 50% à 75%             | 3           |     | Très importante  | 3           |
| De 75% à 100%            | 4           |     |                  |             |

### **5. Indicateurs de pilotage du projet**

Qualité de la motivation : Suivi des horaires de début et de fin

Suivi de la qualité du code : revue de code, discussion, test unitaires, tout obligatoire

Délais: Suivi en temps réel des tâches (logboook, daily report)
        + planification (sprint, gantt, trello)

