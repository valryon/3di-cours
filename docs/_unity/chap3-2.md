---
title: Installation des outils pour Android
layout: default
---

Pour déployer son jeu sur Android, il faut installer plusieurs choses :

1. [L'environnement de développement Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). Prendre la version correspondant à son système (en général WIndows x64).

2. [Android Studio](https://developer.android.com/studio/index.html) qui va installer et configurer le SDK Android sans effort

3. Le plugin Android pour Unity (Android Build Support) s'il n'est pas actif dans les `File->Build Settings`. Le lien pour le técharger est fourni par Unity dans cette fenêtre pour changer de plateforme.

4. Il faut également un *device* (téléphone, tablette) Android qui soit en **mode développeur**. Le plus simple est de chercher sur Google comment faire sur votre modèle de téléphone et avec votre version d'Android. En général il faut cliquer 10 fois sur le numéro de version dans les paramètres ou autre chose cachée du genre.

5. Une fois le téléphone activé, il faut activer le "Debug par USB" dans les options Développeur.

Il devrait ensuite être possible de déployer votre jeu sur votre *device.

## Remote

1. Télécharger l'application "Unity Remote" sur le [Play Store](https://play.google.com/store/apps/details?id=com.unity3d.genericremote&hl=fr).

2. Dans votre projet Unity, `Edit->Project Settings->Editor` et choisir "Any Android Device" dans le paramètre `Remote->Device`.

La remote permet de projeter le jeu sur l'écran du téléphone et de tester les contrôles tactiles via la connexion USB.
