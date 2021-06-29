# JuxFiducial Guide
The application makes use of Unity 2017.4.2f2 + HoloLens MRTK 2017.4.2 to test accuracy of the HoloLens to hold the virtual object in 3D space while moving through 90degrees or more.

Below is the setup and building guide for the Jux3DModel Application.

# Note:
To follow the building guide below basic understanding or working knowledge for Unity, MRTK, Vuforia and Visual studio is required.  
If not please follow the guide developed by Microsoft Academy (https://docs.microsoft.com/en-us/windows/mixed-reality/tutorials) and MRTK (https://github.com/Microsoft/MixedRealityToolkit-Unity) to ensure all necessary applications have been installed on the machine.

# 1. Setting up the project space #
Launch Unity Hub and create new Unity project, build 2017.4.2f2 Long Term Support (LTS).  (https://unity3d.com/unity/whatsnew/unity-2017.4.2)

Import HoloToolkit-Unity-2017.4.2.0.unitypackage into the Assest folder
(https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/tag/2017.4.2.0)

* Go to Mixed reality toolokit > Configure > Apply Mixed Reality Project Setting
* Go to Mixed reality toolokit > Configure > Apply Mixed Reality Scene Settings
 
--> Do not add Spatial Mapping Prefab. 

* Go to Mixed reality toolokit > Configure > Apply UWP capabilities setting 
> Select
InternetClient
•	Microphone
•	Webcam
•	SpatialPerception
•	Internet Client 
 
* Go to Edit > Project Settings > Quality and set UWP default quality to Ultra
 
* Go to Edit > Project Settings > Player
- Under Publishing settings ensure the following capabilities have been selected:
•	InternetClient
•	WebCam
•	SpatialPerception 

# 2. Setting up the scene #
* Go to Assets > Create new folder > Scenes 
* Go to File > Save Scene as > Select Scenes folder  Save as JuxFiducial

# 3. Adding Vuforia 7.0.50 #
## 3.1 Setting up Vuforia project space ## 
A Vuforia account is required - go to https://developer.vuforia.com/ and create a profile
In Unity Go to Asset store > search for “Vuforia Core Samples” > Import package
The Project space should look as below. 
 
* Go to Edit > Project Settings > Player  Under XR settings select the options for
Virtual Reality Supported  Windows Mixed reality
Vuforia Augmented reality 

* In scene hierarchy, Go to MixedRealityCamereParent > MixedRealityCamera > Inspector Tab:
Under Camera > Set clear flags to Solid Color; Background Black.
Under Mixed Reality Camera Manager > 
Opaque Display Settings > Set clear flags to Solid Color; Background Black;
Transparent display Seting > Set clear flags to Solid Color; Background Black;
Add Vuforia Default Initializayion Error Handler Script as Component
Add Vuforia Behaviour component > Set MixedRealityCamera as World Center Mode by selecting camera.

* If the “Vuforia Augmented Reality Supported” option was correctly selected in XR settings the “Open Vuforia Configurations” button should be enabled. Click on the Button. 
 
This will redirect the Inspector screen to VuforiaCinfuguration. Click on Add License > This redirects to Vuforia Developer Dashboard in Web Browser. Or Go to the Vuforia dashboard  Go to “Develop” tab (https://developer.vuforia.com/vui/develop/licenses) 

 * Select “Get Development Key” >
 --> Type Unity Application name in License Name field, select the check box and click on confirm. You should see the screen below:

 - Click on Filename:
  - Copy License Key and paste in App Licesnse Key text box in Unity VuforiaConfiguration Inspector panel.

* Under Digital Eyewear 
> Change Device Type to Digital Eyewear
> Device Config to HoloLens

##  3.2 Using your own assets ##
Fiducial markers (target images) were created using an open source online marker tool (https://shawnlehner.github.io/ARMaker/). The markers were edited using Adobe Illustrator to create 50x50mm and a 100x100m version. 
 
*The target images need to be added to the Vuforia Library with the online dashboard.
--> Click on the “Target Manager” tab and click on “Add database”. Add appropriate Database_name > JuxFiducial_Images > Click Create.

The database should have been created, next click database name and on “Add Target”. 
 
* Select “Single Image” > Choose file path > specify width. 
With Vuforia, the unit scale is meters, ie. The value 1 = 1m. For the 50x50mm a value of 0.05 needs to be entered > Click “Add”  
--> It is important to note the rating quality of the target image, as this defines how well the Vuforia engine will be able to track the target image.

* Select the target image and  click on “Download Database”. This downloads the 
required assest package to be imported in Unity. 

* Adding Target Image and 3D Model to Unity
In Unity > Import Vuforia asset database > Go to Assests > Import package > Custom package > Select database > Import all.
The filename is changed with Import ie. option_one is option_one_scaled > this needs to be rectified. It is important to change and edit fle locations using Unity, rather than  in the corresponding file path folder as a tracking of changes file is created by Unity.  

## Next:
Go to MixedRealityCameraParent > MixedRealityCamera > Open Vuforia configutation
In VuforiaConfiguration > Databases >  Click on “load” and “activate” next to appropriate file names.
In Hierarchy Tab, create empty game object (VuforiaSceneContent). 
Add the target image by right clicking on game object > Vuforia > Image 
	In Inspector Tab > Image Target Behavior > Set 
o	Database to downloaded database (JuxFiducial_Images)
o	Image target to corresponding image file (option_one)
	In advance, enable Etended Tracking.
(Extended Tracking is the concept that a target's pose information will be available even when the Target is no longer in the field of view of the camera or cannot directly be tracked for other reasons. Extended Tracking utilizes the Device Tracker to improve tracking performance and sustain tracking even when the target is no longer in view.)

* Import 3D volumes to assets for JuxFiducial to Models folder under Assets in Project Tab. The scale of FocusPoint needs to be changed.
Use a 3D volume game object of 0.05x0.05 to ascertain scale required for import of inventor obj file Focuspoint, scale factor was 0.02. In Unity unit scale is meters, ie. The value 1 = 1m. 


* Add 3D Volume as child to Image Target and align centres to required real world coordinates and assign new material colour. Test by clicking on play button, the view from your Webcam should be shown in Game tab. Hold Image target in front of your webcam, the 3D object should appear. 
 
> Note, this is the reason why Holographic remoting can’t be used with Vuforia. Vuforia takes control of the video module, and needs to be dsabled to allow for Holographic remoting.

# 4. Exporting application to HoloLens #
Go to File > Build settings > 
Ensure platform is Universal Windows platform
Set 
•	Target Build to HoloLens
•	Build type to D3D
•	SDK to 10.0.17134  (Windows SDK 10.0.17134 is required for 2017.2+)
•	Visual Studio Version to Visuak Studio 2017 or Latest installed
•	Build and Run on Local Machine
•	Select Unity C# Projects
•	Select Development Build
 
 
* Click in Build and create new App folder as destination > Select Folder > This will initiate building of application
 
* In App File Directory > open Visual studio project file (Juxfiducial.sln)
Build the executable from Visual Studio.
In Visual Studio, use the toolbar, change:
The target from Debug to Release 
From ARM to X86 
Set Device to  Remote Machine – use manual IP or auto detect

* Go to Debug > Start Without debugging  Application should deploy to the HoloLens
* Open Application in HoloLens.
 
