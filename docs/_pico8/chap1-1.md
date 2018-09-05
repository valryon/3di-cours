---
title: Instructions et variables
layout: default
---

C'est parti pour programmer un peu.

## Instructions

D'abord, quelques bases.

### La séquentialité

Le code est écrit **ligne par ligne**.

Ces lignes de code sont transformées en **instructions** compréhensibles par l'ordinateur, elles aussi executées les unes après les autres, de manière **séquentielle**.

Ainsi, écrire

```lua
  PRINT("HELLO")
  PRINT("WORLD")
```

affichera **toujours** à l'éxecution

```
HELLO
WORLD
```

![Hello world]({{site.url}}/static/content/pico8/helloworld.png)

### Syntaxe

C'est le langage **Lua** qui est utilisé dans PICO-8 dans une forme simplifié. En effet, l'éditeur ne propose qu'une partie des fonctionnalités du langage et le code est écrit en majuscule<sup>[1](#upper)</sup>, *à l'ancienne*.

Comme dans tous les langages de programmation, on retrouve :

- Des mots clés réservés, que le système reconnaît.
Exemples : `IF` `THEN` `END` `FUNCTION` etc

- Des commentaires. Il s'agit de texte libre qui aide les autres personnes sur le projet ou son soi du futur qui relit cet affreux code.
En Lua, les commentaires commencent par `--`. L'éditeur, doté de **coloration syntaxique**, devrait reconnaître que c'est un commentaire et afficher toute la ligne de manière plus discrète.

```lua
-- AUTHOR: DAMIEN MAYANCE
-- CECI EST MON SUPER JEU SECRET

PRINT("HELLO")

-- AFFICHER LA SUITE DE LA PHRASE
PRINT("WORLD")
```

Si la syntaxe contient des erreurs, le programme vous les signalera a l'éxécution.

D'autres langages, comme le C#, ont une étape intermédiaire de **compilation** pour traduire le code écrit en langage machine. Cela permet de détecter les erreurs plus tôt.

Mais le Lua dans PICO-8 n'a pas cette option, le programme lit les lignes au fur et à mesure, on dit qu'il les **inteprète**.

### Exercice

1. Afficher du texte à l'écran
2. Modifier la position du texte à l'écran
3. Modifier la couleur du texte à l'écran

#### Correction

```lua
PRINT("ici")
PRINT("ou là ?", 50,100)
PRINT("c'est quand même super, 20,30, 8)
```

# Les variables

Il va très vite falloir stocker et manipuler des informations (des chiffres, du texte, des noms, etc).
Pour cela, il nous faut des **variables**.

Elles permettent d'utiliser très facilement **la RAM** (les petites barrettes dans vos machines) qui est un stockage **volatile**, c'est à dire que ce qui est dedans est perdu quand le programme (ou la machine) est éteint(e).

## Qu'est-ce donc

Une **variable** c'est un emplacement, une "boîte", en mémoire dans laquelle on peut ranger une information (points de vie, nom du joueur, niveau, etc). Le contenu peut *varier*, c'est à dire changer au cours de l'exécution du programme.

Concrètement, ça ressemble à ça :

```lua
pseudo="damien" -- Une variable pour un pseudo
x=64
y=64            -- Deux variables, x et y, pour une position à l'écran
wpn=0           -- Une variable pour l'arme utilisée
```

### Attributs d'une variable

Une **variable** a toujours :

1. un **type**

On doit indiquer à l'ordinateur si on stocke un nombre, un texte ou tout autre chose. Car au final, l'ordinateur stocke du binaire et quelque chose comme `01011001` peut signifier des choses très différentes selon le type.

En Lua, le type est *implicite*, c'est à dire que vous n'avez pas à l'indiquer c'est l'ordinateur qui se débrouille. Mais vous risquez néanmoins d'avoir des surprises si vous vous mettez à stocker un texte au lieu des coordonnées du joueur à l'écran.

Dans notre exemple, `pseudo` est une **chaîne de caractère** (**string** en anglais) et les autres sont des **nombres** (**numbers**).

En Lua, les types sont assez simples. On ne fait pas exemple pas la différence entre les nombres entiers et les nombres à virgules.

| type | nom FR | exemples de valeurs |
|------|--------|----------------------------------------|
| **boolean** | booléen | `false` (faux, 0) `true` (vrai, 1)  |
| **number** | nombre | `0`, `1`, `-78.8`, `42.66` |
| **string** | chaîne de caractère | `"damien"`, `"I:0145"`, `"Je suis un texte."` |
| **table** | tableau/liste | `{"pizza", "burger", "raclette"}` |

2. un **nom**

Une variable qui n'est pas utilisée n'a pas d'intérêt. Pour l'utiliser, il faut la nommer (`pseudo`, `x`, etc).
Le nom permet au programmeur de savoir à quoi elle sert.
Le point bonne pratique : même si on peut nommer toutes ses variables `a` `b` `c` `d`, on essayera en pratique de leur donner une signification claire rien qu'avec le nommage (comme dans l'exemple). Si on reprend l'analogie de la variable étant une boîte, lorsque vous rangez vos affaire il est plus pratique et confortable si la boîte qui contient vos ustensiles de cuisines ait le mot "cuisine" ecrit dessus.

3. une **valeur**

Une variable a toujours une valeur. En Lua, la valeur par défaut est `NIL`.
Sinon, la variable aura la dernière valeur qu'on lui a donné.

Une variable n'a **pas d'historique**. Si vous faites

```lua
x=0
x=42
```

alors `x` aura comme valeur `42`. Le `0` est définitivement perdu.

### Opération sur une variable

1. La **déclaration** permet d'initialiser la variable.

```lua
x=42
```

2. On peut ensuite **lire** sa valeur

```lua
PRINT(x)
y=x+5
```

3. Et surtout on peut **écrire** et changer sa valeur. On parle alors d'**affectation** :

```lua
x=42
PRINT(x) -- 42
x = x + 5
PRINT(x) -- 47
```
A noter qu'il est possible de lire et de modifier le contenu d'une variable sur la même ligne. Mais uniquement son **contenu** peut changer : son nom ne pourra pas etre modifié après sa création.

Les opérations mathématiques sont permises et mêmes encouragées :

| Opérateur | Nom | Exemple |
|----|----|----|
| + | addition | `n = 5 + 7`|
| - | soustraction | `n = 5 - 7`|
| * | multiplication | `n = 5 * 7`|
| / | division | `n = 1 / 4`|
| % | modulo | `n = 1 % 2`|
| cos | cosinus | `n = cos(3.14)`|
| sin | sinus | `n = sin(3.14)`|
| abs | valeur absolue | `n = abs(-57) -- n vaut 57`|
| flr | arrondi à l'inférieur (floor) | `n = flr(4.9) -- n vaut 4`|

Et [beaucoup d'autres](https://neko250.github.io/pico8-api/#math).

### Comparaison de valeurs

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

# Exercices

1. Afficher du texte
2. Afficher du texte à des coordonnées précises
3. Mettre ces coordonnées dans des variables `x` et `y`
4. Afficher un autre texte légèrement en dessous du premier
5. Afficher un autre texte légèrement en dessous du second
6. Modifier uniquement `x` et `y` : le texte doit bouger en conséquence

![Faim]({{site.url}}/static/content/pico8/faim.png)

## Correction

```lua
CLS()
x=18
y=21
PRINT("il fait faim",x,y)
y=y+8
PRINT("mais on est encore loin",x,y)
y=y+8
PRINT("de l'heure du repas !",x,y)
```
<a name="upper">1</a>: que le code soit rédigé en majuscule ou minuscule il apparaitra en majuscules dans PICO.
