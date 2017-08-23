# Structures de contrôle

TODO
TODO
(Vieux copié collé)
TODO
TODO
TODO

Le code est exécuté de haut en bas, ligne par ligne.

Très rapidement, il est utile de modifier ce comportement :
- exécuter du code sous certaines **conditions**
- répéter du code grâce aux **boucles**
- réutiliser du code grâce aux **fonctions**

### Conditions

On peut indiquer qu'un bloc de code ne doit être exécuté que si une condition est remplie grâce à `if`.

`if` teste la condition et si elle est satifasfaite (`true`), le code est exécuté.

Exemples :

```csharp
// Si la touche "espace" est enfoncée
if(Input.GetKeyDown(KeyCode.Space) == true)
{
  // Sauter
}
```

```csharp
int vieJoueur = 1;
// ...
if(vieJoueur <= 0)
{
  // GameOver
}
```

```csharp
if(playerName == "Damien")
{
}
```

En complément du `if` (**si**) vient le `else` (**sinon**) qui permet de définir un bloc de code à exécuter si la condition est fausse (`false`).

```csharp
if(playerName == "Damien")
{
  // Code pour le joueur "Damien"
}
else
{
  // Code pour tous les autres joueurs
}
```

On peut même combiner le `else` avec un autre `if`.
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

Remarque :

```csharp
if(Input.GetKeyDown(KeyCode.Space) == true)
```

Est équivalent à

```csharp
if(Input.GetKeyDown(KeyCode.Space))
```

Le `== true` est implicite (on cherche à savoir si c'est vrai).

## Comparaisons

Comme les opérations, il est possible de comparer des valeurs.

| Opérateur | Nom | Exemple |
|----|----|----|
| == | égal | `4 == 4` |
| != | différent | `4 != 2` |
| < | strictement inférieur | `2 < 4` |
| <= | inférieur ou égal | `2 <= 2` |
| > | strictement supérieur | `4 > 2` |
| >= | supérieur ou égal | `4 >= 2` |

Ces comparaisons retournent une valeur **booléenne** : vrai (`true`) ou faux (`false`).

### Boucles

Il est souvent utile de répéter du code. Cela peut par exemple permettre de créer 10 ennemis à la suite avec une seule ligne de code.

A chaque fois que la boucle répète le code, on parle **d'itération**.

#### for

La boucle de base est la boucle `for` :

- Elle répète un nombre de fois précis le code
- On sait à tout moment à quelle itération on est rendu

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

D'ailleurs, un jeu vidéo est une grande boucle `while(jeu_lancé)` !

La **condition** est identique à ce que l'on peut mettre dans un `if`.

Exemples

```csharp

// Tant que le joueur appuie sur le bouton A
while(Input.GetKey(KeyCode.A) == true)
{
  // Faire danser le personnage
}
```

```csharp
while(scoresTelecharges == false)
{
  // Attendre/animer tant que les scores n'ont pas été téléchargés
}
```

Attention aux boucles infinis... si la condition n'est jamais remplie, votre programme restera bloqué pour **toujours** dans la boucle.

Seul un CTRL+ALT+SUPPR pourra l'en sortir en le quittant brutalement.

(Mais ça n'est pas grave, ça fait partie du métier !)

## Exercice

TODO

## Avancé : opérations booléennes

Les booléens sont soumis à des mathématiques particulières, l'algèbre de Boole.

C'est le fameux `1 + 1 = 1`. (vrai et vrai = vrai)

Voir [https://fr.wikipedia.org/wiki/Alg%C3%A8bre_de_Boole_(logique)](https://fr.wikipedia.org/wiki/Alg%C3%A8bre_de_Boole_(logique)) pour en savoir plus.

| Opérateur | Nom | Exemple |
|----|----|----|
| `&&` | ET | `true && false` vaut `false` |
| `||` | OU | `true && false` vaut `true` |
| `!`  | NOT | `!true` vaut `false` et `!false` vaut `true` |

Puisque nos comparaisons retournent `true` ou `false`, on va donc pouvoir combiner les comparaisons avec des opérateurs booléens.

Des exemples

```csharp
// Si le joueur n'a plus de vie ou s'il n'y a plus de temps
if(vieJoueur < 0 || tempsRestant < 0) {
  // Game Over
}
```

```csharp
// Si un bouton est enfoncé et qu'on a le droit de sauter
if(Input.GetKeyDown(KeyCode.Space) == true && peutSauter == true) {
  // Sauter
}
```
