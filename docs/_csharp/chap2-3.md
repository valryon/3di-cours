---
title: Lecture et stockage de données avec des fichiers
layout: default
---

Les fichiers sont le principal moyen de stocker et de lire des informations sur une machine.

## Manipulation des fichiers

Les opérations de base sur des fichiers. Tout est prévu de base, mais il faut ajouter en haut du fichier :

```csharp
using System.IO;
```

- Lire un fichier texte "pizza.txt" sur le bureau

```csharp
string[] fileContent = File.ReadAllLines(@"C:\Users\dam\Desktop\pizza.txt");

// Exemple d'utilisation derrière
for (int i = 0; i < fileContent.Length; i++)
{
  Console.WriteLine("Line " + i + " " + fileContent[i]);
}

```

- Écrire dans un fichier

```csharp
File.WriteAllText(@"C:\Users\dam\Desktop\recette_hamburger.txt", "Aller chez MacDo. PROFIT. ");
```

- Ajouter des lignes à un fichier existant

```csharp
File.AppendAllText(@"C:\Users\dam\Desktop\recette_hamburger.txt", "(Ou pas)");
```

Pour aller plus loin

- Ceci sont des méthodes **simplifiées** de gestion des fichiers qui vous suffiront la plupart du temps. Normalement, on ouvre un fichier, on fait des choses avec et on le ferme quand on a terminé, sur plusieurs lignes et en plusieurs fois.

- Un gros fichier = des gros problèmes et d'autres façons de faire

- Si le fichier n'existe pas : **exception**

## Sérialisation

L'intérêt d'aborder la manipulation des fichiers serait moindre sans la notion de **sérialisation**.

La **sérialisation**, c'est la transformation des données dans un format à un autre.
Par exemple, convertir les scores de joueurs stockés dans un tableau d'entier dans un fichier texte, ligne par ligne.

La **désérialisation**, c'est l'inverse.

Ici nous allons voir comment sérialiser des données dans un fichier `JSON` ou `XML`, les formats les plus populaires.

Note : la sérialisation, c'est le coeur de Unity3D, son mécanisme le plus important qui est utilisé absolument partout.

Prenons un ensemble de données en mémoire :

```csharp
[System.Serializable] // Indique au système que l'on veut sérializer ce type de données
public struct Score
{
  public string pseudo;
  public int points;
}

// ...

Score[] scores = new Score[128];
scores[0] = new Score() { pseudo = "Damien", points = 999876 };
scores[1] = new Score() { pseudo = "Laurent", points = 700121 };
scores[2] = new Score() { pseudo = "Matthieu", points = 50412 };
```

On peut convertir ces scores en XML

```csharp
// Convertir nos scores en XML
XmlSerializer serializer = new XmlSerializer(typeof(Score[]));

// -- Affichage dans la console
serializer.Serialize(Console.Out, scores);

// -- Dans un fichier
TextWriter writer = new StreamWriter(@"C:\Users\dam\Desktop\scores.txt");
serializer.Serialize(writer, scores);
writer.Close();
```

Notre XML ressemblera à ça :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ArrayOfScore xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Score>
    <pseudo>Damien</pseudo>
    <points>999876</points>
  </Score>
  <Score>
    <pseudo>Laurent</pseudo>
    <points>700121</points>
  </Score>
  <Score>
    <pseudo>Matthieu</pseudo>
    <points>50412</points>
  </Score>
  <Score>
    <points>0</points>
  </Score>
  <Score>
    <points>0</points>
  </Score>
  <Score>
    <points>0</points>
  </Score>
  <Score>
    <points>0</points>
  </Score>
  <Score>
    <points>0</points>
  </Score>
</ArrayOfScore>
```

Nous pouvons ici éditer le fichier XML avec un éditeur de texte/code pour changer lse valeurs. Nous pouvons récupérer le fichier de quelqu'un d'autre qui aurait le même format.

Le processus inverse :

```csharp
// Récupérer les scores depuis le fichier
XmlSerializer deserializer = new XmlSerializer(typeof(Score[]));
FileStream fs = new FileStream(@"C:\Users\dam\Desktop\scores.txt", FileMode.Open);
Score[] scoresLus = (Score[])serializer.Deserialize(fs);

Console.WriteLine(scoresLus[0].pseudo + "-" + scoresLus[0].points);
// Affiche "Damien-999876"
```

Le `XML` est de moins en moins utilisé car très verbeux, au profit du `JSON`, du `YAML` et d'autres formats qui n'écrivent pas leurs données pareil mais reposent sur le même principe.
