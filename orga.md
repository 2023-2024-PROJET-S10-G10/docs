# 2023-2024-PROJET-S10-G10

## Objectif

L'objectif du projet est d'effectuer la migration d'un programme de *[Bah je sais même pas en fait ... Grille de calcul?]* écrit en Ruby vers du python.

## Ressources

### AirImag

https://air.imag.fr/index.php/Développement_d'un_intergiciel_de_Grille_de_Calcul

### Git

[Organisation GitHub](https://github.com/2023-2024-PROJET-S10-G10)

[Dépôt `Application`](https://github.com/2023-2024-PROJET-S10-G10/app)

[Dépôt `Documents`](https://github.com/2023-2024-PROJET-S10-G10/docs)

### Trello

https://trello.com/b/zyAMcljZ/projet-s10

## Workflow (standard sur projet déjà lancé)

- Isolation d'une fonctionnalité du programme en ruby
- Recherche de tous les éléments liés à la fonctionnalité
- Documentation des éléments
- Division en tâche(s)
- Documentation de la tâche sélectionnée (In, Processing and Out)
- Réécriture en Python
- écriture des tests unitaires
- PR

## Test Unitaires

### Convention de nommage

Un test unitaire doit être nommé en suivant le pattern suivant :
```python
    def [Cas de test]_[Résultat attendu] :
        # Code
```

De plus il doit être situé dans un classe nommé par le nom de la méthode à tester : 
```python
class [Nom de la méthode] : 
    def [Cas de test]_[Résultat attendu] :
        # Code
```


### Construction

Dans un test unitaire, on défini trois parties : 
- L'initialisation des paramètres et résultats attendus
- L'éxécution du cas de test
- Vérification des résultats avec assertions :
  - `assertTrue(bool)`
  - `assertFalse(bool)`
  - `assertEqual(val, expected)`
  - `assertNotEqual(val, not_expected)`

Chaque test unitaire doit être placé dans une classe qui étend la classe `TestManager`. \
`TestManager` est une classe qui va référencer toutes ses sous classes et executer touts les tests qu'elles contiennent. Il produira ensuite une sortie qui résumera le déroulement des tests (Combien de tests, combien ont réussi, quels tests ne sont pas passés, ...). \
Chaque sous classe de `TestManager` correspond à une méthode à tester et doit être placé dans un fichier correspondant au fichier dans lequel la méthode se trouve.
Le fichier contenant les classes et les tests doivent se trouver dans le dossier `App/Test`

### Contenu

- Nom du module (fichier)
  - Nom de la méthode
    - Nom du test unitaire

Lors des tests un objet avec les informations est remplis, voici sa structure : 
```Json
{
    [
        "method_name" : "NOM_METHODE",
        "status" : "Success | Fail",
        "n_passed" : "NUMBER_OF_PASSED_TEST_FOR_METHOD",
        "tests" : [
            {
                "test_name" : "NOM_TEST",
                "status" : "Success | Fail",
                "details" : "ADDITIONNAL_INFORMATION"
            },
            ...
        ],
        ...
    ]
}
```

### Lancement

```
    python3 ./Test.py [0|1|2]
```

### Sortie

Chaque exécution produit un rapport de test disponible dans le fichier `Test/Logs`.
Il existe trois niveaux de debug:
- `0` : Le minimum -> Status de réussite et pourcentage 
- `1` : Les erreurs -> Détails sur les tests échoués
- `2` : Tout -> détail d'exécution de chaque test

### Exemple

On considère une fonction isInRange qui indique si un nombre est compris entre deux autres nombres, un extrait des tests unitaires associés serait :
```python

class isInRange(TestManager):
    '''
        isInRange : 
            Param1 : The number to test
            Param2 : The lower bound
            Param3 : The upper bound

            Returns : True if the number is between the boundaries (included), else False
    '''

    def inRange_ReturnsTrue :

        # Initiatilisation des paramètres et résultat attendu
        expectedResult = True
        upperBound = 5
        lowerBound = 2


        # Execution du cas de test
        result = isInRange(3, lowerBound, upperBound)


        # Vérification du résultat
        self.assertEqual(result, expectedResult)


    def outOfRange_ReturnsFalse :

        expectedResult = False
        upperBound = 5
        lowerBound = 2
        

        result = isInRange(3, lowerBound, upperBound)


        self.assertEqual(result, expectedResult)
```
## Technologies

### Prefect

[Prefect](https://www.prefect.io/) est un outil permettant de fluidifier l'organisation du travail. En permettant d'orchestrer le workflow d'un projet.

### FastAPI

[FastAPI](https://fastapi.tiangolo.com/) est un framework pour la réalisation d'API Restful suivant les principe du standard OpenAPI.

### SqlAlchemy

[SqlAlchemy](https://www.sqlalchemy.org/) permet d’interagir avec une base de données SQL via du code Python.

### Click/Rich

[Rich-Click](https://github.com/ewels/rich-click) est une bibliothèque Python permettant de générer des interfaces CLI améliorées, avec notamment de meilleurs visuels. La bibliothèque est disponible sur [PyPI](https://pypi.org/project/rich-click/).

### Poetry

[Poetry](https://python-poetry.org/) est un gestionnaire de package permettant la gestion de dépendance mais aussi le packaging d'application python.
