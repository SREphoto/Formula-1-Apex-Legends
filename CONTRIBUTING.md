# 🤝 Co-Developer & Contributor Guide — Formula 1 Apex Legends

Welcome! We are building **Formula 1 Apex Legends** ([formula-1-apex.web.app](https://formula-1-apex.web.app/?utm_source=github&utm_medium=contributing_md&utm_campaign=header))—an interactive 3D WebGL Digital Twin, CFD Wind Tunnel, and 24-Circuit Grand Prix Racing Simulator built around the **2026 FIA Formula 1 "Nimble Car" Technical Regulations**.

This document explains how our **Dual-Repository Workflow** operates, what **Co-Developer Roles** are open, and how to apply to join the engineering team.

---

## 1. Dual-Repository Architecture (Public Showcase vs. Private Core)

To protect licensed 3D motorsport assets and core physics IP while maintaining an open roadmap and community hub, we operate two linked repositories:

1. **Public Showcase & Community Hub (`SREphoto/Formula-1-Apex-Legends` — *this repository*):**
   - Houses the public technical documentation, **[6-Phase Engineering Roadmap (`ROADMAP.md`)](./ROADMAP.md)**, **[Investor & Sponsor Pitch Deck (`FUNDING_AND_PITCH.md`)](./FUNDING_AND_PITCH.md)**, issue tracker, bug reports, and co-developer applications.
2. **Private Production Engineering Repository (`SREphoto/2026-F1-Nimble-Car`):**
   - Houses the full ES6/Three.js source code (`app.js`, `cad/game/`, `cad/track/`, `cad/sim/`, `cad/audio/`), Python TUMFTM quadratic-programming racing-line toolchain, Blender `.glb` pipeline, automated test suite (`tests/`), and Firebase Hosting/Firestore deployment config.
   - **Approved Co-Developers are granted direct collaborator access to `SREphoto/2026-F1-Nimble-Car`.**

---

## 2. Open Co-Developer Tracks

We are actively recruiting **Co-Developers** across four technical tracks. Whether you want to contribute as a core partner (revenue-share / equity / co-author credit) or tackle specific open roadmap modules, we want to hear from you:

### Track 1: Vehicle Dynamics & 2026 FIA Physics Engineer
- **Scope:** Evolve `cad/track/track_mode.js` from our current kinematic bicycle model into a **4-Wheel Dynamic Rigid-Body & Pacejka Magic Formula Tire Solver** ([Phase 1 & Phase 2 of `ROADMAP.md`](./ROADMAP.md)).
- **Key Modules:**
  - Longitudinal & lateral load transfer across `FL`, `FR`, `RL`, `RR` contact patches.
  - Tire compound thermal & mechanical degradation (`Soft`, `Medium`, `Hard`, `Inter`, `Wet`) and off-line "marbles" pickup penalties.
  - 2026 FIA Power Unit rules: `350 kW` MGU-K deployment, `8.5 MJ/lap` regenerative braking harvest, straight-line super-clipping, and Manual Override Mode (`MOM`).
  - Clean vs. dirty air turbulent wake (`15–35%` cornering downforce loss + straight-line slipstream tow).

### Track 2: 3D Graphics, WebGL/WebGPU & Shader Engineer
- **Scope:** Elevate real-time visual fidelity in Three.js r160 (`cad/materials.js`, `cad/track/`, `cad/AeroStreamlineBackground.js`) while maintaining 60 FPS on desktop and iOS Safari PWA.
- **Key Modules:**
  - Custom GLSL shaders for procedural carbon-fiber weave with clearcoat, glowing heat-reactive carbon-ceramic brake discs, and wet-weather planar track reflections.
  - Particle systems for rain spray, lock-up tire smoke, underfloor titanium skid-block sparks, and gravel dust.
  - Cascaded shadow maps, baked stadium ambient occlusion, and dynamic time-of-day skyboxes (Sunset / Night floodlights at Las Vegas, Singapore, Bahrain).

### Track 3: AI Racecraft & Pit Strategy Systems Engineer
- **Scope:** Upgrade our 19 AI constructor rivals and build the **Interactive Race Strategy Simulator** ([Phase 4 of `ROADMAP.md`](./ROADMAP.md)).
- **Key Modules:**
  - Multi-line AI spatial awareness: slipstream pull-out, inside defensive blocks, late-braking dives, and blue-flag/yellow-flag Virtual Safety Car (`VSC`) compliance.
  - Interactive Undercut / Overcut Pit Strategy Planner with real-time stint degradation curves and pit-window loss calculation.
  - 24-Race World Championship progression state machine (`localStorage` + Cloud Firestore sync).

### Track 4: iOS / Mobile PWA, Audio Synthesis & Force-Feedback Input Engineer
- **Scope:** Expand mobile and sim-rig hardware immersion.
- **Key Modules:**
  - Native iOS/iPadOS wrapper (Swift / WKWebView or Capacitor) with CoreHaptics kerb and shift vibrations.
  - Web Gamepad API & steering wheel Force Feedback (`FFB`) curves for self-aligning torque and kerb rumble.
  - Multi-harmonic WebAudio API 2026 1.6L V6 Turbo-Hybrid engine synthesis (`15,000 RPM` ICE + `350 kW` MGU-K electric whine + exhaust overrun crackles).

---

## 3. Codebase Standards (Private Engineering Repo)

Once onboarded to `SREphoto/2026-F1-Nimble-Car`, contributors follow our modular engineering standards:

- **Zero-Build Native ES Modules:** The web application runs directly as native ES6 modules (`import * as THREE from 'three'`) via `<script type="importmap">` for instant local iteration and zero bundler bloat.
- **Spatial Coordinate Convention:** Right-handed 3D world space where `+X` is forward (Rear-to-Nose), `+Y` is vertical up (Ground-to-Roof), and `+Z` is lateral right.
- **Performance Guardrails:**
  - Startup assets must load lazily (`weekend_scenes.js`, `.mp3` audio, and circuit `.glb` geometries stream on demand).
  - Never block the main thread during initial `#apex-loader` boot.
- **Automated Verification (`npm test`):**
  - Every pull request must pass `npm test`, which validates module syntax across 24 core entrypoints, active aero state transitions (`test_aero_state.js`), 3D globe raycasting (`test_globe_raycast.js`), and WebGL memory disposal (`test_track_unloader.js`).

---

## 4. How to Apply

Ready to build the future of browser and mobile motorsport simulation with us?

👉 **[Submit a Co-Developer Application Issue](https://github.com/SREphoto/Formula-1-Apex-Legends/issues/new?template=co-developer-application.yml)**

We review every application personally and typically respond within 48 hours to schedule a quick technical intro and grant private repo access.
