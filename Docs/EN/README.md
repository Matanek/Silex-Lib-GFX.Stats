# GFX.Stats panels

`GFX.Stats` displays live development statistics inside a GFX application. The
package provides a compact render-FPS panel and a detailed rendering-performance
panel.

[Lire cette documentation en français.](../FR/README.md)

## Install the package

```text
silex install GFX.Stats
```

GFX.Stats requires Silex 0.39.0 or newer.

## Display frames per second

The direct API keeps the panel choice and placement explicit:

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

`PanelAnchor` and the margin configure viewport placement. A negative margin
or non-positive refresh interval is rejected.

## Choose the displayed statistics

`FPSPanel` presents the measured render rate in a compact overlay.
`PerformancePanel` labels it explicitly as `RENDER FPS` and adds render-frame
duration, draw calls, triangles, pipeline binds, render passes, uniform
traffic, and texture bindings.

Both panels are alternative views of the same capability. Adding one explicit
view replaces the other during plugin resolution. They install the existing
Scene2D overlay and refresh at a configurable interval.

The counters remain owned by `GFX.Rendering`; GFX.Stats only samples,
aggregates, and presents them. The displayed rate does not measure how often
an asynchronous simulation publishes a new state.

## Use the plugin catalog

The package contributes the same identifiable names to the flattened catalog:

```sx
use GFX.Plugins

application.add_plugin(Plugins.FPSPanel())
application.add_plugin(Plugins.PerformancePanel())
```

This fragment assumes an existing `application:GFX.Application` variable.

## See the complete presentations

The panels are development and test aids. They do not define a UI toolkit,
retain historical samples, or export telemetry. Visual demonstrations belong
to Silex-Examples:

- [FPS panel](https://github.com/Matanek/Silex-Examples/blob/main/Sources/FPSStatsPanel.sx)
- [Performance panel](https://github.com/Matanek/Silex-Examples/blob/main/Sources/PerformanceStatsPanel.sx)
