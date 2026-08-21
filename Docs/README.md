# GFX.Stats panels

`FPSPanel` presents the measured frame rate in a compact overlay.
`PerformancePanel` adds frame duration, draw calls, triangles, pipeline binds,
render passes, uniform traffic, and texture bindings.

Both panels install the existing Scene2D overlay capability and refresh at a
configurable interval. `PanelAnchor` and the margin select their viewport
placement. Negative margins and non-positive refresh intervals are rejected.

The panels are development and test aids. They do not define a UI toolkit,
retain historical samples, export telemetry, or own the counters exposed by
Rendering.
