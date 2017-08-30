---
title: Tableaux et liste
layout: default
---

Vous avez compris le principe des `tables` en Lua, nous allons voir leur équivalent en C# avec les tableaux et les listes.

## Les tableaux

Comme en Lua, les taableaux se reocnnaissent avec les crochets `[] `. Ils viennent ici se placer après le type de données que l'on peut stocker.

On ne peut stocker qu'un **seul et même** type de donnée dans un tableau.

```csharp
string[] players;
```

Les tableaux en C# ont une **taille fixe** donnée à la déclaration. Il faut décider de cette taille à la création, selon le contexte.

Exemple pour stocker 4 pseudos de joueurs :

```csharp
string[] players = new string[4];
```

On peut connaître la taille d'un tableau avec `Length`.

Écrire dans le tableau se fait simplement en accédant à la position de son choix par un nombre :

```csharp
players[0] = "Damien";
players[1] = "Laurent";
players[2] = "Matthieu";
players[3] = "Simon";
```

**Note : Les tableaux commencent à 0 !!!**

On peut aussi créer les tableaux plus directement :

```csharp
string[] players = new string[] { "Damien", "Laurent", "Matthieu", "Simon" };
```


Pour utiliser la valeur, c'est très similaire :

```csharp
Console.WriteLine("Le perdant est " + players[1]);
```

Les tableaux sont typiquement utilisés en combinaison aec une boucle `for`.

```csharp
for (int i = 0; i < players.Length; i++)
{
  Console.WriteLine("Joueur " + i + " : " + players[i]);
}
```

Une syntaxe plus agréable est possible avec les boucles `foreach` qui va parcourir tous les éléments de la collection (mais on perd l'indice de boucle) :

```csharp
foreach (string p in players)
{
  Console.WriteLine("Joueur " + p);
}
```

## Les listes

Il existe beaucoup de type de listes (au sens : forme de stockage dynamique de données dans une variable) en C# : `List`, `Queue`, `Stack`, etc.

La plus courante est la `List<T>` où `T` est le type de donnée à stocker.

Voici un exemple complet :

```csharp
// Création d'une liste
List<string> players = new List<string>();

// Ajouts d'éléments
players.Add("Damien");
players.Add("Laurent");

// Foreach possible, syntaxe identique aux tableaux
foreach (string p in players)
{
 Console.WriteLine("Joueur " + p);
}

// On peut ajouter plus tard
players.Add("Matthieu");

// Suppression
players.Remove("Damien");

players.Add("Simon");

// Foreach possible, syntaxe identique aux tableaux.
// Le nombre d'éléments est indiqué avec Count
for (int i = 0; i < players.Count; i++)
{
 Console.WriteLine("Joueur " + i + " : " + players[i]);
}
```

## Le dictionnaire

Enfin, le plus complexe et coûteux des types est aussi celui qui se rapproche le plus des `table` en Lua.

Le dictionnaire `Dictionary<K,V>` permet en effet d'associer une clé de type `K` à une valeur de type `V`.

```csharp
Dictionary<string, string[]> names = new Dictionary<string, string[]>();
names.Add("Damien", new string[] { "Mayance", "Godlike", "Steredennou" });
names.Add("Laurent", new string[] { "Victorino", "The best", "Night caller" });
```

L'accès aux données dans un dictionnaire se fait en passant la clé dans les crochets :

```csharp
string[] laurentNames = names["Laurent"];
```

Seule une boucle `foreach` est possible sur ce type de structure de données :

```csharp
foreach (string n in names.Keys)
{
  Console.WriteLine("Names count : " + names[n].Length);
}
```
