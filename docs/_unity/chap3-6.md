---
title: Exercice - création d'un shoot them up 2D
layout: default
---

Shoot them up 2D à scrolling vertical. 

## Base

- [Télécharger pack assets]({{site.url}}/static/content/unity/shmup_assets.zip)
- Créer nouveau projet 2D
- Ajouter les assets

## Joueur

- Ajouter des sprites en décor
- Créer le joueur dans la scène (GameObject, sprite, collider2D, Rigidbody2D)
- Ajouter un ennemi (GameObject, sprite, collider2D, Rigidbody2D)
- Ennemi -> Prefab

## Scripting

- Créer un script `MoveScript` 
    - Déplace à chaque frame le transform dans une direction
    - L'ajouter aux ennemis

- Créer un script `PlayerScript`
    - Idem `MoveScript`
    - Déplacement soumis aux conditions d'appuyer sur les flèches

```csharp
if (Input.GetKey(KeyCode.LeftArrow) )
{
    // Appui continu sur flèche de gauche
}
```

- Bonus : Empêcher le joueur de sortir de l'écran

- Faire un défilement du décor avec parallax

- Créer un projectile pour le joueur
    - GameObject, sprite, collider2D, Rigidbody2D
    - MoveScript
    - Sauvegarder en prefab

- Ajouter la création de tirs au joueur

```csharp

public GameObject tirPrefab;
...

if (Input.GetKeyDown(KeyCode.Space) )
{
    // Appui sur ESPACE
    Instantiate(tirPrefab, transform.position, Quternion.Identity);
}
```

- Créer un nouveau script `HealthScript` pour la vie 
    - avec une variable "vie"
    - détecter les collisions avec `OnTriggerEnter2D` 

```csharp

- Bonus : Faire un tir par cannon du joueur, positionné devant les cannons

void OnTriggerEnter2D(Collider2D c)
{
    // Collision tir/ennemi

    // Collision tir/joueur
}

void OnCollisionEnter2D(Collision2D c)
{
    // Collision ennemi/joueur
}

```

- Ajouter un son sur la collision
- Ajouter un son sur le tir
- Ajouter un effet d'explosion en particules sur la mort

- Ajouter le tir ennemi, automatique, régulier

- Bonus : faire apparaître des ennemis régulièrement
- Bonus : avoir un score qui augmente à chaque ennemi détruit 
