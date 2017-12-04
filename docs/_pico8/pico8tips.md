---
title: Petits trucs utiles en Pico-8
layout: default
---

* TOC
{:toc}

## Cheat sheet

Toutes les fonctions de Pico-8: [https://neko250.github.io/pico8-api/](https://neko250.github.io/pico8-api/)

## Math

### -1 ou 1 aléatoirement

```lua
r=1
if(-1+rnd(2)<0) r=-1 
```

## Physique

### Collisions entre 2 rectangles

```lua
function collide(a, b)
    if	a.x+a.w > b.x and
    a.y+a.h > b.y and
    a.x < b.x+b.w and
    a.y < b.y+b.h
    then
     return true
    end
    return false
end
```

## Inputs

### Gérer deux joueurs

Les fonctions `btn` et `btnp` ont un deuxième paramètre pour indiquer le joueur (jusqu'à 7) :

```lua
-- Bouton 1 Joueur 1
if btn(0) then

end

-- Bouton 1 Joueur 1 (identique)
if btn(0,0) then

end

-- Bouton 1 Joueur 2
if btn(0,1) then

end
```

## Effets

### Screenshake

La fonction `CAMERA` permet de faire assez simplement du screenshake. Le plus compliqué est finalement de stocker les infos de mouvement et de les mettre à jour à chaque frame.

```lua
cam={x=0,y=0,frames=0,force=0}

function _update()
	if cam.frames>0 then
		cam.frames-=1
		cam.x=(rnd(2)-1)*cam.force
		cam.y=(rnd(2)-1)*cam.force
	else
		cam.x=0
		cam.y=0
    end

    camera(cam.x,cam.y)
end

function screenshake(f,t)
	cam.force=f
	cam.frames=t
end
```

Exemple : 

```lua
if btn(0) then
    screenshake(3,5)
end
```