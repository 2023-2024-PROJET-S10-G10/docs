# Journal de bord

## 29 Janvier

* Étude de la documentation du Projet.
* Création du Trello et du serveur Dicsord.
* Création de l'organisation GitHub et des différents répertoires (`app` et `docs`). 
* Attribution des rôles.
* Début de mise en place de l'environnement de test

## 30 Janvier

* Reunion avec M. Bruno BZEZNIK
* Mise en commun des notes
* Commencement à l'initiation à Ruby
* Fini de la mise en place l'environnement de test
* Documentation environnement de test
* Mise en place d'un dump en json pour garder une trace des tests
* Récupération d'info sur le passage des tests

## 31 Janvier

* Réunion avec M. Olivier RICHARD
* Finition de l'environnement de test
* Travail sur le workflow
    * Début d'intégration des tests au workflow
* Configurer les connexions ssh pour GRICAD
* Prise de connaissance sur Poetry et NixOS
* Prise de décision  pour les versions (ex: version de python: `3.10.12`)

## 1 Février

* Revue de code de l'environnement pour les tests Unitaires
* Étudier la structure de la BDD
    * Mise au propre de la BDD avec plantuml
* Mise en place de l'environnement virtuel avec Poetry sur nos machines (grâce au fichier de configuration écrite la veille)
* Fin d'intégration des tests au workflow
* Ajout de poetry au workflow pour les tests

## 2 Février

* Discussion et partage sur l'architecture du projet
* Rédaction du document de cadrage demandé par M. Emmanuelle TRÉHOUST

## 5 Février

* Réunion avec M. Olivier RICHARD
* Commencement de la rédaction d'une documentation sur les commandes `grid`
* Planification du sprint d'"Analyse et Documentation" (tâches, temps et priorité)
* Installation de fastAPI

## 6 Février

* Commencement de l'apprentissage de Prefect
* Commencement de la documentation de l'API
* Commencement de l'apprentissage de FastAPI
* Commencement de l'apprentissage de SQLalchemy
* Ajout d'élément dans la documentation sur les commandes
* Création test de campagnes de jobs, utiliser les commandes `grid`
* Création d'API de test via FastAPI
* Commencement de la documentation OAR3 concernant FastAPI.

## 7 Février

* Finalisation de la documentation sur les commandes
* Documentation API
    * Découverte de nouvelles routes via le code ruby et le linkage fournie en réponse
* Apprentissage du protocole ASGI
* Documentation OAR3 concernant la gestion des éléments ASGI
* Avancement dans les recherches sur Prefect
* Apprentissage SQLalchemy (gestion des champs null et des énumérations)

## 8 Février

* Recherche sur le protocole ASGI
* Finalisation de la documentation d'API OAR3
* Recherche d'informations sur Prefect faite
* Apprentissage SQLalchemy continue
* Documentation API de CiGri continue
* Début mise en place encapsulation API OAR3 en python pour cigri

## 9 Février

* Mise en place de l'API-client (pas encore de requête)
* Mise en place de l'API-client stub
* Création de tests unitaire sur l'API-client stub
* Finalisation de la documantation de l'API de CiGri
* Attributions de contraintes sur la BDD
* Prises de rendez-vous
* Tester des usages de prefect (github action, API key prefect, workpool)

## 12 Février

* Création du design de l'API client + début de l'implémentation
* Commencement de la table versionning dans SQLalchemy
* SQLalchemy select
* Poursuite de la documentation du code

## 13 Février

* Reunion avec M. Bruno BZEZNIK
* Mise en commun des notes
* Poursuite de la documentation du code
* Finalisation de la structure pour l'API client oar3
* Commencement d'implémentation des appels aux différentes routes
* Test et observations de l'accès à OAR3
* Poursuite de SQLalchemy

## 14 Février

* Réunion avec M. Olivier RICHARD
* Poursuite de la documentation du code
* Recherche de fonctionnalités dans prefect
* Documentation de l'accès à OAR3
* Suite de l'implémentation des routes

## 15 Février

* Finalisation de la documentation du code
* Tests manuels des flows, task, block (avec utilisation de JSON) de Prefect
* Implémentation d'un test pour l'API + débogage laborieux

## 16 Février

* Finalisation de l'implémentation d'un test unitaire sur le client d'API
* Discussion et schémas autour de l'utilisation de tests unitaires contenant des appel d'API réelle
* Étude des solution d’équivalence pour représenter les campagnes et les jobs dans Prefect
* Finalisation de la documentation de RichClic

## 19 Février

* Composition du schéma d'architecture de CiGri v4 avec l'utilisation de certaines fonctionnalités de Prefect
* Recopie du schéma de la BDD sur SQLalchemy
* implémentation de méthode pour encapsuler les routes de l'API

## 20 Février

* Commencement du diaporama de l'audit de mi-parcours
* Commencement de la remise en forme de la docummentation de Prefect
* Réalisation du schéma de l'architecture
* Poursuite de la rédaction de la liste de fonctionnalités
* Suite des test set des implémentations des méthodes pour les différentes routes de l'API

## 21 Février

* Finalisation du diaporama pour l'audit de mi-parcours
* Finalisation de la remise en forme de la docummentation de Prefect
* Finalisation de la liste des fonctionnalités en précisant l'importance et la difficulté
* Mise à jour du diagramme de Gantt
* Poursuite de l'implémentation des méthodes pour les routes de l'api OAR3

## 22 Février

* Suite de l'implémentation des requêtes aux routes d'oar API
* Avancer le développement du JDL paser + ajout de queries pour la BDD
* Réaliser les descriptions de commandes grid avec RichClic

## 23 Février

* Suite de l'implémentation des requêtes aux routes d'oar API
* Préparer la présentation (Audit)
* Continuer l'implémentation du parser JDL
* Continuer l'implémentation des queries pour la BDD
* continuer d'implémenter la gestion des paramètres cli

## 4 Mars

* Finalisation du poster
* Finalisation encapsulation API OAR3
* Développement d'une FAP pour le scheduler
* Tests unitaires pour les FAP
* Commencement de développement du scheduler
* Finalisation des options cli pour les commandes cigri
* Codage du manager événementiel
* Review de PR
* Ajout de requêtes SQL dans queries.py
* Ajout de tests sur les méthodes de queries
* Amélioration de la configuration de la BDD

## 5 Mars

* Début des commandes grids avec du mocking
* Mise en place des pre commits
* Mise à jour le github action pour les tests de requêtes
* Implémentation des tests pour les requêtes
* Amélioration de la confiiguration de la BDD (contraire d'unicité et autres)
* Initialisation d'un scheduler de base avec tests
* Initialisation d'une base pour l'API de CiGri
* Ajout d'un "ApiClientStub handle multiple mocked value" avec tests

## 6 Mars

* Ajout d'un assert pour les exceptions dans le TestManager
* Finalisation de l'API de CiGri
* Implémentation dde la commande gridcluster
* Commencement de l'implémentation de griddel
* Implémentation des tests pour JDLParser
* Amélioration des requêtes + tests

## 7 Mars

* Poursuite du code de griddel
* Réorganisation de branches locales
* Organisation pour implémentation des routes API CiGri v4

## 8 Mars

* Ajout de la BDD et du jdl parser sur la branche main
* Début d'ajout d'une route dans le backend
* Mise en pause de la fonction griddel (par manque de possibilités de test)
* Commencement de la fonction gridsub (en test)
* Préparation de queries pour les fonctionnalités de priorité 2

## 11 Mars

* Création de requêtes de récupérations de multiples campagnes et évènements, tests associés
* Finalisation de l'implémentation de gridcluster
* Poursuite de la réalisation de gridstat
* Création de l'Initiator

## 12 Mars

* Rédaction du Rapport
* Création du Flyer

## 13 Mars

* Finalisation du Rapport
* Finalisation du diaporama de présentation

## 14 Mars

* Finir les tâches en cours

