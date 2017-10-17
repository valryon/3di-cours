---
title: Unity3D - Petits trucs utiles
layout: default
---

## Playground

Pack de scripts utiles pour faire des petits jeux à cette adresse :
- [https://github.com/valryon/PlaygroundProject/](https://github.com/valryon/PlaygroundProject/releases/tag/0.1)

## Mathématique

### Random

```csharp
// Chiffre entre 0 et 10
int n = Random.Range(0,10);
float nombreAleatoire = Random.Range(0, 1.5f);
```

## Hiérarchie

### Obtenir un composant

```csharp
Rigidbody2D r = GetComponent<Rigidbody2D>();
Collider2D c = GetComponent<Collider2D>();
SpriteRenderer c = GetComponent<SpriteRenderer>();
```

Fonctionne également avec n'importe quel autre composant ou avec **vos scripts** !

### Obtenir un objet

#### Par son type

```csharp
PlayerScript player = FindObjectOfType<PlayerScript>();
if(player != null)
{

}
```

#### Par son nom

```csharp
GameObject o = GameObjet.Find("Nom dans la scène");
if(o != null)
{

}
```

### Déplacer un objet

```csharp
Vector3 movement = new Vector3(1f, 0.5f, 0f); //(x:1, y:0.5, z:0)
transform.position += movement;
```

#### Avec la gravité/la physique

```csharp
Rigidbody2D r = GetComponent<Rigidbody2D>();
Vector3 movement = new Vector3(5f, 2.5f, 0f);
r.velocity += movement;
```


### Détruire un objet

```csharp
Destroy(gameObject);
```

Détruire après N secondes

```csharp
Destroy(gameObject, 3f); // 3 secondes
```


## Modifications visuelles

### Modifier un sprite

```csharp
public SpriteRenderer redSprite;
public SpriteRenderer blueSprite;
public SpriteRenderer greenSprite;

...

SpriteRenderer r = GetComponent<SpriteRenderer>();
r.sprite = redSprite;
```

### Modifier la couleur d'un sprite

```csharp
SpriteRenderer r = GetComponent<SpriteRenderer>();
r.color = Color.red;
```

### Modifier la couleur d'un mesh

```csharp
Renderer mr = GetComponent<Renderer>();
mr.material.color = Color.red;
```

## Structure de données

### Liste de GameObjects

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

## Souris

### Position de la souris

A l'écran :

```csharp
Vector2 p = Input.mousePosition;
```

Dans le monde :

```csharp
Vector2 p = Camera.main.ScreenToWorldPosition(Input.mousePosition);
```

### Clics (maintenu / à l'instant)

```csharp
// Clic
bool click = Input.GetMouseButton(0);
bool clicked = Input.GetMouseButtonDown(0);
```

### Sélection d'un objet

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

## Tactile

### Tap

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

### Position d'un doigt à l'écran

```csharp
if(Input.touchCount >= 1)
{
  Vector3 p = Input.touches[0].position;
  // p est une position sur l'écran, pas dans le monde !
}
```

### Position d'un doigt dans le monde

```csharp
if(Input.touchCount >= 1)
{
  Vector3 p = Camera.main.ScreenToWorldPoint(Input.touches[0].position);
}
```

### Drag

#### Placer un GameObject sous le doigt

```csharp
if (Input.touchCount > 0)
{
  Vector3 positionDoigt = Camera.main.ScreenToWorldPoint(Input.touches[0].position);

  transform.position = positionDoigt;
}
```

## Coroutines

###  Définir une coroutine

```csharp
private IEnumerator WaitAndSay(string text)
{
  yield return new WaitForSeconds(3f);

  Debug.Log(text);
}
```

### Démarrer une coroutine

```csharp
StartCoroutine("WaitAndSay", "Coucou");

// OU

StartCoroutine(WaitAndSay("Coucou"));
```

### Stopper

```csharp
StopCoroutine("WaitAndSay");
```

### Timers

```csharp
private IEnumerator WaitAndDo()
{
  yield return new WaitForSeconds(2f); // Attends 2 secondes

  Debug.Log("I <3 la raclette en été"); // A remplacer par n'importe quoi d'autre ;)
}
```

### Combinaison avec `while`

```csharp
private IEnumerator MoveRight()
{
  float x = transform.position.x + 5f;

  while(transform.position.x < x)
  {
    transform.position += new Vector3(0.1f, 0, 0);

    yield return new WaitForEndOfFrame();
  }
}
```

### Interpolation

```csharp
private IEnumerator Interpolate(Vector3 from, Vector3 to, float duration)
{
  float t = 0;
  while (t < duration)
  {
    // On récupère le % d'avancement entre 0 et 1
    float delta = (t / duration);

    // On interpole (ici linéaire)
    transform.position = Vector3.Lerp(from, to, delta);

    // On attend la frame suivante pour permetre la mise à jour de l'affichage !
    yield return new WaitForEndOfFrame();
    t += Time.deltaTime;
  }
}
```

```csharp
// Exemple d'utilisation
StartCoroutine(Interpolate(transform.position, transform.position+new Vector3(5,0,0), 1f));
```

### Interpolation avec courbe !


```csharp

private IEnumerator InterpolateCurve(Vector3 from, Vector3 to, float duration, AnimationCurve curve)
{
  float t = 0;
  while (t < duration)
  {
    // On récupère le % d'avancement entre 0 et 1
    float delta = (t / duration);

    // On interpole (ici linéaire)
    transform.position = Vector3.Lerp(from, to, curve.Evaluate(delta));

    // On attend la frame suivante pour permetre la mise à jour de l'affichage !
    yield return new WaitForEndOfFrame();
    t += Time.deltaTime;
  }
}
```

```csharp

public AnimationCurve courbe; // Définir une courbe éditable dans Unity

// ...

// Exemple d'utilisation
// Penser à remplir le chambe "courbe" dans l'inspecteur !!!
StartCoroutine(Interpolate(transform.position, transform.position+new Vector3(5,0,0), 1f), courbe);
```
