---
title: Structures de contrôle
layout: default
---

Le code est exécuté de haut en bas, ligne par ligne.

Très rapidement, il est utile de modifier ce comportement :
- exécuter du code sous certaines **conditions**
- répéter du code grâce aux **boucles**
- réutiliser du code grâce aux **fonctions**

## Conditions

On peut indiquer qu'un bloc de code ne doit être exécuté que si une condition est remplie grâce à `if`. `if` teste la condition et si elle est satifasfaite (`true`), le code est exécuté.

En Lua, la condition est suivie de `THEN` et le bloc de code se termine par `END`.

Exemples :

```lua
vies=1
IF (vies == 0) THEN
 PRINT("GAME OVER")
END
-- N'affiche rien
```

Ce bout de code n'affiche rien, car on regarde si `vies` vaut 0, mais il vaut 1.

En complément du `if` (**si**) vient le `else` (**sinon**) qui permet de définir un bloc de code à exécuter si la condition est fausse (`false`).

```lua
vies=1
IF (vies == 0) THEN
 PRINT("GAME OVER")
ELSE
 PRINT("Tout va bien")
END
-- Affiche "Tout va bien"
```

On peut même combiner le `else` avec un autre `if`.
L'intérêt ? La condition n'est testée que **si** et **seulement si** le premier `if` est faux.

```lua
vies=1
IF (vies == 0) THEN
 PRINT("GAME OVER")
ELSEIF (vies == 1) THEN
  PRINT("C'est limite")
ELSE
 PRINT("Tout va bien")
END
-- Affiche "c'est limite"
```

Remarque :

```lua
B=FALSE
IF(B == TRUE) THEN
```

Est équivalent à

```lua
B=FALSE
IF(B) THEN
```

Le `== TRUE` est implicite (on cherche toujours à savoir si c'est vrai).

### Comparaisons

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

### Exercice : dessin d'un carré

1. Afficher un point à l'écran avec `PSET(X,Y,COLOR)`
2. Afficher un carré de plusieurs points
2. Ajouter la fonction `_DRAW()` spécifique à PICO-8 qui est exécutée en boucle

```lua
FUNCTION _DRAW()
  CLS() -- Nettoie l'écran

  -- Votre code

END
```

3. Ajouter un `IF` permettant de savoir si le joueur appuie sur le bouton 4 (`BTN(4)` touche C du clavier) et n'afficher le pixel que si la touche est appuyée

![Exo]({{site.url}}/static/content/pico8/exo12_1.gif)

#### Correction

```lua
FUNCTION _DRAW()
  CLS()

  IF BTN(4) THEN
	  PSET(63,63,8)
	  PSET(64,63,8)
	  PSET(63,64,8)
	  PSET(64,64,8)
	 END
END
```

### Exercice : déplacement d'un carré

1. Afficher un carré à l'écran comme précédemment
2. Ajouter des variables `x` et `y` pour définir sa position à l'écran

Dans une fonction `_UPDATE()`, similaire à `DRAW()` mais pour la logique et les inputs :

3. Utiliser des `if` et `BTN(n)` (n étant un nombre entre 0 et 5) pour détecter l'appui sur les flèches
4. Modifier la valeur de `x` et `y` dans ce `if` pour faire déplacer le carré à l'écran !

#### Correction

```lua
X=64
Y=64

FUNCTION _UPDATE()
  IF BTN(0) THEN X=X-1 END
  IF BTN(1) THEN X=X+1 END
  IF BTN(2) THEN Y=Y-1 END
  IF BTN(3) THEN Y=Y+1 END
END

FUNCTION _DRAW()
  CLS()

  PSET(x-1,y-1,8)
  PSET(x,y-1,8)
  PSET(x-1,y,8)
  PSET(x,y,8)
END
```

## Boucles

Il est souvent utile de répéter du code. Cela peut par exemple permettre de créer 10 ennemis à la suite avec une seule ligne de code.

A chaque fois que la boucle répète le code, on parle **d'itération**.

### for

La boucle de base est la boucle `for` :

- Elle répète un nombre de fois précis le code
- On sait à tout moment à quelle itération on est rendu

Syntaxe :

```lua
FOR i=0,10 DO
  -- Code à répéter
  PRINT(i)
END
```

1. `i=0` : la boucle `for` a besoin d'un **indice** pour stocker la où elle est rendue. Par convention l'indice est appelé `i`, sans réelle raison.
C'est aussi le moment où on lui donne la valeur de départ, ici `0`.

2. `,10` indique jusqu'à quel chiffre la boucle doit continuer. Ici, jusqu'à `10`.

Et à chaque itération de la boucle, le système ajoute `1` à `i` jusqu'à ce que `i` soit égal à `10`.

Si la valeur de départ est plus grande que celle d'arrivée, l'ordinateur ne va pas exploser : le code de la boucle ne sera juste jamais exécuté.

#### Exercices

##### La ligne

1. Dans une fonction `_DRAW` comme l'exercice précédent, afficher un pixel à l'écran en 0,0
2. En utilisant une boucle `for`, afficher 10 pixels à l'écran
3. Afficher cette ligne de pixel à un autre endroit de l'écran (54,64 par exemple)

###### Correction

```lua
FUNCTION _DRAW()
  CLS()

  FOR i=0,10 do
		PSET(54+i,64,8)
	END
END
```

##### Le carré

1. Reprendre l'affichage de ligne comme précédemment
2. Utiliser une AUTRE boucle `for` pour afficher 10 pixels de haut à chaque colonne

###### Correction

```lua
FUNCTION _DRAW()
  CLS()

  FOR i=0,10 do
    FOR j=0,10 do
      PSET(54+i,54+j,8)
    END
	END
END
```

##### Le carré vide

1. Reprendre l'affichage de carré comme précédemment
2. En utilisant un ou plusieurs `if`, n'afficher que les bords du carré (le milieu doit être vide)

###### Correction

```lua
FUNCTION _DRAW()
  CLS()

  FOR i=0,10 do
    FOR j=0,10 do
      IF (i==0)  THEN	PSET(54+i,54+j,8) END
      IF (j==0)  THEN	PSET(54+i,54+j,8) END
      IF (i==10) THEN	PSET(54+i,54+j,8) END
      IF (j==0)  THEN	PSET(54+i,54+j,8) END
    END
	END
END
```

Évidemment, c'est mieux avec un seul `if` :

```lua
FUNCTION _DRAW()
  CLS()

  FOR i=0,10 do
    FOR j=0,10 do
      IF (i==0 or j==0 or i==10 or j==10)  THEN
        PSET(54+i,54+j,8)
      END
    END
	END
END
```

#### while

L'autre boucle très utile est `while`. Littéralement "répéter tant que".

Syntaxe :

```lua
WHILE (condition) DO
  -- Code à répéter
END
```

La différence c'est qu'ici le nombre d'itérations n'est pas **connu**. Et il est potentiellement **infini**.

D'ailleurs, un jeu vidéo est une grande boucle `WHILE(jeu_lancé)` !

La **condition** est identique à ce que l'on peut mettre dans un `if`.

Exemple : reproduire une boucle for

```lua
i=0
WHILE(i<=10) DO
	PRINT(i)
	i=i+1
END
```

Attention aux boucles infinis... si la condition n'est jamais remplie, votre programme restera bloqué pour **toujours** dans la boucle.
`ESC` sur PICO-8 vous permet de l'arrêter brutalement, mais pour d'autres programmes (faits en C# par ex) seul un CTRL+ALT+SUPPR pourra l'en sortir en le quittant brutalement.

(Mais ça n'est pas grave, ça fait partie du métier !)

## Aparté : la boucle de jeu

Un jeu vidéo est en général composé d'une grande boucle infinie.
A chaque itération, on parle de **frame**.

A chaque frame :
- On lit les actions du joueur (clavier, manette) : les **inputs**
- On met à jour le monde du jeu (physique, collision, destructions, points, etc) : **update**
- On construit l'image à afficher : **draw**
- L'image est envoyée à la carte graphique puis à l'écran

En PICO-8, vous êtes dans une boucle infinie sans le savoir :

```lua
_INIT()
WHILE(TRUE) DO
  _UPDATE()
  _DRAW()
END
```

Cette notion de frame est **capitale** dans un jeu vidéo. Si une frame met trop de temps à s'exécuter (car trop de code, trop de calcul), la prochaine frame arrivera elle aussi en retard.

On parle de **FPS** pour *frames par seconds*. Un jeu tourne typiquement à 30 FPS (consoles, PICO-8) ou à 60 FPS (PC). En dessous de 30, le jeu ne semble pas fluide.

## Avancé : opérations booléennes

Les booléens sont soumis à des mathématiques particulières, l'algèbre de Boole.

C'est le fameux `1 + 1 = 1`. (vrai et vrai = vrai)

Voir [https://fr.wikipedia.org/wiki/Alg%C3%A8bre_de_Boole_(logique)](https://fr.wikipedia.org/wiki/Alg%C3%A8bre_de_Boole_(logique)) pour en savoir plus.

| Opérateur | Nom | Exemple |
|----|----|----|
| `AND` | ET | `true OR false` vaut `false` |
| `OR` | OU | `true AND false` vaut `true` |
| `NOT`  | NOT | `NOT true` vaut `false` et `NOT false` vaut `true` |

Puisque nos comparaisons retournent `true` ou `false`, on va donc pouvoir combiner les comparaisons avec des opérateurs booléens.
