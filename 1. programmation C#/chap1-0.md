# "Hello World" en C#

Écrivons notre premier programme C# qui affichera un "Hello World" à l'écran.
(Ne cherchez pas, c'est ce que tout programmeur fait en premier, c'est une coutume).

## Références

Pour aller plus loin, vérifier mes propos, avoir de l'aide sur un mot clé ou une notion :

- [Guide de la programmation C# - Microsoft](https://msdn.microsoft.com/fr-fr/library/67ef8sbd.aspx)
- [Tutoriels C# - Microsoft](https://msdn.microsoft.com/fr-fr/library/aa288436(v=vs.71).aspx)

## Généralités

Le code est un moyen pour l'humain de donner des ordres à un ordinateur.
L'ordinateur exécute ces ordres, appelés **instructions** de manière **séquentielle**, les unes après les autres.

Sauf qu'un ordinateur ne peut pas directement lire du C#. Le C# est un language avec des mots clés en anglais qui est lisible pour un humain entraîné. Et à l'inverse, la machine ne lit que des 0 et 1.

C'est pour cela qu'il faut l'aide du **compilateur** qui transforme le code C# écrit en binaire que la machine peut exécuter. Si le compilateur détecte des erreurs, il les signale au programmeur et ne peut pas créer le programme désiré.

## Syntaxe

Le C#, comme chaque langage de programmation, obéit à une syntaxe particulière qui lui est propre. Notamment :

- Le code (hors `class`) est toujours dans un bloc. Un bloc est délimité par des accolades `{ }`.
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

# Exercice

## Consigne

Afficher "Hello World" dans une console qui reste ouverte tant que l'utilisateur n'appuie pas sur une touche.

## Correction

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
