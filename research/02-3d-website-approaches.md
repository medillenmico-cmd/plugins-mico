# 3D website approaches

**Research date:** 2026-08-31

## Comparison

| Approach | Strengths | Weaknesses / requirements | Performance implications | Best use |
| --- | --- | --- | --- | --- |
| Real-time WebGL 3D | True camera, material, lighting, pointer, and state interaction; widely available relative to WebGPU. | Requires a rendering engine, optimized assets, GPU QA, fallbacks, and context-loss handling. | Continuous rendering competes for GPU, CPU, memory, battery, and main-thread time. | Signature hero object, configurator, spatial story, product demo. |
| Three.js | Mature scene graph, loaders, PBR materials, post-processing, WebGL 2 renderer, and emerging WebGPU renderer. | Imperative state and lifecycle need discipline; bundle and shader cost are still real. | Good when draw calls, texture memory, pixel ratio, and render cadence are controlled. | Custom, art-directed 3D with maximum web control. |
| React Three Fiber (R3F) | Declarative React integration, component composition, ecosystem, suspense/loading patterns, and shared app state. | React does not remove 3D complexity; careless re-renders or state updates in the frame loop can hurt performance. | R3F documents that scenes run in a game-like loop and recommends reuse, instancing, and on-demand rendering where possible ([R3F performance](https://r3f.docs.pmnd.rs/advanced/scaling-performance)). | React/Next.js teams building maintainable custom scenes. |
| Spline embed/viewer | Fast visual authoring, built-in interactions, scroll events, easy embedding, and low-code handoff. | Runtime and scene internals are less controllable; advanced optimization, custom shaders, observability, and graceful failure can be harder. | Acceptable for constrained scenes; generated or multi-object scenes can still be GPU-heavy. Spline itself warns that 3D uses more CPU/GPU than traditional 2D tools ([Spline FAQ](https://docs.spline.design/basics/faq)). | Prototype, small interactive illustration, no-code site, design-led proof of concept. |
| Blender model rendered in browser | Blender gives professional modeling, UV, animation, baking, and material workflow; GLB/GLTF is standard runtime delivery. | Blender materials, lights, modifiers, simulations, and compositing do not all transfer directly; assets must be exported and validated. | Quality depends more on export discipline than authoring tool. Runtime uses WebGL/WebGPU through an engine. | Premium custom object, product visualization, baked animations. |
| Pre-rendered video | Highest offline render quality, predictable art direction, simple playback, and low engineering complexity. | No true camera/object interaction; scroll scrubbing is less precise with a normal video; codecs and autoplay policies matter. | Hardware decoding can be efficient, but large video can dominate transfer and LCP. Use poster/preload strategy ([web.dev video performance](https://web.dev/learn/performance/video-performance)). | Cinematic hero where interactivity is secondary. |
| Image sequence | Frame-perfect scroll scrubbing and offline-rendered quality; no video seek ambiguity. | Many files or a large atlas, decoded image memory, preloading logic, and responsive variants. | Network and memory can become worse than video; canvas draw and decode must be scheduled carefully. | Apple-like scroll-scrubbed product reveal, deterministic transitions. |
| Transparent WebM | Alpha-composited motion over live DOM/background with smaller implementation surface than real-time 3D. | Alpha support is not universal; MDN explicitly notes Safari lacks VP9/WebM alpha support. Edge halos and encoding artifacts are common. | Video decode plus compositing; often efficient but still a large hero asset. | Enhancement with an opaque or static fallback, never the only path. |
| WebGPU experience | Modern GPU model, compute support, more advanced pipelines, and potential scaling for demanding scenes. | MDN marks WebGPU limited availability and HTTPS-only; shader/tooling path differs from WebGL. | Potential gains are scene- and implementation-specific; initialization and pipeline compilation still need management. | Opt-in high-end enhancement, experimental art, compute-heavy rendering. |
| Hybrid 2D + 3D | Keeps content semantic and readable while concentrating GPU cost in one intentional moment. Supports fallbacks cleanly. | Requires careful layering, synchronization, and shared responsive rules. | Best opportunity to meet Core Web Vitals because 3D can be delayed, capped, or omitted. | **Recommended for the stated SaaS/technology marketing target.** |

## Clarifying the terms

“Real-time WebGL,” “Three.js,” “R3F,” and “Blender model in browser” are not mutually exclusive:

```text
Blender-authored GLB asset
        ↓
Three.js renderer (WebGL 2 baseline)
        ↓
React Three Fiber scene components
        ↓
Next.js/React page with DOM content
```

Spline is an alternative authoring/runtime path. Video and image sequences are pre-rendered paths. WebGPU is a rendering-backend choice, not a design style.

## Technical requirements by family

### Real-time family

- A client-only canvas and feature detection.
- A deterministic loading state and poster.
- GLB/GLTF loader plus Draco, Meshopt, and/or KTX2 decoders when those extensions are used.
- Scene budgets for draw calls, triangles, texture memory, shaders, post-processing, and pixel ratio.
- Lifecycle cleanup, resize handling, visibility pausing, and WebGL context-loss behavior. MDN documents the `webglcontextlost` event for drawing-buffer loss ([MDN context lost](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/webglcontextlost_event)).
- A mobile/reduced-motion fallback that does not depend on the canvas.

### Pre-rendered family

- A media matrix: codec/container, resolution, DPR, mobile crop, poster, and opaque fallback.
- A tested preload policy. A hero that autoplays and a below-fold video should not use the same policy.
- Time-to-scroll mapping for sequences, or a playback plan for normal video.
- Alternative text and semantic content outside the media.

### Hybrid family

- Clear ownership: DOM for content and controls; canvas/media for imagery.
- Stable layout dimensions before any asset loads.
- One scroll progress source shared with 3D and DOM choreography.
- Z-index, pointer-event, focus, and contrast rules.

## Recommendation

Use the hybrid family with a custom Three.js/R3F hero when the object must respond to scroll and pointer input. Use a pre-rendered video MVP first if the schedule or 3D skill is uncertain. Keep WebGPU and Spline as evaluated alternatives rather than default dependencies.

