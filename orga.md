# 2023-2024-PROJET-S10-G10

## Objectif

L'objectif du projet est d'effectuer la migration d'un programme de *[Bah je sais même pas en fait ... Grille de calcul?]* écrit en Ruby vers du python.

## Ressources

### AirImag 
https://air.imag.fr/index.php/Développement_d'un_intergiciel_de_Grille_de_Calcul

### Git

https://github.com/2023-2024-PROJET-S10-G10

Application : https://github.com/2023-2024-PROJET-S10-G10/app

Documents : https://github.com/2023-2024-PROJET-S10-G10/docs

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

Dans un test unitaire, on défini trois partie : 
- L'initialisation des paramètres et résultats attendus
- L'éxécution du cas de test
- Vérification des résultats

Chaque test unitaire doit être placé dans une classe qui étend la classe `TestManager`. \
`TestManager` est une classe qui va référencer toutes ses sous classes et executer touts les tests qu'elles contiennent. Il produira ensuite une sortie qui résumera le déroulement des tests (Combien de tests, combien ont réussi, quels tests ne sont pas passés, ...).

### Exemple

On considère une fonction isInRange qui indique si un nombre est compris entre deux deux autres nombre, un extrait des tests unitaires associés serait :
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
        return result == expectedResult


    def outOfRange_ReturnsFalse :

        expectedResult = False
        upperBound = 5
        lowerBound = 2
        

        result = isInRange(3, lowerBound, upperBound)


        return result == expectedResult
```