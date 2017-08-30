---
title: Les fonctions
layout: default
---

Vous avez déjà vu le mot clé `FUNCTION` dans les chapitres précédents. Nous allons nous intéresser à ce mécanisme de base qui permet de réutiliser intelligemment du code.

Une fonction c'est un outil de programmation que l'on peut utiliser à volonté. La puissance vient du fait que l'on aussi peut faire ses propres fonctions, donc ses propres outils adaptés à ses besoins, ou on peut utiliser les fonctions des autres (moteurs de jeux, code trouvé sur Internet, etc).

Vous avez déjà utilisé plusieurs fonctions propres à PICO-8: `PRINT`, `BTN`, `PSET`, `CLS`, etc. Ce sont en fait des bouts de code écrits et mis à disposition par le créateur de la console pour nous simplifier la tâche.

## Caractéristiques d'une fonction

1. Un **nom** : comme les variables, il faut nommer les fonctions pour pouvoir les utiliser. Et toujours comme les variables, le nom est pour vous, humain, et pas pour la machine qui s'en fiche.

2. Une **sortie** : une fonction peut - c'est **optionnelle** - **retourner** une valeur, c'est à dire que le résultat peut être stocké dans une variable. Par défaut, une fonction ne retourne rien en Lua.

3. Des **entrées** : une fonction peut avoir 0 ou plusieurs **paramètres**. Cela permet de rendre notre outil plus polyvalent.

Enfin, quand on utilise une fonction, on parle d'**appel**. C'est le moment où on lui donne la valeur des paramètres.

Des exemples concrets :

```lua
-- Affiche coucou
FUNCTION COUCOU()
  PRINT("coucou")
END

COUCOU()
COUCOU()
```

```lua
-- Affiche coucou à une position donnée
FUNCTION COUCOU(x,y)
  PRINT("coucou",x,y)
END

COUCOU(0,10)
COUCOU(50,50)
```

```lua
-- Affiche un texte à une position donnée
FUNCTION TXT(text, x,y)
  PRINT(text,x,y)
END

TXT("raclette",0,10)
TXT("burger",50,50)
```

```lua
-- Additionne a et b et renvoie le résultat
FUNCTION ADD(a,b)
  RETURN a+b
END

n=ADD(3,8)
PRINT(n) -- 11
```

Note : en Lua, la fonction doit être déclarée avant d'être utilisée.

*Une fonction, c'est un peu comme Yoshi. Il mange des trucs, ça transite là où on veut pas trop savoir et il pond des oeufs. `oeuf = Yoshi(truc)`.*

## Exercice : dessiner une ligne

1. Écrire la fonction `ligne` qui dessine une ligne de 10x1 pixels à l'écran en x et y.
2. Ajouter en paramètre la largeur `w` de la ligne
3. Ajouter en paramètre la hauteur `h` de la ligne et modifier la fonction pour prendre en compte l'épaisseur de la ligne

### Corrections

1.

```lua
FUNCTION ligne(x,y,w)
  FOR i=0,10 do
    PSET(x+i,y,8)
  END
END

ligne(64,64)
```

2.

```lua
FUNCTION ligne(x,y,w)
  FOR i=0,w do
    PSET(x+i,y,8)
  END
END

ligne(64,64,30)
```

3.

```lua
FUNCTION ligne(x,y,w,h)
  FOR i=0,w do
    FOR j=0,h do
      PSET(x+i,y+j,8)
    END
  END
END

ligne(64,64,30,12)
```

Bravo, vous avez grosso modo réécrit `rect` !

## Exercice : CLS

1. Écrire la fonction `colorscreen` : une fonction qui peint dans une couleur donnée tous les pixels de 0 à 128 en x et y.

### Corrections

```lua
FUNCTION colorscreen(c)

	FOR x=0,128 DO
		FOR y=0,128 DO
			PSET(x,y,c)
		END
	END

END

-- Utilisation
CLS()
colorscreen(8)
```

## Exercice : génération d'un fond étoilé

1. Écrire la fonction `drawstar(x,y,col)` qui dessine une croix de pixels `+` à l'écran aux coordonnées `x` et `y` données et dans la couleur `col`
2. Utiliser cette fonction plusieurs fois dans `_DRAW()`

```lua
function drawstar(x,y,col)
	-- dessine un +
	pset(x,y,col)
	pset(x,y-1,col)
	pset(x,y+1,col)
	pset(x+1,y,col)
	pset(x-1,y,col)
end

function _draw()
	cls()
	drawstar(64,64,7)
	drawstar(32,50,7)
	drawstar(78,18,7)
end
```

3. Avec deux boucles `for` (une pour x, une pour y), remplir l'écran d'étoiles.
Pour ne pas avoir un écran d'une seule et même couleur, ajoutez une condition : n'afficher une étoile que quand x et y sont modulos 4 `x % 4 == 0 AND y % 4 == 0`

```lua
function drawstar(x,y,col)
	-- dessine un +
	pset(x,y,col)
	pset(x,y-1,col)
	pset(x,y+1,col)
	pset(x+1,y,col)
	pset(x-1,y,col)
end

cls()

for x=1,128 do
	for y=1,128 do
		-- tous les 4 pixels
		if x%4==0 and y%4==0 then
			-- affiche une etoile
			drawstar(x,y,7)
		end
	end
end
```

C'est rigolo mais pas très naturel.

4. Modifiez la condition pour n'afficher une étoile que si un nombre aléatoire entre 0 et 1 (obtenu avec `RND(1)`) est plus grand que 0.99.

```lua
function drawstar(x,y,col)
	-- dessine un +
	pset(x,y,col)
	pset(x,y-1,col)
	pset(x,y+1,col)
	pset(x+1,y,col)
	pset(x-1,y,col)
end

cls()

for x=1,128 do
	for y=1,128 do

		if rnd(1)>0.99 then
			drawstar(x,y,7)
		end
	end
end
```

5. Déplacer le code d'affichage du fond étoilé dans une fonction `drawstarground` qui prend en paramètre une couleur `col`

6. Appeler plusieurs fois cette fonction avec des couleurs différentes. Rappel, les couleurs :

![Couleurs](https://neko250.github.io/pico8-api/img/colors.png)

7. Ajoutez un paramètre `t` (comme *threshold*) pour définir le seuil du `RND` à dépasser (notre `0.99`).

8. Modifier les appels pour avoir des décors plus ou moins fournis selon la profondeur et ajouter de la couleur

![Résultat]({{site.url}}/static/content/pico8/starground.png)

```lua
-- dessine un +
function drawstar(x,y,col)
	pset(x,y,col)
	pset(x,y-1,col)
	pset(x,y+1,col)
	pset(x+1,y,col)
	pset(x-1,y,col)
end

-- dessine un fond etoile
function drawstarground(col,t)
	for x=1,128 do
		for y=1,128 do

			if rnd(1)>t then
				drawstar(x,y,col)
			end
		end
	end
end

-- utilisation
cls()
drawstarground(5,0.99)
drawstarground(6,0.995)
drawstarground(7,0.9975)
drawstarground(8,0.999)
drawstarground(9,0.999)
```
