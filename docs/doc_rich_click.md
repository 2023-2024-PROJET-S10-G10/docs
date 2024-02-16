# Documentation rich click

## Description de l'outil

Rich click est une librairie python permettant de créer des interfaces CLI pour la documentation d'aide. Dit autrement rich click permet d'améliorer l'affichage de l'aide que l'utilisateur peut accéder en utilisant l'option `--help` mais aussi d'ajouter des options, des paramètres et utiliser les variables d'environnement dans notre programme python. Rich click permet de supporter aisément la lecture de paramètres en ligne de commande.

## Utilisation de l'outil

L'outil s'utilise avec un système de décorateur, globalement toute méthode pouvant être appelée depuis le CLI nécessite un décorateur. Les méthodes contiennent les variables à affecter dans le prompt CLI et des décorateurs balisant les variables.

Dans la suite de cette documentation, nous allons présenter des décorateurs usuels et nous supposerons que `rich click` est importé sous le nom `click`.

### Numéro de version

Il est possible de spécifier le nom et la version d'un programme, cela sera utilisé lors de prompt CLI avec par exemple l'option `--version`

```py
@click.version_option("1.23", prog_name="test")
```

### Déclaration de commande

Le décorateur de déclaration de commande permet de signaler à Rich Click que la méthode suivante doit utiliser les fonctionnalités de Rich Click et qu'elle sera donc appelée par défaut (sauf paramètre rich click contraire). Voici un exemple d'utilisation :

```py
@click.command(context_settings=dict(help_option_names=["-h", "--help"]))
def hello_world()
    pass
```

**Note :** Par défaut, `--help` est utilisée pour l'aide il est possible de changer cela avec les context settings comme montré dans l'exemple ci-dessus.

### Déclaration de groupe

Dans un programme on peut avoir besoin de réaliser plusieurs méthodes pour différentes fonctionnalités, il est donc possible de créer des groupes qui vont permettre de créer une hiérarchie de commande, sous commande.

Le code ci-dessous est extrait de l'exemple numéro 3 de rich click.

```py
import rich_click as click

click.rich_click.OPTION_GROUPS = {
    "03_groups_sorting.py": [
        {
            "name": "Basic usage",
            "options": ["--type", "--output"],
        },
        {
            "name": "Advanced options",
            "options": ["--help", "--version", "--debug"],
            # You can also set table styles at group-level instead of using globals if you want
            "table_styles": {
                "row_styles": ["bold", "yellow", "cyan"],
            },
        },
    ],
    "03_groups_sorting.py sync": [
        {
            "name": "Inputs and outputs",
            "options": ["--input", "--output"],
        },
        {
            "name": "Advanced usage",
            "options": ["--overwrite", "--all", "--help"],
        },
    ],
}
click.rich_click.COMMAND_GROUPS = {
    "03_groups_sorting.py": [
        {
            "name": "Main usage",
            "commands": ["sync", "download"],
        },
        {
            "name": "Configuration",
            "commands": ["config", "auth"],
        },
    ]
}


@click.group(context_settings=dict(help_option_names=["-h", "--help"]))
@click.option(
    "--type",
    default="files",
    show_default=True,
    required=True,
    help="Type of file to sync",
)
@click.option(
    "--debug/--no-debug",
    "-d/-n",
    default=False,
    show_default=True,
    help="Show the debug log messages",
)
@click.version_option("1.23", prog_name="mytool")
def cli(type, debug):
    """
    My amazing tool does all the things.

    This is a minimal example based on documentation
    from the 'click' package.

    You can try using --help at the top level and also for
    specific subcommands.
    """
    print(f"Debug mode is {'on' if debug else 'off'}")


@cli.command()
@click.option("--input", "-i", required=True, help="Input path")
@click.option("--output", "-o", help="Output path")
@click.option("--all", is_flag=True, help="Sync all the things?")
@click.option("--overwrite", is_flag=True, help="Overwrite local files")
def sync(input, output, all, overwrite):
    """Synchronise all your files between two places."""
    print("Syncing")


@cli.command()
@click.option("--all", is_flag=True, help="Get everything")
def download(all):
    """Pretend to download some files from somewhere."""
    print("Downloading")


@cli.command()
def auth():
    """Authenticate the app."""
    print("Downloading")


@cli.command()
def config():
    """Set up the configuration."""
    print("Downloading")


if __name__ == "__main__":
    cli()
```

Après avoir écrit cela le programme pourra appeler 3 différentes méthodes directement depuis le CLI :

- `py test.py` : appellera `cli`
- `py test.py sync` : appellera `sync`
- `py test.py auth` : appellera `auth`

**Notes :** La méthode cli est appelé même lors de l'exécution de la commande : `py test.py sync`

### Déclaration d'options

Il est possible d'affecter des options à une commande, pour cela il suffit de rajouter le décorateur `click.option` et de rajouter une variable dans la méthode.

```py
@click.command()
@click.option("--count", default=1, help="Number of greetings.")
@click.option("--name", prompt="Your name", help="The person to greet.")
def hello(count, name):
    pass
```

Il existe plusieurs paramètres disponible dans `click.option`, les plus usuels sont :

- nom de l'option (obligatoire et premier paramètre à fournir ex : --count)
- default : qui précise la valeur par défaut de l'option
- show_default : qui précise si la valeur par défaut doit être affichée dans le prompt d'aide
- help : qui contient le texte de description de l'option
- prompt : qui permet d'afficher un prompt avec l'attente d'un input utilisateur dans le cas où aucune valeur n'a été fournie pour une option
- is_flag : qui permet de signaler que l'option est un flag et n'attend pas de valeur par exemple `py test.py --version`
- required : qui précise si une option est obligatoire
- envvar : qui précise le nom de variable d'environnement cible
- show_envvar : qui précise si la variable d'environnement doit être affichée dans le prompt d'aide

Il est possible d'envoyer une adresse mail à un programme python comme suit :

- `EMAIL_ADDRESS="foo@bar.com" python test.py`
- `python test.py --email ="foo@bar.com"`

### Déclaration d'argument

Les arguments sont assez proches des options à la différence qu'ils ne contiennent pas de `--` devant par exemple `test.py input` est un argument alors que `test.py -i input` est une option.

```py
@click.command()
@click.argument("input", type=click.Path(), required=True)
def cli(input):
    pass
```

Il existe plusieurs paramètres disponible dans `click.argument`, les plus usuels sont :

- nom de l'option (obligatoire et premier paramètre à fournir ex : --count)
- type : qui précise le type de valeur attendu, rich click fourni plusieurs type de variable
- required : qui précise si une option est obligatoire

### config

Il est possible de configurer plusieurs paramètres généraux dans Rich click, ci-dessous se trouve une liste non exhaustive de ce qu'il est possible de réaliser.

| code                                                                                | fonctionnalité                                                              |
| :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| `@click.rich_config( help_config= click.RichHelpConfiguration( use_markdown=True))` | Active le markdown                                                          |
| `click.rich_click.USE_RICH_MARKUP = True`                                           | Utiliser rich markup dans le texte CLI                                      |
| `click.rich_click.SHOW_ARGUMENTS = True`                                            | Affiche le détail des arguments dans le prompt d'aide                       |
| `click.rich_click.GROUP_ARGUMENTS_OPTIONS = True`                                   | Regroupe les arguments et les groupes dans le prompt d'aide CLI             |
| `click.rich_click.STYLE_ERRORS_SUGGESTION = "magenta italic"`                       | Définit le style des suggestions dans les erreurs                           |
| `click.rich_click.ERRORS_SUGGESTION = "Try running the '--help'..."`                | Définit le message d'aide à afficher en cas d'erreur                        |
| `click.rich_click.ERRORS_EPILOGUE = "To find out more, ..."`                        | Définit le texte à afficher en epilogue des erreurs                         |
| `click.rich_click.SHOW_METAVARS_COLUMN = False`                                     | Cache la colonne des méta variable                                          |
| `click.rich_click.APPEND_METAVARS_HELP = True`                                      | Active l'ajout des meta variables au message d'aide                         |
| `click.rich_click.STYLE_OPTIONS_TABLE_LEADING = 1`                                  | Détermine l'espace vide avant d'afficher la table des options               |
| `click.rich_click.STYLE_OPTIONS_TABLE_BOX = "SIMPLE"`                               | Définit le le style du tableau des options                                  |
| `click.rich_click.STYLE_OPTIONS_TABLE_ROW_STYLES = ["bold", ""]`                    | Définit le style de chaque ligne du tableau d'option                        |
| `click.rich_click.STYLE_COMMANDS_TABLE_SHOW_LINES = True`                           | Affiche les ligne du tableau                                                |
| `click.rich_click.STYLE_COMMANDS_TABLE_PAD_EDGE = True`                             | Définit si du padding doit être ajouté sur les bords du tableau de commande |
| `click.rich_click.STYLE_COMMANDS_TABLE_BOX = "DOUBLE"`                              | Définit le style du tableau de commande                                     |
| `click.rich_click.STYLE_COMMANDS_TABLE_BORDER_STYLE = "red"`                        | Définit le style des bords du tableau de commande                           |
| `click.rich_click.STYLE_COMMANDS_TABLE_ROW_STYLES = ["magenta", "yellow", ...]`     | Définit le cycle de couleurs pour les lignes du tableau                     |

La création de tableau dans le prompt d'aide se fait donc par modification de paramètre de rich click.

## Documentation de méthode

Les commentaires python écrit dans les méthodes python sont utilisés par rich click. Ces derniers permettent de présenter la fonction des commandes/sous commandes dans le CLI.

## Examples

Pour plus d'exemple, il est possible d'accéder au [GitHub](https://github.com/ewels/rich-click/tree/main/examples) du projet [Rich Click](https://github.com/ewels/rich-click/tree/main/examples)
