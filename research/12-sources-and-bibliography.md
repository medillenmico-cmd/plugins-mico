# Sources and bibliography

**Research conducted:** 2026-08-31  
**Method:** Current public web research prioritizing official documentation, browser-vendor/platform documentation, primary specifications, author case studies, and official product pages. Repository workflow references were inspected through the selected GitHub connection.

## Evidence labels used in this research

- **Verified fact:** Directly supported by a cited source.
- **Technical inference:** A reasoned conclusion from architecture/observable behavior; not presented as confirmed implementation detail.
- **Recommendation:** A proposed choice or numeric project budget; not a standard or measured result for this future site.
- **Unknown:** Information that could not be accessed or verified.

## Reference access

- Supplied YouTube reference: <https://youtu.be/8qtUld9IjII?si=K3WVvHT8Nnty7P1x>
- **Status:** Opened in the interactive browser on 2026-08-31. The full 9:59 English transcript was exported and reviewed, and representative frames were inspected at the opening, template-remix, Spline-community, Spline-export, and AI-customization stages.
- **Verified metadata:** “Build an Interactive 3D Website with AI (Step-by-Step),” Profit Studio.
- **Content used as reference evidence:** the four-step workflow stated in the video; its on-screen template examples; Spline Community remix and viewer-export settings; Google AI Studio remix/prompt workflow; and the demonstrated mobile-only size correction.
- No local video or image reference was supplied with the rerun.

## OpenAI and Codex

- [OpenAI/ChatGPT use cases](https://learn.chatgpt.com/use-cases) — official examples for codebase understanding, building, testing, games, deployment, documentation, and other agent workflows.
- [OpenAI Developers home](https://developers.openai.com/) — official description of Codex as a coding agent and entry point to current documentation.
- [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model) — official guidance on multi-step agent autonomy and explicit action boundaries.

## Web rendering and browser platform

- [Three.js WebGLRenderer](https://threejs.org/docs/pages/WebGLRenderer.html) — WebGL 2 renderer API and behavior.
- [Three.js WebGPURenderer manual](https://threejs.org/manual/en/webgpurenderer) — WebGPU renderer and documented WebGL 2 fallback.
- [Three.js WebGPU capability](https://threejs.org/docs/pages/WebGPU.html) — feature detection.
- [MDN WebGPU API](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API) — limited-availability and secure-context status.
- [MDN WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices) — VRAM budgeting, back-buffer scale, batching, textures, shader and API guidance.
- [MDN WebGL context-lost event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/webglcontextlost_event) — context-loss behavior.
- [MDN requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame) — refresh timing, background behavior, and time-based animation warning.
- [Khronos WebGL specification](https://registry.khronos.org/webgl/specs/latest/1.0/) — primary WebGL specification.

## React and application architecture

- [Next.js lazy loading](https://nextjs.org/docs/app/guides/lazy-loading) — dynamic client imports and Suspense patterns.
- [React Three Fiber performance scaling](https://r3f.docs.pmnd.rs/advanced/scaling-performance) — render-loop, reuse, instancing, and on-demand considerations.
- [Motion for React](https://motion.dev/docs/react) — gestures, layout animation, scroll-triggered and scroll-linked animation.
- [Motion scroll animations](https://motion.dev/docs/react-scroll-animations) — `useScroll` and scroll progress.

## Scroll and motion

- [GSAP ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/) — pin, scrub, snap, labels, callbacks, and pinning guidance.
- [Lenis](https://github.com/darkroomengineering/lenis) — official project documentation for smooth scrolling and WebGL synchronization.
- [MDN prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion) — user preference and vestibular-motion context.
- [W3C WCAG 2.2 — Pause, Stop, Hide](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html) — official explanation of moving/auto-updating content requirements.

## 3D formats and asset optimization

- [Khronos glTF](https://www.khronos.org/gltf/) — runtime 3D delivery and ecosystem.
- [glTF 2.0 specification](https://registry.khronos.org/glTF/specs/2.0/glTF-2.0.pdf) — primary format specification.
- [Blender glTF 2.0 exporter manual](https://docs.blender.org/manual/en/latest/addons/import_export/scene_gltf2.html) — export and material/animation behavior.
- [Khronos KTX](https://www.khronos.org/ktx/) — KTX2/Basis Universal purpose, transmission, GPU-memory and transcoding rationale.
- [KHR_texture_basisu](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_texture_basisu) — ratified glTF texture extension.
- [KTX 2.0 developer guide](https://github.com/KhronosGroup/3D-Formats-Guidelines/blob/main/KTXDeveloperGuide.md) — ETC1S/UASTC and runtime concepts.
- [Google Draco](https://google.github.io/draco/) — mesh and point-cloud compression.
- [glTF Transform](https://gltf-transform.dev/) — asset inspection, optimization, and transform toolchain.

## Media and 2D animation

- [MDN web video codec guide](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs) — codec/container guidance and Safari VP9 alpha limitation.
- [MDN video element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video) — native video element, sources, poster, loop, and controls.
- [web.dev video performance](https://web.dev/learn/performance/video-performance) — poster, preload, lazy loading, and LCP considerations.
- [MDN Media Capabilities](https://developer.mozilla.org/en-US/docs/Web/API/Media_Capabilities_API/Using_the_Media_Capabilities_API) — checking whether decoding is supported, smooth, and power efficient.
- [Lottie Web renderer settings](https://github.com/airbnb/lottie-web/wiki/Renderer-Settings) — SVG/canvas renderer settings and progressive loading.
- [Rive web state machines](https://rive.app/docs/runtimes/web/state-machines) — playback, pause/stop, and settled-state performance behavior.

## Spline and AI-assisted 3D

- [Spline Viewer export](https://docs.spline.design/exporting-your-scene/web/exporting-as-spline-viewer) — viewer embedding and global/local events.
- [Spline Viewer demos](https://viewer.spline.design/) — scroll, orbit, follow, look-at, and framework integration examples.
- [Spline play settings](https://docs.spline.design/exporting-your-scene/play-settings) — transparency and performance/export controls.
- [Spline FAQ](https://docs.spline.design/basics/faq) — browser/GPU requirements.
- [Spline AI 3D generation](https://docs.spline.design/generate/ai-3d-generation) — text/image-to-3D workflow and generated-model performance warning.
- [Meshy image-to-3D guide](https://www.meshy.ai/tutorials/api-quickstart-image-to-3d) — export formats, textures, and PBR options.
- [Meshy official documentation](https://docs.meshy.ai/en) — generation, texturing, remeshing, animation, and exports.
- [Tripo model conversion](https://developers.tripo3d.ai/en/docs/models-convert) — GLTF conversion, texture size, and baking options.
- [Tripo generation documentation](https://platform.tripo3d.ai/docs/generation) — text/image/multiview generation parameters.

## Performance, accessibility, and SEO

- [web.dev Core Web Vitals threshold methodology](https://web.dev/articles/defining-core-web-vitals-thresholds) — LCP, INP, CLS thresholds and 75th-percentile evaluation.
- [web.dev LCP](https://web.dev/articles/lcp) — LCP definition and measurement guidance.
- [web.dev Web Vitals](https://web.dev/articles/vitals) — current stable metric set.
- [MDN Web Performance](https://developer.mozilla.org/en-US/docs/Web/Performance) — browser performance overview.
- [MDN animation performance and frame rate](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Animation_performance_and_frame_rate) — frame pipeline and animation performance.

## Case studies and examples

- [Bruno Simon portfolio/behind the scenes](https://bruno-simon.com/?s=03) — author-disclosed Three.js/WebGL/WebGPU/Blender/source details.
- [Active Theory v5](https://v5.activetheory.net/) — live WebGL portfolio surface.
- [Active Theory — Webby Crafted with Code](https://www.webbyawards.com/crafted-with-code/active-theory/) — author case study identifying WebGL and Hydra.
- [ERA — Vide Infra case study](https://videinfra.com/blog/case-study-a-triple-site-of-the-day-winner-powered-by-webgl) — Three.js/WebGL interactive map.
- [More Than a Portfolio — Codrops](https://tympanus.net/codrops/2026/04/28/more-than-a-portfolio-building-a-scroll-driven-3d-world-with-something-to-say/) — author-declared Three.js, GSAP, Blender, KTX2, instancing, shaders, and Draco workflow.
- [84—24 — Codrops](https://tympanus.net/codrops/2024/04/08/case-study-84-24/) — GLB, Three.js, GSAP, and standard-scroll integration.
- [Crafting Scroll Based Animations in Three.js — Codrops](https://tympanus.net/codrops/2022/01/05/crafting-scroll-based-animations-in-three-js/) — hybrid DOM/WebGL scroll tutorial.
- [NASA's Eyes](https://science.nasa.gov/eyes/) and [FAQ](https://science.nasa.gov/eyes/faq/) — browser-based real-time 3D and CAD-to-lightweight-web-model workflow.
- [Codrops Creative Hub](https://tympanus.net/codrops/hub/all/) — tagged technique demos and source references.

## Repository workflow references inspected

The following files in `medillenmico-cmd/plugins-mico` were used as workflow guidance, not as technical evidence for browser/library claims:

- `plugins/product-design/skills/research/SKILL.md` — source-grounded research, evidence/inference separation, and limitation disclosure.
- `plugins/build-web-apps/skills/frontend-app-builder/SKILL.md` — full-surface design definition, responsive/motion/accessibility expectations, browser verification, and fidelity gates.
- `plugins/build-web-apps/skills/react-best-practices/SKILL.md` — bundle, rendering, hydration, event, and performance priorities.

Figma was not invoked because the deliverable was research Markdown and no Figma file or design-editing task was supplied. It remains recommended for later annotation of approved responsive key frames and text-safe areas.

## Known uncertainties

- Which of the several template/example websites shown in the YouTube montage is the intended visual target.
- The underlying source code, renderer internals, asset sizes, and production performance of the websites shown in the video; the video demonstrates the authoring workflow but does not expose those details.
- The eventual hero object's geometry, materials, animation, and brand constraints.
- Target audience/device distribution, analytics, hosting/CDN, browser support policy, and performance baselines.
- Whether mobile must retain real-time 3D or may use a media/static alternative.
- Whether transparent compositing is visually required.
- Final library versions and licensing/pricing at implementation time; these must be rechecked immediately before production.

