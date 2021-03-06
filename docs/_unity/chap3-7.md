---
title: Windows Mixed Reality
layout: default
---

## Installation et téléchargements

### Windows Mixed Reality portal

- Windows 10 avec [Fall Creators Update 2017]( https://support.microsoft.com/en-us/help/4045820)
- Activer le `Mode Développeur` dans Windows->Panneau de contrôle->Pour les développeurs

(Si Windows Update est bloqué / plante)
- [Télécharger et installer](https://docs.microsoft.com/fr-fr/windows/application-management/manage-windows-mixed-reality) le module WMR à la main
    - [Cab file](http://download.microsoft.com/download/6/F/8/6F816172-AC7D-4F45-B967-D573FB450CB7/Microsoft-Windows-Holographic-Desktop-FOD-Package.cab)
        - Ouvrir `cmd` en tant qu'administrateur
        - `dism /online /add-package /packagepath:"path to the cab file"`
    - [KB4054517](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4054517)

Le portail et le casque devrait fonctionner.

- [Unity 2017.3+](https://unity3d.com/fr/get-unity/update)

- Plugin [Steam VR](https://assetstore.unity.com/packages/templates/systems/steamvr-plugin-32647)
  (Pas obligatoire, mais plus simple et compatible avec plusieurs casques)

## Création d'un projet Unity

- 2017.3.0 min
- Activer `Virtual Reality` dans l'onglet XR des PlayerSettings

![XR settings]({{site.url}}/static/content/unity/xr.png)