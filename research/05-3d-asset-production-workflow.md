# 3D asset production workflow

**Research date:** 2026-08-31

## Recommended workflow for an AI-assisted solo creator

Use **AI for breadth and Blender for truth**:

1. Define the hero silhouette, material story, camera-safe angles, and animation beats with sketches or generated concept images.
2. Generate a rough mesh only if it saves blocking time; otherwise model directly in Blender.
3. Rebuild or clean topology, scale, normals, pivots, UVs, and material boundaries in Blender.
4. Author a small PBR material set and bake complex procedural detail/lighting where possible.
5. Animate only the properties required by the scroll story; keep the camera path primarily in the web scene unless baked camera motion is essential.
6. Export a canonical uncompressed GLB/GLTF, validate it, then derive web variants reproducibly.
7. Compress textures to KTX2/Basis, reduce meshes where visually safe, and test decoders on target browsers.
8. Produce a matching poster and opaque video fallback from the same camera, grade, and lighting.

This hybrid workflow preserves premium quality because a human controls the visible silhouette and surface response, while AI accelerates ideation and first-pass geometry.

## Workflow options

| Workflow | Quality potential | Time/cost | Main risk | Recommendation |
| --- | --- | --- | --- | --- |
| Manual Blender modeling | Highest control and cleanest topology | Highest skill/time | Slow iteration for a solo creator | Best for simple iconic objects and final cleanup. |
| Text-to-3D | Fast exploration | Low initial effort | Generic silhouette, messy topology/UVs, baked lighting artifacts | Use for thumbnails/rough props, not final hero without cleanup. |
| Single image-to-3D | Useful when a concept frame exists | Fast | Hidden sides are invented; proportions and depth can drift | Use as blocking mesh and reference. Spline recommends a front-facing single object ([Spline AI](https://docs.spline.design/generate/ai-3d-generation)). |
| Multi-view image-to-3D | Better geometric constraint | Moderate preparation | Views may be inconsistent; cleanup remains | Stronger AI starting point when consistent turnarounds are available. |
| AI texture generation on clean mesh | Can accelerate surface exploration | Moderate | Lighting/shadows may be baked incorrectly; seams and PBR values may be implausible | Useful after UV cleanup, with material review. |
| Pre-rendered AI video | Fast atmospheric concept | Low coding effort | Temporal inconsistency, object mutation, hard-to-loop motion, no true interaction | Use as mood test or fallback only after frame consistency review. |

## Blender production checklist

### Geometry

- Set real and consistent scale.
- Apply transforms where the runtime contract expects them.
- Place pivots/origins around intended rotation points.
- Fix flipped normals, non-manifold geometry, duplicate vertices, and hidden interior faces.
- Retopologize or decimate while preserving silhouette and shading.
- Split meshes by actual material/animation need, not arbitrary modeling history.
- Use instancing for repeated parts and avoid unique duplicates.

### Materials and lighting

- Prefer a few physically plausible PBR materials over many unique shaders.
- Pack metallic/roughness/occlusion consistently with the target loader.
- Bake procedural nodes or unsupported material behavior to textures.
- Use reflection probes/environment maps deliberately; realistic glass is sensitive to scene context and sorting.
- Separate emissive accents from broad bloom. Bloom should support, not create, the design.
- Validate the export in a neutral glTF viewer and the actual browser renderer; Blender viewport parity is not guaranteed.

### Animation

- Use named animation clips only when baked skeletal/object animation is useful.
- Keep scroll-controlled transforms in the runtime when they must align exactly with DOM beats.
- Reduce animation keyframes after visual validation.
- Confirm interpolation, loop seams, start/end pose, pivot behavior, and clip duration after export.

## GLB/GLTF export

Khronos positions glTF as a runtime 3D asset-delivery format, and Blender provides a glTF 2.0 export workflow ([Khronos glTF](https://www.khronos.org/gltf/), [Blender glTF exporter](https://docs.blender.org/manual/en/latest/addons/import_export/scene_gltf2.html)).

Recommended artifacts:

- `hero-source.blend`: editable source and linked textures.
- `hero-canonical.glb`: validated, visually correct master without destructive delivery compression.
- `hero-desktop.glb`: optimized desktop delivery variant.
- `hero-mobile.glb`: simplified geometry/material/texture variant, if real-time mobile is retained.
- `hero-poster.avif` and WebP/JPEG fallback.
- `hero-fallback.webm` plus MP4 as required by the browser matrix.
- An asset manifest recording source hashes, dimensions, extensions, triangle/draw-call counts, texture memory estimates, and compression settings.

## Compression and optimization

### Geometry

Google describes Draco as an open-source library for compressing meshes and point clouds for storage/transmission ([Draco](https://google.github.io/draco/)). Compression reduces transfer size but adds decoder payload and decode work. Compare Draco and Meshopt on the actual hero rather than assuming one is universally better. Preserve a canonical source because compression is a delivery transform.

Recommended sequence:

1. Remove unseen geometry and merge or instance repeated parts.
2. Reduce topology based on silhouette and screen-space size.
3. Quantize attributes within an approved visual tolerance.
4. Apply geometry compression.
5. Record decode time on representative mobile devices.

### Textures

KTX2 with Basis Universal can reduce both downloaded size and GPU-memory pressure by transcoding to a device-supported compressed format ([KTX](https://www.khronos.org/ktx/), [KHR_texture_basisu](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_texture_basisu)).

- Use ETC1S where smaller transfer is more important and artifacts are acceptable.
- Use UASTC for normal maps or high-quality surfaces where block artifacts are visible.
- Generate mipmaps.
- Keep mobile texture dimensions lower than desktop when the visual difference is negligible.
- Use AVIF/WebP for 2D posters; they are not replacements for GPU-compressed 3D textures.

### Lighting and reflections

Bake static shadowing and complex surface detail when it survives camera movement. Keep only the few dynamic lights required to sell motion. Real-time reflections, refraction, screen-space effects, and large HDR environments can dominate performance; prototype them before the asset is finalized.

## Transparent video alternative

If the hero motion is fixed, render the same Blender scene to opaque WebM/MP4 and composite it as a background or contained media element. Transparent WebM is useful only with a tested alternate source because Safari does not support VP9/WebM alpha per MDN ([codec guide](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs)). An opaque video can often preserve premium reflections more reliably across browsers.

## Turning AI-generated video into a seamless hero

1. Generate a short shot with a locked camera description and a simple, reversible motion.
2. Reject outputs where geometry, logos, edges, materials, or light sources mutate across frames.
3. Choose a loop point with matching pose, velocity, exposure, and background.
4. Stabilize, retime, grade, and repair the seam in a video tool.
5. Export multiple codec/resolution variants plus a poster.
6. Test first/last frame, pause/restart, autoplay policy, reduced motion, and battery use.

AI video is most feasible for abstract ambience. It is risky for a recognizable product that must remain dimensionally and brand accurate.

## Acceptance criteria for the hero asset

- Reads clearly as a silhouette at mobile size.
- No visible seams, flipped normals, broken tangents, texture bleed, or unsupported-material surprises.
- Matches approved reference frames in the production renderer.
- Loads and decodes within the agreed budgets on a representative mobile device.
- Uses an approved draw-call, triangle, texture-memory, and shader budget recorded as project targets rather than universal standards.
- Has a visually matched poster and fallback.
- Source, canonical export, optimized variants, and licenses/provenance are documented.

