# Flow Field · Generative Art

An interactive, browser-based generative art canvas built with [p5.js](https://p5js.org/) and [Tone.js](https://tonejs.github.io/). Particles drift through a Perlin noise flow field, tracing organic lines across the canvas — optionally accompanied by a chord-based ambient soundtrack that follows the same field.

---

## Features

### Visual
- **5 flow field modes** — Smooth, Turbulent, Evolving, Chaotic, Fluid (curl noise)
- **5 color modes** — Solid, Velocity, Position, Rainbow, Depth
- **Symmetry options** — horizontal, vertical, quad, 6/8/12-fold radial
- **Attractor system** — click the canvas to place gravity/repulsion points
- **Fade trails** — optional ghost-fade effect for long-exposure aesthetics
- **5 visual themes** — Minimal, Midnight, Neon, Ocean, Desert

### Sound
- **Ambient audio engine** powered by Tone.js
- **4 sonic agents** navigate the flow field and trigger notes based on their position
- Each theme plays a unique chord progression in a fitting key and scale:

| Theme | Scale | Progression |
|---|---|---|
| Minimal | C Major | I – vi – IV – V |
| Midnight | D Natural Minor | i – VII – VI – VII |
| Neon | D Minor Pentatonic | i – bIII – bVII – IV |
| Ocean | F Lydian | I – II – IV – I |
| Desert | C Mixolydian | I – bVII – IV – I |

- Stereo panning follows agent X position in real time
- Filter cutoff and reverb wet mix modulate dynamically based on flow field activity

### Export
- PNG screenshot (1× and 2×)
- WebM video recording (10 / 30 / 60 seconds)
- Wallpaper presets (Full HD, 2K, 4K, Mobile)

---

## How to Use

1. Clone or download the repository
2. Open `index.html` in any modern browser — no build step needed
3. Use the control panel on the right to adjust the simulation
4. Click **♪ Sound** to enable the ambient soundtrack
5. Click **⚂ Seed** to randomize the noise pattern
6. In Attractor mode, click the canvas to place attractors (Shift+click to remove)

---

## Controls

| Section | Control | Description |
|---|---|---|
| Canvas | Width / Height | Resize the output canvas |
| Color | Background / Line | Pick colors for background and particles |
| Color | Color Mode | How particle color is determined |
| Flow Field | Zoom (inc) | Noise sampling scale — lower = smoother curves |
| Flow Field | Strength | How strongly the field steers particles |
| Flow Field | Z Speed | How fast the field evolves over time |
| Flow Field | Curl Mode | Enables divergence-free vortex flow |
| Lines | Stroke Weight | Particle line thickness |
| Lines | Transparency | Per-frame line opacity |
| Lines | Fade | Gradually fades old lines each frame |
| Particles | Count | Number of active particles |
| Particles | Speed | Maximum particle velocity |
| Particles | Lifespan | How many frames before a particle resets |
| Symmetry | Mode | Mirror / radial symmetry options |
| Attractors | Strength / Radius | Gravity or repulsion force and reach |
| Sound | Volume | Master output level |

---

## How the Sound Works

Four invisible "sonic agents" move through the flow field just like visible particles. Each agent is assigned a voice role — bass, mid 1, mid 2, and sparkle — and plays its designated chord tone from the current chord at a fixed interval. This means:

- **Notes are never random** — they always belong to the current chord
- **Timing is regular** per voice, creating a rhythmic pulse
- **Note duration** has a small random jitter (±0.25 s) for a human feel
- **Stereo pan** follows the agent's X position as it drifts through the field
- **Filter and reverb** respond to how busy or chaotic the flow field is at that moment

The result is generative harmony that stays musical while remaining alive.

---

## Dependencies

Both libraries are loaded from CDN — no installation required.

| Library | Version | Purpose |
|---|---|---|
| [p5.js](https://p5js.org/) | 1.9.4 | Canvas rendering, Perlin noise, particle system |
| [Tone.js](https://tonejs.github.io/) | 14.7.77 | Web Audio synthesis, reverb, delay, filter |

---

## Browser Support

Works in any modern browser with Web Audio API support (Chrome, Firefox, Safari, Edge). Video recording requires `MediaRecorder` support (Chrome / Edge recommended for best codec compatibility).

---

## License

MIT — do whatever you like with it.
