# Stride Game Engine - Project Structure Dictionary

## Overview

Stride is an open-source C# game engine originally developed by Silicon Studio and now maintained by the community. It features a complete game development toolkit including a visual editor (GameStudio), multi-platform support, and a sophisticated asset pipeline.

**Repository**: https://github.com/stride3d/stride
**Fork**: https://github.com/roku674/stride
**License**: MIT

---

## Root Directory Structure

| Directory/File | Purpose |
|----------------|---------|
| `build/` | Build scripts, solution files, MSBuild configurations |
| `deps/` | External dependencies (native libs, tools, headers) |
| `samples/` | Sample projects and game templates |
| `sources/` | Main source code (128+ projects) |
| `tests/` | Test projects and test infrastructure |
| `.github/` | GitHub Actions workflows and CI/CD |
| `.editorconfig` | Code style settings |
| `global.json` | .NET SDK version (10.0.100) |
| `nuget.config` | NuGet package sources |
| `LICENSE.md` | MIT License |
| `README.md` | Project overview |

---

## Architecture Layers

```
+--------------------------------------------------------+
|  EDITOR LAYER (GameStudio)                             |
|  - Stride.GameStudio, Editor, Assets.Presentation      |
+--------------------------------------------------------+
|  TOOLS & UTILITIES LAYER                               |
|  - Compilers, Importers, Converters, Plugins           |
+--------------------------------------------------------+
|  ENGINE RUNTIME LAYER                                  |
|  - Graphics, Audio, Input, Physics, Rendering          |
+--------------------------------------------------------+
|  ASSET & DATA MANAGEMENT LAYER                         |
|  - Core.Assets, Serialization, Build Engine            |
+--------------------------------------------------------+
|  CORE FOUNDATION LAYER                                 |
|  - Core, Mathematics, Reflection, Serialization        |
+--------------------------------------------------------+
```

---

## Sources Directory (/sources/)

### Core Foundation (/sources/core/) - 19 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Core` | Central utilities, logging, diagnostics, platform abstraction |
| `Stride.Core.Mathematics` | Vector, matrix, quaternion operations (optimized) |
| `Stride.Core.Serialization` | Binary/YAML serialization framework |
| `Stride.Core.Reflection` | Runtime reflection and type introspection |
| `Stride.Core.IO` | File I/O and virtual file system |
| `Stride.Core.Yaml` | YAML parsing |
| `Stride.Core.Design` | Design-time utilities and type converters |
| `Stride.Core.Translation` | Localization infrastructure |
| `Stride.Core.MicroThreading` | Lightweight coroutine system |
| `Stride.Core.Tasks` | Task scheduling |
| `Stride.Core.AssemblyProcessor` | Post-compilation assembly modification |
| `Stride.Core.CompilerServices` | Roslyn-based compile-time analysis |

### Engine Runtime (/sources/engine/) - 45 Projects

#### Graphics & Rendering
| Project | Purpose |
|---------|---------|
| `Stride.Graphics` | Low-level graphics abstraction (D3D11/12, OpenGL, Vulkan) |
| `Stride.Rendering` | High-level rendering pipeline, materials, lighting |
| `Stride.Shaders` | Shader compilation and linking |
| `Stride.Shaders.Compiler` | Runtime shader compilation |
| `Stride.Shaders.Parser` | Shader language parsing |

#### Game Systems
| Project | Purpose |
|---------|---------|
| `Stride.Engine` | Core game loop, Entity-Component System |
| `Stride.Games` | Window management, platform abstraction |
| `Stride.Input` | Input handling (keyboard, mouse, gamepad, touch) |
| `Stride.Audio` | Audio playback and 3D sound |
| `Stride.Physics` | Physics simulation (Bullet-based) |
| `Stride.BepuPhysics` | Alternative physics engine (BEPU v2) |
| `Stride.Navigation` | Pathfinding and AI navigation |
| `Stride.Particles` | Particle system and effects |
| `Stride.UI` | UI framework (buttons, panels, text) |
| `Stride.Video` | Video playback |
| `Stride.VirtualReality` | VR device support |
| `Stride.Voxels` | Voxel-based rendering |

#### Supporting
| Project | Purpose |
|---------|---------|
| `Stride.Assets` | Asset types for engine content |
| `Stride.Assets.Models` | 3D model loading and conversion |
| `Stride.Native` | Native interop (P/Invoke) |
| `Stride.Debugger` | Debugging utilities |

### Asset Management (/sources/assets/) - 7 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Core.Assets` | Base asset abstraction, versioning, upgrades |
| `Stride.Core.Assets.Yaml` | YAML-based asset format support |
| `Stride.Core.Assets.Quantum` | Model-based asset representation |
| `Stride.Core.Assets.CompilerApp` | Asset compilation CLI tool |
| `Stride.Core.Packages` | Package management |

### Build Engine (/sources/buildengine/) - 3 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Core.BuildEngine` | Distributed build system |
| `Stride.Core.BuildEngine.Common` | Shared build utilities |

### Editor (/sources/editor/) - 11 Projects

| Project | Purpose |
|---------|---------|
| `Stride.GameStudio` | Main visual editor (WPF) |
| `Stride.Core.Assets.Editor` | Asset editing infrastructure |
| `Stride.Assets.Presentation` | Engine asset editors |
| `Stride.Editor` | Core editor framework |
| `Stride.Editor.CrashReport` | Crash reporting |
| `Stride.GameStudio.Plugin` | Plugin system |
| `Stride.Samples.Templates` | Project templates |

### Presentation (/sources/presentation/) - 10 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Core.Presentation` | MVVM framework, base UI controls |
| `Stride.Core.Presentation.Wpf` | WPF-specific implementations |
| `Stride.Core.Presentation.Dialogs` | Dialog system |
| `Stride.Core.Presentation.Quantum` | Model binding |
| `Stride.Core.Quantum` | MVVM model system |

### Tools (/sources/tools/) - 25 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Importer.3D` | 3D model importing |
| `Stride.TextureConverter` | Texture format conversion |
| `Stride.EffectCompilerServer` | Distributed shader compilation |
| `Stride.VisualStudio.Package` | VS extension (VSIX) |
| `Stride.ConnectionRouter` | Network communication |
| `Stride.PublicApiCheck` | API compatibility checking |

### Launcher (/sources/launcher/) - 3 Projects

| Project | Purpose |
|---------|---------|
| `Stride.Launcher` | Project launcher and installer UI |
| `Stride.Samples.Templates` | Sample project templates |
| `Prerequisites` | Dependency installation |

---

## Dependencies Directory (/deps/)

### Graphics/Rendering
| Dependency | Purpose |
|------------|---------|
| `glslang` | GLSL to SPIR-V shader compilation |
| `MoltenVK` | Metal to Vulkan translation (macOS/iOS) |
| `PVRTT` | PowerVR texture compression |
| `TextureWrappers` | Texture format conversion |
| `FreeImage` | Multi-format image loading |
| `msdfgen` | SDF font generation |

### Audio
| Dependency | Purpose |
|------------|---------|
| `OpenAL` | Cross-platform 3D audio |
| `OpenSLES` | Android audio API |
| `FFmpeg` | Audio/video encoding |
| `CELT` | Low-latency audio codec |

### Physics
| Dependency | Purpose |
|------------|---------|
| `BulletPhysics` | 3D physics simulation |
| `VHACD` | Convex decomposition |

### VR/Input
| Dependency | Purpose |
|------------|---------|
| `OpenVR` | SteamVR support |
| `OpenXR` | XR standard API |
| `OculusOVR` | Oculus Rift support |

### Platform
| Dependency | Purpose |
|------------|---------|
| `NativePath` | Cross-platform native runtime |
| `freetype` | Font rendering |
| `LLVM` | C/C++ compilation |

### Build Tools
| Dependency | Purpose |
|------------|---------|
| `Stride.MSBuild.Tasks` | Custom MSBuild tasks |
| `AssemblyProcessor` | .NET assembly processing |
| `Stride.GitVersioning` | Automatic versioning |
| `Nuget` | Package management |

---

## Build Directory (/build/)

### Solution Files
| File | Purpose |
|------|---------|
| `Stride.sln` | Master solution (all platforms) |
| `Stride.Runtime.sln` | Core runtime & graphics |
| `Stride.Android.sln` | Android runtime |
| `Stride.iOS.sln` | iOS runtime |
| `Stride.Launcher.sln` | Project launcher |
| `Stride.VisualStudio.sln` | VS extension |

### Key Scripts
| Script | Purpose |
|--------|---------|
| `compile.bat` | Main compilation script |
| `update_solutions.bat` | Generate platform-specific solutions |

### Supported Platforms
- Windows (D3D11, D3D12, OpenGL, OpenGLES, Vulkan)
- Linux (OpenGL, Vulkan)
- Android (OpenGL, OpenGLES, Vulkan)
- iOS (Metal via MoltenVK)
- UWP (D3D11)

---

## Samples Directory (/samples/)

### Categories
| Category | Samples |
|----------|---------|
| Audio | SimpleAudio |
| Graphics | AnimatedModel, CustomEffect, MaterialShader, SpriteFonts, SpriteStudioDemo |
| Input | TouchInputs, GravitySensor |
| Physics | PhysicsSample, BepuSample |
| Particles | ParticlesSample |
| UI | GameMenu, UIParticles, UIElementLink |
| Games | SpaceEscape, JumpyJet |
| Others | NativeLinking |

### Templates
| Template | Type |
|----------|------|
| FirstPersonShooter | FPS game template |
| ThirdPersonPlatformer | 3D platformer |
| TopDownRPG | Top-down RPG |
| VRSandbox | VR template |

### Tutorials
| Tutorial | Level |
|----------|-------|
| CSharpBeginner | Input, transforms, components |
| CSharpIntermediate | Advanced scripting |

---

## Key File Types

| Extension | Purpose |
|-----------|---------|
| `.sdpkg` | Stride Package (asset bundle) |
| `.sdtpl` | Stride Template |
| `.sdsl` | Stride Shader Language |
| `.csproj` | C# project |
| `.sln` | Visual Studio solution |
| `.slnf` | Solution filter |
| `.props` | MSBuild properties |
| `.targets` | MSBuild targets |

---

## Entity-Component System

### Core Classes
| Class | Purpose |
|-------|---------|
| `Entity` | Container for game objects |
| `EntityComponent` | Base for all components |
| `EntityProcessor` | System for processing entities |
| `SyncScript` | Synchronous update script |
| `StartupScript` | Initialization script |
| `AsyncScript` | Async coroutine script |

### Common Components
| Component | Purpose |
|-----------|---------|
| `TransformComponent` | Position, rotation, scale |
| `ModelComponent` | 3D model rendering |
| `CameraComponent` | Camera parameters |
| `LightComponent` | Lighting |
| `PhysicsComponent` | Physics body |
| `AudioListenerComponent` | Audio listener |
| `AudioEmitterComponent` | Audio source |

---

## Graphics API Configuration

Graphics API is selected at build time via MSBuild properties:

```xml
<StrideGraphicsApi>Direct3D11</StrideGraphicsApi>
<StrideGraphicsApi>Direct3D12</StrideGraphicsApi>
<StrideGraphicsApi>OpenGL</StrideGraphicsApi>
<StrideGraphicsApi>OpenGLES</StrideGraphicsApi>
<StrideGraphicsApi>Vulkan</StrideGraphicsApi>
```

Conditional compilation: `STRIDE_GRAPHICS_API_DIRECT3D11`, etc.

---

## Naming Conventions

| Category | Convention | Example |
|----------|------------|---------|
| Projects | Stride.{Module} | Stride.Graphics |
| Components | {Name}Component | CameraComponent |
| Processors | {Name}Processor | PhysicsProcessor |
| Scripts | {Name}Script | PlayerScript |
| Assets | PascalCase | PlayerModel.sdpkg |
| Shaders | {Name}.sdsl | CustomEffect.sdsl |

---

## Build Commands

```bash
# Windows build (from build/ directory)
compile.bat release

# .NET CLI
~/.dotnet/dotnet build Stride.sln

# MSBuild with specific API
msbuild Stride.sln /p:StrideGraphicsApis=Direct3D11

# Platform-specific
msbuild Stride.sln /p:StridePlatforms=Windows
```

---

## Testing

Tests are organized in `/tests/` and alongside source code:
- Unit tests: `*.Tests` projects
- Graphics regression: `Stride.Graphics.Regression`
- Integration tests: Various `*Tests` directories

```bash
dotnet test Stride.sln
```

---

## Version Information

- **.NET Target**: net10.0 (Desktop), net8.0-android, net8.0-ios
- **Stride Version**: 4.3.0.1+
- **C# Version**: Latest
- **Required SDK**: .NET 10.0.100

---

## Related Documentation

- [PROJECT_WORK.md](./PROJECT_WORK.md) - Active tasks and issues
- [PROJECT_STRUCTURE_VISUAL.md](./PROJECT_STRUCTURE_VISUAL.md) - Architecture diagrams
