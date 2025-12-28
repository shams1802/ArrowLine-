PHASE 1


STEP 1 
Download Erica Archer from https://www.mixamo.com/#/ or use provided ‘Longbow’ 
Make its Structure as
```plaintext
Assets
└── Assets
  	└── Longbow
  	    	├── Animator
  	    	├── Materials
  		├── Textures
  		└── (erika_archer.fbx and 39 other fbx)
Scripts(to be added)
UI(to be added)
```

Drag erika_archer from Assets/Assets/Longbow into Hierarchy
Select erika_archer from Assets/Assets/Longbow, in inspector tab, 
- Under Rig Tab - select Animation Type as Humanoid and select Avatar Defination as Create From This Model , then click Apply.
- Under Materials Tab - Click Extract Textures and select folder Assets/Assets/Longbow/Textures -> a NormalMap settings will pop up, click Fix now and Click Extract Materials and select folder Assets/Assets/Longbow/Materials

- Select every animation slot under Assets/Assets/Longbow Under Rig Tab - select Animation Type as Humanoid and select Avatar Defination as Copy From Other Avatar , then select erika_archerAvatar and click Apply.


STEP 2
In Hierarchy view, right click then select Create Empty name it ENV
Select ENV right click then select 3D Object, click Plane and adjust position and scaling 
Select ENV right click again then select 3D Object, click Cube and adjust position and scaling to make wall make 4 of it.

STEP 3
In Hierarchy view, right click then select Create Empty name it Player, in Inspector tab, under Transform Component in 3 dot click reset
Then drop erika_archer









Hierarchy should look like
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


STEP 4
In Assets/Assets/Longbow/Animator , right click , select Create then select Animator Controller name it PlayerAnim
In Player, in Inspector click add component Animator, 
-> Drag PlayerAnim to Controller slot
-> Click on circle of Avatar, select erika_archerAvatar



STEP 5
Select Window -> Animation -> Animator
In Assets/Assets/Longbow, select standing idle 01, rename from mixamo.com to Idle,
i) tick Loop Time, then tick Loop Pose 
ii) Under Root Transformation Position (Y), tick Bake Into Pose -> in Based upon select Feet 
Click Apply

Select standing walk back/front/left/right, rename from mixamo.com to Walk Back/Front/Left/Right 
i) tick Loop Time, then tick Loop Pose 
ii) Under Root Rotation, tick Bake Into Pose -> in Based upon select Original
iii) Under Root Transformation Position (Y), tick Bake Into Pose -> in Based upon select Feet 
Click Apply

Select standing run back/front/left/right, rename from mixamo.com to Run Back/Front/Left/Right 
i) tick Loop Time, then tick Loop Pose 
ii) Under Root Rotation, tick Bake Into Pose -> in Based upon select Original
iii) Under Root Transformation Position (Y), tick Bake Into Pose -> in Based upon select Feet 
Click Apply

STEP 6
In Animator right click in Base Layer area and select Create State then select From New Blend Tree name it Walk, do it again and name it Run
Select Parameter tab, create 2 float forward strafe and a bool sprint(set false)

Double click Walk, select Blend Tree, in inspector select Blend Type to 2D Simple Directional, select Parameters strafe then forward
Under Motion tab, Click On + then Add Motion Field, repeat it 4 more time
Set it like this 
Idle (0,0)
Walk Forward (0,1)
Walk Back (0,-1)
Walk Left (-1,0)
Walk Right (1,0)

Move to Base Layer and repeat for Run

STEP 7
Right click on Walk, Select Make Transition, select that line(Walk to Run),under Inspector
Disable Has Exit Time, Under Conditions, click + select sprint then true

Do same for Run to Walk when sprint is False

Check if all the all the animation are working by using Animator tab

Dont name anything differently, especially sprint, forward, strafe






PHASE 2 Character Movement and Camera Control


STEP 1
Under Assets/Scripts, add folders Camera and Character
Inside Character, add C# script InputSystem.cs and Movement.cs
Copy contents of Movement.cs from provided Assets/Scripts/Movement.cs



```plaintext
Assets
└── Assets
  	└── Longbow
  	    	├── Animator
  	    	├── Materials
  		├── Textures
  		└── (erika_archer.fbx and 39 other fbx)
Scripts
├── Camera
└── Character (InputSystem.cs and Movement.cs)
UI(to be added)
```

STEP 2
Select Player(in Hierarchy), in Inspector Drag and drop Charater.cs Script, A Character Controller Component will be added and a green Capsule will cover the model, Change Centre, Radius and Height to Cover the model

STEP 3
Copy contents of InputSystem.cs from provided Assets/Scripts/InputSystem/1 just player input/InputSystem.cs
Select Player(in Hierarchy), in Inspector Drag and drop InputSystem.cs Script
Go to Edit -> Project Settings -> Input Manager -> Axes, increase Size by 1, edit that Axes
Name Sprint, Position Button ‘left shift’, Alt Negative Button ‘right shift’

Now Fix Main Camera Positioning and drop it inside Player(just for now) and hit play to check input control system,if working place the camera original place, else fix what errors come

STEP 4
Create an empty Game Object, name it CameraHolder and reset its position to 0,0,0
Right click on Camera Holder and Create an empty Game Object, name it Center and place it around hip of model
Drag and drop Main Camera to Center and adjust its position as pleased


Hierarchy should look like
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
	└── CamPosition (to be added)
```




STEP 5
Inside Assets/Scripts/Camera, add C# script CameraController.cs
Copy contents of CameraController.cs from provided Assets/Scripts/Camera/1 just camera and player/CameraController.cs
Add this Script to Camera Holder

STEP 6
Select Player, in inspector Tag Player
Play and confirm, a problem of collision is still there

STEP 7 Collision fix
Replace contents of CameraController.cs from provided Assets/Scripts/Camera/1 collision/CameraController.cs

Right Click the CameraHolder/Centre and select Create Empty, name it CamPosition 
Under Inspector tool of Main Camera, Select 3 dots then Copy Component
Under Inspector tool of CamPosition, Select 3 dots then Paste Component Value

Under Inspector tool of Main Camera, Camera component change Clipping Plane Value as needed

Play now Collision is removed







