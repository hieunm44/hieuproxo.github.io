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


# 1. Introduction
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
* Is only concerned with CV-based approaches, i.e. passive sensing.
* Survey of publications in CV-based human motion capture from 1980 to 2000.


# 2. Surveys and Taxonomies
## 2.1 Previous Surveys
## 2.2 A Taxonomy Based on Functionalities
* Functional structure of a comprehensive motion capture system:

    $$ Initialization \rightarrow Tracking \rightarrow Pose\;Estimation \rightarrow Recognition $$

    * Initialization: An prropriate model of the subject is established.
    * Tracking: Segment the subject from the background and find correspondences between segments in consecutive frames.
    * Pose Estimation: The pose of the subject’s body often needs to be estimated as this may be the output of the system in a virtual environment, or may be processed further by the recognition process.
    * Recognition: Analyze the pose or other parameters to recognize the actions performed by the subject.

* The majority of the work in human motion capture is carried out within __tracking__ and __estimation__.

## 2.3 Assumptions
* Two classes of typical assumptions:
    * Movement assumptions: Restrict the movements of the subject and/or the camera(s).
    * Appearance assumptions: Concern aspects of the environment and the subject. 

* Movement assumptions:
1. The subject remains inside the workspace
2. None or constant camera motion 
3. Only one person in the workspace at the time
4. The subject faces the camera at all time
5. Movements parallel to the camera-plane
6. No occlusion
7. Slow and continuous movements
8. Only move one or a few limbs Subject:
9. The motion pattern of the subject is known
10. Subject moves on a flat ground plane

* Environment assumptions:
1. Constant lighting
2. Static background
3. Uniform background
4. Known camera parameters
5. Special hardware

* Subject assumptions:
1. Known start pose
2. Known subject
3. Markers placed on the subject
4. Special colored clothes
5. Tight-fitting clothes

* __Note:__ The fewer the assumptions, the higher the complexity.

# 3. Initialization
*  Initialization covers the actions needed to ensure that a system commences its operation with a correct interpretation of the current scene.
    * Camera calibration
    * Adaption to scene characteristics
    * Model initialization

* Camera calibration
    * Offline calibration (mainly)
    * Online calibration

* Adaption to scene chracteristics
    * Appearance assumptions
    * Segmentation methods

* Model initialization
    * Initial pose of a subject
    * Model representing the subject

# 4. Tracking
* Definition of _tracking_: The process if establishing coherent relations of the subject and/or limbs between frames.
* Tracking may be seen as a means to prepare data for:
    * Pose estimation: Tracking extracts specific image info, either low level (e.g. edges) or high level (e.g. hands and head).
    * Recognition: Tracking represents data in an appropriate manner (e.g. walking and running).

* Three common aspects:
    * Nearly every tracking algorithm within human motion capture starts with the __figure–ground__ problem, i.e., segmenting the human figure from the rest of the image.
    *  These segmented images are transformed into another representation to reduce the amount of info or to suit a particular algorithm.
    * How the subject should be tracked from frame to frame is defined.

## 4.1 Figure-Ground Segmentation
* Temporal
* Spatial

### 4.1.1 Temporal data
* Is mostly based on the assumption of a static background (and camera).
* Two sublasses:
    * Subtraction
    * Flow

* Subtraction
    * Subtract the __current image__ from the __previous image__ in a pixel by pixel fashion, using either intensity values or the gradients.
    * Improved version: Use __3__ consecutive images instead of __2__.
    * More advanced version: Update the __background__ image during processing.

* Flow
    * Describe coherent motion of __points__ or __features__ between image-frames.
    * Another version: Each pixel is represented by its optical flow which is grouped into __blobs__ having coherent motion and represented by a mixture of multivariate Gaussians.

* Figure-ground segmentation based on temporal data assumes the subject to be the only moving object in the scene (or rather in the region of interest).
* Temporal data are usually simpler to extract and focus directly on the target of motion capture (e.g. map the motion data directly to human pose through an inverse kinematic framework)

### 4.1.2 Spatial data
* Two subclasses:
    * Thresholding: A process based on special environment assumptions.
    * Stastistical approaches: An advanced class where some of the appearance assumptions exploited by the __subtraction__ methods are relaxed.

* Thresholding: Is used if the subject's color or intensity appears different from the rest of the scene.
    * __Chroma-keying__: One color (usually blue) screen.
    * The object wears one color (usually dark) __clothes__.
    * Special version: The object wears markers (passive or active).
    * Related approach: Use an __IR__ camera.

* Stastistical approaches: 
    * Use the characteristics of individual __pixels__ or groups of __pixels__ to extract the figure from the background.
        * Characteristics: Typically colors and edges.
        * A sequence of background images of the scene is recorded and the mean and variance intensity or color of each pixel are calculated over time.
        * In the current image each pixel is compared to the statistics of the background image and classified as belonging to the background or not.
        * Is popular due to its robustness compared to subtraction approaches.
    
    * __Blob__ approaches
        * The subject is modeled by a number of blobs with individual color and spatial statistics.
        * Each pixel in the current image is then classified as belonging to one of the blobs according to its color and spatial properties 
    

    * Use static or dynamic colors
        * Static colors: Active __contour__.
        * Dynamic colors: Use predefined static structures representing a part of the subject’s outline. These structures consist of edge segments and other attributes.
        * Related approach: Extract the silhouette instead of the contour. 

* __Note:__
    * The use of thresholding to process spatial data is strongly dependent on a number of appearance assumptions. 
    * In more unconstrained applications, the statistical methods are a far better choice due to their adaptability.
    * The use of pixel statistics is a good concept, but region-based methods, (e.g. blobs) tend to be more reliable.
    * It is more difficult to model larger entities of correspondingly higher complexity. The active contours aim directly at extracting the shape of the subject and can be very efficient. However, they require a good initial fit and have difficulties with complex articulated objects such as the human body. The best way to exploit them seems to require an active contour for each body part.

* __Summary:__
<style type="text/css">
.tg .tg-7btt{font-weight:bold;text-align:center}
.tg .tg-0pky{text-align:left}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-7btt" colspan="2">Temporal data</th>
    <th class="tg-7btt" colspan="2">Spatial data</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-7btt">Subtraction</td>
    <td class="tg-7btt">Flow</td>
    <td class="tg-7btt">Threshold</td>
    <td class="tg-7btt">Statistics</td>
  </tr>
  <tr>
    <td class="tg-0pky">Two images</td>
    <td class="tg-0pky">Points</td>
    <td class="tg-0pky">Chroma-keying</td>
    <td class="tg-0pky">Pixels</td>
  </tr>
  <tr>
    <td class="tg-0pky">Three images</td>
    <td class="tg-0pky">Features</td>
    <td class="tg-0pky">Special clothes</td>
    <td class="tg-0pky">Blobs</td>
  </tr>
  <tr>
    <td class="tg-0pky">Background</td>
    <td class="tg-0pky">Blobs</td>
    <td class="tg-0pky">IR</td>
    <td class="tg-0pky">Contours</td>
  </tr>
</tbody>
</table>