# Workflow de Projet pour l'IDE Cursor

## Aperçu

Ce dépôt contient un ensemble de fichiers de configuration pour définir et piloter un workflow de développement structuré au sein de l'IDE Cursor. Il ne s'agit pas d'un projet autonome, mais d'un **modèle de processus** que l'IDE Cursor peut interpréter pour guider un projet à travers un cycle de vie complet, de l'initialisation à la finalisation.

## Principe de Fonctionnement

Ce workflow est conçu pour être exécuté par l'IDE Cursor. Le processus est le suivant :

1.  **Chargement du Plan** : L'IDE Cursor utilise le fichier `TODO.md` comme son plan d'action séquentiel.
2.  **Suivi de la Progression** : L'IDE lit et met à jour le fichier `state.json` pour suivre les phases déjà terminées et déterminer la prochaine étape.
3.  **Exécution des Phases** : Pour chaque phase du plan, l'IDE consulte `snippets/phase_mapping.json` pour trouver le "prompt" correspondant. Il utilise ensuite ce prompt pour exécuter l'action requise (par exemple, générer du code, lancer une analyse, etc.).
4.  **Utilisation des Ressources** : Durant l'exécution, l'IDE peut se servir des `scripts` fournis ou injecter du code à partir des extraits définis dans `snippets/templates.json`.

## 🗂️ Composants du Workflow

Le fonctionnement de ce workflow repose sur les fichiers suivants, tous interprétés par l'IDE Cursor :

* `TODO.md`: Contient la liste des phases qui structurent le projet. C'est la feuille de route que l'IDE suit. Il liste également les actions manuelles ou scriptées à réaliser.
* `state.json`: Le fichier d'état que l'IDE gère pour savoir où en est le projet dans le workflow. Il contient la phase actuelle, les phases complétées et la date de dernière mise à jour.
* `snippets/phase_mapping.json`: La table de correspondance qui indique à l'IDE quel prompt utiliser pour chaque phase définie dans `TODO.md`.
* `snippets/templates.json`: Une bibliothèque d'extraits de code que l'IDE peut proposer pour accélérer le développement.

## ⚙️ Les Phases du Workflow

Le workflow est décomposé en phases séquentielles, tirées de `TODO.md` et mappées à des prompts via `phase_mapping.json`.

| Phase du Workflow | Prompt Associé |
| :--- | :--- |
| **Initialisation du projet** | `onboarding.prompt` |
| **Génération structure** | `onboarding.prompt` |
| **Analyse de la structure** | `analyze.prompt` |
| **Refactorisation du code** | `refactor.prompt` |
| **Génération des tests** | `testgen.prompt` |
| **Génération de la documentation** | `docgen.prompt` |
| **Optimisation finale** | `optimize.prompt` |
| **Nettoyage** | `cleanup.prompt` |
| **Rapport final** | `report.prompt` |

## 🛠️ Ressources pour l'IDE

### Scripts
L'IDE peut être amené à exécuter les scripts suivants listés dans le `TODO.md` :
* `scripts/init_structure.sh`
* `scripts/clean_logs.sh`
* `scripts/update_dependencies.sh`

### Extraits de Code (Snippets)
Les snippets suivants sont définis dans `templates.json` pour être utilisés par l'IDE :

* **`dbg`**: Pour l'affichage rapide de variable de debug.
* **`tst`**: Pour générer un squelette de test unitaire avec pytest.
* **`main`**: Pour insérer un bloc de lancement standard Python (`if __name__ == "__main__"`).
* **`cli`**: Pour générer une structure de base pour une interface en ligne de commande avec `argparse`.