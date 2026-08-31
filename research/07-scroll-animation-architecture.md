# Scroll and interaction architecture

**Research date:** 2026-08-31

## Architecture recommendation

Use one pinned hero section with a normal document-flow spacer, one normalized progress value, one labeled GSAP timeline, and three independent presentation layers:

```text
fixed navigation (DOM)
hero copy + CTA (DOM, semantic and focusable)
poster / video / WebGL canvas (visual layer)
normal next section (DOM flow)
```

ScrollTrigger supports the required pin and scrub behavior directly ([official docs](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)). It also warns against animating the pinned element itself because doing so can invalidate measurements; pin the stage and animate its children.

## Story timeline

| Label | Progress range | 3D/camera action | DOM action | Exit condition |
| --- | --- | --- | --- | --- |
| `arrival` | 0.00–0.15 | Poster swaps to matching loaded scene; low-amplitude idle rotation. | Navigation present; essential page name remains available. | Scene loaded or fallback retained. |
| `headline` | 0.15–0.38 | Object/camera creates left safe area. | Headline becomes visible and readable. | Headline opacity and position settled. |
| `description` | 0.38–0.62 | Object rotates/reframes toward a second product angle. | Right-side description enters; headline can remain or reduce emphasis. | Description readable at normal scroll speed. |
| `cta` | 0.62–0.82 | Motion decelerates; lighting cue supports stable presentation. | CTA appears and can receive focus. | CTA remains reachable without precise scroll. |
| `release` | 0.82–1.00 | Final hero pose; optional shallow depth transition. | Copy remains stable; next section preview appears. | Pin releases with no jump/overlap. |

The timeline is a recommendation derived from the written requirements, not a reconstruction of the inaccessible YouTube reference.

## State model

Keep these states separate:

- **Asset state:** idle, loading, ready, failed.
- **Capability tier:** static, video, low real-time, high real-time.
- **Preference:** normal motion or reduced motion.
- **Layout mode:** desktop, tablet, mobile—not raw width checks scattered through animation code.
- **Story progress:** normalized 0–1 plus named labels.
- **Interaction state:** pointer over object, CTA focus, page hidden, context lost.

GSAP owns the timeline. The renderer samples timeline values. React state changes only for coarse transitions; per-frame values should not trigger React renders.

## Pinned-section design

- Reserve the full pin distance in document flow so the next section never jumps.
- Keep the pinned container dimension stable after load.
- Place visual layers absolutely inside the stage, while copy stays semantic and selectable.
- Compute start/end from actual layout and refresh after font/media/layout changes.
- Avoid nested pinned sections unless unavoidable; ScrollTrigger supports `pinnedContainer`, but nested pinning increases complexity.
- Do not trap wheel/touch input or require users to complete the full animation before accessing content.
- Keep navigation fixed independently from the hero pin.

## Camera and object motion

Use authored start/end states, not cumulative deltas. Each label should specify camera position, look target, object position/rotation/scale, key light intensity/color, and post-effect values. Interpolate from canonical states so resize, reverse scroll, refresh, and deep links remain deterministic.

For responsive framing, preserve **screen-space intent** rather than identical world coordinates:

- Desktop: object can move right to open a left headline safe area, then left to support right copy.
- Tablet: reduce lateral movement and shorten lines; keep the object near center.
- Mobile: stack copy in one safe column, reduce camera motion, and use a simplified object pose or poster/video. Do not force left/right copy simultaneously.

## Pointer and hover interaction

- Add only a small, damped rotation or light response around the scroll-authored pose.
- Clamp input and remove it during CTA focus or when the pointer leaves.
- Do not make the object draggable unless dragging is a product requirement.
- Hover cannot be the only way to reveal information; touch and keyboard users need the same content.
- Disable or greatly reduce parallax under reduced motion.

## Reduced-motion architecture

MDN describes `prefers-reduced-motion` as a user request to remove, reduce, or replace non-essential motion, including large scaling or panning that may trigger vestibular discomfort ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion)).

Reduced-motion path:

- Do not pin for multiple viewports.
- Show the best static hero frame or a user-controlled/non-autoplay media state.
- Present headline, description, and CTA together in normal reading order.
- Disable pointer parallax, smooth-scroll interpolation, camera travel, and continuous idle rotation.
- Retain small opacity changes only if they do not delay access to content.

WCAG 2.2.2 requires a mechanism to pause, stop, or hide certain automatically moving content that starts automatically and lasts more than five seconds unless essential ([W3C explanation](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html)). A looping hero should therefore either stop, be non-essential and user-controllable, or be replaced in reduced-motion mode.

## Mobile alternatives

Preferred order:

1. Static poster plus normal content flow.
2. Short opaque video with restrained playback, if measurements support it.
3. Simplified real-time model with lower DPR, smaller textures, fewer materials/lights, no expensive post-processing, and rendering paused when settled/offscreen.

Choose based on measured frame time, memory, temperature, and input latency—not user-agent labels alone.

## Failure recovery

- If 3D load exceeds the agreed timeout or throws, keep the poster/video and continue the page.
- On `webglcontextlost`, stop the render loop, preserve content, and attempt a controlled restore or fall back. The event is documented by MDN ([context lost](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/webglcontextlost_event)).
- When the page becomes hidden, pause animation/rendering; `requestAnimationFrame` is normally paused in hidden tabs, but explicit resource cleanup and media pause are still useful ([MDN requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame)).
- If fonts or resize change measurements, refresh the timeline without jumping the user to another progress state.

## Acceptance criteria

- Headline, description, CTA, and next section remain available with JavaScript failure, 3D failure, reduced motion, and keyboard-only navigation.
- Reverse scrolling reconstructs the same states without flicker.
- No scroll trapping, accidental snapping, focus loss, or address-bar viewport jump on mobile.
- Fixed navigation never becomes unreadable against the scene.
- The CTA can be reached and activated without stopping at a precise scroll pixel.
- Desktop, tablet, and mobile each have approved framing—not merely scaled desktop coordinates.

