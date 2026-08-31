# Example websites and case studies

**Research date:** 2026-08-31

## Verification method

Technology is listed as **verified** only when the site's author, official case study, or source explicitly states it. Visual/interaction observations from reachable pages are labeled separately. Unknown runtime details remain unknown.

## Examples

### 1. Bruno Simon — portfolio

- **URL:** <https://bruno-simon.com/>
- **Type:** Real-time, navigable 3D portfolio.
- **Verified technology:** The site itself states it uses Three.js and discusses TSL plus WebGL/WebGPU; it also links source and Blender files ([site/behind the scenes](https://bruno-simon.com/?s=03)).
- **Interaction pattern:** Users drive through a 3D world rather than scroll through a conventional document.
- **Why effective:** The interaction is the author's product signal; the world, physics, audio, and discovery system form one coherent idea.
- **Risks:** High onboarding and input cost, weak fit for a short SaaS message, potential accessibility and mobile complexity.
- **Adapt:** The clarity of one memorable interaction and the transparent behind-the-scenes/asset discipline.
- **Do not copy:** Free-roaming navigation for a conversion-focused landing page.

### 2. Active Theory v5 — studio portfolio

- **URL:** <https://v5.activetheory.net/>
- **Type:** Full-viewport immersive WebGL environments.
- **Verified technology:** Active Theory states in a Webby case study that the site is built with WebGL and its internal Hydra JavaScript framework; it expanded to eight 3D environments ([Webby case study](https://www.webbyawards.com/crafted-with-code/active-theory/)).
- **Interaction pattern:** Spatial portfolio navigation with multiple environments and strong atmospheric transitions.
- **Why effective:** The site itself demonstrates the studio's core capability and uses environmental art to communicate brand values.
- **Risks:** The live page explicitly reports unsupported graphics hardware in some contexts; a full-canvas portfolio can make ordinary information retrieval harder.
- **Adapt:** Cohesive lighting, environmental transitions, and the idea that the visual experience should prove the brand promise.
- **Do not copy:** Multiple heavyweight worlds when one hero object can tell the product story.

### 3. ERA residential complex — Vide Infra case study

- **URL:** <https://videinfra.com/blog/case-study-a-triple-site-of-the-day-winner-powered-by-webgl>
- **Type:** Interactive 3D real-estate/product exploration integrated into a website.
- **Verified technology:** The agency states that it primarily used Three.js and WebGL for the interactive 3D map.
- **Interaction pattern:** The 3D map is functional, not only decorative: it supports exploration of the property.
- **Why effective:** The rendering technique serves a domain task—understanding a place—while the surrounding site carries the narrative.
- **Risks:** Map/product detail can create large assets and touch-target problems; technical sophistication can outgrow the marketing need.
- **Adapt:** Connect 3D directly to product meaning and decision-making.
- **Do not copy:** Dense 3D interaction if the hero has no equivalent user task.

### 4. Joseph Santamaria — scroll-driven 3D portfolio case study

- **URL:** <https://tympanus.net/codrops/2026/04/28/more-than-a-portfolio-building-a-scroll-driven-3d-world-with-something-to-say/>
- **Type:** Scroll-driven real-time 3D world.
- **Verified technology:** The author lists Three.js, WebGL, GSAP/ScrollTrigger, Blender, KTX2/Basis textures, instancing, mobile-specific low-resolution shaders, and Draco.
- **Interaction pattern:** Camera/world shifts, timed typography, and shader transitions are choreographed by scrolling.
- **Why effective:** It is unusually close to the requested production pattern and documents the asset/performance techniques rather than only showing the result.
- **Risks:** The case study reports three months of focused work plus final polish, demonstrating that studio-like quality is not a one-prompt task.
- **Adapt:** Blender-to-web pipeline, one scroll story, KTX2, instancing, and explicit mobile shader simplification.
- **Do not copy:** Treating its scope or timeline as a normal lightweight landing page.

### 5. 84—24 — Codrops case study

- **URL:** <https://tympanus.net/codrops/2024/04/08/case-study-84-24/>
- **Type:** Hybrid DOM site with a 3D model animated through page interactions.
- **Verified technology:** The author states that a GLB model was imported with Three.js and individual elements were animated with GSAP.
- **Interaction pattern:** Standard vertical navigation combined with object animation, a useful model for retaining web familiarity.
- **Why effective:** It integrates 3D into a conventional information structure instead of replacing the whole page.
- **Risks:** Complex object-part animation can create too many meshes/draw calls and brittle synchronization.
- **Adapt:** Normal scroll as the navigation model and GLB part naming as an animation contract.
- **Do not copy:** Splitting every decorative part into a separately animated mesh without a performance need.

### 6. NASA's Eyes

- **URL:** <https://science.nasa.gov/eyes/>
- **Type:** Browser-based real-time 3D data visualization suite.
- **Verified facts:** NASA describes the products as browser-based 3D applications, available across devices, and says the team transforms complex mission CAD models into lightweight web models ([NASA Eyes](https://science.nasa.gov/eyes/), [FAQ](https://science.nasa.gov/eyes/faq/)).
- **Technology status:** Current engine/library is not confirmed by the cited pages and is therefore left **unverified**.
- **Interaction pattern:** Camera navigation, time/data exploration, selectable missions and bodies.
- **Why effective:** 3D explains spatial and temporal information that would be harder to understand as flat content.
- **Risks:** Application-like controls and large scientific scope are inappropriate for a simple hero.
- **Adapt:** Aggressive CAD-to-web simplification and meaningful spatial interaction.
- **Do not copy:** A simulation UI or unrestricted navigation for brand storytelling.

### 7. Spline Viewer demos

- **URL:** <https://viewer.spline.design/>
- **Type:** Embedded real-time 3D component.
- **Verified technology:** Official Spline Viewer web component; the documentation states that it can receive global scroll/mouse events and work without an iframe ([Spline Viewer docs](https://docs.spline.design/exporting-your-scene/web/exporting-as-spline-viewer)).
- **Interaction pattern:** Scroll states, orbit/zoom, follow, look-at, and background customization.
- **Why effective:** It demonstrates how quickly a designer-authored scene can become an interactive web element.
- **Risks:** Runtime/scene control, performance budgets, branding/license, and custom failure handling need evaluation per project.
- **Adapt:** Use as a prototype benchmark and design handoff option.
- **Do not copy:** Embedding an unprofiled complex scene and assuming the platform automatically solves mobile performance.

### 8. Codrops Creative Hub

- **URL:** <https://tympanus.net/codrops/hub/all/>
- **Type:** Curated experiments and source-backed interaction references, not one production website.
- **Verified technology:** Entries are tagged with their stated tools; current examples include Three.js, React Three Fiber, GSAP, WebGL, WebGPU, Blender, and TSL.
- **Interaction pattern:** Many focused experiments: glass, parallax, scroll tubes, 3D galleries, shaders, and transitions.
- **Why effective:** Each demo isolates a technique, which makes it useful for feasibility spikes and risk reduction.
- **Risks:** Demo code and visual novelty may not meet production accessibility, loading, SEO, or maintenance requirements.
- **Adapt:** Prototype one risky effect in isolation before including it in the hero.
- **Do not copy:** Combining many unrelated experiments into one landing page.

## Cross-case findings

| Effective pattern | Evidence from examples | Application to this project |
| --- | --- | --- |
| 3D demonstrates the product/creator | Bruno Simon, Active Theory, ERA, NASA Eyes | The hero object should communicate the product, not just “futurism.” |
| Standard web structure can coexist with 3D | 84—24, ERA | Keep DOM copy, CTA, and normal sections. |
| Premium quality needs an asset pipeline | Santamaria case study, NASA CAD simplification | Budget Blender, compression, mobile variants, and polish explicitly. |
| Mobile is a separate rendering decision | Santamaria's mobile shaders, NASA lightweight assets | Approve a mobile composition and quality tier, not a scaled desktop scene. |
| One focused technique is easier to productionize | Codrops demos | Prototype camera/scroll/material risks separately before integration. |

## Recommended inspiration set

Use the Santamaria case study for the closest technical workflow, 84—24 for hybrid information architecture, Active Theory for atmosphere and lighting discipline, and Spline Viewer as a fast prototype comparator. Use Bruno Simon and NASA Eyes as reminders that free exploration works best when exploration itself is the product—not as direct layout templates.

