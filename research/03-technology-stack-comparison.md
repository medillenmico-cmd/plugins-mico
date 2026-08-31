# Technology stack comparison

**Research date:** 2026-08-31

## Recommended stack

| Concern | Default | Decision rationale |
| --- | --- | --- |
| Application shell | Next.js + React + TypeScript | Useful for routing, metadata, server-rendered/streamed DOM, asset handling, and a maintainable component model. Lazy-load the 3D client component; Next.js documents `next/dynamic` and React lazy/Suspense as ways to reduce initial client JavaScript ([Next.js lazy loading](https://nextjs.org/docs/app/guides/lazy-loading)). |
| Renderer | Three.js WebGL 2 | Broadest practical baseline and complete control. Three.js states its WebGL renderer uses WebGL 2 ([docs](https://threejs.org/docs/pages/WebGLRenderer.html)). |
| React integration | React Three Fiber | Good fit when the rest of the page is React and the scene benefits from reusable components/state. Not necessary for a tiny isolated scene. |
| Helpers | Drei, selectively | Useful loaders, environments, controls, staging, and performance helpers. Avoid importing helpers merely for convenience if they add runtime or obscure control. |
| Scroll timeline | GSAP + ScrollTrigger | Pin/scrub/labels are first-class concepts and match the multi-stage hero ([ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)). |
| DOM animation | Motion for React | Use for hover, focus, presence, and layout transitions outside properties controlled by GSAP ([Motion](https://motion.dev/docs/react)). |
| Smooth scroll | Native; optionally Lenis | Lenis is purpose-built for WebGL synchronization, but only add it if testing shows a benefit and native keyboard/touch/anchor behavior remains correct ([Lenis](https://github.com/darkroomengineering/lenis)). |
| 3D authoring | Blender | Professional modeling, UV, animation, texture baking, and glTF export. The official glTF exporter supports the runtime format and geometry compression options ([Blender glTF manual](https://docs.blender.org/manual/en/latest/addons/import_export/scene_gltf2.html)). |
| Asset format | GLB/GLTF + KTX2/Basis; optional Draco/Meshopt | glTF is designed for runtime delivery. KTX2 reduces transfer and GPU memory by transcoding to device formats ([Khronos KTX](https://www.khronos.org/ktx/)). |
| Shader language | GLSL for WebGL-specific custom effects; TSL/WGSL only when WebGPU path is justified | Custom shaders can create premium refraction, emissive, noise, and transition effects, but they raise portability and maintenance cost. |
| Small vector motion | Rive or Lottie, only outside the hero 3D | Better for UI icons/illustrations than for a realistic hero. Rive state machines can settle and stop advancing when idle ([Rive](https://rive.app/docs/runtimes/web/state-machines)); Lottie is suited to exported vector motion. |

## Suitability notes

### Next.js, React, and TypeScript

They solve application structure, not 3D quality. Their value is keeping metadata, headings, links, CTA, responsive layout, analytics, and fallbacks normal web content while isolating the expensive scene. The canvas should be a client boundary; the rest of the hero should be renderable without it.

Use React state for coarse application states—loading, quality tier, active story stage—not for every-frame transforms. Frame-loop values belong in refs/renderer state to avoid unnecessary component updates.

### Three.js vs. R3F

- Choose **plain Three.js** for a self-contained canvas with a small team already comfortable with imperative rendering.
- Choose **R3F** for a React product where scene parts, state, suspense, responsiveness, and reuse matter.
- Neither option reduces the need for Blender, lighting judgment, shader knowledge, or profiling.

### Drei

Use selected helpers such as GLTF loading, environment setup, bounds, adaptive DPR/performance monitoring, and HTML overlays when they reduce well-understood boilerplate. Avoid default-heavy abstractions that make exact camera, material, or cleanup behavior harder to reason about.

### GSAP/ScrollTrigger vs. Motion

Use **one master owner** for each animated property:

- GSAP/ScrollTrigger owns pinned progress, camera position, object rotation/position, section opacity/translation during the hero sequence.
- Motion owns local button/card hover, focus, presence, and later-page micro-interactions.

Do not let both libraries write the same transform or opacity. ScrollTrigger documents pinning and scrub directly, including the warning not to animate the pinned element itself; animate children instead ([ScrollTrigger pinning](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)).

### Lenis and smooth-scroll alternatives

Native scroll is the accessibility and reliability baseline. Lenis can improve the feel of scroll-to-WebGL synchronization, but it must preserve wheel, touch, keyboard, anchors, browser history, focus scrolling, and reduced motion. CSS `scroll-behavior`, ScrollTrigger's own scrub smoothing, or no smoothing may be sufficient.

### Spline

Spline is suitable when speed of authoring and designer control matter more than runtime ownership. Its native viewer can react to global page scroll/mouse events, unlike a plain iframe ([Spline Viewer](https://docs.spline.design/exporting-your-scene/web/exporting-as-spline-viewer)). For the premium hero target, run a spike comparing load size, steady-state frame time, mobile thermals, interaction hooks, fallback behavior, and brand-removal/license requirements before adoption.

### WebGL, WebGPU, GLSL

- **WebGL 2:** production baseline.
- **WebGPU:** optional high-end renderer or future migration. MDN currently marks it limited availability and HTTPS-only ([MDN WebGPU](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API)).
- **GLSL:** appropriate for focused visual effects, but every custom fragment shader increases fill-rate and QA risk. MDN recommends doing work in the vertex shader where visually acceptable and lowering back-buffer resolution as a straightforward performance tradeoff ([MDN WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices)).

### Lottie and Rive

These are complementary 2D motion tools, not replacements for a physically lit 3D hero. Use them for small diagrams, onboarding cues, icons, or stateful illustrations. If the brand needs responsive interactive vector animation, prefer Rive; if the source workflow is After Effects/bodymovin and interaction is simple, Lottie is often sufficient.

### WebM and image sequences

Use opaque WebM/MP4 for a reliable cinematic fallback. Use transparent WebM only as an enhancement because Safari's alpha limitation is documented by MDN ([codec guide](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs)). Use an image sequence only when frame-exact scroll control justifies its request/decode/memory cost.

## Technologies not recommended by default

- A second scroll-controller library in addition to ScrollTrigger.
- A physics engine for purely choreographed hero movement.
- A full game engine or Unity WebGL export for a marketing hero.
- Multiple simultaneous WebGL canvases.
- WebGPU-only shaders without an equivalent fallback.
- Real-time ray tracing for a landing page.
- Heavy post-processing chains used to compensate for weak materials or lighting.

## Final stack decision

Start with Next.js/React/TypeScript, a dynamically loaded R3F scene on Three.js WebGL 2, a single GSAP/ScrollTrigger timeline, Blender-authored GLB assets with KTX2 textures, and static/video fallbacks. Add Drei, Motion, Lenis, custom GLSL, Spline, or WebGPU only when a measured requirement justifies each one.

