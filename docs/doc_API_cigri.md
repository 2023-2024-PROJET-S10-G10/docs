# API

## Routes de l'API

Il est possible d'ajouter `?pretty=true` à une requête API afin de recevoir un json lisible.

| HTTPrequest | URL                                                    | Action                                                                          | Method Name          |
| :---------- | :----------------------------------------------------- | :------------------------------------------------------------------------------ | :------------------- |
| GET         | /                                                      | Liste les routes disponibles dans l'API                                         | routes               |
| GET         | /clusters                                              | Liste les clusters disponibles dans Cigri                                       | clusters             |
| GET         | /clusters/<cluster_id>                                 | Récupère les informations d'un cluster en particulier                           | cluster              |
| GET         | /campaigns                                             | Liste toutes les campagnes en cours                                             | campaigns            |
| GET         | /campaigns/<campaign_id>                               | Récupère les informations d'une campagne en particulier                         | campaign             |
| GET         | /campaigns/<campaign_id>/jdl                           | Récupère le JDL d'une campagne en particulier                                   | campaignJDL          |
| GET         | /campaigns/<campaign_id>/jobs                          | Liste l'ensemble des jobs d'une campagne spécifique                             | campaignJobs         |
| GET         | /campaigns/<campaign_id>/jobs/<job_id>                 | Récupère le détail d'un job spécifique d'une campagne en particulier            | campaignJob          |
| GET         | /campaigns/<campaign_id>/jobs?limit=<int>&offset=<int> | Récupère les jobs à partir d'un offset et d'une limite [offset: offset + limit] | campaignJobs         |
| GET         | /campaigns/<campaign_id>/jobs/finished                 | Récupère les jobs terminés de la campagne spécifiée                             | campaignFinishedJobs |
| POST        | /campaigns                                             | Soumettre une nouvelle campagne                                                 | submitCampaign       |
| PUT         | /campaigns/<campaign_id>                               | Mettre à jour une campagne (status, nom)                                        | updateCampaign       |
| DELETE      | /campaigns/<campaign_id>                               | Supprime une campagne                                                           | deleteCampaign       |
| GET         | /campaigns/<campaign_id>/events                        | Liste les événements d'une campagne donnée                                      | campaignEvents       |
| DELETE      | /campaigns/<campaign_id>/events                        | Corrige (ferme) les événements d'une campagne donnée                            | deleteCampaignEvents |
| GET         | /notifications                                         | Liste les abonnements aux notifications de l'utilisateur actuel                 | notifications        |
| POST        | /notifications/mail                                    | S'abonner au service de notification mail                                       | subscribeMail        |
| POST        | /notifications/jabber                                  | S'abonner au service de notification Jabber                                     | subscribeJabber      |
| DELETE      | /notifications/<mail/jabber>                           | Se désabonner d'un système de notification                                      | unsubscribe          |
| GET         | /events/<id>                                           | Récupère un événement spécifique                                                | event                |
| DELETE      | /events/<id>                                           | Corrige (ferme) l'événement spécifié                                            | deleteEvent          |
| DELETE      | /events/<id>?resubmit=1                                | Corrige (ferme) l'événement spécifié et resoumet le job                         | deleteEvent          |
| GET         | /gridusage                                             | Récupère l'usage actuel de la grille                                            | gridUsage            |
| GET         | /gridusage?from=<date>&to=<date>                       | Récupère l'usage actuel entre 2 dates (unix timestamps)                         | gridUsage            |

## Accéder à l'API

```txt
Getting the links available on the server::

  $ curl http://api-host:port
  {"links":[{"href":"/","rel":"self"},{"href":"/campaigns","title":"campaigns","rel":"campaigns"},{"href":"/clusters","title":"clusters","rel":"clusters"}]}

When posting a campaign, the JSON containing the ID of the submitted campaign is returned::

  $ curl -X POST http://api-host:port/campaigns -d '{"name":"n", "nb_jobs":0,"clusters":{"fukushima":{"exec_file":""}}}'
  {"id":"585","links":[{"href":"/campaigns/585","rel":"self"},{"href":"/campaigns","rel":"parent"}]}

Return codes
``````

## Code de retour de l'API

| Code | HTTPrequest            | Signification                                                            |
| :--- | :--------------------- | :----------------------------------------------------------------------- |
| 200  | GET                    | Demande réussi: Tout s'est bien déroulé                                  |
| 201  | POST                   | Resource créée: La campagne a été soumise                                |
| 202  | PUT, DELETE            | Accepté: Modification appliquée                                          |
| 400  | POST, PUT              | Mauvaise requête: Regardez le contenu de la réponse pour plus de détails |
| 403  | POST, PUT, DELETE      | Interdit: Voir la réponse pour plus de détails                           |
| 404  | GET, POST, PUT, DELETE | Page non trouvée: l'URL n'existe pas                                     |

## Format

Dans cette partie une description des formats des réponses API est fournie, certains retour d'API peuvent être tronqués afin d'en simplifier la lisibilité.

### GET /

Retourne une liste des liens disponibles dans l'API :

```json
{
  "links": [
    {
      "rel": "self",
      "href": "/"
    },
    {
      "rel": "collection",
      "href": "/campaigns",
      "title": "campaigns"
    },
    {
      "rel": "collection",
      "href": "/clusters",
      "title": "clusters"
    }
  ]
}
```

### GET /clusters

Retourne l'ensemble des clusters disponibles sur le système.

```json
{
  "items": [
    {
      "id": "7",
      "name": "ceciccluster",
      "links": [
        { "rel": "self", "href": "/clusters/7" },
        { "rel": "parent", "href": "/clusters" }
      ]
    },
    ...
  ],
  "total": 5,
  "links": [
    { "rel": "self", "href": "/clusters" },
    { "rel": "parent", "href": "/" }
  ]
}

```

## GET /clusters/<cluster_id>

Récupère les informations d'un cluster en particulier

Avec cluster_id = $8$, on obtient :

```json
{
  "id": "8",
  "name": "dahu",
  "api_url": "https://f-dahu.u-ga.fr:6669/oarapi-cigri/",
  "api_auth_type": "cert",
  "api_auth_header": "X_REMOTE_IDENT",
  "ssh_host": "f-dahu.u-ga.fr",
  "batch": "oar2_5",
  "resource_unit": "core",
  "power": "200",
  "properties": null,
  "stress_factor": "0.44/0.8",
  "api_chunk_size": "100",
  "enabled": "t",
  "links": [
    { "rel": "self", "href": "/clusters/8" },
    { "rel": "parent", "href": "/clusters" }
  ],
  "blacklisted": false,
  "under_stress": false
}
```

### GET /campaigns

Liste toutes les campagnes en cours

```json
{
  "items": [
    {
      "id": 23177,
      "name": "gamit_2014_dahu",
      "user": "janexg",
      "state": "in_treatment",
      "has_events": true,
      "submission_time": 1707202798,
      "total_jobs": 4455,
      "finished_jobs": 32,
      "links": [
        {
          "rel": "self",
          "href": "/campaigns/23177"
        },
        {
          "rel": "parent",
          "href": "/campaigns"
        },
        {
          "rel": "collection",
          "href": "/campaigns/23177/jobs",
          "title": "jobs"
        },
        {
          "rel": "collection",
          "href": "/campaigns/23177/events",
          "title": "events"
        },
        {
          "rel": "item",
          "href": "/campaigns/23177/jdl",
          "title": "jdl"
        }
      ]
    },
    ...
  ],
  "total": 3,
  "links": [
    {
      "rel": "self",
      "href": "/campaigns"
    },
    {
      "rel": "parent",
      "href": "/"
    }
  ]
}
```

### GET /campaigns/<campaign_id>

Récupère les informations d'une campagne en particulier

```json
{
  "id": 23177,
  "name": "gamit_2014_dahu",
  "user": "janexg",
  "state": "in_treatment",
  "has_events": true,
  "submission_time": 1707202798,
  "total_jobs": 4455,
  "finished_jobs": 33,
  "links": [
    {
      "rel": "self",
      "href": "/campaigns/23177"
    },
    {
      "rel": "parent",
      "href": "/campaigns"
    },
    {
      "rel": "collection",
      "href": "/campaigns/23177/jobs",
      "title": "jobs"
    },
    {
      "rel": "collection",
      "href": "/campaigns/23177/events",
      "title": "events"
    },
    {
      "rel": "item",
      "href": "/campaigns/23177/jdl",
      "title": "jdl"
    }
  ],
  "clusters": {
    "8": {
      "cluster_name": "dahu",
      "active_jobs": 272,
      "queued_jobs": 583,
      "prologue_ok": true,
      "epilogue_ok": true
    }
  }
}
```

### GET /campaigns/<campaign_id>/jdl

Récupère le JDL d'une campagne en particulier

```json
{
  "name": "gamit_2014_dahu",
  "clusters": {
    "dahu": {
      "project": "biggnss",
      "walltime": "08:00:00",
      "output_gathering_method": "None",
      "dimensional_grouping": "false",
      "temporal_grouping": "false",
      "checkpointing_type": "None",
      "properties": "",
      "resources": "core=1",
      "exec_file": "$HOME/reproc_epos/72_run_gamit.sh",
      "exec_directory": "$HOME",
      "test_mode": "false",
      "type": "best-effort",
      "prologue": [
        "source /applis/ciment/v2/env.bash",
        "mkdir -p \\$HOME/reproc_epos",
        "cd \\$HOME/reproc_epos",
        "iget -f /mantis/gnss/gps_contrib/71_create_scratch_workDir.sh",
        "iget -f /mantis/gnss/gps_contrib/72_run_gamit.sh",
        "iget -f /mantis/gnss/gps_contrib/env_gamit.bash",
        "chmod u+x 71_create_scratch_workDir.sh 72_run_gamit.sh",
        "source env_gamit.bash",
        "rm -f \\$HOME/gg",
        "ln -s /applis/ciment/v2/stow/x86_64/gcc_4.6.2/gamit_10.71 \\$HOME/gg",
        "./71_create_scratch_workDir.sh 2014"
      ]
    }
  },
  "jobs_type": "normal",
  "params": [
    "gamit_2014_045_ne19 2014 045 ne19",
    "gamit_2014_046_ne19 2014 046 ne19",
    "gamit_2014_047_ne19 2014 047 ne19",
    "gamit_2014_048_ne19 2014 048 ne19",
    ...
  ]
}
```

### GET /campaigns/<campaign_id>/jobs

Liste l'ensemble des jobs d'une campagne spécifique

```json
{
  "items": [
    {
      "id": 233608428,
      "name": "gamit_2014_045_ne19",
      "parameters": "gamit_2014_045_ne19 2014 045 ne19",
      "cluster": "dahu",
      "cigri_job_id": 56982687,
      "remote_id": 24267400,
      "state": "terminated",
      "href": "/campaigns/23177/jobs/233608428"
    },
    ...
  ],
  "total": 4455,
  "offset": 0,
  "limit": 100,
  "links": [
    {
      "rel": "self",
      "href": "/campaigns/23177/jobs"
    },
    {
      "rel": "parent",
      "href": "/campaigns/23177"
    },
    {
      "rel": "next",
      "href": "/campaigns/23177/jobs?limit=100&offset=101"
    }
  ]
}
```

### GET /campaigns/<campaign_id>/jobs/<job_id>

Récupère le détail d'un job spécifique d'une campagne en particulier

```json
{
  "id": 233608428,
  "name": "gamit_2014_045_ne19",
  "parameters": "gamit_2014_045_ne19 2014 045 ne19",
  "state": "terminated",
  "links": [
    {
      "rel": "self",
      "href": "/campaigns/23177/jobs/233608428"
    },
    {
      "rel": "parent",
      "href": "/campaigns/23177/jobs"
    }
  ],
  "execution": [
    {
      "id": 56982687,
      "cluster_id": 8,
      "cluster_name": "dahu",
      "state": "terminated",
      "return_code": null,
      "remote_id": 24267400
    }
  ]
}
```

### POST /campaigns

Soumettre une nouvelle campagne

```json
{
  "id": 23256,
  "name": "test-cigri",
  "user": "correidi",
  "state": "in_treatment",
  "has_events": false,
  "submission_time": 1707465468,
  "total_jobs": 2,
  "finished_jobs": 0,
  "links": [
    {
      "rel": "self",
      "href": "/campaigns/23256"
    },
    {
      "rel": "parent",
      "href": "/campaigns"
    },
    {
      "rel": "collection",
      "href": "/campaigns/23256/jobs",
      "title": "jobs"
    },
    {
      "rel": "collection",
      "href": "/campaigns/23256/events",
      "title": "events"
    },
    {
      "rel": "item",
      "href": "/campaigns/23256/jdl",
      "title": "jdl"
    }
  ]
}
```

### PUT /campaigns/<campaign_id>

Mettre à jour une campagne (status, nom)

**Remarque :** N'a pas l'air de fonctionner

### DELETE /campaigns/<campaign_id>

Cette route possède 3 queries possibles :

| Query     | Action                                                     |
| :-------- | :--------------------------------------------------------- |
| ?hold=1   | Met en pause la campagne                                   |
| ?resume=1 | Met en attente la campagne pour exécution                  |
| ?purge=1  | Purge la campagne (seulement pour les campagnes terminées) |

**Note :** Sans query spécifique, cette route supprime la campagne.

```json
{
  "status": 202,
  "title": "Accepted",
  "message": "Campaign 23181 cancelled"
}
```

### GET /campaigns/<campaign_id>/events

Liste les événements d'une campagne donnée

```json
{
  "id": 233608428,
  "name": "gamit_2014_045_ne19",
  "parameters": "gamit_2014_045_ne19 2014 045 ne19",
  "state": "terminated",
  "links": [
    {
      "rel": "self",
      "href": "/campaigns/23177/jobs/233608428"
    },
    {
      "rel": "parent",
      "href": "/campaigns/23177/jobs"
    }
  ],
  "execution": [
    {
      "id": 56982687,
      "cluster_id": 8,
      "cluster_name": "dahu",
      "state": "terminated",
      "return_code": null,
      "remote_id": 24267400
    }
  ]
}
```

### DELETE /campaigns/<campaign_id>/events

Corrige (ferme) les événements d'une campagne donnée

```json
{
  "status": 202,
  "title": "Accepted",
  "message": "Campaign 23264 events closed"
}
```

### GET /notifications

Liste les abonnements aux notifications de l'utilisateur actuel

```json
{
  "items": [],
  "links": [
    {
      "rel": "self",
      "href": "/notifications/"
    }
  ]
}
```

### POST /notifications/mail

S'abonner au service de notification mail. Attention il ne faut pas déjà être abonné au service, si vous souhaitez changer votre sévérité de notification il faut se désabonner et se réabonner avec la bonne sensibilité.

```json
{
  "status": 201,
  "title": "Created",
  "message": "New subscription created"
}
```

### POST /notifications/jabber

S'abonner au service de notification Jabber. Non testé, car obsolète.

### DELETE /notifications/<mail/jabber>

Se désabonner d'un système de notification. Impossible de tester, car nous n'avons pas les droits de suppressions.

### GET /events/<id>

Récupère un événement spécifique

```json
{
  "id": 38306109,
  "class": "log",
  "code": "QUEUED_FOR_TOO_LONG",
  "state": "closed",
  "job_id": null,
  "cluster_id": null,
  "campaign_id": null,
  "parent": null,
  "checked": "no",
  "notified": "f",
  "date_open": "2024-02-05 00:19:42+01",
  "date_closed": "2024-02-05 00:19:42+01",
  "date_update": "2024-02-05 00:19:42+01",
  "message": "Removing 4 jobs from the queue because they were queued for too long",
  "links": [
    {
      "rel": "self",
      "href": "/events/38306109"
    },
    {
      "rel": "parent",
      "href": "/events"
    }
  ]
}
```

### DELETE /events/<id>

Corrige (ferme) l'événement spécifié

```json
{
  "status": 202,
  "title": "Accepted",
  "message": "Event 38341998 closed"
}
```

### DELETE /events/<id>?resubmit=1

Corrige (ferme) l'événement spécifié et resoumet le job

```json
{
  "status": 202,
  "title": "Accepted",
  "message": "Event 38341998 closed"
}
```

### GET /gridusage

Récupère l'usage actuel de la grille

```json
{
  "items": [
    {
      "date": 1707224519,
      "clusters": [
        {
          "cluster_name": "dahu",
          "cluster_id": 8,
          "max_resources": 6080,
          "used_resources": 4467,
          "used_by_cigri": 1318,
          "unavailable_resources": 704
        },
        {
          "cluster_name": "luke",
          "cluster_id": 5,
          "max_resources": 1166,
          "used_resources": 203,
          "used_by_cigri": 16,
          "unavailable_resources": 434
        },
        {
          "cluster_name": "bigfoot",
          "cluster_id": 9,
          "max_resources": 694,
          "used_resources": 417,
          "used_by_cigri": 0,
          "unavailable_resources": 134
        }
      ]
    }
  ],
  "from": null,
  "to": null,
  "total": 1
}
```

### GET /gridusage?from=<date>&to=<date>

Récupère l'usage actuel entre 2 dates (unix timestamps)

```json
{
  "items": [
    {
      "date": 1706742092,
      "clusters": [
        {
          "cluster_name": "dahu",
          "cluster_id": 8,
          "max_resources": 6080,
          "used_resources": 3481,
          "used_by_cigri": 0,
          "unavailable_resources": 872
        },
        ...
      ]
    }
  ],
  "from": "1706742000",
  "to": "1706742100",
  "total": 1
}
```

## Structure générale de réponses

### Links

La majorité des requêtes disposent des liens vers les routes voisines dans l'API, par example la route `/clusters` affichera notamment la route `/clusters/<cluster_id>`

Ces liens sont représentées sous la forme suivante en JSON.

```json
{
  ...
  "links": [
    {
      "rel": "self",
      "href": "/"
    },
    {
      "rel": "collection",
      "href": "/campaigns",
      "title": "campaigns"
    },
    {
      "rel": "collection",
      "href": "/clusters",
      "title": "clusters"
    }
  ]
}
```

### Liste

Les listes sont retournées avec la forme suivante :

```json
{
  "items": [
    {
      data...
    },
    ...
  ],
  "total": ...,
  ...
}
