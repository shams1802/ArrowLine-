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
  - [Phase 5: Arrow Logic and Equipment Systems](#phase-5-arrow-logic-and-equipment-systems)
- [Animation State Machine](#animation-state-machine)
- [Physics Configuration](#physics-configuration)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Important Notes](#important-notes)

---

## Overview
Implements a complete third-person bow and arrow system featuring:
- Humanoid character (Erica Archer) with movement and animation
- 2D blend trees for walk/run/aim locomotion
- Full bow mechanics: equip, draw, aim, and fire
- Arrow physics with Rigidbody and collision detection
- First-person camera with collision avoidance
- Upper body IK for head/spine rotation during aim
- Footstep and impact sound effects
- Ammo system with counter management

---

## Features
- **Character System**: Erica Archer Humanoid rig with full skeleton hierarchy
- **Movement**: Walk/Run blend tree with directional locomotion (forward/back/left/right)
- **Camera**: Third-person with collision detection, zoom on aim, dual-layer rendering (main + UI)
- **Combat**: Bow equip/unequip animations with carry position on spine
- **Aiming**: Spine-based aim with IK head tracking, crosshair UI, dynamic camera positioning
- **Bow Mechanics**: String deformation with animation events, arrow ammo system
- **Arrow Physics**: Rigidbody with continuous collision detection, Capsule collider
- **Audio**: Footstep events, bow draw/release sounds, arrow impact effects
- **Animation States**: Separate upper/lower body layers with sub-state machines for arrow logic

---

## Project Structure

### Provided Resource

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
│   ├── Arrow
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
├── Sounds
│   ├── Bow & Arrow
│   ├── Footsteps
│   └── Impact Sfx
└── UI
    └── arrow-crosshair 1
```

### Hierarchy

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
    └── Hips (Wooden Bow → Spine & Arrow -> RightHand)

CameraHolder
└── Center
    ├── Main Camera
    │   └── UICamera
    └── CamPosition
```



---

## Prerequisites

* **Unity 2020.3 LTS** or newer
* **Visual Studio** or **VS Code** for script editing
* **Mixamo Erica Archer** FBX model (39 animations) - or use provided folder
* **Free Medieval Weapons** asset pack (Unity Asset Store or provided)
* **Basic C# knowledge** and Humanoid rig familiarity
* **Audio files**: WAV or MP3 format for footsteps, bow, and impact sounds

---

## Quick Start

1. **Import Assets**: Add Erica Archer (Humanoid, 39 animations) and Free Medieval Weapons to Assets
2. **Setup Animator**: Create blend trees (Walk/Run/Aim Move) with parameters (forward, strafe, sprint, aim, pullString, fire)
3. **Add Scripts**: Attach Movement.cs, InputSystem.cs, CameraController.cs, Bow.cs, Arrow.cs
4. **Configure Bow**: Attach wooden bow to LeftHand, arrow to RightHand, setup string deformation
5. **Test Movement**: Verify WASD locomotion, Shift sprint, Right-click aim zoom
6. **Enable Audio**: Add footstep events to walk/run animations, bow/arrow sounds to animations
7. **Adjust Ammo**: Set Arrow Count = 10, test fire and ammo decrement
8. **Play & Iterate**: Test aim direction, camera collision, head rotation (IK), crosshair positioning

---

## Step-by-Step Implementation

---
---

## Phase 1: Project Foundation Setup

---

### Step 1.1: Import Character Assets

* Create a 3D project in Unity Hub
* Download **Erica Archer** from [Mixamo](https://www.mixamo.com/#/)
* Under `Characters` tab, search `Erika Archer` then select the one without bow
* Then under `Animations` tab, search for `Pro Longbow Pack`
* Download and rename folder `Longbow`, it should have one archer and 39 animation 
* Create folder structure:

```plaintext
Assets
├── Assets
│   └── Longbow
│       ├── Animator
│       ├── Materials
│       ├── Textures
│       └── (erika_archer.fbx and 39 animation file)
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

* For each animation FBX in `Assets/Assets/Longbow`:
  * Shift-select all animation files
  * Rig Tab → Set **Animation Type** to `Humanoid`
  * Set **Avatar Definition** to `Copy From Other Avatar` → select `erika_archerAvatar`
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
* Root Transform Position (Y) → Enable **Bake Into Pose**, set **Based Upon** to `Feet`
* Click **Apply**

**Walk (Front/Back/Left/Right)**

* Select each `standing walk` animation → rename to `Walk Front/Back/Left/Right`
* Enable **Loop Time** and **Loop Pose**
* Root Transform Rotation → Enable **Bake Into Pose**, set to `Original`
* Root Transform Position (Y) → Enable **Bake Into Pose**, set to `Feet`
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

* Double click `Walk`, select the **Blend Tree** → Set **Blend Type** to `2D Simple Directional`
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

* Select `Player` → Drag `Character.cs` onto it (auto-adds Character Controller)
* Adjust **Center**, **Radius**, **Height** so capsule surrounds character

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

* Create empty → `CameraHolder` → Reset position to (0,0,0)
* Create empty under it → `Center` → Position at character's hip level
* Drag `Main Camera` under `Center`

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

* Add [**Free medieval weapons**](https://assetstore.unity.com/packages/3d/props/weapons/free-pack-of-medieval-weapons-136607) to `Assets/Assets`
* Verify folder structure is correct

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

* Select `Canvas` → `Render Mode` → `World Space` → Position (0,0,0)
* Set **Width** = 10, **Height** = 1
* Select `Image` → `Rect Transform` → `Stretch / Stretch`
⚠️ Don't change Image position/scale

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

## Phase 5: Arrow Logic and Equipment Systems


---

### Step 5.1: Arrow Core Logic

* Go to `Assets/Scripts/Weapon` and create script `Arrow.cs`
  * Copy its content from
    `Assets/Scripts/Weapon/Arrow/1 Arrow Logic`

* Replace scripts:

  * `Bow.cs` → `Assets/Scripts/Weapon/Bow/3 Arrow Logic`
  * `InputSystem.cs` → `Assets/Scripts/Character/InputSystem/7 Arrow Logic`

* Go to `Assets/Scripts/Free medieval weapon/Prefabs`

  * Drag `Arrow` into `Hierarchy`
  * Adjust **rotation only** so arrow faces forward of archer
    *(Do not change position or scale)*

---

### Step 5.2: Arrow Prefab & Physics

* In `Hierarchy`

  * Create `Empty GameObject` → name it `Arrow`
  * Drag rotated `Arrow` (mesh) into this object

* Reposition `Arrow` (parent) to make it visible

* Adjust `Arrow` (child):

  * Rotate `X = 90`

* Select `Arrow` (parent, from Hierarchy)

  * Add `Rigidbody`

    * Disable `Use Gravity`
    * Disable `Is Kinematic`
    * `Interpolate` → `None`
    * `Collision Detection` → `Continuous Dynamic`
  * Add `Box Collider`

    * Use `Edit Collider` to fit arrow shape

* Drag `Arrow` (parent) to `Assets/Prefabs`

* Delete `Arrow` from `Hierarchy`

* In `Assets/Prefabs`, select `Arrow` and add `Arrow.cs` (Script)

* Go to `Wooden Bow` (`Player → LeftHand`)

  * In `Bow` (Script) drag `Arrow` prefab

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%205,%20STEP%202.png)

* **Play & Adjust**

  * `Assets/Prefabs`

    * `Arrow` → `Box Collider`
    * `CrossHair` → `Scale`
  * `Animator → UpperBody`

    * `Draw Arrow` → `EnableArrow`, `Pull`
    * `Fire Arrow` → `Release`, `DisableArrow`
  * `Wooden Bow` (`Player → RightHand`)

    * Adjust `Arrow Force`

---

### Step 5.3: Head Rotation & Gravity

* Replace script:

  * `InputSystem.cs` →
    `Assets/Scripts/Character/InputSystem/8 Head Rotation and Gravity Simulation`

* Go to `Animator`

  * Click ⚙️ on `UpperBody`
  * Enable `IK Pass`

* Play and verify head rotation

  * If head rotation off:

    * `Player → Input System`
    * Adjust `Look At Point`

* **Gravity setup** (move character to ground)

  * `Player → Character Controller`
  * Adjust `Center (Y)`

---

### Step 5.4: Bow Equip & Unequip

* Replace script:

  * `InputSystem.cs` →
    `Assets/Scripts/Character/InputSystem/9 Equip and Unequip Bow`

* Go to `LeftHand`

  * Create `Empty GameObject` → `BowEquipPos`
  * Enable `Gizmo`
  * Copy `Wooden Bow` Transform → Paste into `BowEquipPos`

* Move `Wooden Bow` to `Spine`

  * Reset Transform
  * Position it like bow carried on back

* Go to `Spine`

  * Create `Empty GameObject` → `BowUnEquipPos`
  * Enable `Gizmo`
  * Copy `Wooden Bow` Transform → Paste into `BowUnEquipPos`

* Select `Wooden Bow`

  * In `Bow` (Script):

**Bow Equip & UnEquip Settings**

* `Equip Pos` → `BowEquipPos` (Player → LeftHand)
* `Un Equip Pos` → `BowUnEquipPos` (Player → Spine)
* `Un Equip Parent` → `Spine` (Player → Hips)
* `Equip Parent` → `LeftHand` (Player → LeftForeArm)

![Animator Parameters and Blend Trees Setup](./Images%20of%20Setting/PHASE%205,%20STEP%204.png)

---

### Step 5.5: Footstep Sounds

* Drag `Sounds` folder into `Assets` (or use your own)

* In `Assets/Scripts`

  * Create folder `Sounds`
  * Copy `FootStepSound.cs` script
  * Add it to `Player`

* Under `Player`

  * Create `Empty GameObject` → `FootAudio`
  * Add `Audio Source`

    * Disable `Play On Awake`
    * `Spatial Blend` → `1`
    * `Volume` → `~0.3`

* Select `Player`, in `FootStepSound` (Script)

  * `Player Foot Audio` → `FootAudio`
  * `Foot Clip` → any sound from `Assets/Sounds/Footsteps`

* Go to `Animator`

  * `Base Layer` → `Walk` → `Walk Forward`
  * Add Animation Event → `PlayFootSound`
  * Repeat for:

    * Walk
    * Run
    * Aim Move

* Play and adjust volume

---

### Step 5.6: Arrow & Bow Sounds

* Replace script:

  * `Arrow.cs` → `Assets/Scripts/Weapon/Arrow/2 Arrow Sound`

* In `Assets/Prefabs`, select `Arrow` and add `Audio Source`

  * Disable `Play On Awake`
  * `Spatial Blend` → `1`
  * `Volume` → `~0.5`
  * `Audio Clip` → from `Assets/Sounds/Impact Sfx`

* Play and confirm arrow hit sound

* Replace scripts:

  * `Bow.cs` → `Assets/Scripts/Weapon/Bow/4 Bow Sound`
  * `InputSystem.cs` → `Assets/Scripts/Character/InputSystem/10 Bow and Arrow Sound`

* Go to `Wooden Bow` (`Player → Spine`)

  * Add `Audio Source`

    * Disable `Play On Awake`
    * `Spatial Blend` → `1`
    * `Volume` → `~0.5`

* In `Bow` (Script) of `Wooden Bow`, drag these from `Assets/Sounds/Bow & Arrow`

  * `Pull String Audio` → `Bow String Pull`
  * `Release String Arrow` → `Release String`
  * `Draw Arrow Audio` → `Pick Arrow`

* Go to `Animator → UpperBody → Arrow Logic → Pull String`

  * Add Event → `PlayPullSound`

* Play and confirm sounds

---

### Step 5.7: Ammo Check

* Replace scripts:

  * `Bow.cs` → `Assets/Scripts/Weapon/Bow/5 Ammo Check`
  * `InputSystem.cs` → `Assets/Scripts/Character/InputSystem/11 Ammo Check`

* Play and confirm:

  * Ammo decrement
  * No fire when ammo is zero
  * All animations and sounds synced

✅ **Bow & Arrow System Fully Functional**
[**Watch Demo**](Arrowline%201.mp4)

## Animation State Machine

**Base Layer States** (Lower body locomotion)
| State | Type | Parameters |
|-------|------|-----------|
| **Idle** | Default state | Blend (0,0) in Walk tree |
| **Walk** | 2D Blend Tree | forward/strafe (-1 to 1) |
| **Run** | 2D Blend Tree | forward/strafe (-1 to 1), sprint=true |
| **Aim Move** | 2D Blend Tree | forward/strafe (-1 to 1), aim=true |

**Base Layer Transitions**
- Walk ↔ Run: `sprint == true/false` (no exit time)
- Walk ↔ Aim Move: `aim == true/false` (no exit time)
- Run ↔ Aim Move: `aim == true/false` (no exit time)

**Upper Body Layer** (Independent bow animation)
| State | Loop | Purpose |
|-------|------|---------|
| **Empty** | - | Default, no animation |
| **Draw Arrow** | No | Pulling arrow onto string |
| **Pull String** | No | Holding bowstring at full draw |
| **Fire Arrow** | No | Release and recoil animation |

**Arrow Logic Sub-State Machine**
- Empty → Draw Arrow: `aim == true`
- Draw Arrow → Pull String: `pullString == true`
- Pull String → Fire Arrow: `fire == true` (trigger)
- Fire Arrow → Draw Arrow: (exit time, loops if aim continues)
- Any State → Empty: `aim == false`

**Animator Parameters** (Global)
- `float forward` - Movement forward/back (-1 to 1)
- `float strafe` - Movement left/right (-1 to 1)
- `bool sprint` - Activate Run state (Shift key)
- `bool aim` - Enter aiming mode (Right-click)
- `bool pullString` - Activate full draw (Left hold)
- `trigger fire` - Release arrow (Left release)

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
- Height: Full arrow length excluding tip
- Is Trigger: Disabled (physical collision)

**Layer Setup**
Create layers for proper collision:
- Player (character)
- Weapon (bow/arrows)
- Enemy (targets)
- Environment (surfaces)

Configure Layer Collision Matrix in Project Settings → Physics.

## Best Practices

**Animator Configuration**
- Keep parameter names consistent (`forward`, `strafe`, `sprint`, `aim`, `pullString`, `fire`)
- Use separate layers for upper/lower body (UpperBody mask disables lower body)
- Create sub-state machines for complex logic (Arrow Logic state machine)
- Disable **Loop Time** for non-repeating animations (Draw Arrow, Fire Arrow)
- Enable **Loop Time** for repeating animations (Idle, Walk, Run, Aim Move)
- Use **Bake Into Pose** on Root Transform for animations that move character

**Script Organization**
- Modular structure: Movement.cs (locomotion), InputSystem.cs (controls), Bow.cs (mechanics), Arrow.cs (physics)
- Cache component references in Start() (GetComponent calls expensive)
- Use public fields for inspector adjustments (Arrow Count, Arrow Force, String positions)
- Comment animation event triggers (EnableArrow, Pull, Release, DisableArrow)

**Bow Mechanics**
- Test bow without animations first, then integrate
- Verify string initial position matches `WB.String` (no stretching on start)
- Adjust Arrow Force value for desired firing power
- Enable Gizmos on `StringHandPullPos` to visualize pull distance
- Match `WB.main` transforms for string parent hierarchy

**Audio Implementation**
- Use Animation Events to trigger sounds at correct frame (prevent sound overlap)
- Add `PlayFootSound` events to Walk/Run/Aim Move animations (one per cycle)
- Set Spatial Blend = 1 on arrow/bow audio (3D positional sound)
- Adjust Volume ~0.3 for footsteps, ~0.5 for bow/arrow (prevent clipping)

**Camera Setup**
- Adjust Camera zoom values if too aggressive on aim (Zoom Field of View, Zoom Speed)
- Position Main Camera slightly left to avoid clipping head
- Apply same camera position to CamPosition for consistency
- Use UI Camera layer separation (main renders everything, UI renders only UI layer)

**Debugging Tips**
- Enable `Test Aim` in InputSystem to verify spine/head rotation
- Use Gizmos to visualize string positions and arrow spawns
- Check animation parameter spelling in transitions (case-sensitive)
- Verify audio clips are assigned (not empty) before playing
- Test ammo system: fire arrow, check count decrements, verify fire disabled at zero

## Troubleshooting

**Movement Not Working**
- Verify InputSystem.cs is attached to Player
- Check Input Manager has `Sprint` axis configured (Shift key)
- Ensure Movement.cs has Character Controller attached to Player
- Test with WASD keys in Play mode
- Disable `sprint` parameter in Animator if stuck in Run state

**Animations Not Playing**
- Verify Animator component assigned to Player with PlayerAnim controller
- Check Animator parameters match exactly: `forward`, `strafe`, `sprint`, `aim`, `pullString`, `fire`
- Ensure transitions have correct conditions and **Has Exit Time** disabled
- Verify animation clips assigned in blend trees (not empty)
- Check UpperBody layer has correct Avatar Mask (Lower Body disabled)

**Bow Not Firing**
- Verify Arrow prefab assigned in Bow (Script) component
- Check `fire` parameter is trigger type in Animator
- Ensure Fire Arrow animation event calls `Release` (exact spelling)
- Verify arrow has Rigidbody with **Collision Detection: Continuous Dynamic**
- Test with simpler arrow shape first (cube) before complex mesh

**Arrow Firing But No Damage/Sound**
- Check Arrow.cs script attached to Arrow prefab
- Verify Audio Source added to Arrow prefab with impact sound assigned
- Adjust Audio Source Volume if sound too quiet (~0.5)
- Ensure impact animation event `DisableArrow` fires (removes arrow from scene)
- Check arrow lifetime isn't immediately destroying on spawn

**Camera Issues**
- **Clipping into character**: Enable camera collision (CamPosition setup in Step 2.7)
- **Zoom too aggressive**: Reduce `Zoom Field of View` and `Zoom Speed` in CameraHolder
- **Camera rotates wrong**: Verify Main Camera position is under CameraHolder/Center
- **UI overlapping game**: Set Main Camera `Culling Mask` to exclude UI layer
- **No crosshair visible**: Check Canvas Render Mode is World Space, position near camera

**Aiming Direction Wrong**
- Verify Spine assigned in InputSystem (Player/erika_archer/Hips/Spine)
- Enable `Test Aim` checkbox and adjust `Spine Offset` during Play mode
- Check arrow spawn position (Player/RightHand/Arrow position)
- Verify IK Pass enabled on UpperBody layer in Animator
- Test with Debug.DrawRay visualization if available

**Ammo Not Decreasing**
- Verify Arrow Count set to 10 (or desired value) in Bow (Script)
- Check Bow.cs version is ammo check version (#5)
- Ensure fire event triggers DisableArrow (removes arrow, decrements count)
- Test ammo display if UI text reference assigned

**Audio Not Playing**
- Verify Audio Source components added to Arrow prefab and Wooden Bow
- Check Spatial Blend = 1 (3D positional sound)
- Ensure Volume not at 0 (~0.3 for footsteps, ~0.5 for bow/arrow)
- Verify animation events match exact function names: `PlayFootSound`, `PlayPullString`
- Check AudioListener exists in scene (usually on Main Camera)

**Character Falls Through Ground**
- Verify Plane has Collider (no Rigidbody needed, static)
- Check Player Character Controller height/radius fits on ground
- Ensure ground plane is positioned at Y=0 or adjust character spawn height
- Test with larger ground plane if character sliding off edges

**Head Doesn't Rotate During Aim**
- Verify IK Pass enabled on UpperBody layer (⚙️ icon on layer)
- Check Look At Point assigned in InputSystem
- Test by enabling Test Aim checkbox, adjust Look At Point X/Y/Z
- If rotated 180°, adjust spine offset or Look At Point position

## Important Notes

**Required Setup**
- ⚠️ Character MUST use **Humanoid rig** (not Generic) for bone attachment
- ⚠️ All animation FBX files must use **same Avatar** (Copy From Other Avatar)
- ⚠️ Do NOT rename Animator parameters after setup (will break all transitions)
- ⚠️ Arrow prefab MUST have **Rigidbody** for physics simulation and collision detection

**Critical Folder Structure**
- `Assets/Assets/Longbow/` - Character model and 39 animations
- `Assets/Assets/Free medieval weapons/` - Bow model and weapon prefabs
- `Assets/Scripts/Character/` - InputSystem.cs, Movement.cs
- `Assets/Scripts/Camera/` - CameraController.cs
- `Assets/Scripts/Weapon/` - Bow.cs, Arrow.cs
- `Assets/Prefabs/` - Arrow, CrossHair prefabs
- `Assets/UI/` - arrow-crosshair image
- `Assets/Sounds/` - Footsteps, Bow & Arrow, Impact Sfx folders

**Animator Parameter Rules**
- `forward` and `strafe` are **float** parameters (-1 to 1)
- `sprint` and `aim` are **bool** parameters
- `pullString` is **bool** parameter
- `fire` is a **trigger** (not bool, not float)
- Changing parameter names will break all transitions - do not rename

**Animation Event Triggers**
- `EnableArrow` - called on Draw Arrow at frame arrow appears
- `Pull` - called on Draw Arrow when string starts pulling
- `Release` - called on Fire Arrow when arrow launches
- `DisableArrow` - called on Fire Arrow to remove arrow and decrement ammo
- Use EXACT spelling (case-sensitive)

**Physics and Collision**
- Arrow: **Use Gravity enabled**, **Collision Detection Continuous Dynamic**
- Ground/Walls: Colliders but NO Rigidbody (static)
- Player: **Character Controller** for movement (NOT Rigidbody)
- Camera: Raycast-based collision avoidance (not physics-based)

**Audio Requirements**
- WAV or MP3 format (Unity auto-imports)
- Footstep: ~0.3 volume, Spatial Blend = 1, 3D positional
- Bow draw/release: ~0.5 volume, Spatial Blend = 1, 3D positional
- Arrow impact: ~0.5 volume, Spatial Blend = 1, trigger on collision
- Ensure Audio Listener present (usually on Main Camera)

**Testing Checklist**
- ✅ WASD movement works, Shift activates sprint (Run animation)
- ✅ Right-click enters aim mode (camera zooms, crosshair appears)
- ✅ Mouse hold activates draw (Pull String animation)
- ✅ Mouse release fires arrow (Fire Arrow animation, arrow spawns)
- ✅ Ammo decrements on fire, fire disabled at zero ammo
- ✅ Footstep sounds play on movement
- ✅ Bow draw/release sounds play on draw/fire
- ✅ Arrow impact sound plays on collision
- ✅ Camera collision prevents clipping into character
- ✅ Head rotates toward aim target (IK enabled)
- ✅ Crosshair moves with camera during aim

**Common Mistakes to Avoid**
- ❌ Using Generic rig instead of Humanoid (bones won't attach)
- ❌ Different avatars for animations (inconsistent skeleton)
- ❌ Renaming animator parameters (breaks all transitions)
- ❌ Missing animation events (bow won't draw/fire properly)
- ❌ Arrow without Rigidbody (won't fire or collide)
- ❌ Forgot to add Audio Source to arrow/bow (no sounds)
- ❌ Crosshair in screen space instead of world space (wrong position)
- ❌ Camera collision layer not set to Default (clipping into character)
- ❌ Arrow Force = 0 (arrow doesn't launch)
- ❌ Arrow Count = 0 (can't fire)


## Notes

* Test frequently in Play Mode
* Do not rename Animator parameters
* Use Humanoid rig only
* Modular design allows easy extension