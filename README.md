# GFX.Stats

`GFX.Stats` displays live development statistics inside a GFX application.
It provides a compact render-FPS panel and a detailed rendering-performance panel
without introducing a general-purpose UI system.

```text
silex install GFX.Stats
```

The direct API keeps both presentations explicit:

```silex
use GFX.Application
use GFX.Stats

Application()
    ..add_plugin(Stats.FPSPanel(Stats.FPSPanel.Settings()
        ..anchor = Stats.PanelAnchor.bottom_right
    ))
    ..run()
```

The package contributes the same identifiable names to the flattened plugin
catalog:

```silex
use GFX.Plugins

application.add_plugin(Plugins.FPSPanel())
application.add_plugin(Plugins.PerformancePanel())
```

`FPSPanel` and `PerformancePanel` are alternative views of the same panel
capability. Adding one explicit view replaces the other during plugin
resolution. The rendering statistics themselves remain owned by
`GFX.Rendering`; this package only samples, aggregates, and presents them.
The detailed panel says `RENDER FPS` deliberately: an asynchronous simulation
can publish new visual states less often while the renderer repeats its latest
state.

`Tests/Consumer` verifies both the direct namespace and the flattened catalog
from an anonymous application workspace.
