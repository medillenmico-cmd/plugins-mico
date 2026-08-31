# Performance, accessibility, and SEO

**Research date:** 2026-08-31

## Verified web targets

Google's current Core Web Vitals “good” thresholds, evaluated at the 75th percentile, are:

| Metric | Good threshold | Relevance to a 3D hero |
| --- | --- | --- |
| Largest Contentful Paint (LCP) | ≤ 2.5 s | The initial hero poster or headline is likely the LCP candidate; do not wait for the full 3D scene. |
| Interaction to Next Paint (INP) | ≤ 200 ms | Long JavaScript, asset decode, shader compilation, and frame-loop work can delay clicks/keyboard input. |
| Cumulative Layout Shift (CLS) | ≤ 0.1 | The canvas, poster, video, fonts, and pinned spacer need stable dimensions. |

Source: [web.dev Core Web Vitals thresholds](https://web.dev/articles/defining-core-web-vitals-thresholds).

These are field targets, not a guarantee from a single Lighthouse run. Segment real-user data by mobile/desktop and, where possible, capability tier.

## Proposed project budgets

The following are **starting recommendations**, not browser standards. Replace them with measured budgets after the gray-box prototype.

| Budget | Mobile starting target | Desktop starting target | Validation method |
| --- | --- | --- | --- |
| Initial critical experience | Semantic hero and compressed poster without waiting for 3D | Same | Network waterfall and LCP candidate inspection |
| 3D asset transfer | Aim for roughly 1–3 MB for the initial mobile hero tier | Aim for roughly 3–8 MB for the initial desktop hero tier | Compressed transfer plus repeat/cold load |
| Hero triangles | Roughly 50k–150k visible at once | Roughly 100k–300k visible at once | Renderer statistics plus GPU frame time |
| Draw calls | Prefer below ~60 | Prefer below ~100 | Renderer statistics; measure, do not optimize blindly |
| Texture dimensions | Mostly 512–1024; selective 2K | Mostly 1K–2K; selective 4K only with evidence | KTX2 GPU-memory estimate and visual comparison |
| Render pixel ratio | Cap around 1–1.5 | Cap around 1.5–2, adaptive | Frame time on high-DPR devices |
| Frame-rate goal | Stable 30 fps floor; 60 fps where affordable | Stable 60 fps on target hardware | CPU/GPU frame-time traces and thermal run |
| Long tasks | Avoid animation/load tasks over 50 ms | Same | Performance trace and INP diagnostics |

An excellent scene may exceed one budget and still perform well; a simple scene may miss INP because of unrelated JavaScript. Budgets must be evaluated together.

## Rendering and GPU strategy

MDN's WebGL guidance recommends budgeting VRAM, using smaller back buffers where acceptable, batching draw calls, compressed textures, mipmaps, and avoiding blocking production calls ([MDN WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices)). Apply that guidance through:

- Adaptive DPR/render scale based on sustained frame time, not one device check.
- Pausing or switching to on-demand rendering when the scene is settled or offscreen.
- One canvas and one main scene.
- Few materials, lights, shadow casters, transparent layers, and post-processing passes.
- GPU instancing for repeated geometry.
- Baked lighting/detail where camera motion allows it.
- Shader warm-up or controlled compilation after the poster is visible.
- Explicit disposal of geometries, textures, render targets, and event listeners.
- Handling `webglcontextlost` and retaining a designed fallback ([MDN event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/webglcontextlost_event)).

## Asset loading

### Initial load

- Server-render the title, headline, description, navigation, and CTA.
- Reserve hero aspect ratio/height in CSS before media arrives.
- Preload only the poster and truly critical fonts/assets.
- Dynamically import the 3D client boundary. Next.js documents dynamic imports/lazy loading as a way to reduce initial client JavaScript ([Next.js](https://nextjs.org/docs/app/guides/lazy-loading)).
- Begin 3D loading after the critical DOM/poster is paintable; delay higher tiers until capability and preference are known.
- Use a progress indicator only if it represents real progress; never block the whole page behind it.

### Models and textures

- Validate GLB/GLTF and all required extensions.
- Derive delivery variants from a canonical source.
- Use KTX2/Basis for GPU textures; Khronos explains that the format can reduce transfer and GPU memory by transcoding to supported formats ([KTX](https://www.khronos.org/ktx/)).
- Generate mipmaps and right-size textures based on screen-space use.
- Compare Draco and Meshopt decode cost on low-end mobile; compression trades transfer for decoder and CPU work.
- Lazy-load below-fold scenes or, preferably, avoid additional 3D scenes entirely.

### Video and sequences

- Use a poster and explicit width/height.
- Provide tested source formats and appropriate resolution/crop variants.
- Use `preload="metadata"` or `none` for non-critical video; web.dev describes poster/preload/lazy strategies for video ([video performance](https://web.dev/learn/performance/video-performance)).
- For sequences, preload a first-frame/key-frame subset before the remainder and cap decoded frames in memory.

## Adaptive quality tiers

Use a combination of feature detection, initial benchmark, viewport, DPR, memory signals where available, data-saving preference, and sustained frame time. Do not rely only on device model or user agent.

| Tier | Presentation |
| --- | --- |
| Static | Poster, DOM content, no pin; used for reduced motion, load failure, context loss, or severe constraints. |
| Media | Opaque short video or carefully constrained sequence; no transparent-video dependency. |
| Real-time low | Simplified GLB, lower DPR/textures, no expensive glass/refraction/post effects, 30 fps acceptable. |
| Real-time high | Full approved hero within measured budgets; optional higher-quality reflections/post effects. |
| Experimental WebGPU | Opt-in/automatic only after support and regression tests; always retains WebGL/media/static path. |

## Accessibility

### Motion

- Honor `prefers-reduced-motion`; MDN states that it detects a user's request to minimize non-essential motion and notes large scaling/panning as potential vestibular triggers ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion)).
- In reduced-motion mode, remove the multi-viewport pin, present content together, and use a static frame.
- Provide a pause/stop mechanism for qualifying long automatic motion. WCAG 2.2.2 covers moving content that starts automatically, lasts more than five seconds, and appears alongside other content ([W3C](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html)).
- Avoid rapid flashes, large camera swings, forced snap, and motion tied to every tiny wheel delta.

### Keyboard and focus

- Keep navigation, links, and CTA as native DOM elements with visible focus.
- Ensure focus scrolling works even if Lenis or a pinned stage is active.
- Do not put essential controls only inside WebGL hit-testing.
- Do not allow canvas pointer capture or overlays to block page controls.
- Preserve skip links and logical heading/reading order.

### Screen readers

- Treat decorative 3D as decorative; do not narrate every visual detail.
- Provide a concise text alternative when the object communicates product information.
- Keep product name, proposition, features, and CTA in semantic HTML.
- Announce load errors only if they affect functionality; a decorative fallback swap need not interrupt users.
- Avoid hidden duplicate DOM text used only to align with canvas visuals.

### Contrast and readability

- Define text-safe camera compositions and gradient/backplate behavior before animation.
- Verify contrast in every timeline state, not just the first frame.
- Prevent reflective highlights, bloom, or particles from crossing copy.
- Retain readable copy if the canvas is disabled.

## SEO and sharing

- Server-render a unique title, meta description, canonical URL, H1, visible product copy, and internal links.
- Use normal structured data only when it truthfully represents the page.
- Provide Open Graph/Twitter images from an approved hero frame rather than expecting crawlers to render WebGL.
- Do not hide core copy until a scroll animation completes; search engines and users need stable content.
- Use descriptive URLs and a normal page hierarchy. The 3D canvas should be progressive enhancement, not the information architecture.
- Test that script failure and no-WebGL modes retain indexable content.

## Thermal and battery impact

Continuous high-DPR rendering can keep CPU/GPU clocks elevated, particularly on phones and laptops. Mitigations:

- Stop rendering when offscreen, hidden, settled, or replaced by fallback.
- Lower resolution before removing core message content.
- Avoid continuous particle simulations and unnecessary video texture uploads.
- Use time-based animation; MDN warns that frame-count-based movement runs faster on high-refresh displays ([requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame)).
- Run 5–10 minute device tests, not only 10-second profiler captures.
- Record temperature/throttling symptoms, dropped frames, memory growth, and battery impact qualitatively if hardware power telemetry is unavailable.

## Test matrix

- Current Chrome/Edge, Safari on macOS/iOS, Firefox, and representative Android browsers.
- Low-end Android, recent iPhone, iPad/tablet, integrated-GPU Windows laptop, high-DPR Mac laptop, and one discrete-GPU desktop.
- Slow 4G/high latency, warm cache, cold cache, offline after initial visit where relevant.
- Normal motion and reduced motion.
- Keyboard-only, screen reader smoke test, zoom 200%, and high contrast/forced colors where applicable.
- Context-loss simulation, scene-load failure, missing codec, blocked autoplay, resize/orientation change, background/foreground, and back/forward navigation.

## Launch gate

Do not launch the real-time tier until field-oriented targets, real-device frame stability, reduced-motion behavior, fallbacks, keyboard access, and readable timeline states pass. A visually simpler tier that meets these criteria is more premium than a technically ambitious tier that stutters or blocks content.

