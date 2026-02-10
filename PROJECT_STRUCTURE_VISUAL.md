# Stride Game Engine - Visual Architecture

## Overview Diagram

```
                              STRIDE GAME ENGINE
    +==========================================================================+
    |                                                                          |
    |   +------------------------------------------------------------------+   |
    |   |                      EDITOR LAYER                                |   |
    |   |  +-----------------+  +-----------------+  +-----------------+   |   |
    |   |  | Stride.         |  | Stride.Assets.  |  | Stride.Editor   |   |   |
    |   |  | GameStudio      |  | Presentation    |  |                 |   |   |
    |   |  | (WPF App)       |  | (Asset Editors) |  | (Framework)     |   |   |
    |   |  +-----------------+  +-----------------+  +-----------------+   |   |
    |   +------------------------------------------------------------------+   |
    |                                    |                                     |
    |                                    v                                     |
    |   +------------------------------------------------------------------+   |
    |   |                      TOOLS LAYER                                 |   |
    |   |  +-----------+ +-----------+ +-----------+ +-----------+         |   |
    |   |  | Importer  | | Texture   | | Effect    | | VS        |         |   |
    |   |  | .3D       | | Converter | | Compiler  | | Package   |         |   |
    |   |  +-----------+ +-----------+ +-----------+ +-----------+         |   |
    |   +------------------------------------------------------------------+   |
    |                                    |                                     |
    |                                    v                                     |
    |   +------------------------------------------------------------------+   |
    |   |                   ENGINE RUNTIME LAYER                           |   |
    |   |  +------------+  +------------+  +------------+  +------------+  |   |
    |   |  | Stride.    |  | Stride.    |  | Stride.    |  | Stride.    |  |   |
    |   |  | Engine     |  | Graphics   |  | Rendering  |  | Shaders    |  |   |
    |   |  | (ECS Core) |  | (GPU API)  |  | (Pipeline) |  | (SDSL)     |  |   |
    |   |  +------------+  +------------+  +------------+  +------------+  |   |
    |   |                                                                  |   |
    |   |  +----------+ +----------+ +----------+ +----------+ +--------+  |   |
    |   |  | Audio    | | Input    | | Physics  | | UI       | | VR     |  |   |
    |   |  +----------+ +----------+ +----------+ +----------+ +--------+  |   |
    |   +------------------------------------------------------------------+   |
    |                                    |                                     |
    |                                    v                                     |
    |   +------------------------------------------------------------------+   |
    |   |                   ASSET MANAGEMENT LAYER                         |   |
    |   |  +-----------------+  +-----------------+  +-----------------+   |   |
    |   |  | Stride.Core.    |  | Stride.Core.    |  | Stride.Core.    |   |   |
    |   |  | Assets          |  | BuildEngine     |  | Packages        |   |   |
    |   |  +-----------------+  +-----------------+  +-----------------+   |   |
    |   +------------------------------------------------------------------+   |
    |                                    |                                     |
    |                                    v                                     |
    |   +------------------------------------------------------------------+   |
    |   |                   CORE FOUNDATION LAYER                          |   |
    |   |  +----------+ +------------+ +-------------+ +------------+      |   |
    |   |  | Stride.  | | Stride.    | | Stride.Core.| | Stride.    |      |   |
    |   |  | Core     | | Core.Math  | | Reflection  | | Core.IO    |      |   |
    |   |  +----------+ +------------+ +-------------+ +------------+      |   |
    |   +------------------------------------------------------------------+   |
    |                                                                          |
    +==========================================================================+
```

---

## Entity-Component System (ECS)

```
                         ENTITY-COMPONENT SYSTEM
    +====================================================================+
    |                                                                    |
    |     +-----------+     +-----------+     +-----------+              |
    |     |  Entity   |     |  Entity   |     |  Entity   |              |
    |     |  "Player" |     |  "Enemy"  |     |  "Light"  |              |
    |     +-----------+     +-----------+     +-----------+              |
    |           |                 |                 |                    |
    |     +-----+-----+     +-----+-----+     +-----+-----+              |
    |     |           |     |           |     |           |              |
    |     v           v     v           v     v           v              |
    | +--------+ +--------+ +--------+ +--------+ +--------+ +--------+  |
    | |Transform| |Model   | |Transform| |Physics| |Transform| |Light  |  |
    | |Component| |Component| |Component| |Component| |Component| |Component|  |
    | +--------+ +--------+ +--------+ +--------+ +--------+ +--------+  |
    |     |           |           |           |           |           |  |
    |     v           v           v           v           v           v  |
    | +---------------------------------------------------------------+  |
    | |                     ENTITY PROCESSORS                         |  |
    | |  +-------------+ +-------------+ +-------------+ +---------+  |  |
    | |  | Transform   | | Rendering   | | Physics     | | Light   |  |  |
    | |  | Processor   | | Processor   | | Processor   | | Proc.   |  |  |
    | |  +-------------+ +-------------+ +-------------+ +---------+  |  |
    | +---------------------------------------------------------------+  |
    |                                                                    |
    +====================================================================+
```

---

## Graphics Pipeline

```
                          GRAPHICS PIPELINE
    +====================================================================+
    |                                                                    |
    |   +--------------------+                                           |
    |   | Stride.Graphics    |  <-- Low-Level GPU Abstraction            |
    |   | (GraphicsDevice)   |                                           |
    |   +--------------------+                                           |
    |            |                                                       |
    |            v                                                       |
    |   +--------------------+                                           |
    |   | GRAPHICS API       |                                           |
    |   | +--------+ +--------+ +--------+ +--------+ +--------+         |
    |   | |Direct  | |Direct  | |OpenGL  | |OpenGL  | |Vulkan  |         |
    |   | |3D 11   | |3D 12   | |        | |ES      | |        |         |
    |   | +--------+ +--------+ +--------+ +--------+ +--------+         |
    |   +--------------------+                                           |
    |                                                                    |
    |   +--------------------+                                           |
    |   | Stride.Rendering   |  <-- High-Level Rendering                 |
    |   +--------------------+                                           |
    |            |                                                       |
    |   +--------+--------+--------+--------+                            |
    |   v        v        v        v        v                            |
    | +------+ +------+ +-------+ +------+ +--------+                    |
    | |Forward| |Deferred| |Shadows| |Post  | |Materials|                    |
    | |Pass  | |Pass   | |       | |FX    | |        |                    |
    | +------+ +------+ +-------+ +------+ +--------+                    |
    |                                                                    |
    |   +--------------------+                                           |
    |   | Stride.Shaders     |  <-- Shader System                        |
    |   +--------------------+                                           |
    |            |                                                       |
    |   +--------+--------+                                              |
    |   v                 v                                              |
    | +----------+  +----------+                                         |
    | | .sdsl    |  | Compiled |                                         |
    | | Source   |  | Bytecode |                                         |
    | +----------+  +----------+                                         |
    |                                                                    |
    +====================================================================+
```

---

## Asset Pipeline

```
                           ASSET PIPELINE
    +====================================================================+
    |                                                                    |
    |   RAW ASSETS                                                       |
    |   +----------+ +----------+ +----------+ +----------+              |
    |   | .fbx     | | .png     | | .wav     | | .sdsl    |              |
    |   | .obj     | | .jpg     | | .mp3     | | (shader) |              |
    |   | (models) | | (images) | | (audio)  | |          |              |
    |   +----------+ +----------+ +----------+ +----------+              |
    |        |            |            |            |                    |
    |        v            v            v            v                    |
    |   +----------------------------------------------------+           |
    |   |              ASSET IMPORTERS                       |           |
    |   |  Stride.Importer.3D  |  TextureConverter  | etc.   |           |
    |   +----------------------------------------------------+           |
    |                          |                                         |
    |                          v                                         |
    |   +----------------------------------------------------+           |
    |   |              STRIDE ASSETS (.sdpkg)                |           |
    |   |  +------------+ +------------+ +------------+      |           |
    |   |  | Model      | | Texture    | | Sound      |      |           |
    |   |  | Asset      | | Asset      | | Asset      |      |           |
    |   |  +------------+ +------------+ +------------+      |           |
    |   +----------------------------------------------------+           |
    |                          |                                         |
    |                          v                                         |
    |   +----------------------------------------------------+           |
    |   |              BUILD ENGINE                          |           |
    |   |  Stride.Core.BuildEngine                           |           |
    |   |  - Dependency Tracking                             |           |
    |   |  - Incremental Builds                              |           |
    |   |  - Caching                                         |           |
    |   +----------------------------------------------------+           |
    |                          |                                         |
    |                          v                                         |
    |   +----------------------------------------------------+           |
    |   |              COMPILED ASSETS                       |           |
    |   |  Platform-specific optimized formats               |           |
    |   +----------------------------------------------------+           |
    |                                                                    |
    +====================================================================+
```

---

## Build System

```
                           BUILD SYSTEM
    +====================================================================+
    |                                                                    |
    |   SOLUTION FILES                                                   |
    |   +-------------+ +-------------+ +-------------+ +-------------+  |
    |   | Stride.sln  | | Runtime.sln | | Android.sln | | iOS.sln     |  |
    |   | (Master)    | | (Core)      | |             | |             |  |
    |   +-------------+ +-------------+ +-------------+ +-------------+  |
    |          |                                                         |
    |          v                                                         |
    |   +----------------------------------------------------+           |
    |   |              MSBUILD CONFIGURATION                 |           |
    |   |  +---------------+  +----------------+             |           |
    |   |  | Stride.props  |  | Stride.targets |             |           |
    |   |  +---------------+  +----------------+             |           |
    |   +----------------------------------------------------+           |
    |          |                                                         |
    |   +------+------+------+------+------+                             |
    |   v      v      v      v      v      v                             |
    | +-----+ +-----+ +-----+ +-----+ +-----+ +-----+                    |
    | | Win | | Linux| |Andr | | iOS | | UWP | | Mac |                    |
    | +-----+ +-----+ +-----+ +-----+ +-----+ +-----+                    |
    |   |                                                                |
    |   +-----> Graphics API Selection                                   |
    |          +-------+ +-------+ +-------+ +-------+ +-------+         |
    |          | D3D11 | | D3D12 | | OpenGL| | GLES  | | Vulkan|         |
    |          +-------+ +-------+ +-------+ +-------+ +-------+         |
    |                                                                    |
    |   +----------------------------------------------------+           |
    |   |              CI/CD (GitHub Actions)                |           |
    |   |  - Windows Runtime Build                           |           |
    |   |  - Linux Runtime Build                             |           |
    |   |  - Android Build                                   |           |
    |   |  - iOS Build                                       |           |
    |   |  - Test Execution                                  |           |
    |   +----------------------------------------------------+           |
    |                                                                    |
    +====================================================================+
```

---

## Dependency Graph

```
                         DEPENDENCY FLOW
    +====================================================================+
    |                                                                    |
    |   Stride.GameStudio (Editor)                                       |
    |           |                                                        |
    |           +---> Stride.Core.Assets.Editor                          |
    |           +---> Stride.Assets.Presentation                         |
    |           +---> Stride.Editor                                      |
    |                        |                                           |
    |                        v                                           |
    |   Stride.Engine (Runtime)                                          |
    |           |                                                        |
    |           +---> Stride.Graphics                                    |
    |           +---> Stride.Games                                       |
    |           +---> Stride.Rendering                                   |
    |           +---> Stride.Audio                                       |
    |           +---> Stride.Input                                       |
    |           +---> Stride.Physics                                     |
    |           +---> Stride.Navigation                                  |
    |           +---> Stride.Particles                                   |
    |           +---> Stride.UI                                          |
    |                        |                                           |
    |                        v                                           |
    |   Stride.Core.Assets                                               |
    |           |                                                        |
    |           v                                                        |
    |   Stride.Core.BuildEngine                                          |
    |           |                                                        |
    |           v                                                        |
    |   Stride.Core (Foundation)                                         |
    |           |                                                        |
    |           +---> Stride.Core.Mathematics                            |
    |           +---> Stride.Core.Serialization                          |
    |           +---> Stride.Core.Reflection                             |
    |           +---> Stride.Core.IO                                     |
    |                                                                    |
    +====================================================================+
```

---

## External Dependencies

```
                      EXTERNAL DEPENDENCIES
    +====================================================================+
    |                                                                    |
    |   GRAPHICS                     AUDIO                               |
    |   +-----------+               +------------+                       |
    |   | glslang   | GLSL->SPIR-V  | OpenAL     | 3D Audio              |
    |   | MoltenVK  | Vulkan->Metal | FFmpeg     | A/V Codec             |
    |   | PVRTT     | Textures      | OpenSLES   | Android Audio         |
    |   | FreeImage | Image Load    | CELT       | Audio Codec           |
    |   +-----------+               +------------+                       |
    |                                                                    |
    |   PHYSICS                      VR/XR                               |
    |   +-----------+               +------------+                       |
    |   | Bullet    | 3D Physics    | OpenVR     | SteamVR               |
    |   | VHACD     | Convex Decomp | OpenXR     | XR Standard           |
    |   +-----------+               | OculusOVR  | Oculus SDK            |
    |                               +------------+                       |
    |                                                                    |
    |   PLATFORM                     BUILD                               |
    |   +-----------+               +------------+                       |
    |   | NativePath| Cross-Platform| LLVM       | C++ Compiler          |
    |   | freetype  | Fonts         | NuGet      | Package Mgmt          |
    |   +-----------+               +------------+                       |
    |                                                                    |
    +====================================================================+
```

---

## Sample Organization

```
                         SAMPLES STRUCTURE
    +====================================================================+
    |                                                                    |
    |   /samples/                                                        |
    |       |                                                            |
    |       +--- StrideSamples.sln  (Master Solution)                    |
    |       |                                                            |
    |       +--- Audio/                                                  |
    |       |       +--- SimpleAudio/                                    |
    |       |                                                            |
    |       +--- Graphics/                                               |
    |       |       +--- AnimatedModel/                                  |
    |       |       +--- CustomEffect/                                   |
    |       |       +--- MaterialShader/                                 |
    |       |       +--- SpriteFonts/                                    |
    |       |       +--- SpriteStudioDemo/                               |
    |       |                                                            |
    |       +--- Input/                                                  |
    |       |       +--- TouchInputs/                                    |
    |       |       +--- GravitySensor/                                  |
    |       |                                                            |
    |       +--- Physics/                                                |
    |       |       +--- PhysicsSample/                                  |
    |       |       +--- BepuSample/                                     |
    |       |                                                            |
    |       +--- UI/                                                     |
    |       |       +--- GameMenu/                                       |
    |       |       +--- UIParticles/                                    |
    |       |       +--- UIElementLink/                                  |
    |       |                                                            |
    |       +--- Games/                                                  |
    |       |       +--- SpaceEscape/                                    |
    |       |       +--- JumpyJet/                                       |
    |       |                                                            |
    |       +--- Templates/                                              |
    |       |       +--- FirstPersonShooter/                             |
    |       |       +--- ThirdPersonPlatformer/                          |
    |       |       +--- TopDownRPG/                                     |
    |       |       +--- VRSandbox/                                      |
    |       |                                                            |
    |       +--- Tutorials/                                              |
    |               +--- CSharpBeginner/                                 |
    |               +--- CSharpIntermediate/                             |
    |                                                                    |
    +====================================================================+
```

---

## Project Statistics

```
    +====================================================================+
    |                      PROJECT STATISTICS                            |
    +====================================================================+
    |                                                                    |
    |   Source Projects                                                  |
    |   +---------------------------+------------------+                 |
    |   | Layer                     | Project Count    |                 |
    |   +---------------------------+------------------+                 |
    |   | Core Foundation           |       19         |                 |
    |   | Engine Runtime            |       45         |                 |
    |   | Asset Management          |        7         |                 |
    |   | Build Engine              |        3         |                 |
    |   | Presentation (WPF/UI)     |       10         |                 |
    |   | Editor                    |       11         |                 |
    |   | Tools                     |       25         |                 |
    |   | Launcher                  |        3         |                 |
    |   | Shaders                   |        2         |                 |
    |   | Tests                     |        3+        |                 |
    |   +---------------------------+------------------+                 |
    |   | TOTAL                     |      128+        |                 |
    |   +---------------------------+------------------+                 |
    |                                                                    |
    |   External Dependencies: 27 packages                               |
    |   Sample Projects: 16 samples + 5 templates                        |
    |   Supported Platforms: 5 (Windows, Linux, Android, iOS, UWP)       |
    |   Graphics APIs: 5 (D3D11, D3D12, OpenGL, GLES, Vulkan)            |
    |                                                                    |
    +====================================================================+
```

---

## Related Documentation

- [PROJECT_STRUCTURE_DICTIONARY.md](./PROJECT_STRUCTURE_DICTIONARY.md) - Detailed codebase reference
- [PROJECT_WORK.md](./PROJECT_WORK.md) - Active tasks and issues
