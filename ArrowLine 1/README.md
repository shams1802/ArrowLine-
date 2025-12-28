# Unity Third-Person Bow & Arrow Combat System

A Unity project for a third-person bow and arrow combat system with realistic aiming, animation, and physics. Designed for action-adventure gameplay, supporting character movement, equipment, and combat mechanics.

---

## 📑 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Step-by-Step Implementation](#step-by-step-implementation)
  - [Phase 1: Project Foundation Setup](#phase-1-project-foundation-setup)
  - [Phase 2: Character Movement and Camera Control](#phase-2-character-movement-and-camera-control)
  - [Phase 3: Combat Stance and Animation Rigging](#phase-3-combat-stance-and-animation-rigging)
  - [Phase 4: Advanced Aiming Mechanics](#phase-4-advanced-aiming-mechanics)
  - [Phase 5: Advanced Aiming Mechanics](#phase-5-advanced-aiming-mechanics)
  - [Phase 6: Equipment Management System](#phase-6-equipment-management-system)
  - [Phase 7: Audio and Ammunition System](#phase-7-audio-and-ammunition-system)
- [Animation State Machine](#animation-state-machine)
- [Physics Configuration](#physics-configuration)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Important Notes](#important-notes)

---

## Overview
Implements a third-person bow and arrow system with:
- Character movement and camera control
- Bow drawing, aiming, and arrow physics
- Animation state management
- Equipment and ammo handling

---

## Features
- Third-person movement (keyboard/controller)
- Camera collision handling
- Animator blend trees for walk/run
- Modular scripts for easy extension

---

## Project Structure
```plaintext
Assets
├── Assets
│   ├── Free medieval weapons
│   │   ├── Materials
│   │   ├── Models
│   │   ├── Prefabs
│   │   ├── Scenes
│   │   ├── Textures
│   │   └── README.md
│   └── Longbow
│       ├── Animator
│       ├── Materials
│       ├── Textures
│       └── (erika_archer.fbx and 39 other fbx)
├── Prefabs
│   └── CrossHair
├── Scripts
│   ├── Camera
│   │   └── CameraController.cs
│   ├── Character	
│   │   ├── InputSystem.cs
│   │   └── Movement.cs
│   └── Weapon	
│       ├── Arrow.cs
│       └── Bow.cs
└── UI
    └── arrow-crosshair 1
```

```plaintext
ENV
├── Plane
├── Cube1
├── Cube2
├── Cube3
└── Cube4

Player
└── erika_archer
    ├── Erika_Archer_Meshes
    │   ├── Erika_Archer_Body_Mesh
    │   ├── Erika_Archer_Clothes_Mesh
    │   ├── Erika_Archer_Eyelashes_Mesh
    │   └── Erika_Archer_Eyes_Mesh
    │
    └── Hips
        ├── LeftUpLeg
        │   └── LeftLeg
        │       └── LeftFoot
        │           └── LeftToeBase
        │               └── LeftToe_End
        │
        ├── RightUpLeg (Same as LeftUpLeg)
        │
        └── Spine
            └── Spine1
                └── Spine2
                    ├── LeftShoulder
                    │   └── LeftArm
                    │       └── LeftForeArm
                    │           └── LeftHand
                    │               ├── Wooden Bow
                    │               │   ├── Wooden Bow_1
                    │               │   │   └── WB.main
                    │               │   │       │
                    │               │   │       ├── WB.down.bone
                    │               │   │       │   └── WB.down.bone.001
                    │               │   │       │       └── WB.down.bone.002
                    │               │   │       │           └── WB.down.bone.003
                    │               │   │       │               └── WB.down.bone.004
                    │               │   │       │                   └── WB.down.bone.005
                    │               │   │       │                       └── WB.down.bone.005_end
                    │               │   │       │
                    │               │   │       ├── WB.down.horn
                    │               │   │       │   └── WB.down.horn_end
                    │               │   │       │
                    │               │   │       ├── WB.down.shoulder
                    │               │   │       │   └── WB.down.ik
                    │               │   │       │       └── WB.down.ik_end
                    │               │   │       │
                    │               │   │       ├── WB.string
                    │               │   │       │   └── WB.string_end
                    │               │   │       │
                    │               │   │       ├── WB.top.bone
                    │               │   │       │   └── WB.top.bone.001
                    │               │   │       │       └── WB.top.bone.002
                    │               │   │       │           └── WB.top.bone.003
                    │               │   │       │               └── WB.top.bone.004
                    │               │   │       │                   └── WB.top.bone.005
                    │               │   │       │                       └── WB.top.bone.005_end
                    │               │   │       │
                    │               │   │       ├── WB.top.horn
                    │               │   │       │   └── WB.top.horn_end
                    │               │   │       │
                    │               │   │       ├── WB.top.shoulder
                    │               │   │       │   └── WB.top.ik
                    │               │   │       │       └── WB.top.ik_end
                    │               │   │       │
                    │               │   │       └── StringInitialPos
                    │               │   │
                    │               │   └── wooden bow_1
                    │               │
                    │               ├── LeftHandIndex1
                    │               │   └── LeftHandIndex2
                    │               │       └── LeftHandIndex3
                    │               │           └── LeftHandIndex4
                    │               ├── LeftHandMiddle (1-4)
                    │               ├── LeftHandRing (1-4)
                    │               ├── LeftHandPinky (1-4)
                    │               └── LeftHandThumb (1-4)
                    │
                    ├── Neck
                    │   └── Head
                    │       ├── HeadTop_End
                    │       ├── LeftEye
                    │       └── RightEye
                    │
                    └── RightShoulder (Same as LeftShoulder except for Wooden Bow)

CameraHolder
└── Center
    ├── Main Camera
    │   └── UICamera
    └── CamPosition

```


```plaintext
ENV
├── Plane
├── Cube1
├── Cube2
├── Cube3
└── Cube4
Player
└── erika_archer
CameraHolder
└── Center
    ├── Main Camera
    └── CamPosition
```



---

## Prerequisites

* Unity 2020.3 LTS or newer
* Visual Studio / VS Code
* Mixamo Erica Archer model & animations
* Basic Unity & C# knowledge

---

## Quick Start

1. Import Erica Archer from Mixamo
2. Configure humanoid rig and animations
3. Set up Animator Controller
4. Add movement & camera scripts
5. Test locomotion and camera behavior

---

## Step-by-Step Implementation

---
---

## Phase 1: Project Foundation Setup

---

### Step 1.1: Import Character Assets

* Create a `3D universe` `Project` in `Unity Hub`
* Download **Erica Archer** from [mixamo](https://www.mixamo.com/#/) or use the already provided `Longbow` folder
* Create the following folder structure :

```plaintext
Assets
├── Assets
│   └── Longbow
│       ├── Animator
│       ├── Materials
│       ├── Textures
│       └── (erika_archer.fbx and 39 other fbx)
├── Prefabs(to be added)
├── Scripts(to be added)
└── UI(to be added)
```

* Empty folders `Animator`, `Materials`and `Textures` from `Assets/Assets/Longbow`, if anything in it is present

* Drag `erika_archer.fbx` from `Assets/Assets/Longbow` into the **Hierarchy**

* Now select `erika_archer.fbx` from `Assets/Assets/Longbow` (not the Hierarchy one) and view its **Inspector** tab on the right:

  * **Rig Tab**

    * Set **Animation Type** to `Humanoid`
    * Set **Avatar Definition** to `Create From This Model`
    * Click **Apply**
  * **Materials Tab**

    * Click **Extract Textures** and select the folder `Assets/Assets/Longbow/Textures`
    * A **Normal Map** popup will appear — click **Fix Now**
    * Click **Extract Materials** and select the folder `Assets/Assets/Longbow/Materials`

* For **every animation FBX file** inside `Assets/Assets/Longbow`:

  * Select all the animation file using shift key
  * Go to **Rig Tab**
  * Set **Animation Type** to `Humanoid`
  * Set **Avatar Definition** to `Copy From Other Avatar`
  * Choose `erika_archerAvatar` from the dropdown
  * Click **Apply**

---

### Step 1.2: Environment Setup
* In the **Hierarchy** window, right click → `Create Empty` and rename it to `ENV`
* Select `ENV`, then right click → `3D Object` → `Plane` (this will be the ground)
* Select `ENV` again, then right click → `3D Object` → `Cube`
* Duplicate the Cube until you have **4 cubes**
* Adjust the **position and scale** of the cubes to form simple walls around the plane

---

### Step 1.3: Player Hierarchy

* In the **Hierarchy**, right click → `Create Empty` and rename it to `Player`
* Select `Player`, then in the **Inspector**, open the Transform component
* Click the **three dots** and choose **Reset** to zero all transform values
* Drag `erika_archer` (the one already in the scene) under `Player`

```plaintext
ENV
├── Plane
├── Cube1
├── Cube2
├── Cube3
└── Cube4
Player
└── erika_archer
```

---

### Step 1.4: Animator Controller

* Navigate to `Assets/Assets/Longbow/Animator` in the Project window

  * Right click → `Create` → `Animator Controller`
  * Rename it to `PlayerAnim`
* Select `Player` in the Hierarchy, then in the Inspector:

  * Click **Add Component** → add **Animator**
  * Assign:

    * **Controller** → `PlayerAnim`
    * **Avatar** → `erika_archerAvatar`

---

### Step 1.5: Animation Configurationv

Select `Window` → `Animation` → `Animator` to open the Animator window

Then in the Project window under `Assets/Assets/Longbow`, locate:
`standing idle 01`, `standing walk (front/back/left/right)`, and `standing run (front/back/left/right)`

**Idle**

* Select `standing idle 01`
* In the Inspector, rename it from `mixamo.com` to `Idle`
* Enable **Loop Time** and **Loop Pose**
* Under **Root Transform Position (Y)**:

  * Enable **Bake Into Pose**
  * Set **Based Upon** to `Feet`
* Click **Apply**

**Walk (Front/Back/Left/Right)**

* Select each `standing walk` animation one by one
* Rename from `mixamo.com` to `Walk Front`, `Walk Back`, `Walk Left`, `Walk Right`
* Enable **Loop Time** and **Loop Pose**
* Under **Root Transform Rotation**:

  * Enable **Bake Into Pose**
  * Set **Based Upon** to `Original`
* Under **Root Transform Position (Y)**:

  * Enable **Bake Into Pose**
  * Set **Based Upon** to `Feet`
* Click **Apply**

**Run (Front/Back/Left/Right)**

* Apply the **exact same settings** used for Walk animations

---

### Step 1.6: Blend Trees

* In the **Animator** window, right click inside the **Base Layer**
* Select `Create State` → `From New Blend Tree`
* Rename the state to `Walk`
* Repeat the same process and rename the second one to `Run`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%201,%20STEP%206.png)

**Animator Parameters**

Select the **Parameters** tab, click `+`, and create:

* `float forward`
* `float strafe`
* `bool sprint` (set default value to false)

**Walk Blend Tree**

* Double click `Walk`
* Select the **Blend Tree**
* In the Inspector:

  * Set **Blend Type** to `2D Simple Directional`
  * Set **Parameters** to `strafe` (X) and `forward` (Y)
* Under **Motion**, click `+` → `Add Motion Field` five times
* Go to `Assets/Assets/Longbow` folder and find `standing idle 01`, `standing walk (front/back/left/right)`, and `standing run (front/back/left/right)`
* Click on small triangle there and assign:

  * Idle (0,0)
  * Walk Forward (0,1)
  * Walk Back (0,-1)
  * Walk Left (-1,0)
  * Walk Right (1,0)

**Repeat the same configuration for the Run blend tree**

---

### Step 1.7: Transitions

* Right click on `Walk` then select `Make Transition` then select `Run`. Now select transition line from `Walk` → `Run`

  * Disable **Has Exit Time**
  * Under `Conditions` select `sprint == true`
* Create a transition from `Run` → `Walk`

  * Disable **Has Exit Time** and add condition: `sprint == false`

⚠️ **Do not rename parameters** (`forward`, `strafe`, `sprint`)

---

## Phase 2: Character Movement and Camera Control

---

### Step 2.1: Script Setup

Create the following folder structure:

```plaintext
Assets
├── Assets(Longbow)
├── Prefabs(to be added)
├── Scripts
│   ├── Camera
│   └── Character
│       ├── InputSystem.cs
│       └── Movement.cs
└── UI(to be added)
```


* Copy `Movement.cs` from the provided folder `Assets/Scripts/Character/` and paste its contents into your `Movement.cs`

---

### Step 2.2: Character Controller

* Select `Player` in the Hierarchy
* Drag and drop `Character.cs` onto it
* A **Character Controller** component will be added automatically
* Adjust:

  * **Center**
  * **Radius**
  * **Height**

  so the green capsule correctly surrounds the character model

---

### Step 2.3: Input System

* Copy `InputSystem.cs` from:
  `Assets/Scripts/Character/InputSystem/1 Player Input/`
* Attach `InputSystem.cs` to `Player`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%202,%20STEP%203.png)

**Input Manager**

* Go to `Edit` → `Project Settings` → `Input Manager`

* Select **Axes** and increase **Size** by 1

* Edit the new axis and set:

  * Name: `Sprint`
  * Positive Button: `left shift`
  * Alt Negative Button: `right shift`

* Temporarily move the **Main Camera** under `Player` and press Play

* Verify that movement input works

* If confirmed, move the camera back to its original place

⚠️ **Input System package mismatch** 

* If error like **InvalidOperationExecution** or **InputMismatch** persists

* Go to `Edit` → `Prject Settings`, select `Player`
* Scroll to `Other Settings`, then find `Active Input Handling` and set it to `Both`

---

### Step 2.4: Camera Hierarchy

* Create an empty GameObject named `CameraHolder`
* Reset its position to `(0,0,0)`
* Right click `CameraHolder` → `Create Empty` → rename to `Center`
* Position `Center` roughly at the hip level of the character
* Drag `Main Camera` under `Center` and adjust position as desired

```plaintext
ENV
Player
CameraHolder
└── Center
    ├── Main Camera
    └── CamPosition (later)
```

---

### Step 2.5: Camera Controller

* Inside `Assets/Scripts/Camera`, create `CameraController.cs`
* Copy contents from:
  `Assets/Scripts/Camera/CameraController/1 Camera and Player Integration/CameraController.cs`
* Attach this script to `CameraHolder`
* Go to `Assets/Scripts/InputSystem`, replace `InputSystem.cs` from provided folder:
  `Assets/Scripts/Character/InputSystem/2 Camera Integration/`

---

### Step 2.6: Tagging

* Select `Player`
* Set **Tag** to `Player`
* Press Play and observe that camera collision issues still exist

---

### Step 2.7: Camera Collision Fix

* Replace the contents of `CameraController.cs` with:
  `Assets/Scripts/Camera/CameraController/2 Collision Avoidance/CameraController.cs`

**CamPosition Setup**

* Right click `CameraHolder/Center` → `Create Empty` → rename to `CamPosition`
* Select **Main Camera**

  * Click the **three dots** in Transform → `Copy Component`
* Select **CamPosition**

  * Click the **three dots** → `Paste Component Values`

**CameraHolder Setup**

* In **CameraHolder**'s **Inspector** tab, under **Camera Controller (Script)** component, drag `CamPosition` from `CameraHolder/Center/` to `Cam Position` slot

* In `Cam Collision Layers` select `Default`

**Camera**

* Select **Main Camera**, in **Inspector** tab, under **Camera** component, adjust **Clipping Plane** values as needed

✅ Camera collision is now resolved

---
## Phase 3: Combat Stance and Animation Rigging

---

### Step 3.1: Import Weapon Assets

* Add weapon assets **Free medieval weapons** into `Assets/Assets`
* You can either:
  * Download from Unity Asset Store:  
    https://assetstore.unity.com/packages/3d/props/weapons/free-pack-of-medieval-weapons-136607  
  * OR use the provided `Free medieval weapons` folder from this repository

* After importing or copying, confirm your Project window folder structure looks **exactly** like this:

```plaintext
Assets
├── Assets
│   ├── Free medieval weapons
│   │   ├── Materials
│   │   ├── Models
│   │   ├── Prefabs
│   │   ├── Scenes
│   │   ├── Textures
│   │   └── README.md
│   └── Longbow
├── Scripts
└── UI (to be added)
````

* Go to `Assets/Assets/Free medieval weapons/Materials`, check if texture is added
* If not, click on each individual, select respective Map from `/Textures`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%201%201.png)

* Go to `Assets/Assets/Free medieval weapons/Models`, check if materials are visible
* If not, click on each individually, select respective `On Demand Remap` from `/Materials`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%201%202.png)

* Go to `Assets/Assets/Free medieval weapons/Prefabs`, check if mess and materials are visible
* If not, double click on each individually, select respective `Mesh` and `Materials`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%201%203.png)

---

### Step 3.2: Animator Parameters and Bow Animations Setup

* Go to **Animator** window, under **Parameters** tab, create a new trigger named `fire` (deactive)
* Also create two new bools name them `aim` and `pullString` (default false)

* Navigate to `Assets/Assets/Longbow` and locate the following animation files:

  * `standing aim (overdraw/recoil)`
  * `standing draw arrow`
  * `standing (equip/disarm) bow`
  * `standing aim walk (back/front/left/right)`

**Pull String**

* Select `standing aim overdraw`
* In the Inspector, rename it from `mixamo.com` to `Pull String`
* Disable **Loop Time**
* Under **Root Transform Rotation**, enable **Bake Into Pose** and set **Based Upon** to `Original`
* Under **Root Transform Position (Y)**, enable **Bake Into Pose** and set **Based Upon** to `Feet`
* Click **Apply**


**Fire Arrow, Draw Arrow, Equip Bow, Disarm Bow**

* Apply the **same settings as Pull String**, only change names:

  * `standing aim recoil` → rename to `Fire Arrow`
  * `standing draw arrow` → rename to `Draw Arrow`
  * `standing equip bow` → rename to `Equip Bow`
  * `standing disarm bow` → rename to `Disarm Bow`


**Aim Walk (Front/Back/Left/Right)**

* Select each `standing aim walk` animation one by one
* Rename from `mixamo.com` to `Aim Walk Front`, `Aim Walk Back`, `Aim Walk Left`, `Aim Walk Right`
* Enable **Loop Time** and **Loop Pose**
* Under **Root Transform Rotation**, enable **Bake Into Pose** and set **Based Upon** to `Original`
* Under **Root Transform Position (Y)**, enable **Bake Into Pose** and set **Based Upon** to `Feet`
* Click **Apply**


---

### Step 3.3: Upper Body Avatar Mask and Animator Layer

* Navigate to `Assets/Assets/Longbow/Animator`, right click → `Create` → `Animation` → `Avatar Mask` and rename it to `UpperBody`

* Select `UpperBody`, in the **Inspector** tab, under **Humanoid**, disable `Lower Body`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%203.png)

* Open **Animator**, under **Layers** tab
* Click the `+` button and rename it to `UpperBody` and click the **gear icon**

  * Set **Mask** → `UpperBody`
  * Set **Weight** → `1`

---

### Step 3.4: Upper Body Arrow Logic State Machine

* In the **Project window**, go to `Assets/Assets/Longbow`

* Expand (click small triangle) these animations:

  * `standing draw arrow`
  * `standing aim overdraw`
  * `standing aim recoil`

* Drag and drop these into the **UpperBody layer** in Animator:

  * `Draw Arrow`
  * `Pull String`
  * `Fire Arrow`


* Right click inside **UpperBody layer**, select `Create State` → `Empty` and rename it to `Empty`
* Right click `Empty` → `Set as Layer Default State`


**Transitions**

| From | To | Has Exit Time | Condition |
| :--- | :--- | :---: | :--- |
| **Empty** | **Draw Arrow** | No | `aim == true` |
| **Draw Arrow** | **Pull String** | No | `pullString == true` |
| **Pull String** | **Fire Arrow** | No | `fire == active` |
| **Fire Arrow** | **Draw Arrow** | **Yes** | `aim == true` |
| **Any State** | **Empty** | No | `aim == false` |


* Right click inside **UpperBody** area
* Select `Create Sub-State Machine` and rename it to `Arrow Logic`

* Select and drag `Draw Arrow`, `Pull String` and `Fire Arrow` into `Arrow Logic`

---

### Step 3.5: Aim Movement Blend Tree

* Switch to **Base Layer**, duplicate `Run` and rename it to `Aim Move`

* Open `Aim Move` and change motions to:

  * Idle (0,0)
  * Aim Walk Forward (0,1)
  * Aim Walk Back (0,-1)
  * Aim Walk Left (-1,0)
  * Aim Walk Right (1,0)

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%205.png)

**Transitions**

| From | To | Has Exit Time | Conditions |
| :--- | :--- | :---: | :--- |
| **Walk** | **Aim Move** | No | `aim == true` |
| **Aim Move** | **Walk** | No | `aim == false`, `sprint == false` |
| **Run** | **Aim Move** | No | `aim == true` |
| **Aim Move** | **Run** | No | `aim == false`, `sprint == true` |

---

### Step 3.6: Bow Model Attachment

* Go to `Assets/Assets/Free medieval weapons/Models`, select `Wooden Bow.fbx` and drag it to **LeftHand** (`Player/erika_archer/Hips/Spine/Spine1/Spine2/LeftShoulder/LeftArm/LeftForeArm/LeftHand`)

* Adjust **Position / Rotation** so the bow sits naturally in the left hand **(use Rotation → X = 90, Y = 180, Z = 0)**

* Add textures to `Wooden Bow` from `Wooden Bow_1_Wooden Bow_1_AlbedoTransparency` in `Assets/Assets/Free medieval weapons/Textures`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%203,%20STEP%206.png)

---

### Step 3.7: Bow Script and Input Replacement

* In `Assets/Scripts`, create a folder named `Weapon`
* Inside it, create `Bow.cs` and copy contents from:
  `Assets/Scripts/Weapon/Bow/1 Bow Unlit`
* Attach `Bow.cs` to `Wooden Bow` in (`Player` → `LeftHand`)

* Navigate to `Assets/Scripts/Character` and replace `InputSystem.cs` entire contents with:
  `Assets/Scripts/Character/InputSystem/3 Bow Equipment`



* Press **Play** and Test.

If animations and bow behavior respond, Phase 3 is complete.

⚠️ **Zoom too hard** 

* If Camera Zoom too much on mouse right click

* Go to `CameraHolder`, under `Camera Controller` (Script), change `Camera Move Settings`
* Especially change `Zoom Field of View` and `Zoom Speed`

---

## Phase 4: Advanced Aiming Mechanics

---

### Step 4.1: Crosshair UI Setup

* Go to `Assets/Scripts/Character`, replace `InputSystem.cs` content with provided folder
  `Assets/Scripts/Character/InputSystem/4 Aiming Control`

* Right click in **Hierarchy** → `UI` → `Canvas`, right click on `Canvas` → `UI` → `Image`

* Create folder `Assets/UI`, from provided folder, add image `arrow-crosshair 1` (or your own)

```plaintext
Assets
├── Assets
├── Prefabs (to be added)
│   └── CrossHair (to be added)
├── Scripts
└── UI
    └── arrow-crosshair 1
```

* Select `arrow-crosshair 1`, set `Texture Type` → `Sprite (2D and UI)` and `Sprite Mode` → `Single` then click `Apply`

* Select `Canvas/Image`, in `Image` component, drag `arrow-crosshair 1` to `Source Image`

---

### Step 4.2: World Space Crosshair

* Select `Canvas`

  * `Render Mode` → `World Space`
  * `Rect Transform` → Pos X/Y/Z = `0`
  * Set `Width = 10`, `Height = 1` (adjust if needed)
  * Adjust scale if needed

* Select `Image`, `Rect Transform` → `Stretch / Stretch` 

* Select `Canvas`, adjust scale and position if needed

⚠️ Dont change position and scale of `Image`

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%204,%20STEP%202.png)

* Create folder `Assets/Prefabs`

* Rename `Canvas` → `CrossHair`, and drag `CrossHair` into `Assets/Prefabs`

* Delete `CrossHair` and `EventSystem` from `Hierarchy`

* Go to `Player → LeftHand → Wooden bow`

  * In `Bow (Script)` component, drag `CrossHair` prefab to `Cross Hair Prefab`

---

### Step 4.3: Aim Configuration

* Select `Player`, in `Input System (Script)`:
  * `Bow Script` → `Wooden bow` (Player -> LeftHand)
  * `Spine` → `Spine` (Player/erika_archer/Hips)
  * `Aim Layer` → `Default`

* Play and verify aim direction

  * If incorrect:

    * Enable `Test Aim`
    * Adjust `Spine Offset`
    * Copy Component → Paste Component Values (after Play mode)

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%204,%20STEP%203.png)

⚠️ **Zoom too hard** - Go to `CameraHolder`, in `Camera Controller` adjust `Zoom Field of View` and `Zoom Speed`

* Adjust `Main Camera` position slightly left

* Apply same values to `CameraHolder/Center/CamPosition`

* Verify aiming and disable `Test Aim`

---

### Step 4.4: UI Camera Setup

* Right click on `Main Camera` under `CameraHolder/Center`

* Select `Camera` then rename to `UIcamera`

  * `Culling Mask` → `UI`
  * `Clear Flags` → `Depth Only`
  * Disable `Audio Listener`

* Select `Main Camera`

  * `Culling Mask` → Everything except `UI`

* Replace scripts:

  * `CameraController.cs` → `Assets/Scripts/Camera/CameraController/3 UI CrossHair Updation`
  * `InputSystem.cs` → `Assets/Scripts/Character/InputSystem/5 UI CrossHair Updation`

* Play and verify UI crosshair

⚠️ **If `Clear Flags` not found**
* Select `Main Camera`, `Render Type` → `Base` and `Background Type` → `Skybox`
* Select `UICamera`, `Render Type` → `Base`
* Select `Main Camera`, go to `Stack` then add `UICamera`
---

### Step 4.5: Bow String Logic

* Replace scripts:

  * `Bow.cs` → `Assets/Scripts/Weapon/Bow/2 Bow String Control`
  * `InputSystem.cs` → `Assets/Scripts/Character/InputSystem/6 Bow String Control`

* Open `Animator`, under `UpperBody` layer → `Arrow Logic`, double click on `Draw Arrow`, under `Animation` tab, find `Events` click `+`

* Add Animation Events on suitable time

  * `Draw Arrow` → `EnableArrow` (when arrow is drawn)
  * `Draw Arrow` → `Pull` (when start string pull)
  * `Fire` → `Release` (when arrow shot)
  * `Fire` → `DisableArrow` (when arrow should disappear)

  ⚠️ Use exact naming

---

### Step 4.6: Arrow & String Setup

* Go to `Assets/Assets/Free medieval weapons/Prefabs`

* Drag `Arrow` to `Player → RightHand`

* Create empty under
  `Player → LeftHand/Wooden Bow/Wooden Bow_1/WB.main`

  * Name: `InitialStringPos`
  * Copy position from `WB.String`

* Create empty under `RightHand`

  * Name: `StringHandPullPos`
  * Copy position from `RightHand`

* Fill `Bow (Script)`:

**Arrow Settings**

* `Arrow Count` = 10
* `Arrow Prefab` → `Arrow` (Assets\Assets\Free medieval weapons\Prefabs)
* `Arrow Pos` → `Arrow` (Player → RightHand)
* `Arrow Equip Parent` → `RightHand` (Player → RightForeArm)

**Bow String Settings**

* `Bow String` → `WB.string` (Player → LeftHand/Wooden Bow/Wooden Bow_1/WB.main)
* `String Initial Pos` → `InitialStringPos` (Player → WB.main)
* `String Hand Pull Pos` → `StringHandPullPos` (Player → RightHand)
* `String Initial Parent` → `WB.main` (Player → Wooden Bow_1)

---

### Step 4.7: Final Alignment

* Select `Arrow`

  * Adjust position & rotation (try `Z = -90`)

* Adjust `Wooden Bow` if required

- Select `StringHandPullPos` and enable its **Gizmo** from the icon (triangle next to the cube) in the **Inspector**.
- Reposition it to control how far the bowstring is pulled.
- If the gizmo is hard to see, open **Gizmos** (top of Scene view) and increase the **3D Icons** slider.


* Ensure:

  * `WB.String` and `InitialStringPos` have same values
  * Visually verify position of Bow and Arrow in `Game View` (use Copy Paste where ever needed)

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%204,%20STEP%207.png)

---

## Phase 5: //

---

### Step 5.1: Implement Camera-Based Aiming

**Create AimController Script**
1. Create new script: Assets/Scripts/Weapon/AimController.cs
2. This script will handle aim direction calculation

**Aim Direction Logic**
```csharp
using UnityEngine;

public class AimController : MonoBehaviour
{
    [Header("Aim Settings")]
    public Transform cameraTransform;
    public LayerMask aimLayerMask;
    public float maxAimDistance = 100f;
    
    [Header("References")]
    public Transform characterBody;
    public Transform bowTransform;
    
    private Vector3 currentAimPoint;
    
    void Update()
    {
        UpdateAimDirection();
        RotateCharacterToAim();
        RotateBowToAim();
    }
    
    void UpdateAimDirection()
    {
        // Raycast from camera to determine aim point
        Ray ray = new Ray(cameraTransform.position, cameraTransform.forward);
        
        if (Physics.Raycast(ray, out RaycastHit hit, maxAimDistance, aimLayerMask))
        {
            currentAimPoint = hit.point;
        }
        else
        {
            // If no hit, aim at max distance point
            currentAimPoint = ray.GetPoint(maxAimDistance);
        }
    }
    
    void RotateCharacterToAim()
    {
        // Calculate direction from character to aim point (horizontal only)
        Vector3 aimDirection = currentAimPoint - characterBody.position;
        aimDirection.y = 0; // Keep character upright
        
        if (aimDirection.magnitude > 0.1f)
        {
            Quaternion targetRotation = Quaternion.LookRotation(aimDirection);
            characterBody.rotation = Quaternion.Slerp(
                characterBody.rotation, 
                targetRotation, 
                Time.deltaTime * 10f
            );
        }
    }
    
    void RotateBowToAim()
    {
        // Rotate bow to point at aim location including vertical angle
        Vector3 bowAimDirection = currentAimPoint - bowTransform.position;
        
        if (bowAimDirection.magnitude > 0.1f)
        {
            Quaternion bowRotation = Quaternion.LookRotation(bowAimDirection);
            bowTransform.rotation = Quaternion.Slerp(
                bowTransform.rotation,
                bowRotation,
                Time.deltaTime * 15f
            );
        }
    }
    
    // Public method for other scripts to access aim point
    public Vector3 GetAimPoint()
    {
        return currentAimPoint;
    }
}
```

#### Step 5.2: Configure Aiming System

**Setup AimController on Character**
1. Select your character in Hierarchy
2. Add the AimController component
3. Assign references:
   - Camera Transform: Drag the main camera or camera follow target
   - Character Body: Drag the character's root transform
   - Bow Transform: Drag the Bow GameObject
   - Max Aim Distance: 100
4. Configure Layer Mask to include relevant collision layers

**Integrate with Bow Script**
Update the Bow.cs script to use aim direction:
```csharp
// Add at top of Bow class
private AimController aimController;

void Start()
{
    aimController = GetComponentInParent<AimController>();
}

// Modify ReleaseArrow method
void ReleaseArrow()
{
    if (drawnArrow == null) return;
    
    isDrawing = false;
    float shotPower = (currentDrawTime / maxDrawTime) * maxDrawPower;
    
    drawnArrow.transform.SetParent(null);
    Rigidbody arrowRb = drawnArrow.GetComponent<Rigidbody>();
    
    if (arrowRb != null)
    {
        arrowRb.isKinematic = false;
        
        // Use aim controller direction instead of transform.forward
        Vector3 shootDirection = (aimController.GetAimPoint() - arrowSpawnPoint.position).normalized;
        arrowRb.AddForce(shootDirection * shotPower * arrowSpeed, ForceMode.Impulse);
    }
    
    drawnArrow = null;
    currentDrawTime = 0f;
}
```

This provides precise aiming mechanics that follow the camera's view direction.

### Phase 6: Equipment Management System

This phase implements the ability to equip and unequip the bow using input controls and animation integration.

#### Step 6.1: Create Equipment Manager Script

**Generate EquipmentManager Script**
```csharp
using UnityEngine;

public class EquipmentManager : MonoBehaviour
{
    [Header("Equipment Settings")]
    public GameObject bowGameObject;
    public KeyCode equipToggleKey = KeyCode.E;
    
    [Header("Animation")]
    public Animator characterAnimator;
    public string equipBoolParameter = "BowEquipped";
    
    private bool isBowEquipped = false;
    
    void Start()
    {
        // Start with bow unequipped
        SetBowEquipped(false);
    }
    
    void Update()
    {
        HandleEquipmentInput();
    }
    
    void HandleEquipmentInput()
    {
        if (Input.GetKeyDown(equipToggleKey))
        {
            ToggleBowEquipped();
        }
    }
    
    void ToggleBowEquipped()
    {
        isBowEquipped = !isBowEquipped;
        SetBowEquipped(isBowEquipped);
    }
    
    void SetBowEquipped(bool equipped)
    {
        isBowEquipped = equipped;
        
        // Show or hide bow GameObject
        if (bowGameObject != null)
        {
            bowGameObject.SetActive(equipped);
        }
        
        // Update animator parameter
        if (characterAnimator != null)
        {
            characterAnimator.SetBool(equipBoolParameter, equipped);
        }
        
        // Enable/disable bow script
        Bow bowScript = bowGameObject?.GetComponent<Bow>();
        if (bowScript != null)
        {
            bowScript.enabled = equipped;
        }
    }
    
    public bool IsBowEquipped()
    {
        return isBowEquipped;
    }
}
```

#### Step 6.2: Integrate Equipment System

**Add to Character**
1. Select character in Hierarchy
2. Add EquipmentManager component
3. Configure:
   - Bow Game Object: Drag the Bow GameObject
   - Equip Toggle Key: E
   - Character Animator: Drag the Animator component
   - Equip Bool Parameter: "BowEquipped"

**Setup Animator Controller**
1. Open the CharacterAnimator controller
2. Create a new Bool parameter called "BowEquipped"
3. Create animation states or blend trees for:
   - Combat stance (bow equipped)
   - Normal stance (bow unequipped)
4. Create transitions based on BowEquipped parameter
5. Configure transition conditions and blend times

This allows seamless weapon switching with visual feedback.

### Phase 7: Audio and Ammunition System

This phase adds audio feedback for combat actions and implements an ammunition tracking system.

#### Step 7.1: Implement Audio System

**Create AudioManager for Bow**
```csharp
using UnityEngine;

public class BowAudioManager : MonoBehaviour
{
    [Header("Audio Clips")]
    public AudioClip drawSound;
    public AudioClip releaseSound;
    public AudioClip impactSound;
    
    [Header("Audio Settings")]
    public float volume = 1f;
    
    private AudioSource audioSource;
    
    void Start()
    {
        audioSource = gameObject.AddComponent<AudioSource>();
        audioSource.playOnAwake = false;
        audioSource.volume = volume;
    }
    
    public void PlayDrawSound()
    {
        if (drawSound != null)
        {
            audioSource.PlayOneShot(drawSound);
        }
    }
    
    public void PlayReleaseSound()
    {
        if (releaseSound != null)
        {
            audioSource.PlayOneShot(releaseSound);
        }
    }
    
    public void PlayImpactSound(Vector3 position)
    {
        if (impactSound != null)
        {
            AudioSource.PlayClipAtPoint(impactSound, position, volume);
        }
    }
}
```

**Integrate Audio into Bow Script**
Add to Bow.cs:
```csharp
private BowAudioManager audioManager;

void Start()
{
    audioManager = GetComponent<BowAudioManager>();
}

// In StartDrawing():
audioManager?.PlayDrawSound();

// In ReleaseArrow():
audioManager?.PlayReleaseSound();
```

#### Step 7.2: Implement Ammunition System

**Create AmmoManager Script**
```csharp
using UnityEngine;
using UnityEngine.UI;

public class AmmoManager : MonoBehaviour
{
    [Header("Ammo Settings")]
    public int maxAmmo = 30;
    public int currentAmmo = 30;
    
    [Header("UI")]
    public Text ammoText;
    
    void Start()
    {
        UpdateAmmoUI();
    }
    
    public bool HasAmmo()
    {
        return currentAmmo > 0;
    }
    
    public bool ConsumeAmmo()
    {
        if (currentAmmo > 0)
        {
            currentAmmo--;
            UpdateAmmoUI();
            return true;
        }
        return false;
    }
    
    public void AddAmmo(int amount)
    {
        currentAmmo = Mathf.Min(currentAmmo + amount, maxAmmo);
        UpdateAmmoUI();
    }
    
    void UpdateAmmoUI()
    {
        if (ammoText != null)
        {
            ammoText.text = $"Arrows: {currentAmmo}/{maxAmmo}";
        }
    }
}
```

**Integrate Ammo System into Bow**
Modify Bow.cs StartDrawing():
```csharp
void StartDrawing()
{
    AmmoManager ammoManager = GetComponent<AmmoManager>();
    
    if (ammoManager != null && !ammoManager.HasAmmo())
    {
        // No ammo available, play empty sound or show notification
        return;
    }
    
    isDrawing = true;
    currentDrawTime = 0f;
    
    // Consume ammo
    ammoManager?.ConsumeAmmo();
    
    // Rest of the drawing logic...
}
```

**Create Ammo UI**
1. In Hierarchy: Right-click → UI → Canvas
2. Right-click Canvas → UI → Text (TextMeshPro if available)
3. Position text in corner of screen
4. Configure text appearance
5. Drag text element to AmmoManager component's Ammo Text field

This completes the full implementation of audio and resource management.

## Animation State Machine

**Recommended Animator States**
1. **Idle State** - Default resting pose
2. **Locomotion Blend Tree** - Walk/Run based on speed
3. **Combat Idle** - Armed stance with bow
4. **Draw Bow** - Pulling arrow back on bowstring
5. **Aim Bow** - Holding at full draw
6. **Release Bow** - Firing animation
7. **Equip/Unequip** - Weapon switching animations

**State Transitions**
- Idle ↔ Locomotion: Based on movement speed
- Idle → Combat Idle: BowEquipped = true
- Combat Idle → Draw Bow: isDrawing = true
- Draw Bow → Aim Bow: drawTime > threshold
- Aim Bow → Release Bow: Fire1 released
- Release Bow → Combat Idle: Animation complete

## Physics Configuration

**Arrow Rigidbody Settings**
- Mass: 0.05 kg (realistic arrow weight)
- Drag: 0.1 (air resistance)
- Angular Drag: 0.05 (rotation dampening)
- Use Gravity: Enabled (realistic trajectory)
- Interpolate: Interpolate (smooth visual movement)
- Collision Detection: Continuous Dynamic (fast-moving object)

**Collider Configuration**
- Type: Capsule Collider (matches arrow shape)
- Radius: Match arrow shaft thickness
- Height: Full arrow length including tip
- Is Trigger: Disabled (physical collision)

**Layer Setup**
Create layers for proper collision:
- Player (character)
- Weapon (bow/arrows)
- Enemy (targets)
- Environment (surfaces)

Configure Layer Collision Matrix in Project Settings → Physics.

## Best Practices

**Script Organization**
- Keep scripts modular and single-purpose
- Use public fields for designer-adjustable values
- Add [Header] attributes for Inspector organization
- Comment complex logic sections

**Performance Optimization**
- Use object pooling for arrows instead of Instantiate/Destroy
- Limit arrow lifetime to prevent accumulation
- Cache component references in Start() instead of repeated GetComponent()
- Use FixedUpdate for physics calculations, Update for input

**Animation Tips**
- Use animation events to trigger sounds and effects
- Blend between states with appropriate transition times
- Create sub-state machines for complex behaviors
- Use layers for upper/lower body separation

**Debugging Strategies**
- Use Debug.DrawRay() to visualize aim direction
- Add Debug.Log() statements to trace script execution
- Use Gizmos for visualizing spawn points and ranges
- Test with Time.timeScale adjustment for slow-motion debugging

## Troubleshooting

**Arrow Doesn't Fire**
- Verify ArrowPrefab is assigned in Bow component
- Check ArrowSpawnPoint is correctly positioned
- Ensure Fire1 input is configured in Project Settings → Input Manager
- Confirm arrow has Rigidbody component

**Bow Not Attaching to Hand**
- Verify bow is child of correct hand bone
- Check character has Humanoid rig
- Adjust bow local transform position/rotation
- Test with simple cube before using complex model

**Aiming Direction Incorrect**
- Confirm camera reference is assigned in AimController
- Check LayerMask includes ground and target layers
- Verify character rotation is not locked
- Test raycast visualization with Debug.DrawRay

**Animations Not Playing**
- Ensure Animator component is on character root
- Verify animation controller is assigned
- Check animation parameters are spelled correctly
- Confirm transitions have proper conditions

**No Sound Playing**
- Import audio files to Assets/Audio/
- Assign audio clips to BowAudioManager fields
- Check AudioListener is present in scene (usually on camera)
- Verify audio volume is not muted

**Ammo Not Decreasing**
- Confirm AmmoManager component is attached
- Check ConsumeAmmo() is called in StartDrawing()
- Verify currentAmmo has starting value
- Ensure UI text reference is assigned

## Important Notes

- ❗ Always test in Play Mode after making script changes
- ❗ Save scene frequently to prevent data loss
- ❗ Use version control (Git) to track changes
- ❗ Create backup copies before major refactoring
- ✅ Character must have Humanoid rig for proper bone attachment
- ✅ Arrow Prefab must have Rigidbody for physics simulation
- ✅ Camera raycast requires proper Layer configuration
- ✅ Animation states require matching parameter names
- ✅ Audio files should be in WAV or MP3 format
- ✅ All scripts should be in appropriate folder structure
- ✅ Test bow mechanics without animations first, then integrate
- ✅ Prototype with simple shapes before adding complex models
- ✅ Balance arrow speed and draw power for satisfying gameplay


## Notes

* Test frequently in Play Mode
* Do not rename Animator parameters
* Use Humanoid rig only
* Modular design allows easy extension
