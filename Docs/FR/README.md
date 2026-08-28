# Panneaux GFX.Stats

`GFX.Stats` affiche des statistiques de développement en direct dans une
application GFX. Le package fournit un panneau compact pour le nombre d’images
rendues par seconde et un panneau détaillé sur les performances du rendu.

[Read this documentation in English.](../EN/README.md)

## Installer le package

```text
silex install GFX.Stats
```

GFX.Stats demande Silex 0.39.0 ou une version plus récente.

## Afficher le nombre d’images par seconde

L’API directe garde le choix du panneau et son placement explicites :

```sx
use GFX.Application
use GFX.Stats

func main() {
    Application()
        ..add_plugin(Stats.FPSPanel(Stats.FPSPanel.Settings()
            ..anchor = Stats.PanelAnchor.bottom_right
        ))
        ..run()
}
```

`PanelAnchor` et la marge règlent le placement dans le viewport. Une marge
négative ou un intervalle de rafraîchissement non positif est rejeté.

## Choisir les statistiques affichées

`FPSPanel` présente le débit de rendu mesuré dans un overlay compact.
`PerformancePanel` le nomme explicitement `RENDER FPS` et ajoute la durée d’une
frame, les draw calls, triangles, changements de pipeline, passes de rendu,
transferts d’uniformes et liaisons de textures.

Les deux panneaux sont des vues alternatives d’une même capacité. Ajouter une
vue explicite remplace l’autre pendant la résolution des plugins. Ils
installent l’overlay Scene2D existant et se rafraîchissent selon un intervalle
configurable.

Les compteurs restent la propriété de `GFX.Rendering`; GFX.Stats ne fait que
les échantillonner, les agréger et les présenter. Le débit affiché ne mesure
pas la fréquence à laquelle une simulation asynchrone publie un nouvel état.

## Utiliser le catalogue de plugins

Le package contribue les mêmes noms identifiables au catalogue aplati :

```sx
use GFX.Plugins

application.add_plugin(Plugins.FPSPanel())
application.add_plugin(Plugins.PerformancePanel())
```

Ce fragment suppose une variable `application:GFX.Application` existante.

## Voir les présentations complètes

Les panneaux sont des aides au développement et aux tests. Ils ne définissent
pas de toolkit UI, ne conservent pas d’historique et n’exportent pas de
télémétrie. Les démonstrations visuelles appartiennent à Silex-Examples :

- [Panneau FPS](https://github.com/Matanek/Silex-Examples/blob/main/Sources/FPSStatsPanel.sx)
- [Panneau de performances](https://github.com/Matanek/Silex-Examples/blob/main/Sources/PerformanceStatsPanel.sx)
