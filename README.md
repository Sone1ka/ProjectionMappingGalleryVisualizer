# Gallery Visualizer

A browser-based tool for visualizing projection-mapped gallery installations to scale. Compose multi-canvas layouts, preview animated projections blended onto painted subjects, and make informed decisions about canvas sizing, spacing, and projector field-of-projection — all without a projector or physical setup.

---

## Getting Started

No installation required. Open `gallery-visualizer.html` in any modern desktop browser (Chrome, Firefox, Edge, Safari).

---

## Interface Overview

```
┌─────────────────────────────────────────────────────────────┐
│  Gallery Viz  [Play] [Reset] [Blend ▾] [Snap] [Edit] [Audio]│  ← Toolbar
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                  Gallery Workspace                          │
│            (black background, inch grid)                    │
│                                                             │
│   ┌──────────────┐  ←4"→  ┌──────────────┐                 │
│   │   Canvas A   │        │   Canvas B   │                 │
│   │  24" × 18"   │        │  24" × 18"   │                 │
│   └──────────────┘        └──────────────┘                 │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  ● Paused   Canvases: 2   Composition: 52.0" × 18.0"  100% │  ← Status bar
└─────────────────────────────────────────────────────────────┘
```

---

## Features

### Canvas Management

- **Add canvases** via Edit Mode — set any real-world width and height in inches
- **Drag** canvases freely around the workspace to test different arrangements
- **Snap to grid** — positions round to the nearest 0.5" on drop (toggle on/off)
- **Arrow key nudge** — move selected canvas in 0.5" steps (hold Shift for 1" steps)
- **Resize** — drag corner handles in Edit Mode, or enter exact dimensions in the panel
- **Delete** — remove any canvas individually via the Edit panel

### Media Layers

Each canvas supports two independent layers:

| Layer | Format | Description |
|-------|--------|-------------|
| Base image | PNG | Your painted canvas subject |
| Overlay video | MP4, WebM | The projected animation |

The video is composited over the image using a CSS blend mode to simulate how a projector overlays light onto a painted surface.

### Blend Modes

Select from the toolbar dropdown to change how the video layer blends with the image:

- **Hard Light** *(default — most realistic projector simulation)*
- Screen
- Multiply
- Overlay
- Normal
- Color Dodge
- Luminosity

### Playback Controls

| Control | Action |
|---------|--------|
| **Play / Pause** | Starts or stops all canvas videos simultaneously |
| **Reset** | Rewinds all videos and audio to 00:00, stays paused |
| **Space bar** | Toggle play/pause from anywhere |

### Background Audio

Upload an MP3 or WAV file via the **Audio** button in the toolbar. Audio plays and pauses in sync with the video playback and resets with the Reset button. Volume is adjustable via the toolbar slider.

### Dimension Annotations

All measurements are displayed in **real-world inches**:

- 🟡 **Per-canvas width** — dimension line below each canvas
- 🟡 **Per-canvas height** — dimension line to the right of each canvas
- 🟠 **Gap between canvases** — measured between facing edges, shown in orange
- ⬜ **Total composition size** — outer ruler showing full width × height of the layout

Annotations update in real time as you drag or resize.

### Navigation

| Action | How |
|--------|-----|
| Zoom in/out | Scroll wheel |
| Pan the workspace | Alt + drag |
| Select a canvas | Click it |
| Deselect | Click empty space or Escape |
| Open Edit panel | Enable Edit Mode, then click a canvas |

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` | Play / Pause |
| `R` | Reset |
| `E` | Toggle Edit Mode |
| `Escape` | Deselect / close panel |
| `Arrow keys` | Nudge selected canvas 0.5" |
| `Shift + Arrow` | Nudge selected canvas 1" |
| `Delete / Backspace` | Delete selected canvas (Edit Mode only) |

---

## Workflow Example

1. Open the file in your browser
2. Press **E** to enter Edit Mode
3. Set your canvas dimensions (width × height in inches) and click **+ Add Canvas**
4. Repeat for each panel in your installation
5. Drag canvases into your intended layout — use **Snap** to align edges cleanly
6. Click a canvas, then upload your **PNG** base image and **video** overlay
7. Select a **blend mode** that matches your projection setup (Hard Light recommended)
8. Optionally upload a **background audio** track
9. Press **Space** to preview the full animation
10. Use the dimension annotations and total composition readout to decide on your projector field size and optimal PPI

---

## Technical Notes

- Runs entirely in the browser — no server, no dependencies, no install
- All media is loaded locally via `ObjectURL`; nothing is uploaded anywhere
- Scale is set at **8 pixels per inch** at 100% zoom — zoom in for detail, zoom out for full-layout overview
- The annotation SVG layer lives outside the pan/zoom transform so labels always align precisely with canvas corners

---

## File Support

| Type | Formats |
|------|---------|
| Base image | PNG (any resolution) |
| Overlay video | MP4, WebM |
| Background audio | MP3, WAV |

---

## Browser Compatibility

Recommended: **Chrome** or **Edge** (best video blend mode support).
Firefox and Safari are supported but `mix-blend-mode` rendering on video elements may vary slightly.
