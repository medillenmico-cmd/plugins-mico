# Recommended production roadmap

**Research date:** 2026-08-31  
**Status:** Planning only; no implementation is included.

## Phase plan

### Phase 1 — Research and visual definition

| Field | Plan |
| --- | --- |
| Expected outcome | Approved product message, audience, visual target, reference truth set, and decision on real-time vs media MVP. |
| Tools | Reviewed YouTube reference and transcript, browser, captured/approved key frames, Figma for annotated responsive frames if useful, mood boards. |
| AI responsibilities | Synthesize references, identify patterns, draft storyboard, list unknowns, compare approaches. |
| Human responsibilities | Approve which video example or Spline scene is the actual visual target; approve object, message, style, copy, CTA, and success criteria. |
| Dependencies | Product positioning and rights to use reference material. |
| Risks | Treating the tutorial's montage as one exact design; confusing its Spline MVP workflow with the brief's more advanced scroll choreography; optimizing novelty instead of communication. |
| Acceptance criteria | 8–12 approved key frames or equivalent; desktop/tablet/mobile intent; reduced-motion concept; signed decision memo. |

### Phase 2 — Asset production

| Field | Plan |
| --- | --- |
| Expected outcome | Clean Blender source, canonical GLB, desktop/mobile delivery candidates, poster, and fallback media candidate. |
| Tools | Blender; optional Meshy/Tripo/Spline AI; glTF validator/optimizer; KTX tools; compositor/encoder. |
| AI responsibilities | Generate concepts/rough meshes, automate asset reports and variants, flag topology/material/export issues. |
| Human responsibilities | Final modeling/cleanup, UVs, materials, lighting, animation, brand accuracy, license/provenance review. |
| Dependencies | Approved key frames and asset budget. |
| Risks | AI geometry inconsistency, non-transferable Blender materials, oversized textures, weak silhouette. |
| Acceptance criteria | Canonical asset matches reference in target renderer; manifest complete; delivery variants meet provisional budgets without visible unacceptable loss. |

### Phase 3 — Technical prototype

| Field | Plan |
| --- | --- |
| Expected outcome | Gray-box page proving poster-to-canvas upgrade, one object, camera framing, normalized scroll progress, and fallbacks. |
| Tools | Next.js/React/TypeScript, Three.js/R3F, GSAP/ScrollTrigger, browser profiler. |
| AI responsibilities | Implement bounded prototype, loading/error states, instrumentation, and tests. |
| Human responsibilities | Review motion clarity and decide whether real-time path is viable. |
| Dependencies | Proxy or low-detail asset; target-device access. |
| Risks | Architecture hidden behind final-art work; prototype judged only on a powerful desktop. |
| Acceptance criteria | Works on one representative mobile and desktop; no scroll trapping; fallback activates; critical DOM renders without 3D. |

### Phase 4 — Hero implementation

| Field | Plan |
| --- | --- |
| Expected outcome | Complete five-stage hero: arrival, headline, description, CTA, release. |
| Tools | Approved asset, R3F/Three.js, GSAP/ScrollTrigger, selected Drei helpers, optional Motion for local DOM micro-interactions. |
| AI responsibilities | Integrate assets, implement named timeline states, cleanup, pointer response, context-loss path, automated regression checks. |
| Human responsibilities | Tune camera, lighting, material response, pacing, typography, and visual hierarchy. |
| Dependencies | Technical prototype accepted; final or near-final asset available. |
| Risks | Animation ownership conflicts, copy collisions, fragile pin measurements, shader scope creep. |
| Acceptance criteria | Approved desktop reference match at every label; reverse scroll deterministic; CTA reachable; next section releases cleanly. |

### Phase 5 — Responsive adaptation

| Field | Plan |
| --- | --- |
| Expected outcome | Deliberate desktop, tablet, mobile, reduced-motion, and constrained-device presentations. |
| Tools | Browser responsive modes plus physical devices; alternate GLB/media/poster variants. |
| AI responsibilities | Implement tier selection and layout/camera configurations; run viewport and orientation tests. |
| Human responsibilities | Approve crop, copy order, touch behavior, and acceptable mobile simplification. |
| Dependencies | Stable hero timeline and asset variants. |
| Risks | Scaled-down desktop composition, dynamic viewport bugs, unreadable overlay, excessive mobile thermals. |
| Acceptance criteria | No overflow/overlap; normal mobile scroll; 200% zoom review; reduced-motion content appears without multi-viewport pin. |

### Phase 6 — Performance optimization

| Field | Plan |
| --- | --- |
| Expected outcome | Measured quality tiers and assets that meet agreed field/lab budgets. |
| Tools | Network and performance profilers, renderer stats, bundle analysis, field telemetry, glTF/KTX optimization tools. |
| AI responsibilities | Analyze traces, locate long tasks/draw-call/memory hotspots, automate reports, propose minimal changes. |
| Human responsibilities | Choose visual tradeoffs and validate compressed output. |
| Dependencies | Representative build and real devices. |
| Risks | Optimizing only transfer, hiding decode cost, lowering visual quality indiscriminately. |
| Acceptance criteria | Target Core Web Vitals in representative tests; stable tier frame rate; no sustained memory growth; 5–10 minute thermal run accepted. |

### Phase 7 — Accessibility and SEO

| Field | Plan |
| --- | --- |
| Expected outcome | Semantic, keyboard-usable, screen-reader-compatible, motion-safe, indexable page independent of canvas success. |
| Tools | Accessibility tree, keyboard, screen readers, automated checks, structured-data validator, social preview testing. |
| AI responsibilities | Audit semantics/focus/alternatives/metadata, implement fixes, create repeatable tests. |
| Human responsibilities | Conduct assistive-technology and motion-comfort review; approve text alternatives and content. |
| Dependencies | Stable page content and interactions. |
| Risks | Automated-check false confidence; essential meaning encoded only visually. |
| Acceptance criteria | Logical headings/tab order, visible focus, pause/reduced-motion path, indexable HTML, correct previews, no critical automated or manual issues. |

### Phase 8 — Browser and failure testing

| Field | Plan |
| --- | --- |
| Expected outcome | Browser/device support matrix with reproducible results and accepted fallbacks. |
| Tools | Chrome/Edge/Safari/Firefox, iOS/Android devices, throttling, context-loss simulation, visual regression. |
| AI responsibilities | Execute scripted scenarios, collect logs/screenshots/traces, cluster failures, implement bounded fixes. |
| Human responsibilities | Real-device exploratory QA and go/no-go decisions for each tier. |
| Dependencies | Performance/accessibility candidate. |
| Risks | Driver-specific defects, autoplay/codec differences, touch/address-bar behavior, font/layout drift. |
| Acceptance criteria | All critical scenarios pass or intentionally fall back; no blank canvas; navigation and CTA remain functional everywhere supported. |

### Phase 9 — Final polish and deployment preparation

| Field | Plan |
| --- | --- |
| Expected outcome | Launch candidate, runbook, telemetry, rollback/kill switch, and asset/source archive. |
| Tools | Visual diff, production-like preview, analytics/real-user monitoring plan, CDN/cache configuration review. |
| AI responsibilities | Final consistency audit, documentation, release checklist, telemetry queries, regression summary. |
| Human responsibilities | Brand, copy, legal/license, privacy, analytics, and launch approval. |
| Dependencies | All earlier gates complete. |
| Risks | Late visual changes, cache/header mistakes, missing asset provenance, no production fallback control. |
| Acceptance criteria | Approved key-frame comparison; source and optimized assets archived; monitoring and rollback tested; no unresolved critical risks. |

## Suggested decision gates

| Gate | Decision |
| --- | --- |
| G1 after visual definition | Does the hero communicate the product and have an accessible reference truth set? |
| G2 after asset production | Is the browser asset visually premium and technically feasible? |
| G3 after technical prototype | Does real-time 3D add enough value over video to justify complexity? |
| G4 after responsive adaptation | Is the mobile/reduced-motion version a designed experience, not a degraded accident? |
| G5 after performance/accessibility | Does the real-time tier meet budgets without weakening the message? |
| G6 before launch | Are fallback, telemetry, rollback, provenance, and ownership complete? |

## Realistic sequencing and staffing

Work can overlap only after contracts are stable. Asset concepting and gray-box engineering may proceed in parallel, but final motion should wait for reliable pivots/material boundaries, and optimization should begin during asset production rather than after polish. At minimum, assign the roles of product/content owner, creative/front-end developer, 3D artist (which may be the same skilled person for a simple abstract object), and accessibility/performance reviewer.

## Recommended first production experiment

Build a throwaway gray-box spike—not the website—with one proxy object, three camera poses, the headline/description/CTA timeline, a poster swap, and a static mobile path. Time-box it and compare against a pre-rendered video version. The decision evidence should be load cost, frame stability, motion quality, mobile behavior, implementation complexity, and stakeholder preference. Do not carry prototype code forward automatically; carry forward what was learned.

