---
title: Unity3D - Petits trucs utiles
layout: default
---

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
