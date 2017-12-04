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