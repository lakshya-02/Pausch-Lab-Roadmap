# Pausch Lab Roadmap

A structured learning path for Game Development and Extended Reality (XR). Designed to take you from fundamentals to production-ready work.

Named in honor of Dr. Randy Pausch, professor of Computer Science and Human-Computer Interaction, creator of *Building Virtual Worlds* and author of *The Last Lecture*.

This roadmap is open to everyone. It is maintained by [Next Tech Lab](https://ntlap.in/) and serves as the primary curriculum for Pausch Lab associates.

> **Last verified:** September 2026 | Engine versions: Unity 6.3 LTS, Unreal Engine 5.6, Godot 4.5, Horizon OS / Meta Quest 3/3S, visionOS 26

---

## How to Use This Roadmap

1. Complete **Prerequisites** below — do not skip.
2. Choose a track: **[Game Development](GameDev.md)** or **[Extended Reality (XR)](XR.md)**. You can do both, but start with one.
3. Build in public. Each track ends with milestones — ship them to GitHub.

### Principle: Learn, Don't Vibecode

This roadmap teaches skills, not shortcuts. AI can scaffold code, but it cannot fix motion sickness from a 35 ms pipeline, broken presence from bad interaction, or a 300 draw-call scene on a mobile SoC.

**Fundamentals first → build once from scratch → then use production SDKs → profile on device → ship with a write-up.** See the full rationale in [XR.md — How to Use This Roadmap](XR.md#how-to-use-this-roadmap--learn-dont-vibecode).

---

## Prerequisites

Complete these before specializing. They are non-negotiable for either track.

### 1. Linear Algebra & 3D Mathematics
Vectors (dot/cross product, normalization, projection), coordinate spaces (local/world/view/clip/screen), matrices (translation/rotation/scale/projection), quaternions and Euler angles (gimbal lock, SLERP).

Reference: [Freya Holmér — Math for Game Developers](https://www.youtube.com/@Acegikmo)

### 2. Programming
Pick one from each row:

| Purpose | Options |
|---|---|
| Application scripting | **C#** (Unity, Godot) or **TypeScript** (Web, WebXR) |
| Systems / engine | **C++** (Unreal, Raylib) or **Rust** (Bevy, WASM) |

- C#: [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/)
- TypeScript: [MDN — JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- C++: [learncpp.com](https://www.learncpp.com/)
- Rust: [The Rust Book](https://doc.rust-lang.org/book/)
- Godot scripting: [GDScript](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html)

### 3. Computer Science Fundamentals
Data structures, time/space complexity, composition over inheritance, Entity Component System (ECS), finite and hierarchical state machines (FSM/HSM), memory allocation and cache locality.

### 4. Computer Graphics Basics
Rendering pipeline (vertex processing → rasterization → fragment shading → framebuffer), shaders (GLSL/HLSL/WGSL), materials and lighting.

Reference: [LearnOpenGL](https://learnopengl.com/)

### 5. Version Control
Git fundamentals and Git LFS for binary assets.

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Desktop](https://desktop.github.com/)
- [Git LFS](https://git-lfs.com/)

---

## Tracks

### [Game Development](GameDev.md)
Engine-focused production tracks.

| Track | Stack |
|---|---|
| **Unity** | Unity 6.3 LTS, C#, URP / Render Graph, Input System, Cinemachine, Netcode for GameObjects, DOTS/ECS |
| **Unreal Engine** | UE 5.6, C++ & Blueprints, Nanite, Lumen & MegaLights, Chaos Physics, Niagara, GAS, PCG |
| **Godot** | Godot 4.5, GDScript 2.0 / C# / GDExtension, Forward+ / Mobile / Compatibility renderers |
| **Web** | WebGL 2, WebGPU (Baseline 2026), Three.js / Babylon.js, Phaser / PixiJS, WASM (Rust/Bevy) |
| **Low-Level / FOSS** | Raylib (C), Bevy (Rust), Blender 4.x, LDtk/Tiled, Audacity |

### [Extended Reality (XR)](XR.md)
Standards, hardware and spatial computing.

| Track | Stack |
|---|---|
| **Core & OpenXR** | OpenXR 1.1, 6DoF tracking, motion-to-photon latency, ergonomics |
| **Virtual Reality** | Unity XRI 3.x + XR Hands, Meta XR SDK (Interaction/Haptics), Horizon OS on Quest 3/3S |
| **Augmented Reality** | Unity AR Foundation 6 (ARKit/ARCore), Vuforia (Model/Area Targets), Lightship VPS |
| **Mixed Reality** | Passthrough, Scene Understanding, Spatial Anchors, Meta MRUK, Apple visionOS 26 (RealityKit, SwiftUI) |
| **WebXR** | WebXR Device API, Three.js / Babylon.js WebXR, Wonderland Engine |

---

## Repository Structure

```
README.md          — This overview and prerequisites
GameDev.md         — Game Development tracks
XR.md              — Extended Reality tracks
CONTRIBUTING.md    — Contribution guidelines
```

## Version Control Standards

**1. Track large binaries with Git LFS before first push:**
```bash
git lfs install
git lfs track "*.psd" "*.fbx" "*.obj" "*.blend" "*.wav" "*.mp4" "*.tga"
git add .gitattributes
```

**2. Never commit generated artifacts:**
`Library/`, `Temp/`, `obj/`, `Binaries/`, `DerivedDataCache/`, `Intermediate/`, `Saved/`, `.godot/`, `build/`

Use the canonical gitignore for your engine:
- [Unity](https://github.com/github/gitignore/blob/main/Unity.gitignore)
- [Unreal Engine](https://github.com/github/gitignore/blob/main/UnrealEngine.gitignore)
- [Godot](https://github.com/github/gitignore/blob/main/Godot.gitignore)

**3. Branching:**
- `main` — stable, reviewed, playable
- `dev` — integration
- `feature/<name>` — isolated work

---

## Contributing

This is a curated lab curriculum. See [CONTRIBUTING.md](CONTRIBUTING.md) before proposing changes — please open an issue first for non-trivial edits. Small, version-verified PRs with a clear learning rationale are merged fastest.

---

*Maintained by Pausch Lab @ [Next Tech Lab](https://ntlap.in/).*
