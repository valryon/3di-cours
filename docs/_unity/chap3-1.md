---
title: Unity3D - Petits trucs utiles
layout: default
---

## Playground

Pack de scripts utiles pour faire des petits jeux à cette adresse :
- [https://github.com/valryon/PlaygroundProject/](https://github.com/valryon/PlaygroundProject/releases/tag/0.1)


## Obtenir un composant

```csharp
Rigidbody2D r = GetComponent<Rigidbody2D>();
Collider2D c = GetComponent<Collider2D>();
SpriteRenderer c = GetComponent<SpriteRenderer>();
```

Fonctionne également avec n'importe quel autre composant ou avec **vos scripts** !

## Obtenir un objet

### Par son type

```csharp
PlayerScript player = FindObjectOfType<PlayerScript>();
if(player != null)
{

}
```

### Par son nom

```csharp
GameObject o = GameObjet.Find("Nom dans la scène");
if(o != null)
{

}
```

## Déplacer un objet

```csharp
Vector3 movement = new Vector3(1f, 0.5f, 0f); //(x:1, y:0.5, z:0)
transform.position += movement;
```

### Avec la gravité/la physique

```csharp
Rigidbody2D r = GetComponent<Rigidbody2D>();
Vector3 movement = new Vector3(5f, 2.5f, 0f);
r.velocity += movement;
```

## Modifier un sprite

```csharp
public SpriteRenderer redSprite;
public SpriteRenderer blueSprite;
public SpriteRenderer greenSprite;

...

SpriteRenderer r = GetComponent<SpriteRenderer>();
r.sprite = redSprite;
```

## Modifier la couleur d'un sprite

```csharp
SpriteRenderer r = GetComponent<SpriteRenderer>();
r.color = Color.red;
```

## Modifier la couleur d'un mesh

```csharp
Renderer mr = GetComponent<Renderer>();
mr.material.color = Color.red;
```

## Liste de GameObjects

Ajouter comme variable à la classe :

```csharp
public List<GameObject> trucs;
```

Remplacer `GameObject` par `SpriteRenderer`, `Vector3`, `Color`, etc.

### Récupérer un élément au hasard dans une liste

```csharp
GameObject elementAuPif = trucs[Random.Range(0, trucs.Count)];  
```

Remplacer `GameObject` par `SpriteRenderer`, `Vector3`, `Color`, etc, selon la liste définie !

### Détruire un objet

```csharp
Destroy(gameObject);
```

Détruire après N secondes

```csharp
Destroy(gameObject, 3f); // 3 secondes
```

## Avoir un nombre aléatoire

```csharp
float nombreAleatoire = Random.Range(0, 42f);
```

# Souris

## Position de la souris

A l'écran :

```csharp
Vector2 p = Input.mousePosition;
```

Dans le monde :

```csharp
Vector2 p = Camera.main.ScreenToWorldPosition(Input.mousePosition);
```

## Clics (maintenu / à l'instant)

```csharp
// Clic
bool click = Input.GetMouseButton(0);
bool clicked = Input.GetMouseButtonDown(0);
```

## Sélection d'un objet

```csharp
// Toucher un collider **2D** sur le clic
// Ne fonctionne qu'avec une caméra orthographique
if (Input.GetMouseButtonDown(0))
{
    // Conversion position écran -> position monde
    Vector3 positionSouris = Camera.main.ScreenToWorldPoint(Input.mousePosition);
    // "Ray"cast : tirer un trait imaginaire et voir ce que l'on touche
    RaycastHit2D hit = Physics2D.CircleCast(positionSouris, 0.2f, new Vector2(1, 1));

    // A-t-on touché ?
    if(hit.transform != null)
    {
        // Faire quelque chose
        // ..
    }
}
```

# Tactile

## Tap

```csharp
if(Input.touchCount >= 1)
{

}
```

### Tap à droite ou à gauche

```csharp
if(Input.touchCount >= 1)
{
    Vector3 p = Camera.main.ScreenToViewport(Input.touches[0]);
    if(p.x < 0.5f) 
    {
       // Gauche
    }
    else 
    {
       // Droite
    }
}
```

## Drag

TODO

## Position d'un doigt

```csharp
if(Input.touchCount >= 1)
{
  var p = Input.touches[0].position;
  // p est une position sur l'écran, pas dans le monde !
}
```

# Coroutines

TODO
