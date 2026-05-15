# Resonance Field

A real-time 3D DNA double helix that breathes with sound.

Open `index.html` in any browser — no server, no build step, no dependencies.

---

## What it is

The helix listens to your microphone and maps the frequency content of sound directly onto its form. Bass pulses the radius. Mid frequencies drive strand brightness. Treble lights up the base-pair rungs. The spectral centroid sweeps color along the structure in real time. When the room is silent, the helix breathes on its own.

If microphone access is denied, it runs in demo mode automatically.

---

## Structure

Two helical backbones rotate continuously under perspective projection:

- **Strand A** — cyan `#00D8FF`
- **Strand B** — violet `#CF3DFF`
- **Base pairs** — cross-rungs sweeping **amber → cyan → violet** along the helix, driven by spectral centroid
- **Background** — curl-noise particle field that accelerates with bass

The helix is z-sorted each frame (painter's algorithm) so depth reads correctly as it rotates.

---

## Controls

A collapsible panel on the right edge. Click the **Controls** tab to open or close it.

### Audio Filters
| Slider | Range | Effect |
|---|---|---|
| Bass | 0 – 2 | Scales how much bass energy drives the helix radius |
| Mid | 0 – 2 | Scales mid-band influence on strand brightness |
| Treble | 0 – 2 | Scales treble influence on rung glow |

### Form
| Slider | Range | Effect |
|---|---|---|
| Rotate | 0 – 3 | Helix spin speed |
| Glow | 0 – 2 | Overall brightness and node size |
| Twist | 2 – 10 | Number of full helix turns |
| Radius | 0.3 – 2 | Helix width |

---

## Audio Mapping

| Audio feature | Visual parameter |
|---|---|
| Bass energy | Helix radius pulse |
| Mid energy | Backbone strand brightness |
| Treble energy | Base-pair rung glow + midpoint highlight |
| Total energy | Rotation speed · organic waveform deformation · node scale |
| Spectral centroid | Color position along the amber → cyan → violet sweep |

Detection uses HPS (Harmonic Product Spectrum) for fundamental frequency and FFT band integration for bass / mid / treble splits.

---

## Technical Notes

- Pure HTML5 Canvas 2D — no WebGL, no libraries
- Inline Perlin noise (Ken Perlin's permutation table) — no CDN
- Dual canvas: background particles on `bgCanvas`, helix on `fgCanvas` (both `z-index` stacked)
- 3D projection: Y-axis rotation + static X-tilt (0.42 rad), perspective divide, `FOCAL = 580`
- Additive blending (`globalCompositeOperation = 'lighter'`) for glow layers

---

## Author

Franz Boehmann · franz.boehmann@gmail.com
