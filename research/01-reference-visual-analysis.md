# Reference visual analysis

**Research date:** 2026-08-31  
**Reference:** <https://youtu.be/8qtUld9IjII?si=K3WVvHT8Nnty7P1x>  
**Video:** “Build an Interactive 3D Website with AI (Step-by-Step)” by Profit Studio, 9:59

## Access and evidence status

The YouTube reference was opened in the interactive browser. Its full English transcript was exported and reviewed, and representative frames were inspected across the opening montage, template selection/remix, Spline Community browsing, Spline viewer export, Google AI Studio replacement, brand customization, and mobile correction.

Evidence labels in this document:

- **Observed:** visible in the video or stated by its narration.
- **Inference:** a cautious interpretation of the observed presentation.
- **Recommendation:** proposed for the separate, more ambitious written brief.
- **Unknown:** not established by the video.

## What the video actually is

The reference is a tutorial and workflow demonstration, not a continuous showcase of one canonical website. It opens with a montage of different interactive 3D hero designs, then builds a “Nova AI” example by combining a ready-made Google AI Studio template with a remixed Spline Community scene.

The narrated workflow is:

1. Choose a prepared 3D website template in Profit Studio.
2. Open it in Google AI Studio, continue past the third-party warning, remix it, name the copy, and launch it.
3. Find a mouse-responsive scene in Spline Community and remix it.
4. Set the Spline background to transparent, hide unwanted scene objects, disable orbit/pan/zoom controls, copy the viewer link, and update the viewer.
5. Insert that viewer URL into a prepared prompt and run it in Google AI Studio to replace the template's 3D element.
6. Use a second structured prompt to change brand, purpose, style, hero copy, feature content, and sections.
7. Inspect mobile and issue a mobile-only prompt to reduce the 3D element without changing desktop.
8. Follow a separate tutorial for deployment; deployment is not demonstrated in this video.

This is important: the reference supports a **template + Spline embed + AI customization** workflow. It does not prove that the shown sites use custom Three.js, React Three Fiber, WebGPU, Blender-authored assets, or a scroll-scrubbed render pipeline.

## Observed visual patterns

| Pattern | Observed evidence | Production implication |
| --- | --- | --- |
| Hero-first composition | The opening montage and chosen templates place one oversized 3D object or scene at the center/right of the first viewport. | Reserve a stable, large hero area and keep the first message short. |
| Mouse responsiveness | The narration explicitly distinguishes real websites from videos and selects a Spline scene because it reacts to the mouse. | Use restrained pointer-follow/look-at behavior; do not substitute a noninteractive video if this trait is essential. |
| Dark futuristic option | The AI/SaaS examples use dark backgrounds, high-contrast white type, subdued purple/blue glow, and a glossy robot-like focal object. | Keep the palette narrow and let silhouette, lighting, and negative space carry the premium feel. |
| Alternative art directions | The template gallery also includes cinematic/immersive and nature/editorial examples. | Do not treat “premium 3D” as one mandatory neon-SaaS style; choose one reference variant before production. |
| Minimal controls | The tutorial turns off orbit, pan, zoom, and related viewer controls. | Preserve authored composition and allow only controlled pointer response. |
| Transparent embed | The Spline background is set to zero opacity and unwanted floor geometry is hidden. | Integrate the scene with the page's CSS background rather than displaying it as a visibly boxed iframe/canvas. |
| Conventional page structure | The chosen template already contains a hero, feature sections, footer, and later an AI-added pricing section. | Keep page copy, navigation, CTA, and lower sections in semantic DOM; the 3D is a hero layer, not the entire information architecture. |
| Prompt-preserved consistency | The narration highlights that the added pricing section retains the template's visual style. | Give the AI explicit design tokens, component rules, and “preserve existing style” constraints. |
| Separate mobile treatment | The first mobile pass is acceptable except the 3D object is too large; a mobile-only prompt fixes its scale. | Treat mobile framing as its own art-directed state, not a uniformly scaled desktop scene. |

## Visual grammar worth preserving

| Trait | Interpretation grounded in the video | Failure to avoid |
| --- | --- | --- |
| Dominant focal object | One strong 3D object is sufficient; the narration explicitly advises against overloading the site with many 3D elements. | Multiple competing scenes, constant particles, or decorative objects in every section. |
| Strong silhouette | The focal object remains readable against a restrained background and large type. | Busy imagery or glow that erases the object's outline. |
| Controlled interaction | Pointer response adds life while authored framing remains intact. | Free orbit/pan/zoom that lets users break the composition. |
| Integrated compositing | Transparent scene background allows the DOM and 3D to share one visual surface. | A visible rectangular embed with a mismatched background. |
| Simple hierarchy | Short hero statement, supporting copy, compact actions, then conventional content sections. | Long paragraphs over moving geometry or essential text inside the canvas. |
| Consistent system | New sections inherit the same spacing, color, type, and component language. | AI-generated sections that look like unrelated templates. |

## What the video does not establish

- It does not show the written brief's staged sequence in which scroll reveals a left headline, then a right description, then a CTA while the camera and object continuously move.
- It does not expose the template source code or verify its framework, renderer, shaders, asset sizes, compression, loading strategy, accessibility, SEO, or production Core Web Vitals.
- It does not demonstrate reduced-motion behavior, keyboard access to the 3D interaction, screen-reader alternatives, WebGL context-loss recovery, or constrained-device fallbacks.
- It does not establish that the showcased Spline Community assets have licenses suitable for the eventual commercial project; licensing and attribution must be checked per asset.
- It does not demonstrate deployment in this clip.
- It does not identify one montage example as the exact target. A stakeholder still needs to select the intended design direction.

## Implication for the recommended implementation

Two scopes should be kept distinct:

### Faithful video-style MVP

Use a prepared React/Next.js or equivalent semantic page shell with one Spline viewer hero, transparent background, controlled pointer interaction, normal page scrolling, an immediate poster fallback, and separately authored mobile framing. This is the closest match to the workflow actually demonstrated and is the fastest path for an AI-assisted solo creator.

### Extended written-brief experience

Use the video as art-direction and workflow inspiration, but move to an owned Three.js/React Three Fiber scene with a GSAP/ScrollTrigger story timeline if the product truly requires precise scroll-linked camera states, renderer quality tiers, custom shaders, deterministic fallbacks, and deeper performance control. This is an extension beyond the demonstrated tutorial, not a direct reconstruction.

## Proposed scroll sequence for the written brief

| Scroll stage | Visual state | Content state | Suggested range |
| --- | --- | --- | --- |
| 0 — Arrival | Poster resolves to the same first 3D pose; subtle idle/pointer response only. | Fixed navigation; essential page identity available. | 0–15% |
| 1 — Headline | Object/camera reframes to create a left text safe area. | Left headline enters. | 15–38% |
| 2 — Explanation | Object rotates to a second authored angle with restrained lighting change. | Right description enters after the headline is established. | 38–62% |
| 3 — Action | Object reaches a stable product pose. | CTA becomes visible and keyboard-focusable. | 62–82% |
| 4 — Release | Camera and object settle; pinned stage releases without a jump. | Next semantic section enters normal document flow. | 82–100% |

These ranges are **recommendations derived from the written requirements**, not timings observed in the video.

## Remaining visual decisions

Before production, approve:

- the exact template/example from the montage to emulate;
- the hero object's subject, license, silhouette, material language, and interaction;
- whether Spline-level control is sufficient or the project needs an owned R3F renderer;
- desktop, tablet, mobile, and reduced-motion key frames;
- copy, navigation, CTA, palette, type system, and section inventory;
- whether the extended scroll sequence is a hard requirement or a separate creative enhancement.

Capture 8–12 approved key frames as a “visual truth set”: first/poster frame, each content state, final hero frame, material closeups, and desktop/mobile crop rules. Figma is useful for annotating the DOM overlays and safe areas; Spline or Blender should own 3D authoring, and a browser prototype should validate interaction and responsive framing.

