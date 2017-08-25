# Tableaux

Avec les variables, nous avons vu comment stocker **une valeur** dans **une variable**.

Il existe un mécanisme pour stocker **plusieurs** valeurs dans **une seule** variable : les **tableaux** (`Table` en Lua).

*Note : en Lua, les tableaux sont plus proches des listes C# mais le principe reste le même*

## Création d'un tableau

Attention les yeux, c'est très compliqué !

```lua
array={}
```

## Utilisations

Vérifions :

```lua
PRINT(array) -- TABLE
```

On peut ajouter des valeurs :

```lua
add(array,42)
add(array,24)
add(array,89)
add(array,32)

PRINT(#array) -- Affiche la taille du tableau, ici 4
```

Et on peut lire les valeurs en indiquant la position de l'élément voulu entre crochets `[]`

```lua
PRINT(array[1]) -- 42
PRINT(array[2]) -- 24
PRINT(array[3]) -- 89
PRINT(array[4]) -- 32
```

*Note : Lua est un des seuls langages à faire commencer les tableaux à __1__ !*

L'intérêt ? Appliquer le même code à tous les éléments du tableau.

```lua
FOR i=1,#array DO -- i commence à 1 !
  PRINT(array[i])
END
```

## Exemple

TODO
Tableau de tableau
