# Bringing Blender editor controls to Unreal Engine 5!

Are you tired of clicking gizmos? Whether you're transitioning from Blender to Unreal Engine, or you simply want a faster, hotkey-driven workflow, the Blender Editor Controls plugin is designed to accelerate level design, animation, and scene blocking, by letting you move, rotate, and scale assets using hotkeys, and numeric input.


## [GET IT FOR FREE ON FAB](https://www.fab.com/listings/9bb18e16-0dfa-472b-b421-c9c277dd0d09)

### Manipulate transforms using hotkeys (rebindable)
<img width="470" height="479" alt="overview" src="https://github.com/user-attachments/assets/d6328d34-ee90-4478-8f87-dc962d8c88db" />

### Manipulate transforms using numerical values
<img width="470" height="479" alt="numeric" src="https://github.com/user-attachments/assets/63ee7b32-429b-4333-8522-f5ca361c7237" />

### Constrain transform manipulation to axis/plane of choice
<img width="470" height="479" alt="axis-locking" src="https://github.com/user-attachments/assets/bff946b2-aa7a-42cf-be91-8658479b1ca8" />

---
## Table of Contents
- [Bringing Blender editor controls to Unreal Engine 5!](#bringing-blender-editor-controls-to-unreal-engine-5)
  - [GET IT FOR FREE ON FAB](#get-it-for-free-on-fab)
    - [Manipulate transforms using hotkeys (rebindable)](#manipulate-transforms-using-hotkeys-rebindable)
    - [Manipulate transforms using numerical values](#manipulate-transforms-using-numerical-values)
    - [Constrain transform manipulation to axis/plane of choice](#constrain-transform-manipulation-to-axisplane-of-choice)
  - [Table of Contents](#table-of-contents)
  - [1. Installation](#1-installation)
  - [2. Features](#2-features)
  - [3. Contributing](#3-contributing)
    - [Submission Rules](#submission-rules)
    - [Architecture Overview](#architecture-overview)
      - [Source Directory Tree](#source-directory-tree)
  - [4. Usage Guide \& Hotkeys](#4-usage-guide--hotkeys)
  - [5. Settings \& Customization](#5-settings--customization)
  - [6. Compatibility](#6-compatibility)
  - [7. License](#7-license)
---

## 1. Installation

**Method 1: Git Clone (Recommended)**

1. Navigate to the root directory of your Unreal Engine project (where your `.uproject` file is located).
2. If it does not exist, create a new folder named `Plugins`.
3. Open a terminal inside the `Plugins` folder.
4. Run the command: 
   ```bash
   git clone https://github.com/jefimh/BlenderEditorControlsUE5.git
   ```
5. Open your Unreal Engine project. It will ask to rebuild the plugin modules; click "Yes".
6. Note: This plugin should be enabled by default. If for any reason it is not active, navigate to **Edit > Plugins**, search for "Blender Editor Controls", and ensure the box is checked.

**Method 2: ZIP Download**

1. Download the source code as a ZIP file.
2. Extract the archive.
3. Navigate to the root directory of your Unreal Engine project (where your `.uproject` file is located) and create a `Plugins` folder if it does not exist.
4. Move the extracted folder into your `Plugins/` directory.
5. Open your Unreal Engine project. It will ask to rebuild the plugin modules; click "Yes".
6. Note: This plugin should be enabled by default. If for any reason it is not active, navigate to **Edit > Plugins**, search for "Blender Editor Controls", and ensure the box is checked.

---

*(Note for C++ developers: You can also right-click your `.uproject` file, select "Generate Visual Studio project files", and compile manually via your IDE).*

---

## 2. Features

- **Blender-Style Hotkeys**: Use **G** (Grab/Translate), **R** (Rotate), and **T** (Scale) to immediately start transforming your selection without needing to click or drag gizmo arrows.
- **Mid-Session Tool Switching**: Seamlessly switch between Move, Rotate, and Scale during an active transformation without needing to cancel or click out.
- **Infinite Cursor Wrapping**: Drag endlessly! When your cursor hits the edge of the viewport during an operation, it seamlessly wraps around to the other side.
- **Axis Locking**: Lock transformations to specific axes or planes by pressing **X**, **Y**, or **Z** during an operation. Pressing the axis key twice toggles between Global and Local space.
- **Numeric Input**: Type values directly during an operation for precise adjustments (e.g., press `G`, `X`, type `15.5`, and press `Enter`). Supports unit-aware math parsing.
- **Trackball Rotation**: Press **R** twice to enter freeform Trackball rotation mode.
- **Duplicate & Move**: Press **Shift+D** to duplicate the current actor selection and immediately begin moving it.
- **Advanced Editor Snapping**: Natively supports standard Unreal Engine vertex snapping (hold `V`) and snapping to other actors.
- **Multi-Context Support**: Works seamlessly across:
  - Standard Level Editor Actors (fully supports Orthographic Viewports)
  - Blueprint Components (SCS Tree Nodes)
  - Control Rig Elements (Bones, Controls)
- **Undo & Redo**: Native editor `Ctrl+Z` and `Ctrl+Y` are completely supported for all operations.

> **Note:** If the axis gizmo lines do not appear immediately when axis/plane locking, please wait for all background shaders to finish compiling.
---

## 3. Contributing

Contributions of all kinds are highly welcomed! Please adhere to the following rules when contributing:

### Submission Rules
1. **Target Branch:** All Pull Requests **must** be submitted against the `dev` branch.
2. **Code Style:** Please align with standard Unreal Engine C++ coding conventions.
3. **Commit Messages:** Keep commit messages clear, concise, and focused on the change.
4. **Engine Version:** All bug reports and PRs must specify the Unreal Engine version.

### Architecture Overview 

To help you get up to speed with the project, here is a high-level overview of the main systems in the `Source/` directory. Detailed API documentation is also available via Doxygen comments directly in the header files.

#### Source Directory Tree
```text
Source
└── BlenderEditorControlsPlugin
    ├── BlenderEditorControlsPlugin.Build.cs
    ├── Private
    │   ├── ControlRig
    │   │   └── ControlRigSelectionHelper.cpp
    │   ├── Input
    │   │   ├── InputProcessor.cpp
    │   │   └── Numeric
    │   │       ├── NumericInputProcessor.cpp
    │   │       └── Helpers
    │   │           ├── NumericParser.cpp
    │   │           └── UnitFormatter.cpp
    │   ├── Pivots
    │   │   ├── ActorPivot.cpp
    │   │   ├── ControlRigPivot.cpp
    │   │   └── SCSPivot.cpp
    │   ├── Tools
    │   │   ├── MoveTool.cpp
    │   │   ├── RotateTool.cpp
    │   │   ├── ScaleTool.cpp
    │   │   └── ToolBase.cpp
    │   ├── UI
    │   │   ├── AxisLockGizmoComponent.cpp
    │   │   └── TransformHUD.cpp
    │   ├── Utils
    │   │   └── MathHelpers.cpp
    │   ├── BlenderControlsCommands.cpp
    │   ├── BlenderEditorControls.cpp
    │   ├── Style.cpp
    │   ├── SWelcomeWindow.cpp
    │   └── TransformSession.cpp
    └── Public/ (Header files mirroring Private structure)
```

- [**`InputProcessor`**](Source/BlenderEditorControlsPlugin/Public/Input/InputProcessor.h): The gatekeeper. It hooks into the Slate application to intercept hotkeys (G, R, S, Shift+D) before they reach the viewport and triggers a new transform session.
- [**`TransformSession`**](Source/BlenderEditorControlsPlugin/Public/TransformSession.h): The core state machine. It manages the active tool's lifecycle, caches initial mouse/camera states, and handles Unreal Engine's `FScopedTransaction` to ensure Undo/Redo works flawlessly.
- [**`Tools/`**](Source/BlenderEditorControlsPlugin/Public/Tools/): Contains the logic for specific operations (`MoveTool`, `RotateTool`, `ScaleTool`). They calculate math based on mouse deltas and send the values to the pivots.
- [**`Pivots/`**](Source/BlenderEditorControlsPlugin/Public/Pivots/): Abstractions that handle the actual application of transforms to different object types. For example, `ActorPivot` handles standard actors, while `ControlRigPivot` safely interfaces with RigVM.
- [**`Input/Numeric/`**](Source/BlenderEditorControlsPlugin/Public/Input/Numeric/): Manages keyboard-driven value inputs during an active session, interpreting units and math formulas typed by the user.
- [**`UI/`**](Source/BlenderEditorControlsPlugin/Public/UI/): The screen-space widget (`TransformHUD`) that displays active values, and the `AxisLockGizmoComponent` responsible for drawing the infinite colored lines.

---

## 4. Usage Guide & Hotkeys

| Action | Shortcut | Description |
| :--- | :--- | :--- |
| **Translate (Grab)** | `G` | Moves the selection relative to the screen plane. |
| **Rotate** | `R` | Rotates the selection relative to the view angle. |
| **Trackball Rotate** | `R` then `R` | Rotates freely in all directions. |
| **Scale** | `T` | Scales the selection uniformly. Set to T instead of S to not clash with native editor bindings |
| **Duplicate** | `Shift + D` | Duplicates actors and begins moving them. |
| **Lock Axis (Global)** | `X`, `Y`, or `Z` | Locks the transform to the X, Y, or Z world axis. |
| **Lock Axis (Local)**| Double tap `X`, `Y`, `Z` | Locks the transform to the local coordinate axis. |
| **Lock Plane** | `Shift + X, Y, Z` | Locks the transform to a 2D plane (e.g., Shift+Z locks to XY floor). |
| **Confirm** | `Left Click`, `Enter`, or `Space` | Applies the transformation. |
| **Cancel** | `Right Click` or `Esc` | Reverts the selection to its original state. |
| **Precision Mode** | Hold `Shift` | Slows down mouse influence for fine adjustments. |
| **Toggle Snapping** | Hold `Ctrl` | Inverts the current viewport grid-snapping state. |

---

## 5. Settings & Customization

You can customize the plugin's behavior, including axis colors, precision scalars, and 3D line thickness. 
To access the settings:
1. Go to **Edit > Editor Preferences**.
2. Scroll down to the **Plugins** section.
3. Select **Blender Editor Controls**.

You can also customize the exact keybindings (such as changing Scale back to `S`) by navigating to **Edit > Editor Preferences > General > Keyboard Shortcuts** and searching for **Blender Editor Controls**.

---

## 6. Compatibility

- Supported Unreal Engine versions: **5.0 – 5.8**
- **Supported Target Platforms:** Developed and verified on Windows. It has not been tested on macOS or Linux, so compatibility on those platforms is unknown.

---

## 7. License

This software is dual-licensed based on where you acquire it:

* **Fab / Epic Games Marketplace:** If you acquire or download this plugin through the Fab Marketplace or Epic Games Launcher, your use is governed exclusively by the standard **Fab End User License Agreement (EULA)**.
* **GitHub Repository:** If you clone, download, or build directly from this GitHub repository, your use is governed by the custom license terms below.

---

This software is provided for use in both non-commercial and commercial projects under the following terms:

1. **Development Use:** You may freely use and modify this plugin internally to create commercial products (e.g., video games, renders, media) without any attribution requirement.
2. **Free Redistribution & Attribution:** You may redistribute this plugin or modified versions of it, provided it is distributed entirely for free. If you choose to redistribute it, you must provide exact credit to jefimh and include a link to the original repository: https://github.com/jefimh/BlenderEditorControlsUE5.
3. **No Resale:** You may not repackage, sublicense, or resell this plugin, or any modified version of it, as a standalone tool, plugin, or asset on any marketplace or platform.
