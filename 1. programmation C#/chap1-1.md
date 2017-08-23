# Mémoire vive et stockage volatile de l'information

Il va très vite falloir stocker et manipuler des informations (des chiffres, du texte, des noms, etc).
Pour cela, il nous faut des **variables**.

Elles permettent d'utiliser très facilement **la RAM** (les petites barrettes dans vos machines) qui est un stockage **volatile**, c'est à dire que ce qui est dedans est perdu quand le programme (ou la machine) est éteint(e).

## Les types

Une machine ne comprend que du binaire, une suite de 0 et de 1.

Mais nous, humains, avons besoin de manipuler des chiffres, des lettres.

Il faut donc utiliser des **types** pour indiquer à l'ordinateur ce que sont nos données pour qu'il puisse les stocker et les utiliser correctement.

Les types suivants sont les plus couramment utilisés. Ce sont les types `primitifs`, qui sont définis par le langage et sont à la base de tout.

| type | nom FR | exemples de valeurs | valeur par défaut |
|------|--------|---------------------|-------------------|
| **bool** | booléen | `false` (faux, 0) `true` (vrai, 1)  | `false`  |
| **int** | nombre entier | `0`, `1`, `-78`, `12456` | `0` |
| **float** | nombre à virgule | `0f`, `0.42f`, `784.5368f`, `-87.1f` | `0f` |
| **string** | chaîne de caractère | `"damien"`, `"I:0145"`, `"Je suis un texte."` | `""` (vide) |

De très nombreux types plus complexes sont proposés par C# et on peut créer une **infinité** de nouveaux types: `Player`, `FicheDePaie`, `Message`, `Dialogue`... tout dépend du projet.

La valeur par défaut de ces types non primitifs est, sauf exceptions, `null`.

## Variables

Une **variable** c'est un emplacement, une "boîte", en mémoire dans laquelle on peut ranger une information (points de vie, nom du joueur, niveau, etc).

Le contenu peut *varier*, c'est à dire changer au cours de l'exécution du programme.

Une **variable** a toujours :

- un type
- un nom
- une valeur
- une portée (expliqué après)

### Vie d'une variable

Une variable peut subir 4 opérations. Le programmeur C# peut agir sur 3 d'entre elles.

1/ la **déclaration** (ou *définition*)

Pour utiliser une variable, il faut la déclarer, indiquer qu'elle existe et quel est son **type**.
On peut indiquer une valeur pour **initialiser** la variable comme on le souhaite. Elle aura sinon une valeur par défaut (cf tableau ci-dessus).

Exemples :

```csharp
int hp = 42;
```

```csharp
string playerName;
```

```csharp
float timer = 3f;
```

(On peut déclarer plusieurs variables d'un même type sur une même ligne, mais cela n'est pas toujours très lisible

```csharp
int i,j,k;
```

2/ l' **écriture** d'une valeur

On peut sauvegarder une valeur, un chiffre, un texte en mémoire dans la variable.
Pour cela la variable est à gauche d'un signe `=`.

```csharp
int i;

i = 42;
i = 10;

string playerName = "";
playerName = "Damien";
```

3/ la **lecture** de la valeur

On peut à tout moment utiliser la valeur stockée.

```csharp
int i = 42;

Console.WriteLine(i); // Affiche 42 à l'écran

int b = i; // b vaut i, donc b vaut 42
```

Le stockage d'une variable est fait dans la mémoire vive (RAM). **En C#**, vous n'avez pas à vous inquiéter de cela.

### Portée

Une variable ne peut pas être utilisée avant d'avoir été déclarée.

```csharp
variable = 42; // Erreur : "variable" inconnue
int variable; // NOPE
```

Mais l'imbrication des blocs de code définit aussi une **portée**.

La **portée** d’une variable est la zone de code dans laquelle elle est utilisable. Elle correspond en général au bloc de code dans lequel est **déclarée** la variable.

Un exemple (voir les commentaires) :

```csharp
void Function()
{
  // Ici je n'ai pas encore déclaré de variables

  int var1 = 1;

  // Ici var1 est utilisable
  // Mais pas var2, qui n'existe pas

  if(condition)
  {
    // On déclare var2 dans un nouveau bloc
    // var2 ne sera utilisable que dans ce bloc
    int var2 = 4;

    // var1 et var2 sont utilisables

    var1 = var2;
  }

  // Fin du bloc "if", var2 n'existe plus
  // var1 est utilisable, var2 non
  var1 += 1;
}
```

Plus le bloc est imbriqué dans d'autres blocs, moins la variable est visible. Et vice-versa.

### Aparté sur `null`.

`null` veut dire "rien", "vide". Utiliser une variable `null` génèrera dans la plupart des cas une erreurs (NullReferenceException).

C'est une valeur en soi.

Tous les types qui ne sont pas de base, primitifs, en C# (int, float, bool, etc) ou de base avec Unity (Vector2, Vector3, etc) peuvent avoir comme valeur `null`.

```csharp
Joueur player;

player = null; // On remplit la variable "player" de vide.
```

## Les opérations

La plupart des opérateurs mathématiques sont utilisables dans le code, sur la plupart des types de base.

| Opérateur | Nom | Exemple |
|----|----|----|
| + | addition | `int i = 5 + 7;`|
| - | soustraction | `int i = 5 - 7;`|
| * | multiplication | `int i = 5 * 7;`|
| / | division | `float faction = 1 / 4f;`|
| % | modulo | `int i = 1 % 2;`|

*Remarque :* vous ne pourrez pas utiliser les opérateurs sur les types que vous avez vous-mêmes créés. De même, la plupart des types qui ne sont pas primitifs ne permettent pas d'utiliser les opérateurs. 

## Exercice

TODO
