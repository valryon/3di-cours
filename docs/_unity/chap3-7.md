---
title: Windows Mixed Reality
layout: default
---

## Installation et téléchargements

- Windows 10 avec Fall Creators Update 2017
- Activer le `Mode Développeur` dans Windows->Panneau de contrôle->Pour les développeurs

(Si Windows Update est bloqué / plante)
- [Télécharger et installer](https://docs.microsoft.com/fr-fr/windows/application-management/manage-windows-mixed-reality) le module WMR à la main
    - [Cab file](http://download.microsoft.com/download/6/F/8/6F816172-AC7D-4F45-B967-D573FB450CB7/Microsoft-Windows-Holographic-Desktop-FOD-Package.cab)
        - Ouvrir `cmd` en tant qu'administrateur
        - `dism /online /add-package /packagepath:"path to the cab file"`
    - [KB4054517](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4054517)

- Visual Studio 2017 avec les modules UWP (Universal Windows Platform) et Unity.

- [SDK UWP](https://developer.microsoft.com/fr-fr/windows/downloads/windows-10-sdk) (Ne cocher que ce qui concerne UWP)

- Unity 2017.3+

## Création d'un projet Unity

- 2017.3.0 min
- UWP SDK
- UWP type
- XR