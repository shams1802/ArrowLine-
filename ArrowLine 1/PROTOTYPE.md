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

### Step 1.5: Animation Configuration

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
