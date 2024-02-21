# Liste des fonctionnalités

Ordre d'importance 1 = max \
Difficulté 1 = min

## Commande CLI

| commande    | Fonctionnalité                                                                                   | Importance | difficulté |
| :---------- | :----------------------------------------------------------------------------------------------- | :--------- | :--------- |
| gridcluster | Afficher les clusters disponibles sur Gricad                                                     | 2          | 1          |
|             | Afficher des informations sur les clusters disponibles sur Gricad.                               | 4          | 2          |
|             | Afficher des informations avancés sur les clusters disponibles sur Gricad.                       | 3          | 2          |
|             | Afficher l'utilisation de chaque cluster/l'état de chaque cluster                                | 3          | 3          |
|             | Afficher les informations sous forme visuelle (graphe)                                           | 3          | 4          |
|             |                                                                                                  |            |            |
| griddel     | Supprimer une campagne                                                                           | 1          | 1          |
|             | Suspendre une campagne                                                                           | 2          | 2          |
|             | Reprendre une campagne                                                                           | 2          | 2          |
|             |                                                                                                  |            |            |
| gridevents  | Annuler un job                                                                                   | 1          | 2          |
|             | Afficher les événements d'une campagne                                                           | 2          | 2          |
|             | Afficher tous les événements actuels                                                             | 2          | 3          |
|             | Affiche tous les événements, même ceux qui sont fermés                                           | 4          | 2          |
|             | Afficher les détails d'un événement                                                              | 2          | 2          |
|             | Corriger / fermer un événement                                                                   | 2          | 3          |
|             | Resoumettre un job                                                                               | 2          | 4          |
|             |                                                                                                  |            |            |
| gridnotify  | Afficher la liste des notifications en CLI                                                       | 2          | 2          |
|             | S'abonner aux notifications par e-mail                                                           | 2          | 2          |
|             | S'abonner aux notifications par slack                                                            | 3          | 2          |
|             | Se désabonner des notifications spécifiques                                                      | 2          | 2          |
|             | Choisir le niveau de sévérité des notifications                                                  | 3          | 3          |
|             |                                                                                                  |            |            |
| gridsub     | Ajouter une campagne                                                                             | 1          | 1          |
|             | Ajouter des jobs dans une campagne existante                                                     | 4          | 2          |
|             | Afficher le JDL d'une campagne                                                                   | 2          | 1          |
|             | Spécifier un fichier JDL comme entrée                                                            | 1          | 1          |
|             | Pouvoir spécifier la chaîne de caractères JSON depuis le CLI                                     | 1          | 1          |
|             | Pouvoir spécifier la chaîne de caractères JSON contenant le tableau des paramètres depuis le CLI | 1          | 1          |
|             |                                                                                                  |            |            |
| gridstat    | Obtenir le fichier stderr d'un job                                                               | 2          | 2          |
|             | Obtenir le fichier stdout d'un job                                                               | 1          | 2          |
|             | Afficher les informations d'une campagne spécifique à partir de son ID                           | 3          | 2          |
|             | Afficher toutes les informations d'une campagne                                                  | 2          | 3          |
|             | Afficher le résultat sous forme de JSON                                                          | 5          | 2          |
|             | Afficher les jobs commençant à partir d'un offset défini                                         | 5          | 3          |
|             | Afficher les événements ouverts sur une campagne à partir de l'ID de la campagne                 | 2          | 3          |
|             | Afficher les informations à propos d'un job à partir de son ID                                   | 3          | 2          |
|             | Afficher les informations du planificateur du cluster sur un job                                 | ?          | ?          |
|             | Supprimer le titre des colonnes                                                                  | 5          | 1          |
|             | Afficher le retour au format JSON avec une indentation intelligente                              | 3          | 2          |
|             | Afficher seulement les campagnes d'un utilisateur à partir de son USERNAME                       | 4          | 2          |
|             | Obtenir le fichier JDL d'une campagne à partir d'un ID                                           | 2          | 1          |

## Back end

| Fonctionnalité                                                         | Importance | difficulté |
| :--------------------------------------------------------------------- | :--------- | :--------- |
| Stocker les campagnes                                                  | 1          | 1          |
| Gestion de campagnes multiples                                         | 1          | 2          |
| Création d'une liste de jobs à soumettre pour une campagne             | 1          | 3          |
| Utilisation d'un scheduler sans famine                                 | 1          | ?          |
| Soumission adaptative des jobs d'une campagne                          | 1          | 3          |
| Respecter l'affinité des clusters                                      | 2          | 5          |
| Respecter l'affinité des users                                         | 2          | 3          |
| Ne pas surcharger les clusters (stress factor)                         | 2          | 2          |
| Fournir une API complète pour l'utilisateur                            | 3          | 2          |
| Version locale                                                         | 4          | 5          |
| Utiliser les JWT Token pour l'authentification auprès de l'API d'OAR 3 | 1          | 2          |
| Concaténer des jobs lorsqu'ils sont trop courts                        | 2          | 5          |
| Être capable d’interagir avec l'API d'OAR 3                            | 1          | 3          |
|                                                                        |            |            |
| Supporter les campagnes normales                                       | 1          | 1          |
| Supporter les campagnes en best effort                                 | 1          | 3          |
| Supporter les campagnes en semi best effort                            | 4          | 5          |
| Supporter les campagnes en nightly                                     | 4          | 5          |
|                                                                        |            |            |
| Pouvoir parser des fichiers JDL                                        | 1          | 1          |
| Stocker les données de JDL en BDD                                      | 1          | 2          |
| Supporter les macros variables des fichiers JDL                        | 2          | 2          |
| Retourner des messages claires lors de l’interaction avec l'API        | 2          | 5          |
| Mettre à jour la BDD en fonction de l'état des jobs en cours sur OAR 3 | 1          | 4          |
