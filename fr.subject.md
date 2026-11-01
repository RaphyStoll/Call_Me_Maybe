# call me maybe
**Introduction au function calling dans les LLMs**

*Résumé : Les LLMs parlent-ils le langage des ordinateurs ? On va le découvrir.*
*Réalisé en collaboration avec @ldevelle, @pcamaren, @crfernan. Version : 1.5*

---

## Sommaire

- [Chapitre I : Avant-propos](#chapitre-i--avant-propos)
- [Chapitre II : Instructions sur l'IA](#chapitre-ii--instructions-sur-lia)
- [Chapitre III : Introduction](#chapitre-iii--introduction)
- [Chapitre IV : Instructions communes](#chapitre-iv--instructions-communes)
- [Chapitre V : Partie obligatoire](#chapitre-v--partie-obligatoire)
- [Chapitre VI : Exigences pour le README](#chapitre-vi--exigences-pour-le-readme)
- [Chapitre VII : Partie bonus](#chapitre-vii--partie-bonus)
- [Chapitre VIII : Rendu et évaluation par les pairs](#chapitre-viii--rendu-et-évaluation-par-les-pairs)

---

## Chapitre I : Avant-propos

Les ingénieurs romains gravaient des tablettes de pierre avec des grilles parfaites pour suivre les cargaisons de grain à travers l'empire. Ainsi, aucune livraison ne se perdait à cause d'une écriture illisible. Au XIXe siècle, les marins consignaient les courants océaniques dans des tableaux structurés si précis que certains servent encore aujourd'hui à la navigation.

Les premières prévisions météo étaient envoyées par télégramme dans un code fixe : quelques chiffres suffisaient à décrire un ciel entier. Dans les années 1960, le centre de contrôle de la NASA travaillait avec des organigrammes plastifiés qui indiquaient exactement ce que signifiait chaque voyant clignotant, quelle que soit l'équipe de service. Les lecteurs de codes-barres des supermarchés traduisaient des rayures noires et blanches en données d'inventaire bien avant que la plupart des foyers aient un ordinateur. Même les apiculteurs utilisent depuis des décennies des formulaires standardisés. Ils y notent la santé de la ruche, le flux de nectar et la lignée de la reine dans de petites cases qu'eux seuls savent lire d'un coup d'œil.

Les humains ont toujours construit des structures pour rendre l'information fiable, partageable et exploitable. Ce qui nous amène à aujourd'hui, où le but est de faire parler à l'IA le langage des ordinateurs.

---

## Chapitre II : Instructions sur l'IA

### ● Contexte

Pendant votre apprentissage, l'IA peut vous aider dans de nombreuses tâches. Prenez le temps d'explorer ce que les outils d'IA savent faire et comment ils peuvent soutenir votre travail. Restez toutefois prudent et évaluez les résultats d'un œil critique. Qu'il s'agisse de code, de documentation, d'idées ou d'explications techniques, vous ne pouvez jamais être totalement sûr que votre question était bien posée ni que le contenu généré est exact. Vos pairs sont une ressource précieuse pour éviter les erreurs et les angles morts.

### ● Message principal

- ☛ Utilisez l'IA pour réduire les tâches répétitives ou fastidieuses.
- ☛ Développez des compétences de prompting, en code comme hors code, qui serviront à votre future carrière.
- ☛ Apprenez comment fonctionnent les systèmes d'IA pour mieux anticiper et éviter les risques, les biais et les problèmes éthiques courants.
- ☛ Continuez à développer vos compétences techniques et vos soft skills en travaillant avec vos pairs.
- ☛ N'utilisez que du contenu généré par IA que vous comprenez entièrement et dont vous pouvez assumer la responsabilité.

### ● Règles pour l'apprenant

- Prenez le temps d'explorer les outils d'IA et de comprendre leur fonctionnement, pour les utiliser de manière éthique et réduire les biais potentiels.
- Réfléchissez à votre problème avant de rédiger un prompt. Cela vous aide à écrire des prompts plus clairs, plus détaillés et plus pertinents, avec un vocabulaire précis.
- Prenez l'habitude de vérifier, relire, remettre en question et tester systématiquement tout ce que l'IA génère.
- Demandez toujours une relecture par vos pairs : ne vous fiez pas uniquement à votre propre validation.

### ● Objectifs de la phase

- Développer des compétences de prompting générales et spécifiques à un domaine.
- Améliorer votre productivité grâce à un usage efficace des outils d'IA.
- Continuer à renforcer la pensée computationnelle, la résolution de problèmes, l'adaptabilité et la collaboration.

### ● Commentaires et exemples

- Vous rencontrerez régulièrement des situations (examens, évaluations, etc.) où vous devrez montrer une vraie compréhension. Soyez prêt, et continuez à développer vos compétences techniques et relationnelles.
- Expliquer votre raisonnement et débattre avec vos pairs révèle souvent des lacunes dans votre compréhension. Faites de l'apprentissage entre pairs une priorité.
- Les outils d'IA manquent souvent de votre contexte spécifique et donnent des réponses génériques. Vos pairs, qui partagent votre environnement, peuvent apporter des éclairages plus pertinents et plus précis.
- Là où l'IA tend à générer la réponse la plus probable, vos pairs peuvent apporter d'autres perspectives et des nuances précieuses. Appuyez-vous sur eux comme point de contrôle qualité.

> ✓ **Bonne pratique :** Je demande à l'IA : « Comment tester une fonction de tri ? ». Elle me donne quelques idées. Je les essaie et j'examine les résultats avec un pair. Nous affinons l'approche ensemble.

> ✗ **Mauvaise pratique :** Je demande à l'IA d'écrire une fonction entière et je la copie-colle dans mon projet. Pendant l'évaluation par les pairs, je ne sais pas expliquer ce qu'elle fait ni pourquoi. Je perds en crédibilité et j'échoue mon projet.

> ✓ **Bonne pratique :** J'utilise l'IA pour m'aider à concevoir un parser. Ensuite, je parcours la logique avec un pair. Nous repérons deux bugs et le réécrivons ensemble : il est meilleur, plus propre et entièrement compris.

> ✗ **Mauvaise pratique :** Je laisse Copilot générer le code d'une partie clé de mon projet. Ça compile, mais je ne sais pas expliquer comment il gère les pipes. Pendant l'évaluation, je n'arrive pas à justifier mon code et j'échoue mon projet.

---

## Chapitre III : Introduction

### III.1 Qu'est-ce que le function calling ?

Les grands modèles de langage (LLMs) sont très doués pour comprendre et générer du langage humain. En revanche, ils ne produisent pas naturellement une sortie structurée et exécutable par une machine. Le function calling comble ce manque : il traduit des requêtes en langage naturel en appels de fonction précis, avec des arguments typés.

Exemple : du langage naturel à l'appel de fonction

```
User: "What is the sum of 40 and 2?"

Traditional LLM: "The sum of 40 and 2 is 42."

Function Calling System:
{
  "function": "add_numbers",
  "arguments": {"a": 40, "b": 2}
}
```

Le système de function calling ne répond pas directement à la question. Il fournit plutôt les **outils** pour la résoudre : le bon nom de fonction et les bons arguments, avec les bons types.

### III.2 Pourquoi est-ce important ?

Le function calling permet aux LLMs de :

- **Interagir avec des systèmes externes** : appeler des APIs, interroger des bases de données, contrôler des appareils
- **Exécuter du code** : faire des calculs, transformer des données, manipuler des fichiers
- **Enchaîner des opérations** : découper des tâches complexes en étapes exécutables
- **Produire une sortie structurée** : générer du JSON, du XML ou d'autres formats lisibles par une machine
- **Extraire des données structurées d'un texte non structuré** : par exemple, à partir d'un long livre, extraire des champs comme `{protagonist name, protagonist sex, protagonist age}`

Cette technologie fait fonctionner les assistants IA modernes, les outils de génération de code et les agents autonomes. Elle permet aussi l'extraction automatique d'informations et la structuration de connaissances à partir de texte brut.

### III.3 Le défi

Les petits modèles de langage (comme le modèle de 0,6 milliard de paramètres que vous allez utiliser) sont connus pour leur manque de fiabilité quand il s'agit de générer une sortie structurée. Quand on leur demande du JSON, ils ne réussissent parfois que 30 % du temps. Pourtant, les systèmes en production atteignent plus de 99 % de fiabilité avec ces mêmes petits modèles.

**Comment ?** La réponse est le **décodage contraint** (*constrained decoding*). Cette technique guide la sortie du modèle token par token pour garantir une structure valide, sans compter uniquement sur le prompt.

---

## Chapitre IV : Instructions communes

### IV.1 Règles générales

- Votre projet doit être écrit en **Python 3.10 ou plus récent**.
- Votre projet doit respecter la norme de code **flake8**.
- Vos fonctions doivent gérer les exceptions proprement pour éviter les crashs. Utilisez des blocs `try-except` pour gérer les erreurs possibles. Préférez les context managers pour les ressources comme les fichiers ou les connexions, afin de garantir leur libération automatique. Si votre programme crashe à cause d'une exception non gérée pendant l'évaluation, il sera considéré comme non fonctionnel.
- Toutes les ressources (descripteurs de fichiers, connexions réseau, etc.) doivent être correctement gérées pour éviter les fuites. Utilisez des context managers quand c'est possible.
- Votre code doit inclure des type hints pour les paramètres de fonction, les types de retour et les variables quand c'est pertinent (avec le module `typing`). Utilisez `mypy` pour la vérification statique des types. Toutes les fonctions doivent passer mypy sans erreur.
- Ajoutez des docstrings aux fonctions et aux classes selon la PEP 257 (style Google ou NumPy, par exemple) pour documenter leur rôle, leurs paramètres et leurs valeurs de retour.

### IV.2 Makefile

Incluez un `Makefile` dans votre projet pour automatiser les tâches courantes. Il doit contenir les règles suivantes (la règle lint obligatoire implique les flags indiqués ; il est fortement recommandé d'essayer `--strict` pour une vérification plus poussée) :

- **install** : installe les dépendances du projet avec `pip`, `uv`, `pipx` ou tout autre gestionnaire de paquets de votre choix.
- **run** : exécute le script principal du projet (via l'interpréteur Python, par exemple).
- **debug** : lance le script principal en mode debug avec le débogueur intégré de Python (`pdb`, par exemple).
- **clean** : supprime les fichiers temporaires et les caches (`__pycache__`, `.mypy_cache`, etc.) pour garder l'environnement propre.
- **lint** : exécute les commandes `flake8 .` et `mypy . --warn-return-any --warn-unused-ignores --ignore-missing-imports --disallow-untyped-defs --check-untyped-defs`
- **lint-strict** (optionnel) : exécute les commandes `flake8 .` et `mypy . --strict`

### IV.3 Consignes supplémentaires

- Créez des programmes de test pour vérifier le bon fonctionnement du projet (ils ne sont ni rendus ni notés). Utilisez des frameworks comme `pytest` ou `unittest` pour les tests unitaires, en couvrant les cas limites.
- Incluez un fichier `.gitignore` pour exclure les artefacts Python.
- Il est recommandé d'utiliser un environnement virtuel (`venv` ou `conda`, par exemple) pour isoler les dépendances pendant le développement.

*Si des exigences spécifiques au projet s'appliquent, elles sont indiquées juste en dessous de cette section.*

#### IV.3.1 Exigences supplémentaires

- Toutes les classes doivent utiliser **pydantic** pour la validation.
- Vous pouvez utiliser les paquets **numpy** et **json**.
- L'utilisation de **dspy** (ou de tout paquet similaire) est strictement interdite, y compris pytorch, les paquets huggingface, transformers, outlines, etc.
- Vous devez utiliser les modèles suivants :
  - **Qwen/Qwen3-0.6B** (par défaut)
  - Vous pouvez utiliser d'autres modèles, à condition que votre projet fonctionne avec **Qwen/Qwen3-0.6B**.
- La fonction à appeler doit être choisie par le LLM, et non par des heuristiques ou toute autre forme de magie médiévale.
- Il est interdit d'utiliser des méthodes ou attributs privés du paquet `llm_sdk`.
- Vous devez créer un environnement virtuel et installer les paquets **numpy** et **pydantic** avec **uv**. Pour utiliser **llm_sdk**, vous pouvez le copier dans le même répertoire que celui qui contient `src`.
- L'évaluateur, comme la moulinette, lancera simplement `uv sync`.
- Toutes les erreurs doivent être gérées proprement. Votre programme ne doit jamais crasher de manière inattendue et doit toujours afficher des messages d'erreur clairs à l'utilisateur.

#### IV.3.2 Utilisation

Votre programme doit être lancé avec la commande suivante (où `src` est le dossier qui contient vos fichiers) :

```bash
uv run python -m src [--functions_definition <function_definition_file>] [--input <input_file>] [--output <output_file>]
```

> ℹ️ Par défaut, le programme lit les fichiers d'entrée dans le répertoire `data/input/` et écrit la sortie dans le répertoire `data/output/`. Vous pouvez éventuellement indiquer d'autres chemins avec les arguments `--input` et `--output`. Par exemple :

```bash
uv run python -m src \
  --functions_definition data/input/functions_definition.json \
  --input data/input/function_calling_tests.json \
  --output data/output/function_calls.json
```

---

## Chapitre V : Partie obligatoire

### V.1 Résumé

Dans ce projet, vous allez créer un outil de function calling qui traduit des prompts en langage naturel en appels de fonction structurés. Face à une question comme « What is the sum of 40 and 2? », votre solution ne doit pas renvoyer 42, mais plutôt :

- Le nom de la fonction : `fn_add_numbers`
- Les arguments : `{"a": 40, "b": 2}`

Votre implémentation doit utiliser le **décodage contraint** pour garantir une sortie JSON valide à 100 %. Cela assure une fiabilité quasi parfaite, même avec un petit modèle de 0,6 milliard de paramètres.

### V.2 Fichiers d'entrée

Votre solution traite deux fichiers d'entrée situés dans le répertoire `data/input/` :

**`function_calling_tests.json`** : contient un tableau JSON de prompts en langage naturel que votre système doit traiter.

```json
[
  {
    "prompt": "What is the sum of 2 and 3?"
  },
  {
    "prompt": "What is the sum of 265 and 345?"
  },
  {
    "prompt": "Greet shrek"
  },
  {
    "prompt": "Greet john"
  },
  {
    "prompt": "Reverse the string 'hello'"
  },
  ...
]
```

**`functions_definition.json`** : contient les fonctions que votre système peut appeler. Chaque fonction comprend :

- Le nom de la fonction
- Les noms et types des arguments
- Le type de retour
- Une description

```json
[
  {
    "name": "fn_add_numbers",
    "description": "Add two numbers together and return their sum.",
    "parameters": {
      "a": {
        "type": "number"
      },
      "b": {
        "type": "number"
      }
    },
    "returns": {
      "type": "number"
    }
  },
  {
    "name": "fn_greet",
    "description": "Generate a greeting message for a person by name.",
    "parameters": {
      "name": {
        "type": "string"
      }
    },
    "returns": {
      "type": "string"
    }
  },
  {
    "name": "fn_reverse_string",
    "description": "Reverse a string and return the reversed result.",
    "parameters": {
      "s": {
        "type": "string"
      }
    },
    "returns": {
      "type": "string"
    }
  },
  ...
]
```

> ⚠️ Ces exemples donnent le niveau de complexité attendu. Cependant, votre solution sera testée avec d'autres prompts et d'autres ensembles de fonctions. Vous devez gérer correctement les erreurs JSON des fichiers d'entrée, car ils peuvent contenir du JSON invalide ou être complètement absents.

### V.3 Interaction avec le LLM

#### V.3.1 Le SDK LLM

Le projet est fourni avec une classe wrapper **Small_LLM_Model** dans le paquet `llm_sdk`, que vous pouvez utiliser pour interagir avec le LLM.

Le SDK fournit plusieurs méthodes essentielles :

- `get_logits_from_input_ids(input_ids: List[int]) -> List[float]`
  Prend une liste d'IDs de tokens et renvoie les logits produits par le modèle.
- `get_path_to_vocab_file() -> str`
  Renvoie le chemin du fichier de vocabulaire qui contient la correspondance entre IDs de tokens et tokens.
- `encode(text: str) -> Tensor`
  Encode une chaîne de texte en un tenseur d'IDs de tokens avec le tokenizer du modèle.
- `decode(token_ids: List[int]) -> str` *(optionnel)*
  Décode une liste d'IDs de tokens en chaîne de texte.

#### V.3.2 Le pipeline de génération

La génération d'un LLM suit ces étapes :

1. **Prompt** : votre question en langage naturel.
   Exemple : *"What is the sum of 2 and 3?"*
2. **Tokenisation** : le texte est découpé en unités sous-lexicales (tokens). Contrairement à un simple découpage en mots, les tokenizers incluent souvent les espaces initiaux, gèrent la ponctuation et découpent les mots en plus petits morceaux avec des algorithmes comme BPE ou SentencePiece.
   Exemple (réaliste) : `["What", "Ġis", "Ġthe", "Ġsum", "Ġof", "Ġ2", "Ġand", "Ġ3", "?"]`
   Note : le symbole « Ġ » indique un espace devant le token. Les vrais tokenizers conservent ces détails pour reconstruire le texte exactement.
3. **Input IDs** : les tokens sont convertis en IDs numériques que le modèle comprend.
   Exemple (illustratif) : `[892, 318, 262, 4771, 286, 16, 290, 17, 30]`
4. **Traitement par le LLM** : le modèle fait passer ces nombres dans son réseau de neurones.
5. **Logits** : le modèle produit un score de probabilité pour chaque token suivant possible.
   Exemple : `token_5: 0.001, token_42: 0.85, token_100: 0.02, …`
6. **Sélection du token** : le token suivant est choisi selon ces probabilités, généralement celui qui a le score le plus élevé.
   *C'est à cette étape qu'on peut appliquer des techniques comme le **décodage contraint**, pour restreindre les choix de tokens et garantir que la sortie suit une structure précise, par exemple du JSON valide à 100 %.*

**Important** : ce processus se répète token par token. Chaque token généré est ajouté au prompt, et les étapes 2 à 6 se répètent jusqu'à ce que la réponse soit complète.

**Vue simplifiée :**

```
Prompt -> Tokenization -> Input IDs -> LLM -> Logits -> Next Token Selection
```

#### V.3.3 Comprendre le décodage contraint

Les modèles de langage génèrent du texte un token à la fois. À chaque étape, le modèle produit une distribution de probabilité (les logits) sur tous les tokens suivants possibles. Normalement, on échantillonne dans cette distribution ou on choisit le token le plus probable.

Le **décodage contraint** intervient dans ce processus en modifiant les logits *avant* la sélection du token :

1. Le modèle produit les logits de tous les tokens possibles.
2. Vous identifiez les tokens qui préservent à la fois une structure JSON valide *et la conformité au schéma attendu*.
3. Vous mettez à moins l'infini les logits des tokens invalides (ceux qui cassent le schéma ou la structure).
4. Vous échantillonnez uniquement parmi les tokens valides restants.

Dans ce projet, le décodage contraint doit non seulement garantir un JSON syntaxiquement valide, mais aussi imposer un schéma précis. Par exemple, si un champ doit être un nombre d'après `functions_definition.json`, le décodeur limite le choix des tokens aux valeurs qui forment un entier ou un flottant. La validité JSON et la conformité au schéma sont ainsi préservées toutes les deux. Chaque token généré respecte donc la validité structurelle et sémantique, et le schéma demandé est imposé. Le JSON produit est ainsi exploitable à 100 % et peut toujours être parsé sans erreur.

> ⚠️ Votre solution ne doit **PAS** compter sur le modèle pour produire spontanément du JSON correct à partir d'un prompt. Donner les définitions de fonctions au modèle dans le prompt en espérant une sortie structurée n'est pas fiable, et ce n'est pas la compétence qu'on attend de vous ici.

> ℹ️ Réfléchissez à la façon d'utiliser le fichier JSON de vocabulaire pour faire la correspondance entre les tokens et leur représentation textuelle. C'est essentiel pour déterminer quels tokens sont valides à chaque étape de génération.

### V.4 Format du fichier de sortie

Votre programme produit un seul fichier JSON : `data/output/function_calling_results.json`.
Pour chaque prompt, ajoutez un objet JSON à ce fichier. Chaque objet du tableau doit contenir exactement les clés suivantes :

- `prompt` (string) : la requête originale en langage naturel
- `name` (string) : le nom de la fonction à appeler
- `parameters` (object) : tous les arguments requis, avec les bons types

#### V.4.1 Exemple de sortie

```json
[
  {
    "prompt": "What is the sum of 2 and 3?",
    "name": "fn_add_numbers",
    "parameters": {"a": 2.0, "b": 3.0}
  },
  {
    "prompt": "Reverse the string 'hello'",
    "name": "fn_reverse_string",
    "parameters": {"s": "hello"}
  }
]
```

#### V.4.2 Règles de validation

- Le fichier doit être du JSON valide (pas de virgule finale, pas de commentaire).
- Les clés et les types doivent correspondre exactement au schéma de `functions_definition.json`.
- Aucune clé supplémentaire ni aucun texte libre n'est autorisé dans la sortie.
- Tous les arguments requis doivent être présents.
- Les types des arguments doivent correspondre à la définition de la fonction (number, string, boolean, etc.).

> ⚠️ Les fichiers d'entrée fournis peuvent changer pendant l'évaluation. Ne codez pas en dur des solutions basées sur les exemples fournis.

### V.5 Performance et fiabilité

Votre implémentation doit atteindre :

- **Une précision quasi parfaite** : plus de 90 % de bonnes sélections de fonction et de bonnes extractions d'arguments
- **100 % de JSON valide** : chaque sortie doit être parsable et conforme au schéma
- **Une vitesse raisonnable** : traiter tous les prompts de test en moins de 5 minutes sur du matériel standard
- **Une gestion d'erreurs robuste** : gérer proprement les entrées mal formées, les fichiers manquants et les cas limites

> ℹ️ Le modèle Qwen3-0.6B n'a que 500 millions de paramètres. Pourtant, avec un décodage contraint correct, il peut atteindre une fiabilité comparable à celle de modèles bien plus gros. Cela montre la puissance du guidage structurel par rapport à la taille brute du modèle.

### V.6 Tester votre implémentation

Pour vérifier que votre solution fonctionne :

1. Assurez-vous que les fichiers d'entrée sont dans le répertoire `data/input/`.
2. Lancez : `uv run python -m src [--functions_definition <function_definition_file>] [--input <input_file>] [--output <output_file>]`
3. Vérifiez que `output/function_calling_results.json` est bien créé.
4. Validez la structure et le contenu du JSON.
5. Vérifiez que les noms de fonction et les types d'arguments correspondent aux définitions.

> ⚠️ Testez avec divers cas limites : chaînes vides, grands nombres, caractères spéciaux, mauvais types, prompts ambigus et fonctions à plusieurs paramètres.

---

## Chapitre VI : Exigences pour le README

Un fichier `README.md` doit se trouver à la racine de votre dépôt Git. Son but est de permettre à quelqu'un qui ne connaît pas le projet (pairs, staff, recruteurs, etc.) de comprendre rapidement de quoi il s'agit, comment le lancer et où trouver plus d'informations sur le sujet.

Le `README.md` doit contenir au minimum :

- Une toute première ligne en italique qui dit : *This project has been created as part of the 42 curriculum by \<login1\>[, \<login2\>[, \<login3\>[...]]].*
- Une section « **Description** » qui présente clairement le projet, son objectif et un bref aperçu.
- Une section « **Instructions** » avec toute information utile sur la compilation, l'installation et/ou l'exécution.
- Une section « **Resources** » qui liste les références classiques sur le sujet (documentation, articles, tutoriels, etc.). Elle doit aussi décrire comment l'IA a été utilisée : pour quelles tâches et sur quelles parties du projet.

➠ **D'autres sections peuvent être exigées selon le projet** (exemples d'utilisation, liste de fonctionnalités, choix techniques, etc.).

*Les ajouts requis sont listés explicitement ci-dessous.*

Pour ce projet, le `README.md` doit aussi contenir :

- **Explication de l'algorithme** : décrivez en détail votre approche du décodage contraint
- **Choix de conception** : expliquez les choix clés de votre implémentation
- **Analyse des performances** : discutez de la précision, de la vitesse et de la fiabilité de votre solution
- **Difficultés rencontrées** : documentez les difficultés et la façon dont vous les avez résolues
- **Stratégie de test** : décrivez comment vous avez validé votre implémentation
- **Exemples d'utilisation** : donnez des exemples clairs d'exécution du programme

> ℹ️ Votre README doit être rédigé en anglais.

---

## Chapitre VII : Partie bonus

Fonctionnalités bonus évaluées (optionnelles, non requises pour valider) :

- Support de plusieurs modèles LLM en plus de Qwen/Qwen3-0.6B
- Recoder le tokenizer : éviter d'utiliser directement `encode` et `decode` dans le code principal, et utiliser plutôt `get_logits_from_input_ids` et `get_path_to_vocab_file`
- Mécanismes avancés de récupération d'erreur
- Optimisations de performance (cache, batching)
- Suite de tests complète
- Visualisation du processus de génération
- Support d'arguments de fonction complexes et imbriqués
- Implémentation publique des méthodes `encode` (et éventuellement `decode`) du tokenizer
- Démonstration de l'intégration de l'encodage et du décodage avec le décodage contraint

Les bonus doivent être implémentés et fonctionnels, pas seulement décrits dans le `README.md`. On pourra vous demander de les montrer pendant l'évaluation.

---

## Chapitre VIII : Rendu et évaluation par les pairs

Rendez votre travail dans votre dépôt Git comme d'habitude. Seul le contenu de votre dépôt sera évalué pendant la soutenance. N'hésitez pas à revérifier les noms de vos fichiers.

Votre dépôt doit contenir :

- Le répertoire `src/` avec votre implémentation
- `pyproject.toml` et `uv.lock` pour la gestion des dépendances
- Le répertoire `llm_sdk/` (copié depuis le paquet fourni)
- Le répertoire `data/input/` avec les fichiers de test (pour la démonstration)
- Un `README.md` avec une documentation complète
- Tout fichier supplémentaire nécessaire pour lancer votre solution

> ⚠️ N'incluez pas le répertoire `output/` dans votre dépôt. Il sera généré pendant l'évaluation.

Pendant l'évaluation, on pourra vous demander une brève **modification du projet** : un petit changement de comportement, quelques lignes de code à écrire ou réécrire, ou une fonctionnalité facile à ajouter.

Cette étape **ne s'applique pas forcément à tous les projets**, mais vous devez y être préparé si elle figure dans la grille d'évaluation.

Elle sert à vérifier que vous comprenez vraiment une partie précise du projet. Vous pouvez faire la modification dans l'environnement de développement de votre choix (votre setup habituel, par exemple). Elle doit pouvoir se faire en quelques minutes, sauf si un délai précis est fixé dans l'évaluation.

Par exemple, on peut vous demander de faire une petite mise à jour d'une fonction ou d'un script, de modifier un affichage, ou d'adapter une structure de données pour stocker une nouvelle information.

Les détails (périmètre, cible, etc.) sont précisés dans la **grille d'évaluation** et peuvent varier d'une évaluation à l'autre pour un même projet.
