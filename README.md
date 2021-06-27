#MSc BME Repo #

The repo contains the Unity packages that enabled my MSc project. 

Dissertation  link: https://open.uct.ac.za/handle/11427/32211

# Abstract of the project # 
Computer-mediated reality technologies have the potential to improve the image-guided surgery (IGS) workflow; specifically, pre-surgical planning, intra-operative guidance, post-surgical assessment, and rehabilitation. Augmented reality (AR), a form of computer-mediated reality, uses an electronic display or projection module to add a hologram in the user’s field of view (FOV). For intra-operative guidance, AR could aid in reducing the cognitive overload experienced by clinicians due to integrating multi-modal imaging data from several sources while performing the intervention on the patient.

Three AR HMD systems were developed to explore the capabilities of the Microsoft HoloLens as an AR HMD to be used in developing an AR HMD medical system. The three AR HMD systems required different software and hardware system architectures, however, each of the AR HMD system’s software applications were developed in Unity combined with the MixedRealityToolkit (MRTK). Each of the AR HMD systems implemented different registration techniques to localize the virtual object in the real-world coordinate system. The registration techniques were user calibration alignment to identified anatomical landmarks, fiducial marker tracking, and markerless tracking.

For user calibration with anatomical landmarks, MRTK was manipulated to allow alignment of the virtual object. 
For fiducial registration, the Vuforia Software Development Kit (SDK) was added to assess the alignment and spatial anchoring of the virtual object as specified. 
Finally, the Leap Motion Controller (LMC) and Leap’s Orion SDK was used for exploring markerless tracking.

The AR HMD systems developed enabled performance assessments, and alignment errors were identified during trials of the three systems. 

Most notably the location drift of the 3D virtual object in the spatial space due to the clinician moving around the registered location. 

This project entailed preliminary development towards the AR HMD medical system to create an in-vivo view of 3D patient-specific bone geometries as a hologram in the clinician’s FOV.
