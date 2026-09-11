# Extended Reality (XR) Learning Path

> **Last verified:** September 2026 — OpenXR 1.1, Meta XR SDK v205.0 (Horizon OS), visionOS 26, WebXR + WebGPU, Unity 6.3 LTS / UE 5.6 / Godot 4.5

A complete learning path for anyone starting in Extended Reality — Virtual Reality, Augmented Reality, Mixed Reality, and WebXR. From first principles to a shippable portfolio.

No prior headset required to start. Each section tells you what to learn, why it matters, and how to practice it.

---

## How to Learn XR Properly

XR is not web development. Constraints are physical — latency makes people nauseous, bad interaction breaks presence, and unoptimized scenes drop frames on mobile chips. You cannot prompt your way past that.

**How this roadmap works:**

1.  **Fundamentals before tools.** Understand 3D math, rendering basics, and OpenXR before installing any SDK. If you cannot explain a quaternion or a frame budget, you are not ready for hand tracking.
2.  **Build once from scratch, then use the SDK.** Implement a grab, a raycast, or a passthrough shader manually once. Then switch to production tools (XRI, Interaction SDK, MRUK). You will understand what the abstraction hides.
3.  **Read the documentation.** Tutorials get you started — official docs keep you current. Every section links to the docs for a reason.
4.  **Measure on device.** Emulators and editor play mode are for iteration. Frame time, draw calls, and memory must be verified on a headset.
5.  **Ship and write up.** A private project you cannot explain is not a skill. Each milestone asks for a public repo, a short write-up of trade-offs, and a playable build or URL.

Follow the order. Do the exercises. Do not skip to Mixed Reality before you can hold a frame rate in VR.

---

## 1. Core Standards & Foundations

Start here regardless of whether you want VR, AR, or MR.

### OpenXR — The Industry Standard

XR used to be fragmented — Oculus SDK, OpenVR, Windows Mixed Reality, ARKit each had their own API. Today, the industry builds on **OpenXR 1.1** (Khronos Group), an open, royalty-free standard that sits between your engine and the headset runtime.

- **What it does:** One code path can target Quest (Horizon OS), SteamVR, Pico, and others.
- **Where it runs:** Native in Unity (OpenXR Plugin), Unreal (OpenXR), Godot 4.5 (OpenXR 1.1), and in the browser via WebXR.
- **What to actually learn:** Action-based input, session lifecycle, reference spaces, and interaction profiles. Skim the [OpenXR 1.1 overview](https://www.khronos.org/openxr/) — you don't need to memorize the spec, but you need to understand the layer you are building on.

### Tracking, Latency & Comfort

These are not optional details — they determine whether your app is usable.

| Concept | What it means | Why you need to know it |
|---|---|---|
| **3DoF** | Rotation only (yaw / pitch / roll) | Enough for 360 viewers, not for interaction |
| **6DoF** | Rotation + translation (x / y / z) | Required for room-scale, hands, and grabbing |
| **Motion-to-photon latency** | Time from head movement to display update — keep **below 20 ms** | Above this, people get sick |
| **Framerate** | Lock to **72 / 90 / 120 Hz**, no dropped frames | Reprojection is a last resort, not a plan |
| **Reference spaces** | `local`, `stage`, `unbounded` | Wrong space = floor at the wrong height, drift |
| **Locomotion** | Teleport (fade), snap turn, vignette, optional smooth movement | Comfort is accessibility — always offer alternatives |

### Spatial Math & Ergonomics

Coordinate spaces (local / world / view / clip), pose prediction, and comfort zones. Keep primary interaction between 0.5–3 m, avoid forcing neck strain, and respect natural arm reach.

**Exercise:** Build a minimal OpenXR scene — empty room + visible controllers — and verify a stable frame rate with on-device metrics. If you cannot hold it here, you will not hold it in a full app.

---

## 2. Virtual Reality (VR)

Fully immersive, 6DoF environments. Standalone headsets (no PC) are the default target — design for a mobile chip, not a desktop GPU.

### What You Will Be Able To Do

Configure an XR rig, implement grab / ray / poke / socket interaction from first principles, choose locomotion that does not make people sick, and keep a scene inside performance budgets.

### Engine Paths — Pick One to Start

**Unity**
- Packages: XR Plugin Management, OpenXR Plugin, **XR Interaction Toolkit (XRI 3.x)**, XR Hands
- Rig: `XR Origin` — represents the tracking space and camera offset; all locomotion goes through it
- Interaction: Ray / Direct / Poke / Socket Interactors + Grab / Affordance Interactables — learn the Interactor–Interactable contract before copying prefabs
- For Quest-class hardware: add **Meta XR SDK** alongside OpenXR/XRI (see Section 3) for hand tracking, haptics, and voice — not instead of it

**Unreal Engine**
- VR Template: `VRPawn`, motion controller input, Enhanced Input
- Plugins: Meta XR Plugin for Unreal + Meta XR Simulator for desktop iteration
- Rendering: Single-Pass Instanced (Multiview), Lumen with hardware ray-tracing optimizations targeting 60 FPS open worlds (UE 5.6)

**Godot**
- Native OpenXR 1.1 module — desktop PCVR and Android / Horizon OS builds
- **Godot XR Tools (GXDK)** — hands, grab, teleport curves, spatial UI
- Godot 4.5 adds: visionOS target and OpenXR Vendor Extensions 4.0

### Performance Budgets — Standalone VR

Use Quest 3 / 3S (Snapdragon XR2 Gen 2) as your reference. These numbers are targets, not suggestions.

- **Rendering:** URP (Unity) / Forward+ (Godot) with Single-Pass Instanced — transforms computed once per stereo pair
- **Foveated rendering:** Fixed Foveated Rendering (FFR) and eye-tracked where available
- **Draw calls:** **< 150 per eye** — batch static geometry, atlas textures, reduce unique materials
- **Lighting:** Bake static lighting; limit real-time shadow casters to one directional light or use blob shadows
- **Memory:** Horizon OS limit is ~5.75 GiB PSS on Quest 3/3S — stay well below, profile with `adb`
- **Refresh:** Lock to 72 / 90 / 120 Hz and verify with on-device metrics, not editor play mode

**Exercises:**
1. Implement a grab without XRI (plain OpenXR input + rigidbody constraint), then replace it with XRI and compare.
2. Take a scene at 200+ draw calls and bring it below 150 per eye using atlasing, batching, and light baking.

**Resources:**
- [Valem Tutorials — Unity VR](https://www.youtube.com/@ValemTutorials)
- [Justin P Barnett — XRI 3.x](https://www.youtube.com/@JustinPBarnett)
- [Bastiaan Olij — Godot OpenXR](https://www.youtube.com/@BastiaanOlij)
- [Meta Horizon OS — Performance Guides](https://developers.meta.com/horizon/)

---

## 3. Standalone VR & Mixed Reality — Meta Quest (Horizon OS)

Quest 3 and Quest 3S are currently the most accessible standalone headsets and the fastest way to iterate on VR and Mixed Reality without a PC. The skills here transfer to other OpenXR headsets.

**Current platform state (2025–2026):**

| Item | Details |
|---|---|
| **Headsets** | Quest 3 / 3S — Snapdragon XR2 Gen 2, 8 GB RAM, 4 MP RGB passthrough, Touch Plus controllers, 1832×1920 per eye |
| **OS** | Horizon OS v74–v83 — Space Setup now handles multi-height floors and slanted ceilings (v81+), Passthrough Camera API public since v76 (Apr 2025) |
| **Refresh** | 72 / 90 / 120 Hz |
| **Memory** | ~5.75 GiB PSS kill limit — profile and stay below |

### Meta XR SDK (v205.0, July 2026)

The old "Oculus Integration" package is deprecated. The current SDK is modular via Unity Package Manager. **Meta XR All-in-One SDK (`com.meta.xr.sdk.all`)** is a wrapper that pulls the latest of each module below. Minimum Unity: **6000.0.66f2** (Unity 6.x).

| SDK Package | What it teaches you | When you need it |
|---|---|---|
| **Meta XR Core SDK** | Initialization, entitlements, boundary, passthrough setup | Every Quest project — install first |
| **Meta XR Interaction SDK + Essentials** | Hand tracking, controller input, grab / poke / ray, locomotion (Climbing, Telepath, Walking Stick), `ThrowTuner` + `ThrowPhysicsProfile` for designer-tunable throwing, agnostic `LocomotionEvents` | Any project with hands or controllers |
| **Meta XR Haptics SDK** | Unified haptic clips authored in Haptics Studio, auto-optimized per controller | Polish — feedback that communicates state |
| **Meta XR Audio SDK** | Spatial audio, reverb, occlusion | Any immersive scene |
| **Meta XR Voice SDK** | Voice commands and intents | Hands-busy or accessibility cases |
| **Meta XR Platform SDK** | Matchmaking, entitlements, cloud | Multiplayer / store builds |
| **Mixed Reality Utility Kit (MRUK)** | `EffectMesh`, `AnchorPrefabSpawner`, `Environment Raycast`, Space Setup handling | Every MR project — don't rebuild scene understanding |
| **Meta XR Simulator** *(separate install)* | Test without a headset, generate synthetic rooms | Daily iteration |
| **Meta XR Operator** *(new, v205.1)* | AI agent that can drive Touch input, read room geometry, and capture screenshots for automated testing | CI / agent testing |

**Notable changes in 2025–2026:**

- **Passthrough Camera API (PCA):** Direct access to the forward-facing RGB cameras on Quest 3/3S for computer vision and ML, built on Android Camera2. Timeline: v74 experimental → v76 public (store-shippable after review) → v83 adds Unreal support and a new 1280×1280 resolution. Not available over Link or in the Simulator. Never hardcode a resolution — enumerate at runtime. See [PCA Overview](https://developers.meta.com/horizon/documentation/unity/unity-pca-overview).
- **Interaction SDK locomotion:** New sample scenes for Climbing, Telepath, and physical Walking Stick, plus `ThrowTuner` for tuning spin/drag/flight forces without code.
- **Niantic Spatial SDK on Quest 3 (v3.15, 2025):** Visual Positioning System (VPS), on-device meshing, semantic segmentation, and object detection now run on Quest 3 through the PCA — same SDK works across phone and headset.

**Setup path (Unity):**
1. Install **Unity OpenXR Plugin** via XR Plug-in Management.
2. Install **Meta XR All-in-One SDK (UPM)** via Package Manager → run **Meta → Tools → Project Setup Tool → Fix All / Apply All**.
3. For Mixed Reality: add MRUK and configure Space Setup scenes.
4. For headset-free iteration: install Meta XR Simulator and Synthetic Environment Builder.

**Resources:**
- [Meta Horizon OS — Unity Getting Started](https://developers.meta.com/horizon/develop/unity/)
- [Meta XR All-in-One SDK — UPM (v205.0)](https://developers.meta.com/horizon/downloads/package/meta-xr-sdk-all-in-one-upm)
- [Passthrough Camera API — Unity Overview](https://developers.meta.com/horizon/documentation/unity/unity-pca-overview)
- [MRUK Documentation](https://developers.meta.com/horizon/documentation/unity/unity-mr-utility-kit-overview/)
- [Interaction SDK — Setup](https://developers.meta.com/horizon/documentation/unity/unity-isdk-setup)
- [Niantic Spatial SDK on Quest 3](https://www.nianticspatial.com/en/blog/niantic-spatial-sdk-meta-quest-3-passthrough-camera-api)

---

## 4. Augmented Reality (AR)

Digital content overlaid on the physical world through a phone, tablet, or optical see-through glasses.

### What You Will Be Able To Do

Detect planes and point clouds, convert a screen tap into a world-space hit, choose the right tracking method for the job (image vs. model vs. space), and make virtual lighting match the real environment.

### Core Skills

- **Plane detection & tracking** — Horizontal / vertical surfaces, point clouds, depth (ToF / stereo)
- **Raycasting** — Screen tap → hit against detected geometry
- **Tracking types:**
  - **Image / Marker (2D)** — Posters, QR codes, VuMarks
  - **Object / Model (3D)** — Recognize a physical object from any angle using its 3D model
  - **Area / Space (room-scale)** — Track an entire room or venue from a pre-scanned mesh
- **Faces & bodies** — Blendshapes, skeletal joints
- **Light estimation** — Match virtual lights to ambient camera input
- **Visual Positioning (VPS)** — Persistent, city-scale anchors from pre-scanned locations

### Tooling — Choose by Task

| SDK | What you learn | When to use it |
|---|---|---|
| **Unity AR Foundation 6** (ARKit + ARCore) + **XR Simulation** | Cross-platform AR abstraction: planes, anchors, raycasting, light estimation, meshing. In-editor simulation for fast iteration. | Default for mobile AR. Learn this first. |
| **Vuforia Engine** (PTC) | Industrial-grade tracking: **Image Targets**, **Model Targets** (Model Target Generator with deep learning), **Area Targets** (LiDAR / Matterport / NavVis / Leica scans via Area Target Generator), **VuMarks** (custom fiducials), **Ground Plane**. Strong on object- and space-scale pose estimation. | When you need robust model-based or room-scale tracking — factory instructions on a specific machine, museum guide from a Matterport scan — beyond what ARKit/ARCore anchors handle reliably. Requires Vuforia Developer Portal datasets; commercial use often needs a license. |
| **Niantic Lightship ARDK** | Semantic meshing, real-time occlusion, VPS at city scale | Outdoor and location-anchored experiences |
| **XREAL / Snap Spectacles SDKs** | Optical see-through glasses workflows | Dedicated glasses hardware |

**How Vuforia relates to AR Foundation:**
AR Foundation is the cross-platform engine layer; Vuforia is a specialized tracker that can sit alongside or replace the AR provider for specific jobs. It does not replace ARKit/ARCore — it complements them. Use AR Foundation for general AR; bring in Vuforia when you need reliable pose on a known object or a room-scale localization from a pre-scanned dataset. Area Targets require a dataset built with the Area Target Generator (ATG) — understand that capture-to-import workflow before committing.

**Exercises:**
1. AR Foundation: build a placement tool — detect planes → raycast → place / scale / rotate with light estimation.
2. Vuforia: generate an Image Target and a Model Target (MTG) from a simple model and compare tracking stability in different lighting.

**Resources:**
- [Unity AR Foundation 6 Manual](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@6.0/manual/index.html)
- [ARCore Developer Guides](https://developers.google.com/ar)
- [ARKit Documentation](https://developer.apple.com/augmented-reality/arkit/)
- [Vuforia Engine Library — Model & Area Targets](https://developer.vuforia.com/library/)
- [Vuforia Model Target Generator — Guide](https://developer.vuforia.com/library/vuforia-engine/images-and-objects/model-targets/model-target-generator/model-target-generator-user-guide)
- [Vuforia Area Targets — Overview](https://developer.vuforia.com/library/vuforia-engine/environments/area-targets/area-targets)
- [Lightship Developer Portal](https://lightship.dev/)

---

## 5. Mixed Reality & Spatial Computing

Mixed Reality merges VR and AR via stereoscopic color passthrough — virtual objects live inside the real room and respect its geometry.

### What You Will Be Able To Do

Capture and reason about scene understanding data, place content with environment raycasts, handle occlusion correctly, design for direct hand interaction, and persist spatial anchors.

### Core Skills

- **Passthrough** — Full-color stereo, edge highlighting, portal clipping. Know where the passthrough texture ends and your rendering begins.
- **Scene Understanding (Scene API)** — Room scan that returns labeled geometry (walls, floors, tables, doors, windows) for physics and placement. Since Horizon OS v81: multi-height floors, slanted ceilings, inner walls.
- **Environment Raycast** — Place content using real-time depth without a full room scan — faster for spontaneous placement.
- **Spatial Anchors** — Persist transforms across sessions relative to physical features.
- **Interaction** — Hand tracking, direct touch / poke, pinch + gaze (visionOS pattern).
- **Occlusion & depth** — Real surfaces occlude virtual ones via environment depth. Test it — floating content breaks presence instantly.
- **Passthrough Camera API (advanced)** — Custom CV/ML on the raw RGB feed. Learn the permission model (`HEADSET_CAMERA` vs `CAMERA`) and dynamic resolution handling.

### Platforms

**Quest 3 / 3S via MRUK + Scene API**
- `EffectMesh` — visualize surfaces, cut passthrough portals
- `AnchorPrefabSpawner` — spawn on labeled furniture
- `Environment Raycast` — depth-based placement
- Space Setup with synthetic scenes via XR Simulator for headset-free testing

**Apple visionOS 26**
- **SwiftUI** — Windows and Volumes for 2D/3D interfaces
- **RealityKit** — Rendering, materials (MaterialX), physics, particles — new in visionOS 26: MeshInstances, Environment Blending, hover improvements
- **ARKit / Spatial Tracking** — Plane detection, hand tracking via AnchorEntity
- **Unity PolySpatial / Compositor Services** — Ship Unity content as native shared or immersive visionOS spaces; Godot 4.5 adds visionOS + CompositorServices support
- **Reality Composer Pro** — Scene assembly and particle authoring

**Exercises:**
1. Surface-aware placement: spawn on tables / floors via scene labels, then add physics so objects collide with real desks.
2. Occlusion check: place a virtual object behind a real table and verify depth behavior.
3. *(Advanced)* Stream a camera frame via PCA, run a lightweight detector (QR or bounding box), and overlay a label — handle resolution changes dynamically.

**Resources:**
- [Meta Horizon OS — Mixed Reality Overview](https://developers.meta.com/horizon/documentation/unity/unity-sample-mruk-basic)
- [MRUK Documentation](https://developers.meta.com/horizon/documentation/unity/unity-mr-utility-kit-overview/)
- [Apple visionOS Documentation](https://developer.apple.com/visionos/)
- [LearnXR — Quest & MRUK Guides](https://learnxr.io/)

---

## 6. WebXR — The Immersive Web

VR and AR delivered through the browser. No install, no store submission.

**Core API — W3C WebXR Device API:**
- Session modes: `inline`, `immersive-vr`, `immersive-ar`
- Reference spaces: `local`, `local-floor`, `bounded-floor`, `unbounded`
- Input: 6DoF controllers, hand tracking, transient pointers (mobile AR taps)
- Features: hit-testing, anchors, light estimation, depth sensing (where supported)

**Current state (2026):** WebGPU + WebXR interop is progressing. Babylon.js 8 supports WebGPU-backed WebXR via XRGPUBinding (experimental, requires `xrCompatible: true`). Three.js WebGPURenderer is the forward path but still maturing for XR. Learn WebGL-backed WebXR first, then add a WebGPU path where browsers support it — don't block on WebGPU for XR.

**Engines & Frameworks:**

| Framework | Strength |
|---|---|
| **[Wonderland Engine](https://wonderlandengine.com/)** | WASM-native, visual editor, low overhead — built for 90/120 FPS on standalone |
| **[Babylon.js 8 — WebXR](https://doc.babylonjs.com/features/featuresDeepDive/webXR)** | All-in-one: teleport, hands, GUI, experimental WebGPU path |
| **[Three.js — WebXR](https://threejs.org/examples/?q=webxr)** | Modular blocks (`renderer.xr.enabled`, `VRButton` / `ARButton`) |
| **[A-Frame](https://aframe.io/)** | Declarative HTML entity-component — fastest prototyping |

**Testing:** [WebXR API Emulator](https://github.com/MozillaReality/WebXR-emulator-extension) — simulate headsets and controllers in desktop browser dev tools.

**Exercise:** Ship one URL that runs on desktop (inline), phone AR (immersive-ar), and headset VR (immersive-vr). Verify all three in the emulator before claiming it works.

---

## 7. Milestones — Prove Your Skills

Each milestone is a proof of skill. Include a public repo, a short write-up of decisions and trade-offs (what you tried, what you cut, measured performance), and a playable build or URL.

| # | Milestone | Skills proven | Stack | Deliverable |
|---|---|---|---|---|
| 1 | **6DoF Physics Playground** — grab, distance grab, socket, teleport + smooth locomotion | Interaction model, locomotion, comfort options, profiling | OpenXR + XRI 3.x or GXDK; or Interaction SDK native | Sideloadable APK or PCVR build on GitHub + frame-time screenshot |
| 2 | **AR Placement Tool** — plane detection, raycast placement, rotate / scale gestures, light estimation | AR tracking, raycasting, lighting, gesture handling | AR Foundation 6 (optionally: Vuforia Model Target variant) | Android APK / iOS TestFlight + video |
| 3 | **Room-Scale MR Experience** — room mesh collision, surface-aware spawning (e.g., tabletop game), hand tracking, occlusion | Scene understanding, spatial anchors, hand interaction, occlusion | MRUK or visionOS | Demo video + write-up + open repo |
| 4 | **Cross-Platform WebXR App** — runs on desktop, mobile AR, and headset from one URL; verified with emulator | WebXR lifecycle, reference spaces, cross-device input | Babylon.js / Three.js / Wonderland | Public URL on GitHub Pages or Vercel |

**Complete them in order: 1 → 2 → 3 → 4. Do not jump to Mixed Reality before you can hold a frame rate in VR or place reliably in AR.**

---