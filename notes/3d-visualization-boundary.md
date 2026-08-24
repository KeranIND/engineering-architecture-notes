# 3D Fit Visualization as a Versioned System Boundary

Chanamill's 3D work combines a body/avatar asset, garment mesh, fit profile and camera/presentation state. The visualization layer should consume versioned inputs rather than become the source of truth for fit.

## Boundary

```text
FitID version
Garment spec version
Avatar asset id
Garment mesh id
        ↓
Visualization request
        ↓
Renderer
  ├── front preset
  ├── side preset
  ├── back preset
  └── world-anchored measurement callouts
```

## Important design choices

- fit logic remains outside the renderer
- camera presets are deterministic
- callouts attach to model/world anchors, not fixed screen coordinates
- cache keys include FitID and garment-spec versions
- mesh revisions are immutable inputs to a render request
- visual confidence must not be confused with measurement confidence

This keeps visualization useful for explanation without allowing presentation code to silently change the decision model.