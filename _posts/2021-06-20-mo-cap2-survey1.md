---
layout: post
title: A Survey of Computer Vision-Based Human Motion Capture (2001)
date: 2021-06-20 23:26:18 +0700
category: Motion Capture
---




[T. B. Moeslund and E. Granum, “A survey of computer vision-basedhuman motion capture, ”Computer  vision  and  image  understanding, vol. 81, no. 3, pp. 231–268, 2001.](https://doi.org/10.1006/cviu.2000.0897)

* A comprehensive survey of CV-based human motion capture literature from 1980 to 2000.
* Focus on a general overview based on a taxonomy of system functionalities.
* Four processes: Initialization, Tracking, Pose Estimation, and Recognition.


# __1. Introduction__
* Human motion capture: head, arms, torso, and legs.
* Definition of _motion capture_: The process of capturing the large scale body movements of a subject at some resolution.

## 1.1 Application Areas
* Three major application areas:
    * Surveillance: parking lot.
    * Control: games, virtual environments, animation, control of remotely located implements.
    * Analysis: diagnostics of orthopedic patients, improvement of performance of athletes.

## 1.2 Alternative Technologies for Motion Capture
* Two subsystems: _sensing_ and _processing_.
* Trade-off between active sensing and passive sensing:

|        Active Sensing        |           Passive Sensing          |
|------------------------------|------------------------------------|
| Place devices on the subject | Is based on “natural” signal sources  |
| Simpler processing           | Use computer vision for processing |
| Apps: analysis, control      | Apps: surveillance, control        |

* CV allows in principle for touchfree and more discrete “pure”
motion capture systems.

## 1.3 Content of This Paper
* Is only concerned with CV-based approaches, i.e. passive sensing
* Survey of publications in CV-based human motion capture from 1980 to 2000


# __2. Surveys and Taxonomies__ 
## 2.1 Previous Surveys
## 2.2 A Taxonomy Based on Functionalities
* Functional structure of a comprehensive motion capture system:

    $$ Initialization \rightarrow Tracking \rightarrow Pose\;Estimation \rightarrow Recognition $$

    - Initialization: An prropriate model of the subject is established.
    * Tracking: Segment the subject from the background and find correspondences between segments in consecutive frames.
    * Pose Estimation: The pose of the subject’s body often needs to be estimated as this may be the output of the system in a virtual environment, or may be processed further by the recognition process.
    * Recognition: Analyze the pose or other parameters to recognize the actions performed by the subject.

* The majority of the work in human motion capture is carried out within tracking and estimation.

## 2.3 Assumptions
* Two classes of typical assumptions:
    * Movement assumptions: Restrict the movements of the subject and/or the camera(s).
    * Appearance assumptions: Concern aspects of the environment and the subject. 
* Movement assumptions:
1. The subject remains inside the workspace
2. None or constant camera motion 
3. Only one person in the workspace at the time
4. The subject faces the camera at all time: Simplifies the calculation of the overall body pose.
5. Movements parallel to the camera-plane: Reduces the dimensionality from 3D to 2D
6. No occlusion: Simpilfies the task of tracking since the entire posture of the subject is visible in every frame
7. Slow and continuous movements
8. Only move one or a few limbs Subject
9. The motion pattern of the subject is known
10. Subject moves on a flat ground plane

mcmvn cmv ncmn vmcvn mcvn mcvn mcnvm ncmvn mcvn mcnvm cnvmc nvmcnvmcn mvn cmnv mcnvmcn mcvn mcvn cmvn mcvn mcvnmcvn mcvn mcvnm