---
title: Coroutines
layout: default
---

## Les quoi ?

Une coroutine est un mécanisme qui permet l'éxecution de code en parallèle de la boucle principale.

C'est très pratique pour tout ce qui a besoin de *timings* ou d'interpolations sur plusieurs frames.

Une coroutine peut être longue, courte, boucler ou n'être qu'un traitement de données. On peut lancer plusieurs coroutines en même temps. Beaucoup, mais pas une infinité : elles prennent des ressources CPU/mémoire et du temps à chaque frame).

## Concrètement ?

Une coroutine est une fonction qui doit forcément renvoyer un `IEnumerator`. Cette classe très spéciale en C# permet au programme d'exécuter le code contenu dans la coroutine sur plusieurs frames.

Comment ? Grâce à l'instruction `yield return`.

A chaque `yield return`, la fonction s'arrête à cette ligne pour cette frame. Puis, à la frame suivante, la fonction est appelée à nouveau automatiquement mais au lieu de reprendre au début, elle reprend **là où elle s'est arrêtée**.

```csharp
// Définit une coroutine qui attend un peu et affiche "Coucou" dans la console
private IEnumerator WaitAndCoucou()
{
  // Attend 3 secondes
  yield return new WaitForSeconds(3f);

  // Une fois les 3 secondes écoulées, l'éxécution recommence ici

  // Affiche dans la console "Coucou"
  Debug.Log("Coucou");
}
```

### Comment ça s'utilise ?

Très simplement. Deux syntaxes possibles.

```csharp
StartCoroutine("WaitAndCoucou");

// OU

StartCoroutine(WaitAndCoucou());
```

La première syntaxe est plus simple mais ne permet de passer qu'un seul paramètre, là où la deuxième syntaxe permet d'envoyer plus de paramètres à l'appel.

Exemples.

```csharp
private IEnumerator WaitAndSay(string text)
{
  yield return new WaitForSeconds(3f);
  Debug.Log(text);
}
StartCoroutine("WaitAndSay", "Coucou");
```

```csharp
private IEnumerator WaitAndSay(float wait, string text)
{
  yield return new WaitForSeconds(wait);
  Debug.Log(text);
}
StartCoroutine(WaitAndSay(2.5f, "Coucou"));
```

On peut arrêter une coroutine à tout moment :

```csharp
StopCoroutine("WaitAndSay");
```

## Instructions yield

Unity met à disposition plusieurs instructions compatibles avec `yield return` pour nos coroutines :

- `WaitForSeconds`: fait attendre la coroutine sur la durée indiquée
- `WaitForSecondsRealtime`: fait attendre la coroutine sur la durée indiquée en temps réel (et non delta time qui peut être stoppé)
- `WaitForEndOfFrame`: fait attendre la coroutine sur une frame et permet d'éxecuter du code à la toute fin de la frame
