# Stride Game Engine - Project Work

## Overview

This file tracks active work items, open issues, and planned improvements for the Stride Game Engine fork.

**Fork Owner**: roku674
**Original Repo**: stride3d/stride

---

## Quick Links

- [PROJECT_STRUCTURE_DICTIONARY.md](./PROJECT_STRUCTURE_DICTIONARY.md) - Codebase reference
- [Open Issues on GitHub](https://github.com/stride3d/stride/issues)

---

## Open GitHub Issues (Mapped to Codebase)

### Good First Issues

| Issue | Title | Area | Files/Modules |
|-------|-------|------|---------------|
| #2705 | Make Stride work on Mesa RADV driver | Graphics | `sources/engine/Stride.Graphics/` |
| #2617 | Improve warning message for missing compiler | Build | `sources/tools/Stride.EffectCompilerServer/` |
| #2562 | Change a couple debug logs to verbose logs | Core | `sources/core/Stride.Core/` (logging) |
| #2491 | Parameterless attribute with positional parameters generates warning | Build | `sources/core/Stride.Core.CompilerServices/` |
| #2375 | Stride.Core.CompilerServices should be an analyzer package | Build | `sources/core/Stride.Core.CompilerServices/` |
| #2373 | Obsolete attribute not respected in editor | Editor | `sources/editor/Stride.Assets.Presentation/` |
| #2311 | Static extension method warning with collection expressions | Build | `sources/core/Stride.Core.CompilerServices/` |
| #2310 | TransformChildrenGetter missing param on constructor | Engine | `sources/engine/Stride.Engine/` |
| #2309 | Navigation component exposes multiple irrelevant items | Engine | `sources/engine/Stride.Navigation/` |
| #1923 | Helix SDK should be used for VS package | Tools | `sources/tools/Stride.VisualStudio.Package/` |

### Recent Bugs

| Issue | Title | Area | Priority | Files/Modules |
|-------|-------|------|----------|---------------|
| #2706 | Default Game Template fails on Android | Platform | High | `build/Stride.Android.Build.props` |
| #2704 | App crashes when using XAML islands | UI | Medium | `sources/engine/Stride.UI/` |
| #2702 | AnimatedModelTests randomly fail | Engine | Medium | `sources/engine/Stride.Engine/` (animation) |
| #2700 | Entity disappears on reorder children | Editor | High | `sources/editor/Stride.Editor/` |
| #2696 | Android dotnet build failed | Platform | High | `build/Stride.Android.Build.props` |
| #2686 | Veldrid + Vulkan crash in debug mode | Graphics | Medium | `sources/engine/Stride.Graphics/` (Vulkan) |
| #2682 | NuGet package restore broken | Build | High | `nuget.config`, build system |
| #2679 | Game.GraphicsContext always null | Engine | Medium | `sources/engine/Stride.Games/` |

### Feature Requests

| Issue | Title | Area | Files/Modules |
|-------|-------|------|---------------|
| #2703 | Better exception for invalid effect name | Graphics | `sources/engine/Stride.Shaders/` |
| #2693 | Loading screen for scene changes | Engine | `sources/engine/Stride.Engine/` (scenes) |
| #2681 | Add support for NativeAOT | Build | Cross-cutting (all projects) |
| #2663 | Generate collision mesh from model groups | Physics | `sources/engine/Stride.Physics/` |
| #2641 | Improve editor entity paste performance | Editor | `sources/editor/Stride.Editor/` |
| #2639 | Multi-object editing | Editor | `sources/editor/Stride.Assets.Presentation/` |

### Engineering/Chores

| Issue | Title | Area | Files/Modules |
|-------|-------|------|---------------|
| #2653 | Remove StrideCore MSBuild task | Build | `deps/Stride.MSBuild.Tasks/` |
| #2567 | Migrate Stride.Shaders.Parser to Parlot | Shaders | `sources/engine/Stride.Shaders.Parser/` |
| #2466 | Review and minimize file allocations | Performance | Cross-cutting |
| #2268 | Add ImGui package to Stride | UI | `sources/engine/Stride.UI/` |

---

## Priority Work Items

### P0 - Critical (Blocking)

1. **#2706 - Android Template Failure**
   - Module: `build/Stride.Android.Build.props`
   - Impact: Cannot create Android builds
   - Related: #2696

2. **#2682 - NuGet Package Restore**
   - Module: Build system
   - Impact: Cannot build from fresh clone

### P1 - High Priority

1. **#2700 - Entity Reorder Bug**
   - Module: `sources/editor/Stride.Editor/`
   - Impact: Data loss in editor

2. **#2705 - Mesa RADV Support**
   - Module: `sources/engine/Stride.Graphics/`
   - Impact: Linux AMD GPU users

### P2 - Medium Priority

1. **#2704 - XAML Islands Crash**
2. **#2702 - Animation Test Flakiness**
3. **#2686 - Veldrid Vulkan Debug Crash**
4. **#2679 - GraphicsContext Null**

### P3 - Low Priority / Enhancements

1. **#2703 - Better Effect Error Messages**
2. **#2693 - Loading Screen Support**
3. **#2641 - Editor Paste Performance**
4. **#2639 - Multi-object Editing**

---

## Pending Tasks

### Documentation

- [ ] Create PROJECT_STRUCTURE_VISUAL.md with architecture diagrams
- [ ] Document contribution workflow
- [ ] Map remaining issues to specific files

### Investigation

- [ ] Investigate Android NDK issues (#2696, #2706)
- [ ] Profile NuGet restore failures (#2682)
- [ ] Test Mesa RADV driver compatibility (#2705)

### Development

- [ ] Pick first "good first issue" to work on
- [ ] Set up local build environment
- [ ] Run full test suite

---

## Completed Tasks

- [x] Clone Stride repository
- [x] Fork to roku674/stride
- [x] Configure git remotes (origin=fork, upstream=original)
- [x] Read CLAUDE*.md global rules
- [x] Explore codebase structure
- [x] Document sources/ architecture
- [x] Document build system
- [x] Document dependencies
- [x] Document samples
- [x] Create PROJECT_STRUCTURE_DICTIONARY.md
- [x] Create PROJECT_WORK.md
- [x] Map GitHub issues to codebase

---

## Build Status

| Platform | Status | Notes |
|----------|--------|-------|
| Windows | Unknown | Need to test |
| Linux | Unknown | Need to test |
| Android | Broken | #2696, #2706 |
| iOS | Unknown | Need to test |

---

## Notes

### Build Requirements
- .NET SDK 10.0.100
- Visual Studio 2022 with C++ tools
- Windows 11 SDK (26100)

### Recommended First Issues
Based on codebase familiarity needed:

1. **#2562** - Debug log changes (simple, good intro)
2. **#2617** - Warning message improvement (small scope)
3. **#2373** - Obsolete attribute (editor knowledge)
4. **#2309** - Navigation cleanup (engine knowledge)

### Areas Needing Attention
- Android build pipeline (multiple issues)
- NuGet package management
- Mesa/AMD Linux support

---

## Session Log

### 2026-02-10
- Cloned stride3d/stride
- Forked to roku674/stride
- Configured git with roku674@gmail.com
- Explored full codebase (128+ projects)
- Created PROJECT_STRUCTURE_DICTIONARY.md
- Created PROJECT_WORK.md
- Mapped 28 open issues to codebase areas
