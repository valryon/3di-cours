---
title: Découverte du C#
layout: default
---

je pars du principe que vous avez acquis les bases de la programmation dans le cours PICO-8 précédent.

## Généralités

Le code est un moyen pour l'humain de donner des ordres à un ordinateur.
L'ordinateur exécute ces ordres, appelés **instructions** de manière **séquentielle**, les unes après les autres.

Sauf qu'un ordinateur ne peut pas directement lire du C#. Le C# est un language avec des mots clés en anglais qui est lisible pour un humain entraîné. Et à l'inverse, la machine ne lit que des 0 et 1.

C'est pour cela qu'il faut l'aide du **compilateur** qui transforme le code C# écrit en binaire que la machine peut exécuter. Si le compilateur détecte des erreurs, il les signale au programmeur et ne peut pas créer le programme désiré.

## Syntaxe

Le C#, comme chaque langage de programmation, obéit à une syntaxe particulière qui lui est propre. Notamment :

- Le code est toujours dans un bloc. Un bloc est délimité par des accolades `{ }`.
- Beaucoup de mots clés ouvrent un bloc après leur utilisation : `class`, `if()`, `for()`, etc.
- Chaque ligne de code se termine par un point-virgule ";"
- Les commentaires (texte libre pour le programmeur) commencent par `// Mon texte explicatif` ou sont écrits entre `/*` et `*/`

```csharp
// Ceci est un commentaire qui prend toute la ligne

/*
  Ceci est un commentaire
  sur
  plusieurs lignes
*/
```
- L'espacement du code est cosmétique, il est utile à l'homme mais pas à la machine.


## Visual Studio

Pour gagner du temps et réduire les erreurs, il faut utiliser les bons outils. Microsoft Visual Studio est un IDE (Integrated Development Environment), c'est à dire un éditeur de code avec moults outils prêts à l'emploi.

Accessible gratuitement dans des éditions suffisantes, Visual Studio est un excellent compagnon du programmeur C# sur Windows :

- Auto-complétion (vous commencez à taper, il propose des possibiltés)
- Coloration syntaxique (les mots clés, le code, tout ce que vous tapez est différenciable)
- Boutons magiques pour compiler et lancer le projet
- Explorateur de fichiers

Et des centaines (miliers ?) d'autres outils...

## Types de projet

Liste non exhaustive de ce que l'on peut faire avec le C# :

- Programme console
- Programme avec UI (fenêtre, boutons, images, etc)
- Serveurs d'applications
- Sites webs
- Jeux vidéo multiplateformes

Actuellement, à peu près tout ce qui se programme peut être écrit en C# (après, c'est plus ou moins pratique et efficace).

### Les applications consoles

L'interface graphique (UI / GUI) est récente dans l'histoire de l'informatique. Et il n'est pas nécessaire d'afficher une fenêtre avec des boutons à l'écran pour la plupart des programmes.

Une application console est une application qui écrit ligne par ligne dans la... **console** (pensez `cmd` sur Windows).

Quelques **fonctions** vont nous intéresser :

- `Console.WriteLine("text")` : Affiche la donnée ou le texte entre parenthèse dans la console
- `Console.ReadLine()` : Attend que l'utilisateur tape quelque chose et appuie sur entrée

En plus de cela, chaque programme doit définir un **point d'entrée**, c'est à dire quelle est la première ligne de code qui doit être exécutée.

Par convention, on appelle `Main` cette fonction qui sera reconnue par le compilateur.

## Exercice : "Hello World"

Afficher "Hello World" dans une console qui reste ouverte tant que l'utilisateur n'appuie pas sur une touche.

### Correction

1. Ouvrir Visual Studio
2. Créer un nouveau projet "Visual C# -> Windows -> Console Application"
3. La nommer comme vous le sentez. "HelloWorld" serait par exemple très original.

Tout l'IDE bouge et apparaît devant vous (ici simplifié):

```csharp
using System;

class Program
{
  static void Main(string[] args)
  {
  }
}
```

- "Démarrer" ou "Start" en haut dans la barre des tâches lance l'application
(Celle-ci ne fait rien, donc pour l'instant ça lance une application qui ne fait rien, du coup il ne se passe pas grand chose)

- On va ajouter l'attente de l'appui sur "Entrée":

```csharp
using System;

class Program
{
  static void Main(string[] args)
  {
    Console.ReadLine();
  }
}
```

- Puis l'affichage du texte

```csharp
using System;

class Program
{
  static void Main(string[] args)
  {
    Console.WriteLine("Hello World");
    Console.ReadLine();
  }
}
```

Et c'est tout !

Voyons d'autres différences/points communs avec le Lua de PICO-8.

## Les types

| type | nom FR | exemples de valeurs | valeur par défaut |
|------|--------|---------------------|-------------------|
| **bool** | booléen | `false` (faux, 0) `true` (vrai, 1)  | `false`  |
| **int** | nombre entier | `0`, `1`, `-78`, `12456` | `0` |
| **float** | nombre à virgule | `0f`, `0.42f`, `784.5368f`, `-87.1f` | `0f` |
| **string** | chaîne de caractère | `"damien"`, `"I:0145"`, `"Je suis un texte."` | `""` (vide) |

## Les variables

Similaire à Lua, mais un peu plus contraignant.

1. la **déclaration**

Il faut indiquer le **type** de la variable en plus de la nommer.

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

2. l'**affectation** d'une valeur

On peut sauvegarder une valeur, un chiffre, un texte en mémoire dans la variable.
Pour cela la variable est à gauche d'un signe `=`.

```csharp
int i;

i = 42;
i = 10;

string playerName = "";
playerName = "Damien";
```

Contrairement à Lua, on ne peut pas changer le type d'une variable en cours de route (et c'est tant mieux !).

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

## Structures de contrôle

### Conditions

```csharp
int vieJoueur = 1;

if(vieJoueur <= 0)
{
  if(playerName == "Damien")
  {
  }
}
```

On peut ajouter un `else` et combiner le `else` avec un autre `if`.
L'intérêt ? La condition n'est testée que **si** et **seulement si** le premier `if` est faux.

```csharp
if(playerName == "Damien")
{
  // Code pour le joueur "Damien"
}
else if(playerName == "Laurent")
{
  // Code pour le joueur "Laurent"
}
else
{
  // Code pour tous les autres joueurs
}
```

### Boucles

#### for

Syntaxe :

```csharp
for(int i=0; i<10; i++)
{
  // Code à répéter
}
```

Le for est découpé en 3 morceaux, séparés par des points-virgules.

1. `int i=0` : la boucle `for` a besoin d'un **indice** pour stocker la où elle est rendue. Par convention l'indice est appelé `i`, sans réelle raison.
C'est aussi le moment où on lui donne la valeur de départ, ici `0`.

2. `i<10` indique jusqu'à quel chiffre la boucle doit continuer. Ici, jusqu'à 9 (car 10 n'est pas strictement inférieur à 10.)

3. `i++` après une itération de boucle, il faut augmenter l'indice.
`i++` est une manière plus rapide d'écrire `i = i + 1`, autrement dit d'ajouter 1 au compteur.

Donc ici, à chaque itération de la boucle, on ajoute `1` à `i` jusqu'à ce que `i` soit égal à 10.

Si la valeur de départ est plus grande que celle d'arrivée, l'ordinateur ne va pas exploser : le code de la boucle ne sera juste jamais exécuté.

#### while

L'autre boucle très utile est `while`. Littéralement "répéter tant que".

Syntaxe :

```csharp
while(condition)
{
  // Code à répéter
}
```

La différence c'est qu'ici le nombre d'itérations n'est pas **connu**. Et il est potentiellement **infini**.

La **condition** est identique à ce que l'on peut mettre dans un `if`.

## Fonctions

Très proche de la syntaxe en Lua. La différence c'est qu'il faut donner le **type de retour** de la fonction, c'est à dire la valeur qu'elle retourne.

Si elle ne retroune pas de valeur, on indiquera `void` (*néant*), mais on est obligé d'écrire un type de retour en C#.

```csharp

void Start()
{

}

int Puissance2(int entree)
{
  return entree * entree;
}

string GetPlayerName(int id, string system)
{
  return "krokmou";
}

```

Exemples d'appels :

```csharp
  int a = Puissance2(2);
  int b = Puissance2(4);
  string joueur1 = GetPlayerName(0, "windows");
  string joueur2 = GetPlayerName(1, "macOS");
```

## Les erreurs

Le C# dispose d'un mécanisme de gestion des erreurs puissant. Ces erreurs sont appelées des **exceptions** et elles sont **levées** (*throw*) quand quelque chose ne va pas : ouvrir un fichier qui n'existe pas, division par 0, etc.

Une exception est destinée à faire planter le programme si elle n'est pas prise en charge.

Il est donc possible de les récupérer en entourant le code qui génère des erreurs avec un `try/catch` :

```csharp
try
{
  File.ReadAllLines(@"C:\Windows\kikoo.txt");
}
catch(Exception e)
{
  Console.WriteLine("Une erreur s'est produite : " + e);
}
```
