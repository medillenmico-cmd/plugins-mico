# Reference visual analysis

**Research date:** 2026-08-31  
**Reference:** <https://youtu.be/8qtUld9IjII?si=K3WVvHT8Nnty7P1x>

## Access status

The YouTube watch page could not be fetched by the available research tools, and web search did not return trustworthy title, transcript, creator, or scene descriptions for video ID `8qtUld9IjII`. No local reference video or image was included with this run. Accordingly:

- This document does **not** claim the video was watched.
- The following is a **target hypothesis derived from the written brief**.
- Exact object shape, palette, typography, timing, camera path, transitions, and mobile behavior remain unknown.

## Brief-derived visual target

The requested experience belongs to the cinematic product-storytelling family rather than a game or free-roaming 3D world. Its likely visual hierarchy is:

1. A single oversized hero object dominates the first viewport.
2. Dark or restrained environmental lighting creates metal, glass, emissive, and reflective cues.
3. Copy appears in timed stages around the object rather than competing with it at load.
4. Scroll behaves as a timeline controller: object transform and camera framing continue while headline, description, and CTA enter.
5. The page transitions from spectacle to a conventional readable marketing surface.

This pattern should be implemented as a **composed sequence with a fixed message**, not as unconstrained camera controls. The user should always know where to scroll, what to read, and what to do next.

## Visual grammar to preserve

| Trait | Production interpretation | Failure to avoid |
| --- | --- | --- |
| Cinematic scale | Hero object occupies roughly 45–75% of the visual field, with crop deliberately changing by stage. | Treating the 3D object as a small decorative icon. |
| Premium materials | A few excellent PBR materials, controlled roughness, reflection hierarchy, emissive accents, and carefully authored environment lighting. | Many generic glossy materials or random neon glows. |
| Depth | Foreground particles or geometry used sparingly, main object mid-ground, atmospheric background, and 2D copy on a stable plane. | Heavy depth-of-field or fog that harms text contrast. |
| Motion | Slow base motion plus scroll-linked transforms; easing used for state transitions, not to detach the object from scroll. | Constant fast rotation, wobble, or decorative motion without narrative purpose. |
| Parallax | Small pointer or gyroscope influence, clamped and disabled when reduced motion is requested. | Large camera movement that causes nausea or makes copy difficult to track. |
| Typography | Real DOM text with a strict width, high contrast, and deliberate left/right balance around the object. | Rasterized text inside the canvas or low-contrast copy over reflections. |
| Futuristic direction | Precision, light discipline, strong silhouette, and spatial transitions. | Generic blue-purple gradient, excessive glass cards, or “sci-fi HUD” clutter. |

## Proposed sequence for validation

The written brief defines a useful first storyboard:

| Scroll stage | Visual state | Content state | Suggested duration |
| --- | --- | --- | --- |
| 0 — Arrival | Poster immediately; 3D object resolves into the same first frame; subtle idle motion only. | Fixed navigation visible; no essential message hidden indefinitely. | 0–15% |
| 1 — Headline | Object shifts slightly right/back or camera reframes to create a left text safe area. | Left headline fades/translates in. | 15–38% |
| 2 — Explanation | Object rotates to a second hero angle; lighting accent changes subtly. | Right description appears after the headline is established. | 38–62% |
| 3 — Action | Object reaches a stable presentation angle; background contrast supports action. | CTA becomes visible and keyboard-focusable. | 62–82% |
| 4 — Release | Camera/object settles; pinned stage ends without a jump. | Next semantic section enters in normal document flow. | 82–100% |

Percentages are **recommendations**, not observations of the inaccessible reference.

## Art-direction questions still unresolved

- What is the exact hero object, and is it an abstract sculpture, device, logo, vehicle, or architectural form?
- Does the reference use true real-time reflections/refractions, baked textures, or pre-rendered media?
- Are the copy positions, nav labels, CTA wording, colors, and typeface visible in the source?
- Is scroll continuous or snapped? Is the stage pinned for more than one viewport?
- Does the object respond to pointer hover, drag, or device orientation?
- What behavior is shown on mobile?

These questions materially affect asset topology, shader work, camera framing, content layout, and the fallback plan. Before production, obtain one of: an accessible video file, 8–12 representative frame captures, or a written time-coded breakdown.

## Reference-handling recommendation

Turn the validated reference into a small “visual truth set” before code:

- first frame and loading/poster frame;
- each content reveal frame;
- the final frame before the next section;
- material closeups;
- desktop and mobile crop rules;
- motion notes including duration, easing, and scroll distance.

Figma is useful for annotating 2D overlays, typography, safe areas, and responsive frames, but it is not required to author the actual 3D scene. Blender or Spline should own 3D form/material exploration; a browser prototype should validate camera and scroll behavior.

