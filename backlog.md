# Backlog

Ce fichier contient les tâches associées aux sprints. Pour chaque tâches, nous avons le temps estimé pour sa réalisation, la priorité (allant de 1 le plus prioritaire, à 4 la moins prioritaire), et des informations complémentaires.

## Sprint **Analyse et Documentation** 

| Numéro | Tâche | Temps de réalisation (en journée) | Priorité | Information complémentaire | Progression |
|:---|:---|:---|:---|:---|:---|
| 1 | Documenter les 7 commandes `grid` (gridsub, gridstat, ...) | 1 | 1 | Description + Commentaires (fonctionne ou pas, comportement) | :heavy_check_mark: |
| 2 | Documenter le code | 20 | 1 | Déterminer le rôle des composants de l'architecture (Description, Entrées / Sorties, *Traduction ou Adaptation*) | :heavy_check_mark: |
| 3 | Déterminer comment communiquer avec OAR en python | 2.5 | 2 | Documenter l'API (classe pour encapsuler) | :heavy_minus_sign: |
| 4 | Faire un programme pour job | 0.5 | 4 |  | :heavy_check_mark: |
| 5 | Apprentissage: SQLAlchemy | 4 | 2 |  | :heavy_minus_sign: |
| 6 | Apprentissage: Richclic | 1 | 4 |  | :heavy_check_mark: |
| 7 | Apprentissage: FastAPI | 2 | 1 |  | :heavy_minus_sign: |
| 8 | Apprentissage: Prefect | 2 | 1 |  | :heavy_check_mark: |
| 9 | Adapter la structure de la BDD | 0.5 | 3 |  | :x: |
| 10 | Finir le document du cadrage | - | BE | À finir avant le 13/02 | :heavy_check_mark: |
| 11 | Bot Discord | - | BE | bot pour notifier les PR sur le serveur discord | :heavy_check_mark: |

***

Légende:

+ :heavy_check_mark: : Fait
+ :heavy_minus_sign: : En cours
+ :x: : Non traité

## Sprint **Choix et Réalisation**

### Commande CLI

| commande    | Fonctionnalité                                                                                   | Importance | Progression |
| :---------- | :----------------------------------------------------------------------------------------------- | :--------- | :------ |
| gridcluster | Afficher les clusters disponibles sur Gricad                                                     | 2          |  |
|             | Afficher des informations sur les clusters disponibles sur Gricad.                               | 4          |  |
|             | Afficher des informations avancés sur les clusters disponibles sur Gricad.                       | 3          |  |
|             | Afficher l'utilisation de chaque cluster/l'état de chaque cluster                                | 3          |  |
|             | Afficher les informations sous forme visuelle (graphe)                                           | 3          |  |
|             |                                                                                                  |            |  |
| griddel     | Supprimer une campagne                                                                           | 1          |  |
|             | Suspendre une campagne                                                                           | 2          |  |
|             | Reprendre une campagne                                                                           | 2          |  |
|             |                                                                                                  |            |  |
| gridevents  | Annuler un job                                                                                   | 1          |  |
|             | Afficher les événements d'une campagne                                                           | 2          |  |
|             | Afficher tous les événements actuels                                                             | 2          |  |
|             | Affiche tous les événements, même ceux qui sont fermés                                           | 4          |  |
|             | Afficher les détails d'un événement                                                              | 2          |  |
|             | Corriger / fermer un événement                                                                   | 2          |  |
|             | Resoumettre un job                                                                               | 2          |  |
|             |                                                                                                  |            |  |
| gridnotify  | Afficher la liste des notifications en CLI                                                       | 2          |  |
|             | S'abonner aux notifications par e-mail                                                           | 2          |  |
|             | S'abonner aux notifications par slack                                                            | 3          |  |
|             | Se désabonner des notifications spécifiques                                                      | 2          |  |
|             | Choisir le niveau de sévérité des notifications                                                  | 3          |  |
|             |                                                                                                  |            |  |
| gridsub     | Ajouter une campagne                                                                             | 1          |  |
|             | Ajouter des jobs dans une campagne existante                                                     | 4          |  |
|             | Afficher le JDL d'une campagne                                                                   | 2          |  |
|             | Spécifier un fichier JDL comme entrée                                                            | 1          |  |
|             | Pouvoir spécifier la chaîne de caractères JSON depuis le CLI                                     | 1          |  |
|             | Pouvoir spécifier la chaîne de caractères JSON contenant le tableau des paramètres depuis le CLI | 1          |  |
|             |                                                                                                  |            |  |
| gridstat    | Obtenir le fichier stderr d'un job                                                               | 2          |  |
|             | Obtenir le fichier stdout d'un job                                                               | 1          |  |
|             | Afficher les informations d'une campagne spécifique à partir de son ID                           | 3          |  |
|             | Afficher toutes les informations d'une campagne                                                  | 2          |  |
|             | Afficher le résultat sous forme de JSON                                                          | 5          |  |
|             | Afficher les jobs commençant à partir d'un offset défini                                         | 5          |  |
|             | Afficher les événements ouverts sur une campagne à partir de l'ID de la campagne                 | 2          |  |
|             | Afficher les informations à propos d'un job à partir de son ID                                   | 3          |  |
|             | Afficher les informations du planificateur du cluster sur un job                                 | ?          |  |
|             | Supprimer le titre des colonnes                                                                  | 5          |  |
|             | Afficher le retour au format JSON avec une indentation intelligente                              | 3          |  |
|             | Afficher seulement les campagnes d'un utilisateur à partir de son USERNAME                       | 4          |  |
|             | Obtenir le fichier JDL d'une campagne à partir d'un ID                                           | 2          |  |

### Back end

| Fonctionnalité                                                         | Importance | Progression |
| :--------------------------------------------------------------------- | :--------- | :------ |
| Stocker les campagnes                                                  | 1          |  |
| Gestion de campagnes multiples                                         | 1          |  |
| Création d'une liste de jobs à soumettre pour une campagne             | 1          |  |
| Utilisation d'un scheduler sans famine                                 | 1          | :heavy_check_mark: |
| Soumission adaptative des jobs d'une campagne                          | 1          |  |
| Respecter l'affinité des clusters                                      | 2          |  |
| Respecter l'affinité des users                                         | 2          |  |
| Ne pas surcharger les clusters (stress factor)                         | 2          |  |
| Fournir une API complète pour l'utilisateur                            | 3          |  |
| Version locale                                                         | 4          |  |
| Utiliser les JWT Token pour l'authentification auprès de l'API d'OAR 3 | 1          | :heavy_check_mark: |
| Concaténer des jobs lorsqu'ils sont trop courts                        | 2          |  |
| Être capable d’interagir avec l'API d'OAR 3                            | 1          | :heavy_check_mark: |
|                                                                        |            |  |
| Supporter les campagnes normales                                       | 1          |  |
| Supporter les campagnes en best effort                                 | 1          |  |
| Supporter les campagnes en semi best effort                            | 4          |  |
| Supporter les campagnes en nightly                                     | 4          |  |
|                                                                        |            |  |
| Pouvoir parser des fichiers JDL                                        | 1          | :heavy_check_mark: |
| Stocker les données de JDL en BDD                                      | 1          |  |
| Supporter les macros variables des fichiers JDL                        | 2          |  |
| Retourner des messages claires lors de l’interaction avec l'API        | 2          |  |
| Mettre à jour la BDD en fonction de l'état des jobs en cours sur OAR 3 | 1          |  |

***

Légende:

+ :heavy_check_mark: : Fait
+ :heavy_minus_sign: : En cours
+ :x: : Non traité