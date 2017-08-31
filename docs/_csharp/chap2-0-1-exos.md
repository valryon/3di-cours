---
title: Exercices de programmation C#
layout: default
---

## Fonctions d'une calculatrice

1. Écrire la fonction `Add(a,b)` qui fait l'addition de `a` et `b` et retourne le résultat
2. Écrire la fonction `Mul(a,b)` qui fait la multiplication de `a` et `b` et retourne le résultat

3. Division
  - Écrire la fonction `Div(a,b)` qui fait la division de `a` et `b` et retourne le résultat.
  - Tester la division quand `a` vaut 0 puis quand `b` vaut 0
  - Gérer le cas où il y a une erreur avec un 0

### Corrections

1. Addition

```csharp
static int Add(int a, int b)
{
  return a + b;
}

// Usage:
// int r = Add(3,5);
```

2. Multiplication

```csharp
static int Mul(int a, int b)
{
  return a * b;
}

// Usage:
// int r = Mul(3,5);
```

3. Division

```csharp
static int Div(int a, int b)
{
  if(b == 0)
  {
    return 0;
  }
  return a / b;
}

// Usage:
// int r = Div(3,5);
```

## Quel types pour quels variables ?

1. Un interrupteur basique pour la lumière d'une pièce
2. Une approximation de valeur de Pi
3. Le nombre d'élèves dans une classe
4. Un nom et prénom
5. Le temps d'un sportif à une course olympique (en millisecondes)
6. Le solde de votre compte en banque
7. Le nombre d'onglets ouverts sur votre navigateur web
8. Le titre d'une chanson
9. Le résultat (gagné/perdu) à une épreuve
10. Les scores de Steredenn

## Résultats d'exécution et code avec erreurs

1. Suite à l'exécution du code ci-dessous, quelle sera la valeur de `nombre` ?

```csharp
int nombre = 42;

for (int i = 0; i < 13; i++)
{
  nombre = nombre + i;
}
```

2. Suite à l'exécution du code ci-dessous, quelles seront les valeurs de `r1` et de `r2` ?

```csharp
private static string FonctionMystere(string a, string b)
{
  return b + a;
}

//...

string r1 = FonctionMystere("JOUR", "BON");
string r2 = FonctionMystere(r1, " ! ");
```

3. Le code ci-dessous compile-t-il ? Si non, pourquoi ?

```csharp
int a = 1
a = a + " Steredenn";
```

4. Le code ci-dessous compile-t-il ?
  - Si oui, quelle est la valeur de `a` ?
  - Si non, pourquoi ?

```csharp
int a = 1;
a = b * 3;
int b = 15;
```  

## Plus ou moins

Créons un petit jeu simple et complet en ligne de commande : le plus ou moins. L'ordinateur choisit un chiffre et le joueur doit le deviner. S'il se trompe, l'ordinateur indique si le chiffre à trouver est plus petit ou plus grand que ce qui a été entré.

### Aide

- Récupérer un nombre tapé au clavier :

```csharp
// Fonction pour lire au clavier un chiffre (plante sur des lettres)
static int LireEntier()
{
  Console.WriteLine("Entrez un nombre :");
  return int.Parse(Console.ReadLine());
}
```

- Choisir un nombre aléatoirement :

```csharp
// Définir un nombre à trouver entre [0, 100[
Random random = new Random();
int nombre = random.Next(0, 100);
```

### Étapes

1. Utiliser le random pour choisir un nombre aléatoirement. L'afficher à l'écran pour aider à la suite (on le cachera dans le jeu final).
2. Après cela, utiliser la fonction `LireEntier` pour récupérer un nombre tapé au clavier par le joueur
3. Comparer le nombre du joueur avec le nombre de l'ordinateur et afficher en conséquence s'il est plus petit, plus grand ou égal
4. En utilisant une boucle `while`, faites en sorte que le joueur puisse rejouer autant de fois que nécessaire jusqu'à ce qu'il trouve

### Bonus

5. Afficher au joueur "Perdu !" s'il dépasse un certain nombre d'essais (5 par exemple). Le joueur ne doit plus pouvoir saisir d'autres chiffres
6. Gérer les cas où le joueur tape n'importe quoi

### Correction

```csharp
class Program
  {
    static void Main(string[] args)
    {
      // Définir un nombre à trouver entre [0, 100[
      Random random = new Random();
      int chiffreADeviner = random.Next(0, 100);
      // Console.WriteLine(chiffreADeviner); // TRICHE

      bool trouvé = false;
      int essais = 5;

      while (trouvé == false && essais > 0)
      {
        Console.WriteLine("Il reste " + essais + " essais");

        // Lire nombre au clavier
        int nombre = LireEntier();

        // Comparer chiffreADeviner et nombre
        if (chiffreADeviner < nombre)
        {
          Console.WriteLine("Le nombre à trouver est plus petit !");
          essais = essais - 1;
        }
        else if (chiffreADeviner > nombre)
        {
          Console.WriteLine("Le nombre à trouver est plus grand !");
          essais = essais - 1;
        }
        else
        {
          trouvé = true;
        }
      }

      if (essais == 0)
      {
        Console.WriteLine("Plus d'essais :( La réponse était " + chiffreADeviner);
      }
      else if (trouvé)
      {
        Console.WriteLine("Trouvé !");
      }

      Console.ReadLine();
    }

    // Fonction pour lire au clavier un chiffre (plante sur des lettres)
    static int LireEntier()
    {
      Console.WriteLine("Entrez un nombre :");
      try
      {
        return int.Parse(Console.ReadLine());
      }
      catch(Exception e)
      {
        return -1; // Valeur arbitraire en cas d'erreur
      }
    }
  }
```

## Blackjack simplifié

Le but de l’exercice est de coder en C# un mini-jeu de cartes contre l’ordinateur.

Déroulement d’une partie :

1. Un croupier (l’ordinateur) tire entre 1 carte face cachée
2. Le joueur peut ensuite à son tour tirer entre 1 carte face visible
3. On retourne en 1. jusqu'à ce que le joueur ait tiré 3 cartes ou qu’il arrête de piocher
4. On compare les points et on affiche le vainqueur (ou ex aequo)
5. Bonus : gérer correctement le fait qu'un joueur puisse taper autre chose que "n"/"o"

### Aide

Ici nous n'allons pas représenter ou gérer les cartes. On simplifiera l'exercice ainsi :

- C’est une application console (pas d’interface)
- Pas de figures. Uniquement des chiffres entre 1 et 10
- Tirer une carte = Choisir un nombre au hasard entre 1 et 10 :

```csharp
// Au début du programme
Random random = new Random();

// Obtenir un nouveau nombre entre 1 et 10 inclus :
int nombre = random.Next(1,11);
```

- Face cachée = on n’affiche pas le résultat au joueur dans la console, et inversement face visible
- On ne gardera pas en mémoire la liste des "cartes" tirées, on gardera uniquement le total des nombres.

Exemple : le joueur tire la carte 1 puis la carte 6 -> on stocke 1 puis 7 dans une variable.

Pour continuer/arrêter, le joueur devra taper O ("Oui" -> "Je continue") ou N ("Non" -> "J'arrête") dans la console :

```csharp
bool tirerCarteJoueur = true;
Console.WriteLine("Tirer une nouvelle carte ? (O pour oui, N pour non)");
string lettre = Console.ReadLine();
if (lettre.ToLower().StartsWith("o"))
{
  tirerCarteJoueur = true;
}
else
{
  tirerCarteJoueur = false;
}
```

### Correction

```csharp
using System;

namespace BlackJack
{
  class Program
  {
    static void Main(string[] args)
    {
      const int CARTES_MAX = 3;

      Console.WriteLine("Black Jack");
      Console.WriteLine();

      Random random = new Random();

      int joueur = 0;
      int croupier = 0;
      int cartes = 0;
      bool continuer = true;

      while (continuer && cartes < CARTES_MAX)
      {
        cartes++;

        // On fait piocher le croupier
        croupier += random.Next(1, 11);

        // Première carte : pas besoin de demander
        // Ensuite : seulement si le joueur tape "o" / "O"
        bool tirerCarteJoueur = true;
        if (cartes > 1)
        {
          Console.WriteLine("Tirer une nouvelle carte ? (O pour oui, N pour non)");
          string lettre = Console.ReadLine();
          if (lettre.ToLower().StartsWith("o"))
          {
            tirerCarteJoueur = true;
          }
          else
          {
            tirerCarteJoueur = false;
            continuer = false;
          }
        }

        if (tirerCarteJoueur)
        {
          int carteJoueur = random.Next(1, 12);
          joueur += carteJoueur;

          Console.WriteLine("Le joueur pioche un " + carteJoueur + ". Total joueur=" + joueur);
        }

        Console.WriteLine();
      }

      Console.WriteLine("Croupier=" + croupier + " Joueur=" + joueur);

      if (joueur > croupier) Console.WriteLine("Le joueur gagne !");
      else if (croupier > joueur) Console.WriteLine("Le joueur a perdu...");
      else Console.WriteLine("Ex aequo!");

      Console.ReadLine();
    }
  }
}

```
