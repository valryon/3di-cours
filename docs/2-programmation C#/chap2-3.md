# Les fonctions

TODO
TODO
(Vieux copié collé)
TODO
TODO
TODO

### Fonctions

Il devient vite très utile de découper notre code en petits morceaux.

Il est également souvent utile de réutiliser du code, or le copier/coller est une source infinie de bugs et de lourdeur.

D'où l'intérêt des **fonctions**.

Une fonction est un morceau de code qui peut être utilisé ailleurs et plusieurs fois.

C# et Unity3D fournissent **énormément** de fonctions (`Input.GetKeyDown`, `AudioSource.PlayClipAtPoint`, `Instantiate`, etc).

Pour définir une fonction, il faut :

- un nom
- des paramètres d'entrées
- un type de retour (sortie)

Rappelez-vous de vos cours de maths :

```
y = f(x)
```

Exemples

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

Une fonction, comme une variable, doit avoir un nom unique qui si possible explique à quoi elle sert.

Les **entrées** sont des variables qui doivent être fournies pour pouvoir utiliser la fonction. Une fonction peut avoir entre 0 et une dizaine de paramètres (rarement plus).

La **sortie** est la valeur qui est **retournée** par la fonction à la fin de son code. Comme une variable, il faut indiquer le type de cette valeur au programme.

- `void` est un type particulier qui signifie "pas de valeur"
- tous les autres types (`int`, `GameObject`, etc) peuvent être utilisés
- si un type de retour non `void` est précisé, le compilateur obligera à avoir un `return valeur` ou `return variable` à la fin de la fonction.

On parle ensuite **d'appel** de la fonction quand on l'utilise.

Exemples d'appels :

```csharp
  int a = Puissance2(2);
  int b = Puissance2(4);
  string joueur1 = GetPlayerName(0, "windows");
  string joueur2 = GetPlayerName(1, "macOS");
```

## Exercice

TODO
