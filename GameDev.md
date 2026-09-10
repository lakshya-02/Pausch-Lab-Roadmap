# Game Development Roadmap

> **Last verified:** September 2026 — Unity 6.3 LTS (support through Dec 2027), Unreal Engine 5.6 (June 2025), Godot 4.5 (Sept 2025), WebGPU Baseline 2026

## 1. Foundational Principles

Before touching an engine, understand these. They apply everywhere.

- **The Game Loop** — Update vs FixedUpdate vs render. Frame delta time, tick rate, and determinism.
- **Architecture** — Composition over inheritance. Entity Component System (ECS) and data-oriented design.
- **State Management** — Finite and Hierarchical State Machines for player controllers, AI, and game states.
- **Game Feel** — Feedback systems: input buffering, coyote time, hit stop, screen shake, easing, audio timing.
- **Profiling** — Profile from prototype zero. CPU, GPU, memory, GC allocations, draw calls.

---

## 2. Engine Tracks

Pick one to start. All three are production-viable — choice depends on team size, target platform, and hiring context.

### 2.1 Unity — Unity 6.3 LTS

C#-based. Strongest for mobile, indie, and XR. Widest hiring base.

**Use when:** small-to-medium team, cross-platform (mobile/PC/console/Web), rapid iteration, XR.

**Core competencies:**
- **C#** — Delegates/events, ScriptableObjects for data, async (async/await, UniTask), zero-allocation tick code
- **Rendering** — Universal Render Pipeline (URP) with Render Graph, Shader Graph, VFX Graph, APV and light baking
- **Systems** — New Input System (Input Actions / PlayerInput), Cinemachine, Physics (Rigidbody, Character Controller, raycasting)
- **Performance** — DOTS, Entities/ECS, Job System, Burst Compiler
- **Multiplayer** — Netcode for GameObjects (NGO) + Unity Gaming Services
- **Platform** — Build Profiles, Platform Browser, WebGPU support for Unity Web (mobile browsers)

**Resources:**
- [Unity Learn — Junior Programmer Pathway](https://learn.unity.com/pathway/junior-programmer)
- [Unity Manual — Unity 6](https://docs.unity3d.com/Manual/index.html)
- [Catlike Coding — C# and Shader Tutorials](https://catlikecoding.com/unity/tutorials/)
- [Code Monkey — Kitchen Chaos Project](https://www.youtube.com/@CodeMonkeyUnity)
- [Tarodev — Architecture & Game Feel](https://www.youtube.com/@Tarodev)

---

### 2.2 Unreal Engine — UE 5.6

C++ & Blueprints. Industry standard for high-fidelity 3D and AAA pipelines.

**Use when:** high-fidelity PC/console, large team, graphics-heavy project.

**Core competencies:**
- **Framework** — GameMode, GameState, PlayerController, Pawn/Character, PlayerState
- **Blueprints + C++** — Blueprint for prototyping; C++ (`UCLASS`/`UPROPERTY`/`UFUNCTION`, smart pointers, GC) for systems
- **Rendering:**
  - **Nanite** — Virtualized micropolygon geometry, now with improved foliage and decal support
  - **Lumen** — Dynamic global illumination; HWRT optimizations for 60 FPS at scale in 5.6
  - **MegaLights** — Many-light solution introduced in 5.5, refined in 5.6
- **Simulation** — Chaos Physics (rigid body, destruction), Niagara VFX
- **Gameplay Systems** — Gameplay Ability System (GAS), Procedural Content Generation (PCG) Framework, Motion Matching / Anim Next
- **MetaHuman** — Now fully in-engine (Creator + Animator)
- **Ecosystem** — UEFN + Verse

**Resources:**
- [Unreal Engine 5.6 Release Notes](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-5.6-release-notes)
- [Epic Developer Community](https://dev.epicgames.com/community/)
- [Tom Looman — UE C++ Architecture](https://www.tomlooman.com/)
- [Druid Mechanics — GAS & C++](https://www.youtube.com/@DruidMechanics)

---

### 2.3 Godot — Godot 4.5

MIT-licensed, lightweight. Best for 2D, smaller 3D projects, and teams that value open source and full engine control.

**Use when:** 2D-first, open-source requirement, low overhead, Web or small-team 3D.

**Core competencies:**
- **Scene System** — Node/Scene tree, composition, instancing
- **Scripting** — GDScript 2.0 (typed, `@export`/`@onready`, `await`), C#/.NET, GDExtension (C++/Rust without engine fork)
- **Rendering** — Forward+ (desktop Vulkan), Mobile (Vulkan), Compatibility (OpenGL/WebGL 2); SDFGI / VoxelGI, stencil buffer (new in 4.5)
- **2D** — TileMap layers, 2D lighting, physics, pixel-perfect scaling
- **3D / XR** — NavigationServer3D, Jolt Physics (integrated since 4.4), OpenXR 1.1, visionOS support (new in 4.5), 16KB page support for Android 15
- **Tooling** — Embedded game window, interactive in-game editing

**Resources:**
- [Godot 4.5 Release Notes](https://godotengine.org/releases/4.5)
- [Godot Documentation](https://docs.godotengine.org/en/stable/)
- [Brackeys — Godot 4](https://www.youtube.com/@Brackeys)
- [GDQuest — Learn GDScript From Zero](https://gdquest.github.io/learn-gdscript/)

---

## 3. Web Games & Browser Graphics

No install, instant distribution, cross-platform. WebGPU reached Baseline across major browsers in 2026 — this is now the modern path.

**Standards:**
- **WebGL 2** — Stable fallback (OpenGL ES 3.0 in JS)
- **WebGPU** — Direct GPU access, compute shaders, lower JS overhead. Use where available; fall back to WebGL.

**2D Frameworks:**

| Framework | Notes |
|---|---|
| **Phaser 3 / 4** | Standard for commercial HTML5 2D |
| **PixiJS v8** | High-performance 2D renderer, WebGPU support |
| **LittleJS** | Minimal (<50KB), good for jams |
| **Kaplay** | Beginner-friendly wrapper |

**3D Frameworks:**

| Framework | Notes |
|---|---|
| **Three.js (r160+)** | Industry standard; WebGPURenderer + TSL now stable |
| **Babylon.js 8** | Full engine: Havok physics, Node Material, WebGPU + WebGL co-support |
| **React Three Fiber + Drei** | Declarative React layer over Three.js |

**WebAssembly:** Emscripten (C++) or wasm-bindgen / Bevy (Rust) for near-native performance.

**Resources:**
- [Three.js Journey — Bruno Simon](https://threejs-journey.com/)
- [WebGPU Fundamentals](https://webgpufundamentals.org/)
- [Babylon.js Documentation](https://doc.babylonjs.com/)
- [MDN — WebGPU API](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API)

---

## 4. Low-Level & Open-Source Tooling

For engine architecture, graphics programming, and toolchain independence.

**Frameworks:**
- **[Raylib](https://www.raylib.com/)** — Pure C, zero dependencies. Learn framebuffers, input, audio from first principles.
- **[Bevy](https://bevyengine.org/)** — Rust, ECS-native. Data-driven engine design.
- **[LÖVE (Love2D)](https://love2d.org/)** — Lua, minimal 2D.

**Content Pipeline:**

| Category | Tools |
|---|---|
| 3D Modeling | [Blender 4.x](https://www.blender.org/) — modeling, UVs, rigging, Geometry Nodes, glTF export |
| 2D Art | [Krita](https://krita.org/), [GIMP](https://www.gimp.org/) |
| Pixel Art | [LibreSprite](https://libresprite.github.io/), [Pixelorama](https://orama-interactive.itch.io/pixelorama) |
| Level Design | [LDtk](https://ldtk.io/), [Tiled](https://www.mapeditor.org/) |
| Audio | [Audacity](https://www.audacityteam.org/), [LMMS](https://lmms.io/), [Bfxr](https://www.bfxr.net/) |

**Graphics fundamentals:**
- *Game Engine Architecture* — Jason Gregory
- [LearnOpenGL](https://learnopengl.com/) — Joey de Vries
- [The Cherno — Engine Series](https://www.youtube.com/@TheCherno)

---

## 5. Asset Repositories

All free for prototyping. Check licenses before shipping.

- [Kenney.nl](https://kenney.nl/) — CC0 modular 3D/2D/UI/audio
- [OpenGameArt.org](https://opengameart.org/) — Community 2D/3D/audio
- [Poly Pizza](https://poly.pizza/) — Low-poly 3D
- [Mixamo](https://www.mixamo.com/) — Rigged characters + animations
- [ambientCG](https://ambientcg.com/) — CC0 PBR materials
- [Freesound.org](https://freesound.org/) — Collaborative audio
- [Soniss GDC Bundles](https://soniss.com/gameaudiobundles) — Commercial-grade audio packs

---

## 6. Suggested Progression

Build and ship — do not just follow tutorials.

1. **Micro-game** — One mechanic, one level, polished. Ship to itch.io.
2. **Systems project** — Inventory, save/load, state machines, pooling. Profile it.
3. **Multiplayer or procedural** — NGO lobby or PCG-generated level.
4. **Portfolio piece** — 2–3 minute polished vertical slice with trailer and GitHub repo.
