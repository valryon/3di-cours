# Programmation C# dans Unity3D

## Généralités

### Outils

Unity3D ne permet pas de coder directement, il faut utiliser un éditeur de code.

Le plus populaire et le plus pratique sur Windows est **Visual Studio**.
(Sur Mac, **Visual Studio Code** ou **MonoDevelop** qui est fourni avec)

Unity3D installe toujours un éditeur de code avec son installation.

### Organisation des fichiers

- Chaque script est **une classe**.
- Le **nom de la classe** doit être exactement le même que le **nom du fichier**
- Autant que possible, essayer de n'avoir qu'**une classe par fichier**

### "Scripts" ?

On parle de **scripts** dans Unity3D car on ne code finalement que la partie utile à notre jeu, dans un environnement géré par Unity3D. On ne s'occupe pas de comprendre comment une image est transformée en pixels à l'écran.

Un script unity3D est un fichier.

Un script n'est exécuté que s'il est ajouté à un `GameObject`. Le script est alors un **composant** ! On peut avoir plusieurs fois le même script sur le même objet (l"intérêt est très limité).

## Boucle de jeu

Peu importe le langage, un jeu vidéo se compose globalement de la boucle suivante :

```csharp
while(jeuLancé)
{
  LireManetteClavier();

  MettreAJourLeJeu();

  AfficherJeu();
}
```

Soit :

- La lecture des **inputs** (manettes, clavier, souris, etc)
- La **mise à jour** (update) du monde soit avec le temps qui passe soit avec les inputs de(s) joueur(s)
- Le **rendu** (draw/render) : l'affichage à l'écran du jeu

Chaque tour de boucle est une **frame**.

Un jeu essaie autant que possible de tourner de manière fluide et stable. Pour cela, il doit fonc produire un certain nombre d'images par secondes, de **frames** par secondes (FPS).

En général les jeux AAA tournent entre 30 et 60 FPS selon la plateforme. En dessous, le jeu donnera l'impression justifiée de "ramer" / "lagger".

Unity3D se charge de gérer cette boucle pour nous.

La seule préoccupation qu'il faut garder en tête est qu'il faut exécuter le moins de code possible à chaque frame pour éviter des ralentissements.

## Fonctions principales pour Unity

### Fonctions "timeline"

Pour intégrer notre code avec la boucle de jeu, Unity3D utilise automatiquement certaines fonctions que nous pouvons mettre dans nos fichiers.

Il faut respecter **exactement** la syntaxe de ces fonctions pour qu'elle soit reconnue.

Voici une liste non exhaustive :

|Fonction|Exécuté quand ?|
|----|----|
|Awake()|Dès que l'objet est dans la scène (ou dès que le jeu est lancé)|
|OnEnable()|A chaque fois que l'objet est activé|
|Start()|Après la première fois que l'objet est activé (au démarrage du jeu par exemple)|
|Update()|A chaque frame, 30 à 60 fois par secondes|
|LateUpdate()|A chaque frame, comme Update, mais après tous les Update des autres scripts|
|OnTriggerEnter(Collider c)|Quand le moteur physique 3D détecte une collision collider/trigger|
|OnCollisionEnter(Collision c)|Quand le moteur physique 3D détecte une collision collider/collider|
|OnTriggerEnter2D(Collider2D c)|Quand le moteur physique 2D détecte une collision collider/trigger|
|OnCollisionEnter2D(Collision2D c)|Quand le moteur physique ED détecte un collision collider/collider|
|OnDisable()|Quand l'objet est désactivé|
|OnDestroy()|Quand l'objet est détruit|

Jetez un oeil à la [liste complète avec l'ordre d'exécution](https://docs.unity3d.com/Manual/ExecutionOrder.html).

### Fonctions utiles

|Fonction|Description|
|----|----|
|Input.GetAxis("Horizontal")|Retourne une valeur entre -1 et 1 pour le déplacement gauche/droite au clavier ou à la manette|
|Input.GetAxis("Vertical")|Retourne une valeur entre -1 et 1 pour le déplacement haut/bas au clavier ou à la manette|
|Input.GetKey(KeyCode.Space)|Indique si la touche donnée (ici Espace) vient juste d'être enfoncée|
|Input.GetKeyDown(KeyCode.A)|Indique si la touche donnée (ici A) est enfoncée|
|Instantiate(prefab)|Crée une copie du GameObject passé en paramètre (un prefab par exemple)|
|Destroy(gameObject)|Détruit un composant ou un GameObject|
|AudioSource.PlayClipAtPoint(son, position)|Jouer un son à un endroit donné|

### Comment trouver d'autres fonctions ?

- [Le manuel scripting Unity](https://docs.unity3d.com/ScriptReference/)
- [StackOverflow](http://stackoverflow.com/questions/tagged/unity3d)
- [Google](http://ohquandmême!)
