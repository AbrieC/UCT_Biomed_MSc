# Jux3DModel Guide
The application makes use of Unity 2017.4.2f2 + HoloLens MRTK 2017.4.2 to test accuracy of the HoloLens to hold the virtual object in 3D space while moving through 90degrees or more.

Below is the setup and building guide for the Jux3DModel Application.

# Note:
To follow the building guide below basic understanding or working knowledge for Unity, MRTK, and Visual studio is required.  
If not please follow the guide developed by Microsoft Academy (https://docs.microsoft.com/en-us/windows/mixed-reality/tutorials) and MRTK (https://github.com/Microsoft/MixedRealityToolkit-Unity) to ensure all necessary applications have been installed on the machine.

# 1. Setting up the project space #

1.	Create a new unity project, build 2017.4.2f2
Import the MixedRealityToolKit package (Assets -> Import Package -> Custom Package) Import HoloToolkit-Unity-2017.4.2.0.unitypackage 
(https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/tag/2017.4.2.0)
Make sure all assets are selected and click on import.

2.	Apply Mixed reality Project Settings: Go to Mixed reality toolkit > Configure > Appy Mixed Reality Project Settings.
3.	Apply Mixed Reality Scene Settings: Go to Mixed Reality Toolkit > Configure > Apply Mixed Reality Scene Settings.
4.	Apply Universal Windows Platform (UWP) Settings: Go to Mixed Reality Toolkit > Configure > Apply UWP Capability Settings > Select Spatial Perception. 
5.	Quality settings, go to Edit > Project Settings > Quality and set UWP default quality to High. 
6.	Enable depth buffer sharing --> To enable this feature in the Unity Project Open Player XR Settings (go to Edit > Project Settings > Player > XR Settings). Select the checkbox for Enable Depth Buffer Sharing under Virtual Reality SDKs > Windows Mixed Reality expansion (Virtual Reality Supported checkbox must be checked). Further, it is recommended to select 16-bit depth under the Depth Format setting in this panel, especially for Microsoft HoloLens Development. Selecting 16-bit compared to 24-bit will significantly reduce the bandwidth requirements as fewer data will need to be moved/processed.

# 2. Confirm project settings #
1.	Go to Edit > Project Settings > Player. 
Under XR settings > The options for Virtual Reality Supported should be selected
Edit > Project Settings > Player > Under publishing settings the following capabilities should be selected:
•	InternetClient
•	WebCam
•	SpatialPerception 

2.	Verify .NET Configuration – can also be IL2CPP (this depends on asset support and Unity build, for example, with Leap modules, IL2CPP is only supported on 2018.1+builds)
3.	Go to Edit > Project Settings > Player (you may still have this up from the previous step). In the Inspector Panel for Player Settings, select the Windows Store icon.
In the Other Settings Configuration section, make sure that Scripting Backend is set to .NET

# 3. Setting up the scene #
1.	Go to Assets > Create new folder > Scenes  Go to Save Scene > Select a scenes folder and save the scene

2.	Setup the main virtual camera
•	In the Hierarchy Panel, select the Main Camera.
•	In the Inspector set its transform position to 0,0,0.
•	In camera find the Clear Flags property and change the dropdown from Skybox to Solid colour.
•	Click on the Background field to open a colour picker > Set R, G, B, and A to 0. 
•	Set clipping to 0.1 for near; 10 for far.

3.	Create Spatial Manager
•	In the Hierarchy tab > Create a new GameObject Parent and rename it SpatialManager.
•	Drag the SpatialMapping prefab as a child into SpatialManager.
•	The SpatialMapping prefab is responsible for scanning the real-world scene and generating a mesh in which the virtual object can interact. As an example, with this prefab added, you can put the virtual object on a surface you’ve scanned. If the prefab is not in the Hierarchy tab, locate the prefab at HoloToolKit/SpatialMapping/Prefabs folder and drag the SpatialMapping prefab to the Hierarchy Tab. In the Inspector tab for Spatialmapping, uncheck the Draw Visual Meshes option in the Spatial Mapping Manager component.
•	Drag the InputManager Parent into SpatialManager
•	Create a new child game object and rename it WorldAnchor > Add World Anchor Manager (script) as a component.

# 4. Add the virtual objects to the scene #
1.	In the Hierarchy tab > create new GameObject and rename SceneContent
2.	In the project tab, create new Models folder under assets and add .obj files to folder from 3D Models root folder.
3.	Create a cube game object with the scale set as required.
4.	Use the FocusPoint and the cube game object to ascertain required scale value for imported 3D models Scale Factor in their inspector tabs, the value was 0.001 to move from Autodesk to Unity. 
5.	Add the CTboneG_LeftHand.obj to SceneContent as a child and reset the Transform in the inspector view. 
6.	Arrange all virtual objects in the scene appropriately. 
7.	Add scene content adjuster script to SceneContent > This aligns the VO at head height when the application is launched.

# 5. Allow for user interaction with Virtual Object #
1.	Add a Box Collider Component to each of the virtual object (VO) and edit the collider to match the VO.
2.	Add Twohand manipulation in inspector to each virtual obect
> Add BoundingBoxBasic to Bounding Box Prefab to allow for UI visual 

# 6. Deploy the Unity build to the Microsoft HoloLens #
1.	Set up the build settings for Visual Studio deploy Go to File > Build settings > 
•	Change Platform to Universal Windows Platform and click Switch Platform.
•	For Target device switch to HoloLens.
•	Set UWP Build Type should be D3D.
•	Set UWP SDK could be left at Latest installed. SDK should be latest installed but make sure to match the requirements stated on the GitHub MRTK Unity package page. For 2017.2+ Windows SDK 10.0.17134 is required.
•	Check Unity C# Projects under Debugging.
•	Click “Add Open Scenes” to add the scene and add the most recent scene.

2.	Click Build 
•	In the file explorer, click New Folder and name the folder "App".
•	With the App folder selected, click the Select Folder button.
•	When Unity is done building, a Windows File Explorer window will appear.

3.	Build the executable from Visual Studio.
•	Open the App folder in file explorer > In-App File Directory > open Visual Studio project file 
•	In Visual Studio, use the toolbar, change the target from Debug to Release and ARM to X86 
•	Set Device to Remote Machine – use manual IP or autodetect
•	Go to Debug > Start Without Debugging  Application should deploy to the HoloLens

4.	Open the application on Microsoft HoloLens if deploy succeeded.

