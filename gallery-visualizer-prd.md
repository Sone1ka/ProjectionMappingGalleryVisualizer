# Product Requirements Document
## Projection Mapping Gallery Visualizer

**Version:** 1.0  
**Status:** Draft  
**Last Updated:** 2026-03-13

---

## 1. Overview

### 1.1 Purpose

The Gallery Visualizer is a browser-based tool designed to simulate a projection-mapped gallery installation at scale. It enables artists and designers to compose multi-canvas layouts, preview animated projections layered onto painted subjects, and make informed decisions about canvas sizing, spacing, and projector field-of-projection — all without physical equipment.

### 1.2 Goals

- Provide a to-scale, labelled visual representation of a real-world gallery layout
- Simulate projection animation layered onto canvas subjects using blend modes
- Allow flexible canvas arrangement and sizing to optimize projection PPI output
- Support audio-visual synchronization for a complete installation preview

### 1.3 Non-Goals

- This tool is not a projection mapping engine or real-time 3D renderer
- It does not generate projection calibration files
- It does not manage or export installation schedules or event timelines

---

## 2. User Stories

| ID | As a... | I want to... | So that... |
|----|---------|--------------|------------|
| US-01 | Artist | Upload a PNG image and a video animation per canvas | I can preview how my projection will look on the painted surface |
| US-02 | Artist | Set real-life canvas dimensions | The layout is rendered accurately to scale |
| US-03 | Artist | Drag canvases around the visualizer | I can test different spatial arrangements |
| US-04 | Artist | Snap canvases to a half-inch grid | I can align edges precisely |
| US-05 | Artist | Pause and resume all video playback | I can reposition canvases without distraction |
| US-06 | Artist | Reset playback to the beginning | I can review the animation from the start at any time |
| US-07 | Artist | Upload a background audio file | I can preview the full audiovisual experience |
| US-08 | Artist | Edit individual canvases (resize, replace media, delete) | I can iterate on each element independently |
| US-09 | Artist | Add new canvases to the layout | I can expand my composition dynamically |
| US-10 | Artist | See labelled dimensions and gaps between canvases | I can evaluate spacing decisions for the real installation |
| US-11 | Artist | Switch between overlay blend modes | I can assess how different projection blending options affect the result |

---

## 3. Feature Requirements

### 3.1 Canvas & Grid System

#### 3.1.1 To-Scale Grid

- The visualizer workspace renders a grid measured in **inches**
- Grid lines appear at regular intervals (e.g., every 1 inch), with major lines at every 6 or 12 inches
- The grid is visible as a subtle underlay behind all canvases
- The grid and canvas positions must remain proportionally consistent regardless of zoom level

#### 3.1.2 Dimension Labels

- Each canvas displays its **width × height** in inches as a persistent label
- The overall composition (bounding box of all canvases) displays its **total width** and **total height** in inches
- Gaps between adjacent canvases are labelled with the distance in inches
- Labels update in real time as canvases are moved or resized

#### 3.1.3 Canvas Sizing

- Users may specify real-life canvas dimensions (width and height in inches) per canvas
- Minimum canvas size: 1 × 1 inch
- No enforced maximum; large canvases should remain navigable via pan/zoom

---

### 3.2 Media Layering & Blend Modes

#### 3.2.1 Per-Canvas Media

Each canvas supports two media layers:

| Layer | Type | Description |
|-------|------|-------------|
| Base | PNG image | Represents the painted canvas surface |
| Overlay | Video file | Represents the projected animation |

- Both layers are uploaded independently per canvas
- Either layer may be absent (canvas renders a placeholder if no media is uploaded)

#### 3.2.2 Overlay Blend Modes

- The video layer is composited over the PNG using a selectable blend mode
- Default blend mode: **Hard Light** (simulates projector light on a painted surface)
- Additional modes available via a global overlay mode selector:
  - Hard Light *(default)*
  - Screen
  - Multiply
  - Overlay
  - Normal (video only, no blending)
- Blend mode applies globally to all canvases simultaneously

---

### 3.3 Drag, Drop & Snap

#### 3.3.1 Dragging

- Each canvas is individually draggable within the visualizer workspace
- Dragging is disabled while videos are playing (users must pause first, or dragging auto-pauses)
- Canvas z-order adjusts on drag (active canvas moves to front)

#### 3.3.2 Snap to Grid

- A **"Snap" toggle** enables snapping behaviour
- When enabled, canvas positions round to the nearest **0.5 inch** on drop
- Snapping applies to all four edges of a canvas, not just the origin point
- Visual snap guides (hairlines) appear when a canvas edge aligns with another canvas edge or grid line

---

### 3.4 Playback Controls

#### 3.4.1 Global Play / Pause

- A **Play/Pause button** in the main toolbar controls all canvas videos simultaneously
- Background audio (if uploaded) plays and pauses in sync with video playback
- Playback state is visible at all times (icon changes between play and pause states)

#### 3.4.2 Reset

- A **Reset button** rewinds all videos and audio to the 00:00 mark
- Reset does not clear canvas layout or media uploads
- After reset, playback remains paused until the user presses Play

---

### 3.5 Background Audio

- Users may upload a single background audio file (MP3 or WAV)
- Audio plays and pauses in sync with the global play/pause control
- Audio resets to the beginning when the Reset button is pressed
- Audio volume is adjustable via a slider in the toolbar
- Audio upload is optional; the visualizer functions normally without it

---

### 3.6 Edit Mode

Activating **Edit Mode** from the main toolbar allows per-canvas editing. When Edit Mode is active:

- Clicking a canvas opens its **Canvas Editor Panel**, which exposes:

| Action | Description |
|--------|-------------|
| Resize | Adjust width and height in inches via numeric input fields |
| Replace Image | Upload a new PNG to replace the existing base layer |
| Replace Video | Upload a new video to replace the existing overlay layer |
| Delete Canvas | Permanently removes the canvas from the layout |

- An **Add Canvas** button (visible in Edit Mode) creates a new blank canvas with default dimensions (e.g., 12 × 12 inches) placed at the centre of the viewport

- Exiting Edit Mode returns to the standard interactive view

---

### 3.7 Main Layout & UI

#### 3.7.1 Layout Structure

```
┌─────────────────────────────────────────────────────┐
│                     Toolbar                         │
│  [Play/Pause] [Reset] [Overlay Mode ▾] [Edit Mode]  │
│                   [Volume ───●───]                  │
├─────────────────────────────────────────────────────┤
│                                                     │
│              Gallery Workspace                      │
│         (Black background, grid overlay)            │
│                                                     │
│    ┌──────────┐       ┌──────────┐                  │
│    │ Canvas A │ 4"──► │ Canvas B │                  │
│    └──────────┘       └──────────┘                  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### 3.7.2 Toolbar Elements

| Element | Type | Description |
|---------|------|-------------|
| Play / Pause | Toggle button | Global video + audio playback control |
| Reset | Button | Rewinds all media to 00:00 |
| Overlay Mode | Dropdown | Selects the blend mode for video overlays |
| Edit Mode | Toggle button | Enables per-canvas editing and canvas creation |
| Volume | Slider | Controls background audio volume |
| Snap | Toggle | Enables/disables half-inch snapping |

#### 3.7.3 Visual Design

- Background: solid black (`#000000`)
- Grid: low-opacity white or grey lines
- Canvas labels and dimension annotations: high-contrast white or light grey text
- Toolbar: docked to the top of the screen, always visible

---

## 4. Technical Considerations

### 4.1 Scale Representation

- The visualizer uses a configurable **pixels-per-inch (PPI) scale factor** to translate real-world inches to screen pixels
- A zoom control (or pinch-to-zoom on supported devices) adjusts the visible scale without changing canvas dimensions
- All dimension labels always reflect real-world inches, regardless of zoom

### 4.2 Video Performance

- Videos are loaded and decoded locally in the browser (no server-side processing)
- Playback is synchronised across all canvases using a shared time reference
- Pausing before dragging is enforced (or auto-triggered) to prevent dropped frames affecting layout decisions

### 4.3 Blend Mode Implementation

- Blend modes are applied using CSS `mix-blend-mode` or Canvas 2D API `globalCompositeOperation`
- Hard Light is the required default and must render accurately relative to projector simulation intent

### 4.4 File Support

| Media Type | Accepted Formats |
|------------|-----------------|
| Base image | PNG |
| Overlay video | MP4, WebM |
| Background audio | MP3, WAV |

---

## 5. Out of Scope (v1.0)

- Multi-user / collaborative editing
- Export to video or image file
- Undo / redo history
- Saving and loading layout sessions (local storage or file export)
- Keystone correction or perspective warping simulation
- Mobile / touch-first interface (desktop browser is the primary target)

---

## 6. Open Questions

| # | Question | Owner |
|---|----------|-------|
| OQ-01 | Should snap behaviour apply while dragging (live) or only on drop? | To be decided |
| OQ-02 | Should blend mode be configurable per canvas or only globally? | To be decided |
| OQ-03 | Is a zoom/pan control required in v1.0, or is a fixed scale sufficient? | To be decided |
| OQ-04 | Should canvas layout persist between sessions (e.g., via local storage)? | To be decided |
| OQ-05 | What is the target maximum number of canvases in a single session? | To be decided |
