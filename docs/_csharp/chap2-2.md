---
title: Classes et objets
layout: default
---

Assurez-vous d'avoir le maximum de cerveau disponible avant d'aborder ce chapitre. Non pas que ce soit compliqué, mais nous allons en quelques lignes passer d'un mode de programmation à un autre.

Jusqu'à présent, nous avons vu la programmation **impérative** (opérations en séquences d'instructions) et nous allons découvrir la programmation **objet**.

😱😱😱😱😱

Ce chaptire contient beaucoup de vocabulaire spécifique. Il ne s'agit pas tant d'être tatillons sur les termes que de vous permettre de retrouver de la documentation en cas d'erreur. Difficile de connaître le nom des choses instinctivement.

## Les bases de la programmation objet

Il s'agit d'abord d'une façon d'organiser son code, en **classe** (vous avez probablement remarqué le mot clé `class` dans vos fichiers C# précédents).

Une classe c'est, pour faire simple, un type avancé : ce type peut contenir des variables et des fonctions.

Par exemple, nous pouvons imaginer une classe `Personnage`

```csharp
public class Personnage
{
  public string nom;
  public string classe;
  public int vie;
}
```

On stocke dans notre Personnage toutes les données qui lui sont propres.

On peut ensuite utiliser cette classe comme un type, en utilisant le mot clé `new` :

```csharp
Personnage p1 = new Personnage();
```

Et on peut utiliser les variables du personnage avec la notation pointée :

```csharp
p1.nom = "Damien";
p1.classe = "Internationale"
p1.vie = 9999;
```

L'intérêt devrait sembler immédiat avec un exemple qui suit le précédent :

```csharp
Personnage p2 = new Personnage();
p1.nom = "Laurent";
p1.classe = "Grande"
p1.vie = 4;
```

On a donc 2 variables `Personnage` et chaque variable possède ses propres variables `nom`, `classe` et `vie`.
Chaque `Personnage` est un **objet** et chaque variable de cet objet est un **membre**.

Les membres peuvent être des objets d'autres classes, pas juste des litéraux (types de base).

En plus de variables, une classe peut contenir des fonctions, qu'on appelera **méthodes** :

```csharp
public class Personnage
{
  public string nom;
  public string classe;
  public int vie;

  public void Blesser(int degats)
  {
    vie -= degats;
  }

  public void Parler(string text)
  {
    Console.WriteLine(nom + ": " + text);
  }
}
```

```csharp
p1.Blesser(42);
p1.Parler("Ha, ça chatouille, mais pas plus !");

p2.Blesser(20);
p2.Parler("MOI, J'AI MAL");
```

## Encapsulation

En programmation objet, `public` et `private` sont des notions importantes :

- Tout ce qui est `public` doit pouvoir être modifié par n'importe quel autre bout de code à n'importe quel moment
- Ce qui est `private` ne peut être utilisé que par des méthodes de la classe, on est donc sûr que rien d'autre ne va modifier la valeur

Ces mots clés sont la **visibilité** et s'appliquent aux membres et aux méthodes.

Autrement dit, surtout quand on travaille en équipe ou quand on met du code à disposition, il ne faut rendre publique que ce qui a un intérêt à l'être. C'est l'**encapsulation**.

## Statique

Nous avons vu que chaque **objet** avait ses propres **membres**. Il est également possible d'avoir des variables ou des méthodes qui ne dépendent pas d'un objet grâce à `static`.

```csharp
public class Personnage
{
  public static string NomParDefault = "Pizza";

  public static void AfficherPersonnage(Personnage p)
  {
    Console.WriteLine("Personnage "+ p.nom);
    Console.WriteLine("- Classe : " + p.classe);
    Console.WriteLine("- Vie : " + p.vie);
  }
}
```

On peut les utilisers (s'ils sont publics !) partout par la suite :

```csharp
Personnage p3 = new Personnage();
p3.nom = Personnage.NomParDefaut;
Personnage.AfficherPersonnage(p3);

// p1, p2 et p3 partagent le même "NomParDefaut" !
```

## Héritage

Le gros morceau. On respire 2 fois profondément et on s'installe bien sur sa chaise.

Une **classe** peut hériter d'une autre **classe**. Si on reprend notre `Personnage`, on peut imaginer une classe `Magicien` qui en dérive.

```csharp
public class Magicien : Personnage {}
```

L'intérêt ? Un `Magicien` aura tout d'un personnage et pourra avoir des membres et des méthodes en plus !

```csharp
public class Magicien : Personnage
{
  public int mana;
}

public class Guerrier : Personnage
{
  public int rage;
}
```

En C#, une classe ne peut hériter que d'un **seul parent** et c'est déjà bien assez compliqué (car ce parent peut également être enfant d'une autre classe).

```csharp
Magicien m = new Magicien();
// On peut remplir ce qui vient du Personnage
m.nom = "Simon";
m.vie = 500;
m.Parler("Salut salut");
// Et ce qui est propre au magicien
m.mana = 42;
```

On peut convertir le magicen en Personnage

```csharp
Personnage p4 = m;
```

Mais l'inverse n'est pas implicite, il y a un risque de se tromper. On parle de **cast** :

```csharp
Magicien magicien = (Magicien)p4; // OK
Magicien magicienNul = (Magicien)p1;
// magicienNul vaudra `null` car p1 n'est pas Magicien
```

On peut tester le type avant le cast :

```csharp
if(p1 is Magicien)
{
  Magicien magicienNul = (Magicien)p1;
}
```

### Polymorphisme

Nous avons vu comment étendre une classe avec des nouvelles méthodes et de nouveaux membres en plus des données de son parent.

Mais il est possible de modifier, étendre ou réécrire les méthodes existantes. La condition, c'est quelles soient marquées comme `virtual` (ou `abstract` mais je n'aborderai pas cette notion ici).

Reprenons le Personnage et modifions `Blesser(int)`

```csharp
public class Personnage
{
  // ...

  public virtual void Blesser(int degats)
  {
    vie -= degats;
  }

  // ...
}
```

Dans notre Magicien, il suffit de prendre la méthode et **l'écraser** avec `override` :

```csharp
public class Magicien : Personnage
{
  public int mana;

  public override void Blesser(int degats)
  {
    Console.WriteLine("Je suis invincible !");
  }
}
```

Mais il n'est pas obligatoire de perdre totalement le comportement précédent. Avec `base` il est possible d'appeler le même code que le parent et d'ajouter d'autres lignes de code :

```csharp
public class Guerrier : Personnage
{
  public int rage;

  public override void Blesser(int degats)
  {
    base.Blesser(degats); // Appel le code de Personnage#Blesser

    rage = rage + 1;
  }
}
```

Cela permet d'utiliser une méthode de la même façon sans se préoccuper de comment les enfants la gère :

```csharp
Personnage a = new Magicien();
Personnage b = new Guerrier();

a.Blesser(42);

b.Blesser(3);

// a est invincible et b a augmenté sa rage de +1
```
