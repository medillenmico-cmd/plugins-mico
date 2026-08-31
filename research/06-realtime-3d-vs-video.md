# Real-time 3D versus video

**Research date:** 2026-08-31

## Decision matrix

Ratings are relative for the stated cinematic hero, not universal scores.

| Criterion | Real-time 3D | Pre-rendered opaque video | Transparent WebM | Image sequence | Hybrid |
| --- | --- | --- | --- | --- | --- |
| Visual quality ceiling | High, constrained by browser GPU and real-time budget | Very high; offline renderer | Very high, but alpha/edge encoding can degrade | Very high; exact offline frames | Very high where it matters |
| True interaction | Full | None beyond playback | None beyond playback | Scroll frame selection only | Real-time on capable devices |
| Scroll precision | Excellent | Moderate; video seeking may be uneven | Moderate | Excellent | Excellent with 3D; reliable fallback |
| Development difficulty | High | Low–medium | Medium due cross-browser alpha | Medium–high delivery/decode logic | High initially, best risk control |
| Mobile compatibility | Variable; requires tiers | Generally strong with correct codecs | Weak as sole path | Variable memory/network cost | Strongest because mobile can simplify |
| Initial load | Asset/decoder/shader dependent | Video/poster dependent | Video/poster dependent | Many frames or bundle dependent | Poster-first, enhancements delayed |
| Runtime GPU/CPU | Continuous render unless on-demand/paused | Hardware decode/composite | Decode/composite | Decode + canvas draw | Adaptive |
| File size | Efficient if a reusable model and textures; can grow quickly | Efficient for fixed motion at sane duration/bitrate | Often larger than opaque equivalent | Frequently large in aggregate | Controlled per tier |
| Browser support | WebGL 2 broad; scene-dependent | Strong with multiple sources | Safari alpha gap documented | Strong image/canvas primitives | Strongest with fallback matrix |
| Accessibility | Requires semantic DOM/fallback | Requires alternative text/content and controls when applicable | Same as video | Same as decorative sequence | Best when DOM remains primary |
| Maintenance | Engine, libraries, drivers, assets | Re-render for visual changes | Re-render plus codec QA | Re-render many frames | More paths, but graceful degradation |
| AI-assisted feasibility | Code is feasible; final art still hard | High if render/video tools are available | Medium; encoding/support pitfalls | Medium; generation consistency and asset pipeline | Highest practical success rate |

## Detailed analysis

### Real-time interactive 3D

Choose this when the value proposition includes interaction: the object must respond to pointer movement, change material/state, maintain parallax against the page, or move continuously through a camera path that adapts to viewport shape. It produces the closest match to “the object exists in the page.”

The costs are continuous rendering, shader compilation, asset decoding, GPU memory, driver variation, context loss, and art/engineering coordination. MDN recommends explicit VRAM budgeting, smaller back buffers where acceptable, batching draw calls, compressed textures, and attention to high-DPI rendering ([WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices)).

### Pre-rendered opaque video

Choose this when visual fidelity and schedule are more important than direct object interaction. A normal `<video>` path benefits from mature browser decoding. Supply a poster, dimensions, and multiple sources; web.dev recommends poster and preload strategy because video can affect LCP and transfer ([video performance](https://web.dev/learn/performance/video-performance)).

Video is not automatically lightweight: a long, high-resolution, high-bitrate loop can be worse than an optimized GLB. Its strength is predictability, not guaranteed small size.

### Transparent WebM

Choose only as an enhancement where alpha compositing materially improves the layout. MDN's current codec guide notes Safari does not support alpha transparency for VP9/WebM, so the production matrix needs an alternative, commonly an opaque asset, static poster, or separately validated Apple-compatible path ([MDN codec guide](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs)). Do not assume that “WebM playback supported” implies “WebM alpha supported.”

### Image sequence

Choose when the art must be offline rendered and the scroll position must select an exact frame. This is strong for deterministic product reveals and weak for free interaction. Delivery should use responsive resolution, prioritized key frames, constrained cache, and decode scheduling; otherwise network requests and decoded-memory spikes can exceed video.

### Hybrid

Hybrid means the browser always has a valid non-3D presentation, then upgrades according to capability and preference:

```text
Semantic DOM + poster
        ↓ capability / preference / data checks
Opaque video or simplified static motion
        ↓ sufficient GPU and successful asset load
Real-time WebGL scene
        ↓ optional supported high-end path
WebGPU-specific enhancement
```

The fallback should not be presented as an error screen. It should be a designed version of the same story.

## Recommended option for the reference style

Use the hybrid with:

- A visually matched AVIF/WebP poster in the initial HTML/CSS layout.
- One dynamically loaded real-time WebGL 2 hero for desktop and proven mobile tiers.
- An opaque pre-rendered video or static poster for reduced motion, weak GPUs, load failure, or constrained data conditions.
- No transparent WebM dependency unless the fallback matrix has been tested and the compositing benefit is substantial.
- Optional image-sequence prototype only if the inaccessible reference is later confirmed to be frame-scrubbed rather than interactive 3D.

## MVP decision rule

If the approved hero object and browser-ready asset are not available by the end of the asset-production phase, ship the media-led MVP rather than delaying the entire site or forcing an unpolished real-time scene. The architecture can retain the upgrade point for a later R3F scene.

