# Flow Field · Generative Art

> An interactive, browser-based generative art canvas — particles drift through a Perlin noise flow field, tracing organic lines accompanied by a chord-based ambient soundtrack.

![No build step](https://img.shields.io/badge/build-none-brightgreen?style=flat-square)
![Vanilla JS](https://img.shields.io/badge/vanilla-JS-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![p5.js](https://img.shields.io/badge/p5.js-1.9.4-ed225d?style=flat-square)
![Tone.js](https://img.shields.io/badge/Tone.js-14.7.77-blue?style=flat-square)
![License: MIT](https://img.shields.io/badge/license-MIT-9b59b6?style=flat-square)

---

## Table of Contents

- [Quick Start](#quick-start)
- [Features](#features)
- [Controls Reference](#controls-reference)
  - [01 · Canvas](#01--canvas)
  - [02 · Color](#02--color)
  - [03 · Flow Field](#03--flow-field)
  - [04 · Lines](#04--lines)
  - [05 · Particles](#05--particles)
  - [06 · Symmetry](#06--symmetry)
  - [07 · Attractors](#07--attractors)
  - [08 · Sound](#08--sound)
  - [09 · Wind & Forces](#09--wind--forces)
  - [10 · Export](#10--export)
- [Topbar Actions](#topbar-actions)
- [How the Sound Engine Works](#how-the-sound-engine-works)
- [Flow Field Modes](#flow-field-modes)
- [Visual Themes](#visual-themes)
- [Dependencies](#dependencies)
- [Browser Support](#browser-support)
- [License](#license)

---

## Quick Start

No installation, no build step, no dependencies to install.

```bash
git clone https://github.com/your-username/flow-field.git
cd flow-field
open index.html   # or just double-click it
```

Open `index.html` in any modern browser and the simulation starts immediately. Both libraries are loaded from CDN.

---

## Features

### Visual

| Feature | Description |
|---|---|
| **5 flow field modes** | Smooth, Turbulent, Evolving, Chaotic, Fluid (curl noise) |
| **5 color modes** | Solid, Velocity-mapped, Position-mapped, Rainbow, Depth |
| **7 symmetry options** | None, X-mirror, Y-mirror, 4-fold, 6-fold, 8-fold, 12-fold radial |
| **Attractor system** | Place gravity or repulsion wells anywhere on the canvas by clicking |
| **Turbulence Burst** | Detonate a scatter-burst at any canvas point |
| **Wind & Gravity** | Persistent directional forces layered over the noise field |
| **Fade trails** | Ghost-fade effect for long-exposure aesthetics |
| **5 visual themes** | Minimal, Midnight, Neon, Ocean, Desert |

### Sound

- Ambient audio engine built on Tone.js with **6 voice roles**: bass, sub, mid1, mid2, sparkle, melody
- Each theme plays a unique chord progression in a fitting key and scale
- Stereo panning follows each agent's X position in real time
- Filter cutoff and reverb wet mix modulate dynamically with field activity
- Optional melody voice that walks the scale independently of the harmonic bed

| Theme | Scale | Progression |
|---|---|---|
| Minimal | C Major | I – vi – IV – V |
| Midnight | D Natural Minor | i – VII – VI – VII |
| Neon | D Minor Pentatonic | i – ♭III – ♭VII – IV |
| Ocean | F Lydian | I – II – IV – I |
| Desert | C Mixolydian | I – ♭VII – IV – I |

### Export

- **PNG** — 1× and 2× pixel density
- **WebM video** — 10, 30, or 60 second recordings via `MediaRecorder`
- **Wallpaper presets** — Full HD (1920×1080), 2K, 4K UHD, Mobile (1080×1920)

---

## Controls Reference

The right-hand panel is organised into 10 collapsible sections. Click any section header to expand or collapse it. On mobile, the panel slides up from the bottom as a drag-up sheet.

---

### 01 · Canvas

| Control | Description |
|---|---|
| Width | Output canvas width in pixels (400–2000) |
| Height | Output canvas height in pixels (300–1500) |
| Apply Resize | Commits the new dimensions and resets all particles |

---

### 02 · Color

| Control | Description |
|---|---|
| Background | Canvas background color picker |
| Line Color | Particle stroke color — visible in Solid mode only |
| ⇄ Invert | Swaps background and line colors and clears the canvas |
| Color Mode | How each particle's color is determined (see below) |
| Saturation | Color vividness — only applies in non-Solid modes |
| Lightness | Color brightness — only applies in non-Solid modes |
| Hue Shift | Rotates the entire color palette by 0–359° |

**Color Modes**

| Mode | How color is assigned |
|---|---|
| Solid | Single fixed line color |
| Velocity | Particle speed maps to hue — fast = warm, slow = cool |
| Position | Horizontal position maps to hue across the full spectrum |
| Rainbow | Hue cycles globally over time |
| Depth | Particle direction angle maps to hue |

---

### 03 · Flow Field

| Control | Range | Description |
|---|---|---|
| Zoom | 0.005 – 0.25 | Noise sampling scale. Lower = broad smooth curves. Higher = tight complex swirls. |
| Cell Size | 2 – 30 | Grid resolution of the vector field. Smaller = finer detail, higher CPU cost. |
| Force | 0 – 1.5 | How strongly the field steers particles each frame |
| Octaves | 1 – 8 | Perlin noise octave count. More octaves = more fractal complexity. |
| Curl Noise | On / Off | Divergence-free vortex flow with no sources or sinks. Automatically enabled in Fluid mode. |
| Z Depth | 0 – 2 | Noise Z-axis offset. Active in Evolving and Chaotic modes — higher values mean a more evolved field state. |

---

### 04 · Lines

| Control | Range | Description |
|---|---|---|
| Opacity | 1 – 80 | Per-particle stroke alpha. Lower = more transparent, ghostly. |
| Weight | 0.2 – 5 | Stroke thickness in pixels |
| Fade Trail | On / Off | Overlays a semi-transparent wash each frame, gradually erasing old marks |
| Fade Speed | 1 – 40 | Opacity of the fade wash per frame. Lower = longer persistence. |

---

### 05 · Particles

| Control | Range | Description |
|---|---|---|
| Count | 50 – 2000 | Number of simultaneously active particles |
| Max Speed | 0.5 – 8 | Upper velocity limit per particle per frame |
| Lifespan | 30 – 1200 | Frames before a particle resets to a new random position |

---

### 06 · Symmetry

Applies a mirroring transform to every particle stroke before drawing. The canvas centre is the axis of symmetry.

| Mode | Effect |
|---|---|
| None | No mirroring |
| ⇔ X | Mirror left–right |
| ⇕ Y | Mirror top–bottom |
| 4-fold | Quad mirror — both axes simultaneously |
| ✦ 6 | 6-fold radial (60° rotational symmetry) |
| ✦ 8 | 8-fold radial (45° rotational symmetry) |
| ✦ 12 | 12-fold radial (30° rotational symmetry) |

---

### 07 · Attractors

Attractors are invisible point forces that pull or repel particles within a defined radius.

| Control | Description |
|---|---|
| Place Mode | Enable attractor placement. The canvas cursor switches to a crosshair. |
| Strength | Force magnitude. Positive = attract. Negative = repel. Range: −3 to 3. |
| Radius | Influence radius in pixels (30–500) |
| Active | Live count of placed attractors |
| Clear Attractors | Remove all attractors at once |

**Placement shortcuts**

| Action | Result |
|---|---|
| Click canvas | Place an attractor at that point |
| Shift + click | Remove the nearest attractor within 60px |
| Mobile tap | Same as click |

---

### 08 · Sound

All controls only apply when sound is enabled via the **♪ Sound** topbar button. The first enable requires a user gesture to satisfy browser autoplay policy.

| Control | Range | Description |
|---|---|---|
| Enable | On / Off | Master sound on/off |
| Volume | 0 – 1 | Master output level |
| Tempo (BPM) | 30 – 180 | Musical tempo. Notes snap to this grid. Affects trigger density of all voices. |
| Texture | 0.2 – 3.0 | Note density multiplier. Low = sparse, meditative. High = busy, complex. |
| Reverb | 0 – 1 | Wet/dry mix of the reverb effect. Higher = more spacious and diffuse. |
| Delay | 0 – 1 | Echo amount. Adds rhythmic delay taps. |
| Voicing | Auto / Close / Open / Wide | Chord spread across octaves. Auto follows the theme's default. |
| Melody | On / Off | Enables a floating melodic voice that walks the scale |
| Show Agents | On / Off | Renders the 6 sonic agents as coloured dots on the canvas |

When sound is active, a live readout displays the current **scale**, **chord name**, **timbre**, and a real-time **energy bar**.

---

### 09 · Wind & Forces

Persistent physical forces layered on top of the noise field. Collapsed by default.

| Control | Range | Description |
|---|---|---|
| Wind | On / Off | Enable a directional bias applied to all flow vectors |
| Wind Angle | 0 – 360° | Direction of the wind force |
| Wind Strength | 0 – 1 | Wind force magnitude |
| Gravity | On / Off | Enable downward particle pull. Negative values cause upward float. |
| Gravity Strength | −0.5 – 0.5 | Gravity force per frame. Negative = float upward. |
| Turbulence Burst | On / Off | Click the canvas to detonate a scatter-burst at that point |

> **Note:** Enabling Turbulence Burst automatically disables Attractor mode. The canvas shows a crosshair cursor in both modes.

---

### 10 · Export

| Control | Description |
|---|---|
| PNG 1× | Saves the current canvas frame at native resolution |
| PNG 2× | Saves at 2× pixel density for retina-quality output |
| Duration | Sets video recording length: 10s / 30s / 60s |
| ⏺ Record WebM | Starts a WebM video capture. Click again or wait for the timer to stop. A red badge counts elapsed seconds. |
| Full HD | Renders and saves a 1920×1080 wallpaper |
| 2K | Renders and saves a 2560×1440 wallpaper |
| 4K UHD | Renders and saves a 3840×2160 wallpaper |
| Mobile | Renders and saves a 1080×1920 portrait wallpaper |

Wallpaper export temporarily resizes the canvas, renders for ~3 seconds, saves the PNG, then restores the original canvas dimensions.

---

## Topbar Actions

| Button | Action |
|---|---|
| ⏸ Pause / ▶ Play | Freeze or resume the simulation |
| ✕ Clear | Wipe the canvas and start fresh |
| ↺ Seed | Randomize the Perlin noise seed — completely changes the flow pattern |
| ♪ Sound / ♪ On | Toggle the ambient audio engine |
| Theme dots | Switch between Minimal, Midnight, Neon, Ocean, Desert |
| FPS counter | Live frame-rate display (desktop only) |

---

## How the Sound Engine Works

Six invisible **sonic agents** drift through the flow field identically to visible particles. Each is permanently assigned one of six voice roles and plays its designated chord tone at a rhythmic interval governed by Tempo and Texture.

| Voice | Role |
|---|---|
| Bass | Root tone, low octave |
| Sub | Deep sub-bass reinforcement |
| Mid 1 | Third or fifth of the chord |
| Mid 2 | Complementary inner voice |
| Sparkle | High-register accent tone |
| Melody | Walks the scale independently (optional) |

**Why it always sounds musical**

- Notes are never random — every note belongs to the current chord and scale
- Each voice fires at a fixed interval, creating a rhythmic pulse
- Note duration has a small random jitter (±0.25 s) for a human feel
- Stereo pan follows the agent's X position in real time as it drifts across the field
- Filter cutoff and reverb wet mix respond to how chaotic the field is at that moment

**Theme switching** immediately resets the chord index to the new progression, scale, and timbre — the change is seamless.

---

## Flow Field Modes

| Mode | Icon | Behaviour |
|---|---|---|
| Smooth | ⟿ | Standard Perlin noise. Clean, organic curves with no time evolution. |
| Turbulent | 〜 | Per-particle random jitter layered over the noise. Rougher, more varied traces. |
| Evolving | ◎ | The Z-axis of the noise field advances slowly each frame. Patterns morph continuously. |
| Chaotic | ✦ | Evolving + jitter combined. Z Depth control becomes active. |
| Fluid | ∿ | Curl noise — divergence-free flow producing vortex aesthetics. Overrides the Curl toggle. |

---

## Visual Themes

Switching themes changes both the UI colour palette and the ambient sound character simultaneously.

| Theme | Palette | Sound character |
|---|---|---|
| Minimal | Light gray, charcoal | C Major · Serene, resolving |
| Midnight | Deep navy, cool blue | D Natural Minor · Cinematic, brooding |
| Neon | Black, electric green | D Minor Pentatonic · Driving, synthetic |
| Ocean | Sky blue, deep teal | F Lydian · Floating, expansive |
| Desert | Warm sand, burnt orange | C Mixolydian · Warm, modal |

---

## Dependencies

Both libraries are loaded from CDN — no `npm install` required.

| Library | Version | Purpose |
|---|---|---|
| [p5.js](https://p5js.org/) | 1.9.4 | Canvas 2D rendering, Perlin noise, particle system |
| [Tone.js](https://tonejs.github.io/) | 14.7.77 | Web Audio synthesis, reverb, delay, filter, transport clock |

---

## Browser Support

| Browser | Visual | Audio | Video Export |
|---|---|---|---|
| Chrome / Edge | ✅ | ✅ | ✅ Best codec support |
| Firefox | ✅ | ✅ | ✅ |
| Safari | ✅ | ✅ | ⚠ WebM may have limited support |

Video recording requires the `MediaRecorder` API. Chrome and Edge offer the best codec compatibility — the app automatically falls back through `vp9 → vp8 → webm`.

---

## License

MIT — do whatever you like with it.
