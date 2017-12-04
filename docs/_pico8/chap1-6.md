---
title: Coroutines
layout: default
---

Les coroutines permettent d'exécuter du code en parallèle de la boucle de jeu principale. Grâce à un mot clé spécifique (`yield`) on peut très facilement définir du code à exécuter sur la première frame qui suit l'appel de l'a couroutine, puis sur les frames suivantes.

Cela permet de très facilement de jouer sur les *timings* d'une actions : attendre N frames avant de faire une action, changer de sprites toutes les N secondes, etc.

## Création

Prenons par exemple une fonction qui joue un son, attend 5 frames puis affiche un message :

```lua
function routineExemple()

	sfx(0)

	yield()
	yield()
	yield()
	yield()
	yield()

	print("Coucou")

end
```

Nous avons ici une fonction assez simple, sauf pour `yield`. Ici, `yield` veut dire "fait une pause jusqu'à la prochaine frame.
En effet, une coroutine peut être exécutée sur plusieurs frames, c'est d'ailleurs sa principale force : sa capacité à être en parallèle de la boucle principale mais sur son propre timing.

A chaque `yield`, l'éxecution de la fonction est mis en pause et sera repris à la frame suivante. 

Ici on a 5 fois l'instruction, donc on attendra 5 frames avant le `print`. 

Note : une boucle `for` serait plus élégante :

```lua
-- Attend 5 frames
for i=1,5 do
	yield()
end
```

Note : la coroutine ne peut pas avoir de paramètres d'entrées. Elle a en revanche accès à toutes les variables du programme, comme les autres morceaux de code.

Mais avec juste cette déclaration de fonction, nous n'avons pas une coroutine. Pour qu'elle le devienne, il faut appeler cette fonction avec `cocreate` :

```lua
f = cocreate(routineExemple)
```

Nous avons désormais une coroutine `f` qui exécutera le code de la fonctione `routineExemple`. Remarquez l'absence de paranthèse quand on passe le nom de la fonction "modèle" : on lui donne la fonction mais on ne l'appelle pas.

La création c'est bien mais pas suffisant.

## Exécution

Il faut maintenant appeler à chaque frame `coresume` pour faire avancer l'exécution de la coroutine. Aussi, `costatus` nous indique si la coroutine est terminée ou non.

Donc si on a notre coroutine `f` :

```lua
if costatus(f) then
	coresume(f)
end
```

Une coroutine **peut** être **infinie** : cela n'est pas dérangeant tant que chaque tour de boucle infinie se termine avec un `yield`.

## Gestion simplifiée de plusieurs coroutines

Pour gérer plus simplement nos coroutines, on peut les stocker dans une collections. Il nous suffit ensuite de boucler sur cette collection à chaque frame.

```lua
coroutines={}

function _update()

	for c in all(coroutines) do
		-- Active ou terminée ?
		if(costatus(c)) then
			-- Active : on l'exécute
			coresume(c)
		else
			-- Terminée : on la supprime 
			del(coroutines,c)
		end
	end

end
```

Il faudra bien sûr penser à ajouter notre coroutines créée à la collection :

```lua
f = cocreate(routineExemple)
add(coroutines,f)
```

## Exemples

```lua
function waitAndReset() 
	-- Attend 1 sec (60 frames)
	for i=1,60 do
		yield()
	end
	balle.x = 60
	balle.y = 90
end
```

```lua
function animBall() 

	while(1) do -- inifini
		for i=1,5 do
			yield()
		end
		balle.sprite+=1
		if(balle.sprite > 3) balle.sprite = 1
	end

end
```