---
title: Amusons-nous avec PICO-8
layout: default
---

## Sprites

1. Dessiner un sprite dans le 2e onglet
2. Dans `_DRAW()`
	- `SPR(n, x, y, [w, h], [flip_x], [flip_y])` pour afficher le sprite `n` (position dans la spritesheet) en x,y à la taille w*h
3. Besoin d'animations ? Il faut changer le numéro de sprite par le suivant.

```lua
frame=1

function _UPDATE()
	frame=frame+1
	if frame>2 then frame=1 end
end

function _DRAW()
	cls()
	spr(frame,64,64)
end
```

## Map

1. Dessiner des sprites dans le 2e onglet
2. Placer les sprites sur la map dans le 3e onglet
3. Dans `_DRAW()`
	- `MAP(x,y,0,0,w,h)` pour afficher la carte entre (x,y,w,h)

```lua
cam={x=0,y=0,w=16,h=32}

function _DRAW()
	cls()
	map(cam.x,cam.y,0,0,cam.w,cam.h)
end
```

## Collisions

### Avec la map

1. Dessiner des sprites dans le 2e onglet. Un bloc par exemple.
2. Affecter un "flag" à ce sprite, typiquement le premier.
3. Utiliser ce sprite sur la map
4. Dans `_UPDATE()` :
	- Récupérer le sprite utilisé dans la map avec `mget(x,y)`
	- Récupérer si un flag est utilisé sur un sprite avec `fget(sprite, flag)`

### Avec un autre élément

Pas d'astuces faciles... quelques pistes :

1. tester si deux carrés se chevauchent
2. tester si les pixels avant/après notre sprite sont noirs/vides ou non

Une fonction pratique :

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

Exemple :

```lua
bullet={x=0,y=0,w=3,h=3}
spaceship{x=0,y=0,w=8,h=8}

if collide(spaceship,bullet) then
	-- boom
end
```

Une version avec hitbox:

```lua
function collide(obj, other)
    if
        other.pos.x+other.hitbox.x+other.hitbox.w > obj.pos.x+obj.hitbox.x and
        other.pos.y+other.hitbox.y+other.hitbox.h > obj.pos.y+obj.hitbox.y and
        other.pos.x+other.hitbox.x < obj.pos.x+obj.hitbox.x+obj.hitbox.w and
        other.pos.y+other.hitbox.y < obj.pos.y+obj.hitbox.y+obj.hitbox.h
    then
        return true
    end
end
```

Exemple :

```lua
bullet.pos={x=10,y=10}
bullet.hitbox={x=0,y=0,w=3,h=3}

spaceship.pos={x=15,y=15}
spaceship.hitbox={x=0,y=0,w=10,h=5}

if collide(spaceship,bullet) then
	-- boom
end
```

--


Moins de théorie, plus de pratique ! Voici des exercices divers et variés.

## Exercice : tunnel épileptique

Premier effet visuel facile et inutile :

![Tunnel]({{site.url}}/static/content/pico8/tunnel.gif)

1. Dessiner un cercle avec `circfill(x,y,rayon,color)`
2. Le rayon du cercle doit devenir une variable `r`. Augmenter cette variable à chaque frame dans `_UPDATE()` et dessinez le cercle dans `_DRAW()`
3. Au lieu d'avoir un seul rayon, créons un tableau de rayons de cercle. Chaque rayon doit être augmenter et dessiner à chaque frame.
Ajouter 3-4 rayons (et donc cercle) pour tester.
4. Créez automatiquement des cercles régulièrement (par exemple toutes les 30 frames). On peut obtenir une couleur aléatoire avec `flr(rnd(15))`
5. Supprimez automatiquement des cercles (par exemple quand le rayon d'un cercle est > 100 ou quand on a plus de 5 crecles à l'écran)

### Correction

```lua
circles={}

function addcircle()
	add(circles, {
		r=1,
		col=flr(rnd(15))
	})
end

function _init()
	addcircle()
end

function _update()
	for c in all(circles) do
		c.r=c.r+1
		if c.r==42 then
			addcircle()
		end
	end

	if #circles>4 then
		del(circles, circles[1])
	end
end

function _draw()
	cls()
	for c in all(circles) do
		circfill(64,64,c.r,c.col)
	end
end
```

## Exercice : exploser un hamburger

A un moment quelqu'un me dira que j'ai un problème avec la bouffe.

En attendant, un effet visuel sympa :

![Goodbye Hamburger]({{site.url}}/static/content/pico8/hamburger.gif)

1. Dessiner un hamburger à l'écran. Pour cela, on va stocker dans une variable la position `x`,`y` et la couleur de chaque pixel du hamburger.
2. On utilisera ensuite une boucle `for` dans `_DRAW()` pour afficher en une seule ligne chaque pixel du hamburger.
3. Ajouter un booléen `exploding` qui commence à `false`
4. Ajouter la détection de l'appui sur un bouton (X ou C - 5 ou 4) pour passer le booléen à `true`
5. Ajouter dans la fonction `_UPDATE()` :
  1. Seulement si `exploding` est vrai
  2. Parcourir tous les pixels
  3. Leur ajouter en x et en y un nombre aléatoire (`RND(1)`)

On a un mouvement de destructuration un peu moche, mais c'est un début !

Pour faire mieux, il va falloir ajouter de la gravité. Vous avez peur ? C'est en fait tout simple : en plus de la position x, y et de la couleur on va ajouter la vélocité en x et y.
La vélocité, c'est la valeur que l'on va ajouter à chaque frame à la position. Si la vélocité augmente ou diminue, le pixel va accélérer ou ralentir !

Exemple pour un pixel `p`. On nommera `dx` et `dy` la vélocité en x et y en hommage aux cours de physique.

```lua
-- Impulsion initiale
p.dx=1
p.dy=-3

-- A chaque frame, faire
p.x=p.x+p.dx
p.y=p.y+p.dy

-- Pour la gravité, modifier dy :
p.dy=p.dy+1
```

6. Ajouter la vélocité à chaque pixel
7. Affiner : ajouter du random en x et y au bon moment pour donner un effet sympa

### Correction

```lua
hamburger={
  -- buns
  {x=63,y=64,c=9},
  {x=64,y=64,c=9},
  {x=65,y=64,c=9},
  {x=66,y=64,c=9},
  {x=67,y=64,c=9},
  {x=63,y=60,c=9},
  {x=64,y=60,c=9},
  {x=65,y=60,c=9},
  {x=66,y=60,c=9},
  {x=67,y=60,c=9},
  {x=63,y=59,c=9},
  {x=64,y=59,c=9},
  {x=65,y=59,c=9},
  {x=66,y=59,c=9},
  {x=67,y=59,c=9},
  -- steack
  {x=63,y=62,c=4},
  {x=64,y=62,c=4},
  {x=65,y=62,c=4},
  {x=66,y=62,c=4},
  {x=67,y=62,c=4},
  {x=63,y=63,c=4},
  {x=64,y=63,c=4},
  {x=65,y=63,c=4},
  {x=66,y=63,c=4},
  {x=67,y=63,c=4},
  -- salad & cheese
  {x=63,y=61,c=11},
  {x=64,y=61,c=11},
  {x=65,y=61,c=10},
  {x=66,y=61,c=10},
  {x=67,y=61,c=11},
}

boom=false

function _update()
	-- press x to destroy hamburger
	if(btn(5)) then
		boom=true

		-- initial velocity for all pixels
		for p in all(hamburger) do
			p.dx=rnd(1)-rnd(1)
			p.dy=-3
		end
	end

	if boom then
		-- move all pixels
		for p in all(hamburger) do

			-- add velocity		
			p.x=p.x+p.dx
			p.y=p.y+p.dy

			-- gravity
			p.dy=p.dy+rnd(1)

		end
	end
end

function _draw()
	cls()
	-- draw all pixels
	for p=1,#hamburger do
		pset(hamburger[p].x,hamburger[p].y,hamburger[p].c)
	end
end
```

## Exercice : casse-brique

![Breakout]({{site.url}}/static/content/pico8/breakout.gif)

1. Faire un sprite de balle
2. Afficher la balle
3. La faire bouger à chaque frame en x et y. La vitesse doit être une variable.
4. Faire rebondir sur les murs et le plafond (inverser la vitesse en x ou y )
5. Ajouter une palette pour joueur
6. Déplacer la palette en x avec les flèches dans les limites de l'écran
7. Ajouter la collision balle/joueur (rebond sur la palette)
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
8. Faire des sprites de blocks
9. Ajouter des blocks et les afficher
10. Ajouter collision balle/block (détruire block + rebond)
Bonus: Ajouter scores, vie, effets, sons, etc!

### Correction

```lua
-- breakout
-- damien mayance (@valryon)

-- vars
player={x=54,y=114,w=24,h=8,dx=2}
ball={x=0,y=0,w=8,h=8,s=5,dx=1,dy=1}
blocks={
	{x=16,y=24,w=8,h=8,s=1},
	{x=24,y=24,w=8,h=8,s=1},
	{x=32,y=24,w=8,h=8,s=1},
	{x=40,y=24,w=8,h=8,s=1},
	{x=48,y=24,w=8,h=8,s=1},
	{x=56,y=24,w=8,h=8,s=1},
	{x=64,y=24,w=8,h=8,s=1},
	{x=72,y=24,w=8,h=8,s=1},
	{x=80,y=24,w=8,h=8,s=1},
	{x=88,y=24,w=8,h=8,s=1},
	{x=96,y=24,w=8,h=8,s=1},
	{x=104,y=24,w=8,h=8,s=1},
	{x=16,y=36,w=8,h=8,s=2},
	{x=24,y=36,w=8,h=8,s=2},
	{x=32,y=36,w=8,h=8,s=2},
	{x=40,y=36,w=8,h=8,s=2},
	{x=48,y=36,w=8,h=8,s=2},
	{x=56,y=36,w=8,h=8,s=2},
	{x=64,y=36,w=8,h=8,s=2},
	{x=72,y=36,w=8,h=8,s=2},
	{x=80,y=36,w=8,h=8,s=2},
	{x=88,y=36,w=8,h=8,s=2},
	{x=96,y=36,w=8,h=8,s=2},
	{x=104,y=36,w=8,h=8,s=2},
	{x=16,y=48,w=8,h=8,s=3},
	{x=24,y=48,w=8,h=8,s=3},
	{x=32,y=48,w=8,h=8,s=3},
	{x=40,y=48,w=8,h=8,s=3},
	{x=48,y=48,w=8,h=8,s=3},
	{x=56,y=48,w=8,h=8,s=3},
	{x=64,y=48,w=8,h=8,s=3},
	{x=72,y=48,w=8,h=8,s=3},
	{x=80,y=48,w=8,h=8,s=3},
	{x=88,y=48,w=8,h=8,s=3},
	{x=96,y=48,w=8,h=8,s=3},
	{x=104,y=48,w=8,h=8,s=3},
	{x=16,y=12,w=8,h=8,s=4},
	{x=24,y=12,w=8,h=8,s=4},
	{x=32,y=12,w=8,h=8,s=4},
	{x=40,y=12,w=8,h=8,s=4},
	{x=48,y=12,w=8,h=8,s=4},
	{x=56,y=12,w=8,h=8,s=4},
	{x=64,y=12,w=8,h=8,s=4},
	{x=72,y=12,w=8,h=8,s=4},
	{x=80,y=12,w=8,h=8,s=4},
	{x=88,y=12,w=8,h=8,s=4},
	{x=96,y=12,w=8,h=8,s=4},
	{x=104,y=12,w=8,h=8,s=4},
}

function _init()
	reset()
end

-- loop
function _update()

	-- move player on inputs
	if(btn(0) and player.x>8) then
		player.x=player.x-player.dx
	elseif(btn(1) and player.x<(128-player.w)) then
		player.x=player.x+player.dx
	end

	-- move ball
	ball.x=ball.x+ball.dx
	ball.y=ball.y+ball.dy
	if ball.x<0 or ball.x>128-ball.w then
		ball.dx=-ball.dx
	end
	if ball.y<0 then
		ball.dy=-ball.dy
	elseif ball.y>128+ball.h then
		-- todo game over
		sfx(2)
		reset()
	end

	-- collisions
	---- ball/player
	if collide(ball,player) then
		sfx(1)

		-- rebound
		ball.dy=-abs(ball.dy)

		---- x is related to the side hit
		if ball.x+(ball.w/2)>player.x+(player.w/2) then
			d=1
		else
			d=-1
		end
		ball.dx=d*abs(ball.dx)

		-- replace above
		ball.y=player.y-ball.h

		-- speed up (velocity+0.25)
		ball.dx=ball.dx+(sgn(ball.dx)*0.25)
		ball.dy=ball.dy+(sgn(ball.dy)*0.25)
	end

	---- ball/blocks
	for b in all(blocks) do
		if collide(ball,b) then
			-- rebound (direction matters)			
			ball.dy=-ball.dy
			if ball.y>b.y+1 and
						ball.y<b.y+b.h-1
		 then
				ball.dx=-ball.dx
			end
			-- remove
			explode(b)
			-- one block per frame
			break
		end
	end
end

function _draw()
	cls()

	-- draw player
	spr(16,player.x,player.y)
	spr(17,player.x+8,player.y)
	spr(18,player.x+16,player.y)

	-- draw ball
	spr(ball.s,ball.x,ball.y)

	-- draw bricks
	for b in all(blocks) do
		spr(b.s,b.x,b.y)
	end

	-- draw rect around screen
	rect(0,0,127,129,5)
end

-- functions
function reset()
	ball.x=54
	ball.y=88

	if(-1+rnd(2)<0) then ball.dx=-1
	else ball.dx=1	end
	ball.dy=-1
end

function explode(b)
	sfx(0)
	del(blocks,b)
end

-- utils
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
