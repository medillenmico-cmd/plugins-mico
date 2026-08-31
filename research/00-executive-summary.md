# Executive summary

**Research date:** 2026-08-31  
**Scope:** Research and planning for a premium, cinematic, scroll-controlled 3D marketing website. No website or application code was produced.

## Main conclusion

The strongest implementation for the stated visual target is a **progressively enhanced hybrid**: semantic HTML and CSS provide the message, navigation, CTA, SEO, and accessibility; a single optimized real-time 3D scene provides the hero object and scroll-linked camera/object movement on capable devices; and a high-quality poster or pre-rendered video provides an immediate and dependable fallback. This preserves the feeling of a premium 3D experience without making the entire page dependent on a GPU canvas.

The recommended baseline is **WebGL 2 with Three.js through React Three Fiber**, not WebGPU-only. Three.js currently documents `WebGLRenderer` as WebGL 2, while MDN still marks WebGPU as limited availability; Three.js's WebGPU renderer can fall back to WebGL 2, but it should be treated as an enhancement until the target-browser matrix proves otherwise ([Three.js WebGLRenderer](https://threejs.org/docs/pages/WebGLRenderer.html), [Three.js WebGPURenderer](https://threejs.org/manual/en/webgpurenderer), [MDN WebGPU](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API)).

## Recommended implementation

| Layer | Recommendation | Why |
| --- | --- | --- |
| Page shell | Next.js, React, TypeScript, semantic DOM | Strong routing/rendering/tooling while keeping copy and navigation outside the canvas. |
| 3D runtime | Three.js + React Three Fiber + selected Drei helpers | Full control over a cinematic GLB/GLTF scene with React integration; R3F documents performance scaling for the continuous render loop ([R3F scaling performance](https://r3f.docs.pmnd.rs/advanced/scaling-performance)). |
| Scroll choreography | One GSAP timeline with ScrollTrigger | ScrollTrigger directly supports pinning, scrubbing, snapping, and timeline labels; one owner avoids animation conflicts ([ScrollTrigger docs](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)). |
| DOM micro-motion | Motion for React, limited to elements GSAP does not control | Useful for hover, focus, presence, and small layout transitions; its official API supports both triggered and scroll-linked motion ([Motion docs](https://motion.dev/docs/react)). |
| Smooth scrolling | Native scroll first; Lenis only after user testing | Lenis is designed for WebGL synchronization and parallax, but it adds another motion/scroll layer and is not necessary for the target ([Lenis repository](https://github.com/darkroomengineering/lenis)). |
| 3D production | Blender-authored hero, with AI used for concepts or rough meshes; human cleanup and art direction | AI generation can accelerate exploration, but premium silhouette, topology, UVs, materials, reflections, and animation still need deliberate review. |
| Delivery format | GLB/GLTF, reduced geometry, baked PBR textures, KTX2/Basis textures, optional geometry compression | glTF is designed for runtime asset delivery; KTX2/Basis reduces transmission and GPU-memory pressure ([Khronos glTF](https://www.khronos.org/gltf/), [KTX](https://www.khronos.org/ktx/)). |
| Fallback | Responsive poster and opaque MP4/WebM; static DOM version for reduced motion | Transparent WebM must not be the sole fallback because MDN notes Safari does not support alpha transparency for VP9/WebM ([MDN video codecs](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs)). |

## Why not the alternatives as the default

- **Spline-only:** fastest for prototyping and embeds, and its viewer can receive global scroll/mouse events, but it offers less control over asset loading, rendering budgets, advanced shaders, and failure recovery than an owned Three.js scene ([Spline Viewer](https://docs.spline.design/exporting-your-scene/web/exporting-as-spline-viewer)).
- **Pre-rendered-only video:** gives maximum offline render quality and predictable playback, but cannot provide true object interaction, camera response, or material changes. It is an excellent fallback and a valid MVP.
- **Image sequence:** offers deterministic scroll scrubbing and high visual fidelity, but can create many requests, substantial decoded-memory use, and complex responsive delivery.
- **Transparent WebM:** visually convenient in supporting browsers, but alpha support is not dependable enough for the only hero path.
- **WebGPU-only:** promising for compute-heavy scenes, but not a safe baseline while MDN marks it non-Baseline/limited availability.

## Practical quality strategy

1. Make the first viewport useful before 3D loads: fixed navigation, real headline/description/CTA in the DOM, fixed hero dimensions, and a poster that matches the first 3D frame.
2. Load one deliberately constrained hero scene, not a virtual world. Prefer baked lighting, a small material set, instancing for repeated geometry, limited post-processing, and adaptive render scale.
3. Map scroll to a finite labeled story: object-first, headline, description, CTA, then release the pinned stage.
4. Keep native scrolling and keyboard access intact. Honor `prefers-reduced-motion`, which MDN describes as a request to remove, reduce, or replace non-essential motion ([MDN reduced motion](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion)).
5. Measure real devices and field data. The current “good” Core Web Vitals thresholds are LCP no more than 2.5 seconds, INP no more than 200 ms, and CLS no more than 0.1 at the 75th percentile ([web.dev thresholds](https://web.dev/articles/defining-core-web-vitals-thresholds)).

## Decision

Proceed eventually with a **hybrid R3F/WebGL hero plus DOM storytelling and media/static fallbacks**. Use AI and Codex aggressively for architecture, implementation, testing, and optimization assistance, but reserve final art direction, model cleanup, lighting, motion feel, and cross-device sign-off for a human designer/developer and, if realism is central to the brand, a professional 3D artist.

## Important limitation

The supplied YouTube URL could not be fetched, and no transcript or reliable metadata was available through search. No local visual media accompanied the prompt. Therefore the visual direction in this research is based on the explicit written target, not a claimed frame-by-frame analysis of the video. See [01-reference-visual-analysis.md](./01-reference-visual-analysis.md).

