# Risks and failure modes

**Research date:** 2026-08-31

## Risk register

| Risk | Early signal | Prevention | Mitigation / fallback |
| --- | --- | --- | --- |
| Oversized GLB/textures | Multi-megabyte textures, long decode, GPU-memory spikes | Set asset budgets before modeling; validate canonical and delivery variants; KTX2 and geometry optimization | Load lower tier, replace with poster/video, remove unseen geometry/materials |
| Poor mobile frame rate | Sustained frame time above ~33 ms, dropped input, hot device | Mobile-first gray-box; lower DPR, texture size, materials, shadows, post effects; cap work | Switch to media/static tier and end continuous rendering |
| Thermal/battery drain | Smooth first minute, then throttling and stutter | 5–10 minute device runs; pause offscreen/settled/hidden; avoid needless particles/video textures | Reduce render scale/frame cadence or fall back for the session |
| Scroll-jacking | Wheel/touch feels delayed; keyboard/anchors break; users cannot skip | Native scroll baseline; one scroll controller; no trapped input; restrained scrub | Disable smooth scrolling and pin on affected tier/preferences |
| Excessive motion | Nausea reports, difficulty reading, CTA constantly moving | Small camera amplitudes; stable reading states; reduced-motion path; pause control | Static composition with all content visible |
| Unreadable hero copy | Highlights/particles cross text; low contrast changes by frame | Approved text-safe camera frames and contrast checks across timeline | Add controlled local backing/fade or choose alternate scene frame; never hide copy |
| Broken responsive layout | Object covers copy; mobile address bar causes jumps; pin height wrong | Separate desktop/tablet/mobile compositions; dynamic viewport testing; stable dimensions | Mobile unpinned static/media layout |
| Hydration mismatch/flicker | Poster disappears before canvas is ready; server/client layout differs | Render deterministic DOM/poster on server; isolate client canvas; swap only after ready | Retain poster beneath canvas until verified first frame |
| WebGL context loss | Blank canvas after tab switch/GPU pressure | Handle lifecycle and disposal; monitor context loss; keep fallback mounted | Controlled restore once; otherwise show poster/video. MDN documents the event ([source](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/webglcontextlost_event)). |
| Browser/GPU incompatibility | Shader compile error, black material, missing extension | Feature detection, neutral glTF validation, conservative shader path, browser matrix | Lower renderer tier or static/media fallback |
| WebGPU overreach | Works in Chromium lab, unavailable elsewhere | WebGL 2 baseline; WebGPU only as enhancement. MDN marks it limited availability ([source](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API)). | Automatic WebGL/media fallback |
| Animation timing conflicts | Jitter, transforms snapping, GSAP and Motion overwrite each other | One owner per property; one master timeline; explicit state contract | Remove duplicate writer; reconstruct from canonical states |
| Pin measurement drift | Jump on font load/resize; overlapping next section | Pin stable wrapper, animate children, reserve flow space, refresh after layout | Disable pin on affected layout and use normal flow |
| Video fails autoplay | Poster remains or play promise rejects | Muted/playsinline as appropriate; never depend on autoplay for content | Designed poster plus user play control |
| Video loop seam | Exposure/pose jump at first frame | Match pose, velocity, grade, and GOP/encode; test decoded loop | Crossfade if appropriate or stop on final frame |
| Transparent video incompatibility | Black background/ignored alpha in Safari | Treat alpha video as enhancement; test per browser; MDN notes Safari VP9 alpha limitation ([source](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Video_codecs)). | Opaque video or static poster |
| Image-sequence memory spike | Tab reload/crash, long decode, many simultaneous images | Responsive variants, key-frame priority, bounded decoded cache | Reduce frame count/resolution or use video |
| AI asset inconsistency | Geometry, logo, or materials mutate between views/frames | Use AI for concepts/rough mesh; require turntable review and Blender cleanup | Rebuild critical form manually or use abstract/non-branded asset |
| Weak AI topology/UVs | Shading artifacts, too many triangles, seams | Clay-mode and wireframe inspection; retopology, UV, bake, validation | Use generated model only as reference/blockout |
| Accessibility hidden behind canvas | CTA not focusable, copy absent to screen readers | Semantic DOM content and native controls; canvas decorative unless functional | Disable canvas interaction and retain equivalent DOM path |
| Core Web Vitals regression | Poster/headline LCP delayed, INP rises, CLS on scene swap | Performance budgets, fixed dimensions, dynamic import, field monitoring | Hold 3D enhancement until after critical paint; roll back tier |
| SEO collapse | Empty server HTML or content revealed only by timeline | Server-render headings/copy/links/metadata | Static DOM presentation independent of animation |
| Overdependence on effects | Users remember animation but not product/CTA | Message-first storyboard; every effect tied to a beat | Remove effects that do not improve comprehension or action |
| Maintenance fragility | Minor copy/layout change breaks camera or timeline | Named stages, asset manifest, shared responsive tokens, visual regression | Freeze validated interface contracts and document recalibration steps |

## Common technical failure chains

### “It runs on my desktop”

High-DPR desktop testing hides transfer latency and gives a powerful GPU. The same scene on a phone combines slower decode, unified memory, thermals, touch scrolling, dynamic viewport height, and limited alpha/codec behavior. Prevention is a mobile gray-box milestone before final material polish, not a last-week responsive pass.

### Compression without measurement

Maximum compression can reduce transfer while increasing decode time or creating texture/normal artifacts. Geometry compression also adds decoder payload. Keep a canonical asset, test multiple settings, compare visible loss, and record cold-load decode on target devices.

### More libraries, less control

GSAP, Motion, Lenis, R3F state, browser scroll, and CSS transitions can all influence the same frame. Without an ownership map, each library is locally reasonable and globally conflicting. The prevention rule is simple: one normalized progress source and one writer per animated property.

### Canvas becomes the website

When text, links, loading, and interactions move inside WebGL, accessibility, SEO, localization, selection, focus, and responsive layout all become harder. Keep the canvas as a visual layer and the page as a web document.

### Loading screen as a design crutch

A long branded loader does not solve loading. It delays LCP and hides useful content. The poster and semantic hero should be the first experience; the scene upgrades in place.

## Governance

- Assign a named owner for 3D assets, runtime performance, motion, accessibility, and content.
- Treat asset changes as code changes: source, settings, output hashes, screenshots, and performance delta.
- Require evidence at each gate: reference comparison, real-device run, accessibility check, and fallback screenshot.
- Keep a one-click kill switch or configuration path to disable real-time 3D if production telemetry reveals regressions.
- Do not raise budgets silently to accommodate a late visual change; trade quality elsewhere or seek explicit approval.

## Highest-priority mitigations

1. Poster-first hybrid architecture.
2. Separate mobile/reduced-motion design.
3. Canonical Blender asset plus reproducible delivery variants.
4. Single ScrollTrigger timeline and animation ownership map.
5. Real-device thermal/performance testing before polish is locked.
6. Designed fallback for load failure, context loss, codec failure, and unsupported GPU.

