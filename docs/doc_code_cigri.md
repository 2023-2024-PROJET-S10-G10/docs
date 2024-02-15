# PROJET S10 - Analyse du code en Ruby

***

Nous avons réalisé l'analyse du code de CiGri V3. Notre analyse est découpé selon les répertoires utilisés:

- [`api`](#api):
- `bin`: Contient l'implémentation des commandes `grid`. [voir la documentation réalisée](doc_cmd.md)
- [`database`](#database):
- [`debian`](#debian):
- [`doc`](#doc): Contient la documentation déjà présente
- [`etc`](#etc):
- [`lib`](#lib):
- [`modules`](#modules):
- [`sbin`](#sbin):
- [`spec`](#spec):
- tmp: Contient des fichiers de tests supposément temporaires (création de cluster, de campagne et de job, exemple de JDL et script pour reset / initialisé la base de données)
- `tools`: Contient des fichiers de configuration d'OAR et de CiGri, et des recettes KAMELEON pour la génération.
- [`/`](#) :

***

## api

### cigri-api.rb

Fichier contenant l'ensemble du code de l'API incluant notamment les routes disponibles dans l'API avec le code backend de leur comportemet. (Voir doc API)

### config.ru

Fichier permettant de configurer le path et de lancer l'API de CiGri.

### launch_api.sh.in

Lance l'API avec l'utilisateur CiGri.

***

## database

### init_db.rb

Permet d'initialiser la base de données de CiGri.

### psql_structure.sql

Contient la structure de la base de données en PostGreSQL.

***

## debian

### changelog

Changelog de CiGri (vide, car une seule version existe de l'application).

### cigri-server.dirs

Définie un ensemble de directory utilisé par d'autres script côté serveur.

### cigri-server.postinst

Script de post install côté serveur.

### cigri-user.dirs

Définie un ensemble de directory utilisé par d'autres scripts côté client.

### Compat

Défini le niveau de compatibilité (la version) du debhelper¹ qui est requis pour les différents helpers utilisés dans `debian/rules`. La version de debhelper renseignée est la 9.

¹: ensemble d'outils pour simplifier la construction des paquets Debian

### control

Contient des informations importantes comme ses caractéristiques (Nom et version de l'application), sa dépendance vis-à-vis d'autres packages, sa version, sa source, son mainteneur, sa licence, sa description, etc.

Les packages décrits sont : cigri-server, cigri-user et cigri-common.

### copyright

Contient les copyrights de CiGri.

### docs

Ne contient pas d'information.

### rules

Makefile permettant d'installer les différents agents de l'application (serveur/client).

### source/format

Précise la version du format `3.0 (quilt)` des paquets sources de Debian. Cela est utilisé lors de la construction du paquet Debian à partir de son code source.

***

## doc

### documentation

Contient toute la documentation de CiGri.

#### cigri_db.dia

Diagramme représentant la base de données de CiGri au format dia.

#### cigri_metascheduler.dia

Diagramme représentant le fonctionnement global du meta scheduler au format dia.

#### doc_admin.rst

Ce fichier contient toute la documentation reservée à l'admin. Et contient majoritairement une documentation non terminée sur comment installer CiGri, setup les certificats pour l'API OAR et tester l'installation.

#### doc_api.rst

```bash
=========== ======================================= ==========================================================
HTTPrequest URL                                     Purpose
=========== ======================================= ==========================================================
GET         /                                       List the available links
GET         /clusters                               List all clusters available in Cigri
GET         /clusters/<cluster_id>                  Get details on a specific cluster
GET         /campaigns                              List of all running campaigns
GET         /campaigns/<campaign_id>                Get details on a specific campaign
GET         /campaigns/<campaign_id>/jdl            Get the expanded JDL of a campaign
GET         /campaigns/<campaign_id>/jobs           List all jobs of a specific campaign (See `API options`_)
GET         /campaigns/<campaign_id>/jobs/<job_id>  Get details of a specific job of a specific campaign
POST        /campaigns                              Submit a new campaign
PUT         /campaigns/<campaign_id>                Update a campaign (status, name)
DELETE      /campaigns/<campaign_id>                Delete a campaign
GET         /campaigns/<campaign_id>/events         List the open events for the given campaign
DELETE      /campaigns/<campaign_id>/events         Fix (close) all the events for the given campaign
GET         /notifications                          List notification subscriptions for the current user
POST        /notifications/mail                     Subscribe to the mail notification service
POST        /notifications/jabber                   Subscribe to the jabber notification service
DELETE      /notifications/<mail|jabber>            Unsubscribe from a notification service
GET         /events/<id>                            Get a specific event
DELETE      /events/<id>                            Fix (close) a specific event
DELETE      /events/<id>?resubmit                   Fix (close) a specific event and resubmit the job
GET         /gridusage                              Get the current usage state of the grid
GET         /gridusage?from=<date>&to=<date>        Get usage stats between two dates (unix timestamps)
=========== ======================================= ==========================================================
```

Contient la documentation de l'API. De plus, une [documentation plus détaillées](doc_API_cigri.md) est disponible.

#### doc_client.rst

Contient la documentation des commandes CiGri. La documentation est toutefois très légéré au point d'avoir plus de détail avec l'option `-h` des commandes.

#### doc_database.rst

Contient la documentation de la base de données. Concrétement, le fichier est vide et n'apporte que très peu d'information.

#### doc_devel.rst

Fichier de la documentation développeur, ce fichier inclus d'autres fichiers de documentation.

#### doc_header.rst

Contient l'entête de toutes les documentations, avec notamment les auteurs du documents.

#### doc_jdl.rst

Contient la documentation du format de fichier JDL (Job Description Language), ce format de fichier permet de soumettre des campagnes à OAR et cette documentation explique comment utiliser ce langage.

#### doc_lib.rst

Décris les librairie utilisées par CiGri avec une description de ces dernières :

- conflib
- iolib
- clusterlib
- apilib

#### doc_modules.rst

Décris les modules utilisées par CiGri avec une description de ces derniers :

- Columbo
- Monitoring
- Spritz
- Metascheduler
- Scheduler
- Runner
- Nikita
- Almighty
- Collector
- JDL_parser

#### doc_user.rst

Contient la documentation utilisateurs en important d'autres fichiers rst.

#### example.json

Contient un exemple de fichier JDL.

#### global_diagram.dia

Diagramme représentant les relations inter classe de manière générale au format dia.

#### Makefile

Permet de générer la documentation sous différents formats tels que les formats pdf et html.

***

## etc

### api-apache.conf.in

Fichier de configuration de l'API apache qui autorise l'accès depuis les adresses IP `localhost` et `localhost.localdomain` et refuse toutes les autres adresses IP. Ce fichier configure les droits d'accès des utilisateurs.

### api-clients.conf.in

Contient les valeurs pour les variables de l'API (host, port, timeout, SSL).

### cigri.conf.in

Un fichier de configuration en trois parties:

- Unit: fournit une description du service et informe qu'il doit être lancé après le service PostgreSQL.
- Service: fournit ses paramètres et instructions; PermissionsStartOnly, WorkingDirectory, RuntimeDirectory, ExecStart, User, ...
- Install: Indique comment le service doit être installé; dans notre cas, Il est spécifié que le service doit être actif dans la target par défaut.

### ssl/cigri.cnf

Contient un exemple de fichier ssl pour générer un certificat.

### sudoers.d/cigri

Ce fichier permet à tous les utilisateurs de lancer les commandes `gridsub`, `gridstat` et `griddel` sans avoir à saisir de mot de passe. Il permet également de conserver la valeur de la variable d'environnment `CIGRIDIR` quand nous changeons de contexte (utilisateur à SUDO).

### systemd/system/cigri.service

Fichier de setup du service CiGri.

### user_lists

Contient un JSON qui liste les utilisateurs autorisés à lancer des jobs qui ne sont pas en best-effort sur un/des clusters données.

***

## lib

### cigri-clientlib.rb.in

Fichier Ruby contenant les méthodes de bases de requêtage HTTP (get, post, etc) et 2 fonctions de log/d'affichage (affichage de job et log d'événement).

### cigri-clusterlib.rb

Librairie permettant l'accès aux ressources d'un cluster. Cette librairie permet notamment de de récupérer des informations sur les clusters (noms, stress factor, etc) de savoir si le cluster est blacklisté. Mais aussi de gérer le lancement de jobs avec des méthodes pour savoir si un cluster possède des jobs en lancement, des campagnes en cours ou en pause ainsi que son niveau de stress. Ensuite, il y a des méthodes permettant de nettoyer le cache et les robinets. Et finalement, des méthodes de gestion de base des clusters sont présentes pour par exemple soumettre un job.

### cigri-colombolib.rb

La librairie Colombo permet la gestion des notifications et des events. Il y a donc des méthodes permettant le gestion d'événements et de l'envoie de notification. Pour cela, la librairie dispose dans un premier d'une méthode pour collecter des informations sur l'état des clusters. Pour la gestion d'événements, il y a par exemple, des méthodes pour récupérer tous les événement actuellement ouvert, il y a aussi des méthodes pour analyser et essayer de corriger automatiquement les events. Enfin, pour les notifications, plusieurs méthodes permettent la gestion de base du système de notification en se basant sur les méthodes de gestion d'événements, comme notifier l'utilisateur des différents événements.

### cigri-conflib.rb

Cette librairie contient les méthodes de configuration de CiGri. Cela consiste à lire le fichier de configuration et à accèder au différentes variables qui y sont stockées.

### cigri-eventlib.rb

Cette librairie contient les méthodes de gestion d'événement avec notamment la gestion des états des events.

### cigri-exception.rb

Librairie contenant l'ensemble des exceptions possibles dans le système telles que "Not found", "Parse error", "Unauthorized", etc

### cigri-iolib.rb

Librairie très longue contenant des méthodes d'input/output vers la BDD basiques.

### cigri-joblib.rb

Librairie contenant les méthodes liées aux à la gestion de Job pouvant être associé à une extention du fichier `cigri-iolib.rb`.

### cigri-logger.rb

Cette librairie permet de formater et colorer les messages.

### cigri-notificationlib.rb

Librairie permettant le filtrage, le formatage ainsi que l'envoie de notification.

### cigri.rb

Module Ruby important toutes les autres libs du dossiers.

### cigri-restclientlib.rb

Librairie contenant des appels API rest.

### cigri-runnerlib.rb

Librairie contenant des classes utilisées dans le module Runner. Ce fichier contient la class tap qui représente pour chaque cluster s'il est possible d'envoyer des jobs et si oui à quelle fréquence. Cette classe contient des méthodes pour charger les tap de la BDD mais aussi des méthodes de manipulation basiques pour ajuster l'ouverture des taps et leur fréquence.

### cigri-scheduler-affinity.rb

Contient le code du scheduler avec affinité de CiGri.

Les méthodes sont appelés dans cette ordre :

- La méthode `do` qui permet de lancer le process de scheduling :
  - La méthode `compute_stacks` permet de parcourir les couples (clusters, campagnes) et de déterminer les jobs à mettre en attente. Ces jobs sont mis en attente dans la stack.
  - La méthode `setup_queues` construit une file d'attente (queue) par Cluster triée par pair de (task_id, campaign_id). On enlève ensuite les têtes de chaque file d'attente pour les envoyer aux clusters.
  - La méthode `batch_tasks` regroupe les tâches par campagnes.

### cigri-scheduler-fifo.rb

Contient le code du scheduler FIFO de CiGri.

### cigri-xmpp4r-encoding-patch.rb

Fix de xmpp4r, une maintenance qui n'est plus maintenue. Ce fix permet de corriger des problèmes de parsing d'XML (d'après le commentaire du code)

### jdl-parser.rb

Code Ruby permettant la manipulation de JDL ceci inclut :

- Le parsing de JDL
- La sauvegarde de JDL
- L'extention d'un JDL (ajout d'un cluster à un JDL existant)
- La modification de paramètre d'un JDL existant à partir d'un autre JDL (JSON)
- Une méthode pour ajouter les variables de maccros dans un JDL type {CAMPAIGN_ID}

### rack_debugger.rb

Le rack_debugger agit comme un middle ware servant de logger des requêtes HTTP.

### version.rbv

Le module Cigri attribue un numéro de version à la constante VERSION.

***

## modules

### almighty.rb

Ce module s'occupe du chargement des autres modules.

### judas.rb

Juda est un module de notification.

### meta-scheduler.rb

Le meta-scheduler partage les ressources entre les différentes campagnes.

### nikita.rb

Nikita supprime les jobs qui devraient être tués.

### runner.rb

Le runner s'occupe de la soumission de jobs aux clusters. Ce programme genére un fork par cluster qui va gérer tous les aspects de l'envoie de jobs (éviter la surchage, check l'état des jobs en cours, etc)

### updator.rb

L'updator met à jour les métriques afin d'adapter le comportement de CiGri. Par exemple, il récupére les stress factor des clusters.

***

## sbin

### cigri_start.in

### delete_running_campaigns.rb

Il commence par établir une liste de répertoires dans lesquels Ruby recherche les fichiers à charger pour le `require`.

Ensuite, il récupère une liste des campagnes en cours et parcourt chaque ID de campagne. Pour chaque ID, il supprime la campagne de la base de données en tant que root.

### grid_test_cluster.rb

Tout d'abord, il vérifie que le nom de l'utiliateur qui exécute le programme est soit cigri ou root. Si ce n'est pas le cas, un message d'erreur apparait et le programme se termine.

Ensuite, une liste de répertoires est établi. Puis, il parse les options de commande utilisées pour affecter les différentes variables.

Il vérifie si toutes les informations necessaires ont été renseignées précédemment. Si c'est le cas, alors un job sera soumit, et l'ID et l'état du job seront affichés.

### new_cluster.rb

Après avoir effectuer une vérification sur le nombre d'arguments, il établi une connexion à la base de données et crée un nouveau cluster dans la base de données.

***

## spec

Contient des fichiers de tests, qui sont des ensembles de tests Rspec (format `it... do... end`). Les tests couvrent des fonctions implémentées et des scénarios.

Les fichiers de tests existants sont:

- `api/cigri-api_spec.rb`

- `clusterlib/cigri-clusterlib_spec.rb`

- `conflib/cigri-conflib_spec.rb`

- `Error/cigri-exception_spec.rb`

- `iolib/cigri-iolib_spec.rb`

- `jdl-parser/dl-parser_spec.rb`

- `joblib/cigri-joblib_spec.rd`

- `logger/cigri-logger_spec.rd`

Pour lancer les tests, un environnement est configuré pour CiGri à l'aide du fichier `spec_helper.rb`.

***

## tmp

Probablement un dossier contenant du code en sandbox.

***

## tools

Outils permettant le build et le deploiement de CiGri.

### cirods

Permet de configurer irods.

### kameleon1

Permet de bluid et deployer CiGri.

### kameleon2

Permet de bluid et deployer CiGri.

### oardocker

Permet d'installer CiGri dans un oardocker.

### sudowrapper.sh

Permet de lancer une commande en sudo avec l'utilisateur CiGri.

***

## Gemfile

Ce fichier déclare les dépendances utilisées pour le développement de CiGri V3. Nous pouvons voir des bibliothéques déclarées en lien avec des fonctionnalités de base de données, de requêtes HTTP, de manipulation de JSON, de communication XMPP, et le framework web Sinatra.

## INSTALL

Guide rapide de l'installation de CiGri V3 (prérequis, installation, création d'utilisation, de base de données, de cluster et le lancement de CiGri)

## CHANGELOG

Liste de changement selon les versions (obsolète)

## README.md

Décris globalement ce que contient ce projet.

## MAKE-DEB.md

Liste de commande pour générer un package Debian.

## Makefile

Makefile permettant l'installation de CiGri

## shell.nix

Fichier nix pour générer un shell avec un environnement de run minimaliste.
