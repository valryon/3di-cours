---
title: Scriptable Objects
layout: default
---

Format de données sérialisé automatiquement chargé par Unity3D.

## Définir un ScriptableObject

Il suffit de faire une classe composée de données sérializable elles aussi.

```csharp
[System.Serializable]
public class PlayerData : ScriptableObject
{
  public int hp;
  public float speed;
}
```

## Classe utile pour créer des ScriptableObjects

A mettre dans une dossier `Editor`.

```csharp
#if UNITY_EDITOR

using UnityEngine;
using UnityEditor;
using System.IO;

/// <summary>
/// ScriptableObject helper
/// </summary>
/// <remarks>Source: http://www.jacobpennock.com/Blog/?page_id=715 </remarks>
public static class ScriptableObjectUtility
{
  public static T CreateAsset<T>() where T : ScriptableObject
  {
    return CreateAsset<T>("New " + typeof(T).ToString() + ".asset");
  }

  public static T CreateAsset<T>(string name) where T : ScriptableObject
  {
    if (name.EndsWith(".asset") == false)
    {
      name = name + ".asset";
    }

    string path = AssetDatabase.GetAssetPath(Selection.activeObject);
    if (path == "")
    {
      path = "Assets";
    }
    else if (Path.GetExtension(path) != "")
    {
      path = path.Replace(Path.GetFileName(AssetDatabase.GetAssetPath(Selection.activeObject)), "");
    }

    return CreateAsset<T>(path, name);
  }

  public static T CreateAsset<T>(string path, string name) where T : ScriptableObject
  {
    if (name.EndsWith(".asset") == false)
    {
      name = name + ".asset";
    }

    string assetPathAndName = AssetDatabase.GenerateUniqueAssetPath(path + "/" + name);

    T asset = ScriptableObject.CreateInstance<T>();

    AssetDatabase.CreateAsset(asset, assetPathAndName);

    AssetDatabase.SaveAssets();
    EditorUtility.FocusProjectWindow();
    Selection.activeObject = asset;

    return asset;
  }
}
#endif
```