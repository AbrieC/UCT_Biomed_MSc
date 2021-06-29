JuxL_Combo Guide

JuxL_Combo is a markerless tracking system which combines the Microsoft HoloLens with Leap Motion’s hand-tracking sensor, the Leap Motion Controller (LMC). 

Markup :
* The Leap Motion Core Assets 4.4.0 SDK for Unity enable the porting of the processed pose data to the JuxL_Combo Unity built application running on the PC
  * To process the pose data of the 3D printed hand the LMC needs to be connected to a separate PC via Universal Serial Bus (USB) configured with the Leap Motion Orion SDK. 
  * Although the HoloLens Gen 1 has a USB mini port it does not support external peripherals. 
  * Consequently, a PC needs to be configured with the Orion SDK for Windows OS.
* The Holographic Remoting Player (HRP) application enabled the streaming of the real environment footage and pose data from the HoloLens to the JuxL_Combo Unity application.
* A 3D printed hand was used as the real-world hand to be tracked via the LMC. 
* Video of project = https://www.youtube.com/watch?v=hb1170OhSA8

Notable Leap Motion Core prefabs used in combination with the MRTK from Jux3Dmodel:
Markup: 
* LeapHandController --> Queries the Leap Motion service for tracking data and uses it to place hands in the scene. The tracking data from the service is transformed relative to the prefab’s position and orientation in the scene. The scripts in the controller manage the hand objects that represent the physical hands detected by the Leap Motion device.
* RigidRoundHand	--> Includes a rigid body and collider composition of for the arm, palm and all of the digits so to animate the graphic visualization
* Capsule Hand	--> Dynamic graphic visualization to be combined with RigidroundHand
