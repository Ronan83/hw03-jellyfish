# Procedural Jellyfish

A procedural, animated jellyfish built in Houdini with SOPs, VEX and Vellum.

## Video

https://github.com/user-attachments/assets/9cb47216-1556-4fed-a80d-4aa19b2f59b8

## Breakdown

| Part | Approach |
| --- | --- |
| **Bell** | A bent line (two `Bend` nodes) revolved into a dome. Bend angles are driven by `sin($F)` for the pulse; a `Transform` adds the upward swim. Animated and rest-frame copies of the surface drive all `Point Deform` nodes. |
| **Oral arms** | Grids shaped in VEX (taper, ruffled edges, 300° twist), copied ×4 around the center. Simulated as Vellum cloth with the root row pinned to the bell's motion. |
| **Veins** | Bell `Remesh`ed to triangles; `Find Shortest Path` from the apex to random rim/mid points with a noise-based point cost for wandering branches. `Fuse` → `Resample` → `Smooth` → tapered `Sweep`, then `Point Deform` onto the animated bell. |
| **Organs** | Open-arc circles copied ×4, noise-wobbled, swept into tapered tubes, and `Point Deform`ed to the bell. |
| **Tentacles** | 50 polylines generated in VEX along the rim (random lengths). Simulated with Vellum Hair, roots pinned with Match Animation, plus a `POP Force` noise inside the solver for drifting. Swept into thin tubes. |

## Extra Credit

**Refined bell** (single VEX pass after the revolve, weighted from apex to rim):
- **Scalloped margin**: 16 lobes that bulge outward and sag at the rim.
- **Puckering**: radial grooves and noise-based dents across the mid-bell.
