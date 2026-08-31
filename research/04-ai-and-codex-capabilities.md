# AI and Codex capabilities

**Research date:** 2026-08-31

## Evidence boundary

Official OpenAI material presents Codex as able to understand codebases, build and deploy apps, create browser-based games, test, refactor, and maintain documentation ([OpenAI Codex use cases](https://learn.chatgpt.com/use-cases)). Those examples establish that Codex can perform multi-step engineering work with tools; they do **not** establish that it can independently produce professional 3D art, guarantee performance on untested hardware, or replace aesthetic approval.

## Responsibility matrix

| Task | Codex autonomy | Human/external dependency | Notes |
| --- | --- | --- | --- |
| Requirements and architecture | High for first draft | Product owner validates message, scope, and tradeoffs | Codex can turn the storyboard into components, state boundaries, asset contracts, budgets, and acceptance criteria. |
| Page structure and responsive DOM | High in a bounded repository | Designer reviews hierarchy and typography | Strong candidate for autonomous implementation and tests. |
| Three.js/R3F scene setup | High for conventional scenes | Senior 3D/web engineer reviews rendering architecture | Codex can load GLB, create lights/cameras, connect state, and build fallbacks, but scene quality depends on assets and art direction. |
| Scroll-driven interactions | High for a specified storyboard | Motion designer reviews pacing and feel | Codex can implement a labeled GSAP timeline, cleanup, resize behavior, and reduced-motion path. |
| Shaders and post-processing | Medium | Graphics specialist for complex refraction, temporal effects, or cross-GPU correctness | AI can generate plausible GLSL that compiles yet performs poorly or fails on edge hardware. Visual and numerical validation are required. |
| 3D asset integration | High after assets are supplied | Artist supplies approved GLB/textures and export contract | Codex can integrate loaders, compression decoders, animation clips, and quality variants. |
| Asset optimization | Medium–high | Human checks visible loss and material fidelity | Codex can run or script optimization tools, compare sizes, and automate validation, but cannot decide whether an artifact is aesthetically acceptable without reference evidence. |
| Debugging | High for reproducible failures | Human supplies device/browser evidence for hardware-specific issues | Console logs, screenshots, performance traces, and minimal reproductions materially improve results. |
| Responsive fallbacks | High | Product/design owner chooses acceptable mobile simplification | Codex can implement capability tiers and posters/videos; the brand tradeoff is human. |
| Automated testing | High | Real-device lab remains necessary | Unit, integration, end-to-end, visual, accessibility, and performance-budget tests are automatable. GPU/thermal diversity is not fully emulated. |
| Performance profiling | Medium–high | Human interprets field data and makes visual compromises | Codex can inspect traces and recommend budgets; it cannot infer real-user thermals or GPU faults without measurements. |
| Premium model creation | Low | Blender artist or 3D generalist | Silhouette, topology, UV, material response, lighting, and final polish are artistic production tasks. |
| High-end motion direction | Medium for implementation; low for taste ownership | Motion designer or experienced creative developer | AI can execute a defined beat sheet, but “premium” depends on timing, restraint, and composition. |

## Tasks Codex can complete autonomously in a well-scoped build

- Inspect an existing repository and propose a bounded architecture.
- Create the semantic page shell, responsive layout, client-only 3D boundary, loading/poster states, and error fallback.
- Implement a conventional Three.js/R3F scene from an approved asset contract.
- Connect one normalized scroll progress value to a GSAP/ScrollTrigger timeline.
- Add pointer interactions with clamps, focus-safe DOM controls, and reduced-motion behavior.
- Add lazy loading, visibility pause, adaptive DPR/quality tiers, and context-loss fallback.
- Create tests for loading, timeline stages, keyboard navigation, reduced motion, resize, and fallback activation.
- Run supported linters, type checks, browser tests, bundle reports, Lighthouse-style lab checks, and visual regression comparisons.
- Write documentation, asset manifests, performance budgets, and QA checklists.

“Autonomous” here means Codex can carry out the engineering loop when requirements, repository access, tools, and acceptance criteria are available. It does not mean the output should bypass review.

## Tasks that need human review

- Choosing the hero concept and deciding whether it communicates the product rather than merely displaying technical skill.
- Selecting the final camera angles, crop, lighting, material roughness, glow intensity, and text safe areas.
- Judging whether compression or lower quality tiers visibly damage the brand.
- Reviewing motion for nausea, distraction, scroll-jacking, and message comprehension.
- Testing representative low-end Android devices, iPhones/iPads, integrated GPUs, high-DPR laptops, and assistive technologies.
- Approving claims, CTA, product copy, and SEO content.

## Tasks that need external tools

| External tool | Why it is needed |
| --- | --- |
| Blender | Modeling, UVs, retopology, rigging, baking, lighting references, animation, GLB export. |
| Meshy, Tripo, or Spline AI | Optional concept/rough-model generation; outputs still need inspection and cleanup. Meshy documents GLB plus optional PBR maps, while Tripo documents GLTF conversion and baking ([Meshy image-to-3D](https://www.meshy.ai/tutorials/api-quickstart-image-to-3d), [Tripo conversion](https://developers.tripo3d.ai/en/docs/models-convert)). |
| glTF validator/optimizer, glTF-Transform, KTX tools | Validate extensions, reduce geometry, resize/compress textures, and produce reproducible asset variants. |
| Browser developer tools and performance tooling | Measure CPU/GPU frame time, long tasks, memory, network, layout stability, and interactions. |
| Real-device test matrix | Validate drivers, thermal throttling, touch behavior, codec support, and accessibility. |
| Video compositor/encoder | Render, grade, loop, and encode fallback media with verified codecs and alpha strategy. |

## When a professional 3D artist or motion designer is justified

Hire or involve a specialist when the hero depends on photoreal product accuracy, brand-critical industrial design, realistic glass/refraction, complex organic modeling, character/cloth/fluid animation, seamless procedural motion, or an exact match to a high-end reference. A solo AI-assisted creator can often deliver an excellent abstract/product-like object; matching a studio reel is a different scope.

## Recommended Codex working contract for production

1. Give Codex the approved storyboard, first/final frames, camera notes, asset manifest, target browsers, budgets, and fallbacks.
2. Require a plan before implementation and one animation owner per property.
3. Build a low-detail gray-box prototype before final assets.
4. Require desktop and mobile screenshots/video plus performance evidence at each milestone.
5. Treat generated code, shaders, and optimization settings as hypotheses until verified.
6. Stop automated iteration at explicit human gates: concept, gray-box motion, material look, mobile fallback, and launch candidate.

## Bottom line

Codex can plausibly own most of the software engineering and verification workflow. It should be treated as a strong implementation and debugging agent paired with human art direction—not as an autonomous creative studio or 3D artist.

