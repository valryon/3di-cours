---
title: Éditeurs customs
layout: default
---

L'une des grandes forces de Unity3D est de laisser aux développeurs.ses la possibilité d'avoir leurs propres outils directement intégré à l'éditeur.

Deux possibilités :

- La **fenêtre éditeur personnalisée**. Elle peut contenir et absolument tout ce qu'il est possible de faire dans le jeu et dans Unity. Quelques exemples : spawns de mobs, soin du joueur, changer d'arme, changer de niveaux, etc.

![Steredenn 1]({{site.url}}/static/content/unity/customeditor1.png)
![Steredenn 2]({{site.url}}
/static/content/unity/customeditor2.png)
![LV ;)]({{site.url}}/static/content/unity/customeditor5.png)

- L'**inspecteur personnalisé**. L'inspecteur est lié à un composant ou à un *ScriptableObject*. Il permet de remplacer ou d'ajouter à la suite de l'inspecteur de base des boutons, des champs, des informations.

![Steredenn 3]({{site.url}}/static/content/unity/customeditor3.png)
![Pon]({{site.url}}/static/content/unity/customeditor4.png)

Tous les composants et toutes les fenêtres de base peuvent être refaites.

L'inspecteur et les fenêtres partagent les mêmes instructions, les mêmes *widgets*, pour dessiner des éditeurs. La structure de la classe change un peu, mais on est dans les deux cas sur de l'*Immediate GUI*, c'est à dire que l'interface est affichée et re-dessinée plusieurs fois par seconde comme une frame du jeu.

Ces outils sont uniquement disponibles dans **l'éditeur** et pas dans un build. Pour éviter des erreurs de compilation il faut :

    - mettre ces fichiers dans un dossier `Editor/`
    - entourer le code d'un `#if UNITY_EDITOR` (ça ne fait pas de mal)

Ensuite il faut penser à ajouter `using UnityEditor;` pour avoir accès à ces fonctionnalités.

## Fenêtre custom

```csharp
#if UNITY_EDITOR

using UnityEngine;
using System.Collections;
using UnityEditor;

public class MyWindow : EditorWindow
{
    void OnGUI()
    {
        this.titleContent = new GUIContent("MyGreatWindow");

        // Ici nous allons dessiner les widgets et modifier l'état du jeu
    }

    // OnEnable, Update, etc, sont aussi disponibles ici.

    // Ajouter un menu pour l'afficher
    [MenuItem("Window/MyWindow")]
    public static void ShowWindow()
    {
        EditorWindow.GetWindow(typeof(MyWindow));
    }
}
```

## Inspecteur

```csharp
#if UNITY_EDITOR

using UnityEngine;
using System.Collections;
using UnityEditor;

  [CustomEditor(typeof(MyScript))]
  public class MyScriptEditor : Editor
  {
    private MyScript myScript;

    void OnEnable()
    {
        myScript = (MyScript)t;
    }

    public override void OnInspectorGUI()
    {
      // Pour avoir l'inspecteur de base
      // Laisser cet appel
      base.OnInspectorGUI();

      // Affichge de widgets
    }
}
#endif
```

## Widgets disponibles

| Fonction ou champ | Description | 
| ----------------- | ----------- |
| EditorGUILayout.LabelField(text) | Affiche un texte |
| GUILayout.Button("Reload") | Affiche un bouton. À utilisr dans un `if` pour récupérer le clic |
| EditorGUILayout.BeginScrollView(scroll) | Affiche une barre de défilement |
| EditorGUILayout.EndScrollView(scroll) |  |
| EditorGUILayout.BeginHorizontal() | Dessine les composants sur la même ligne jusqu'au `EndHorizontal` |
| EditorGUILayout.EndHorizontal() |  |
| EditorGUILayout.BeginVertical() | Dessine les composants sur la même colonne jusqu'au `EndVertical` |
| EditorGUILayout.EndVertical() |  |
| EditorGUI.indentLevel | Décaler à gauche `--` ou à droite `++` |

## Autres outils

| Fonction ou champ | Description | 
| ----------------- | ----------- |
| Application.isPlaying | Indique si le jeu est lancé |

## Inspecteur pour plusieurs fichiers à la fois

```csharp
#if UNITY_EDITOR

using UnityEngine;
using System.Collections;
using UnityEditor;

[CustomEditor(typeof(MyScript))]
[CanEditMultipleObjects]
public class MyScriptEditor : Editor
{
    void OnEnable()
    {
    }

    public override void OnInspectorGUI()
    {
        base.OnInspectorGUI();

        foreach(var t in targets)
        {
            var myScript = (MyScript)t;
        }
    }
}
#endif
```

