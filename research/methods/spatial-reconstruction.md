# Spatial Reconstruction

**Function**: Reconstruct real locations as navigable, renderable 3D spaces from photographic capture.

**Used in**: [*Virus*](../projects/virus-2024.md), [Ciclic Residency](../projects/vendome-residency-2024.md)

---

## What problem this solves

Some locations in a film carry the weight of the narrative but cannot be filmed — they're inaccessible, destroyed, or need to appear from impossible angles. Spatial reconstruction allows the filmmaker to enter a location once, photograph it systematically, and then return to it indefinitely as a renderable space.

The result is materially different from photogrammetry or 3D modeling: it's a document of the real with a specific softness — no clean polygon edges, no textured geometry. The image reads as both captured and constructed.

---

## Method: Gaussian Splatting

Gaussian Splatting (3DGS, Inria 2023) reconstructs a 3D scene from a multi-angle photo series by positioning millions of colored ellipsoids (splats) in space. Unlike point clouds or polygon meshes, splats use radial opacity gradients — fully opaque at the center, transparent at the edges — producing renders that are visually softer and more immersive than classical 3D methods.

The reconstruction happens through iterative neural optimization: the network positions splats until their projected views match the input photographs from each angle.

### Capture protocol

- Systematic coverage of the location: every wall, floor, ceiling
- Multiple distances (close, medium, far) from each point
- Controlled exposure consistency across the series
- Avoid reflective surfaces (mirrors, glass) — they confuse reconstruction

### Processing

1. Colmap or equivalent for camera pose estimation from the photo series
2. 3DGS training (several hours on a high-end GPU per location)
3. Export for real-time use in Unreal Engine (via Akiya Research plugin)

### Why this over photogrammetry

Photogrammetry produces clean polygon geometry with baked textures — useful for architectural documentation but reads as synthetic. Gaussian Splatting retains the visual quality of photography while producing a 3D space. The slight instability at the edges of splats, the soft translucency at depth — these become expressive properties rather than technical failures.

---

## Integration into production

In *Virus*, reconstructed locations were loaded directly into Unreal Engine 5 alongside Metahuman avatars. Scenes were "filmed" in real time: a cinematographer operated a virtual camera through the reconstructed space while a performer's movements were captured via mocap and applied to the avatar.

The pipeline:
```
Location photographs → 3DGS training → Unreal Engine scene
                                              ↕
                               Metahuman avatar (Metahuman Creator)
                                              ↕
                               Mocap (Dollars MoCap + LiveLink iPhone)
                                              ↕
                               Virtual camera operator (gamepad / iPhone)
```

---

## Tools referenced

- 3DGS (Inria) — open source
- Akiya Research UE5 plugin — Gaussian Splatting integration for Unreal
- Unreal Engine 5 (Epic Games) — real-time rendering
- Metahuman (Epic) — photorealistic avatar creation
- Dollars MoCap — markerless body capture
- LiveLink (Epic) — iPhone facial capture → Metahuman sync
