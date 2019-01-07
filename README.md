# Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

---
The Project
---

**Goals:** Use advanced computer vision to detect lane boundaries in a video

**Tools:** Python and OpenCV

**Techniques :**
* Camera calibration and image distortion correction  
* Gradients and color transforms 
* Perspective transform
* Detect lane pixels
* Average lane pixels to remove shekiness 

[//]: # (Image References)
[image1]: ./output/distorted.png "undistorted Image"
[image2]: ./output/distorted2.png "distorted2 Image"
[image3]: ./output/grad.png "grad Image"
[image4]: ./output/color.png "color images"
[image5]: ./output/combine.png "combine images"
[image6]: ./output/pre.png "pre images"
[image7]: ./output/window1.png "window1 images"
[image8]: ./output/window2.png "window2 images"
[image9]: ./output/final.png "final images"

---

The Steps
---

The steps of this project are listed below. You can have a look at Advanced Lane Finding.ipynb for the code.

### 1. Camera calibration  and image distortion correction
Use chressboard images to compute the camera calibration matrix and distortion coefficients
![alt text][image1]
Apply to our test images
![alt text][image2]

### 2.Create a thresholded binary image
Gradients thresholded
![alt text][image3]
Color thresholded 
![alt text][image4]
Combine Gradients and color thresholds to obtain binary thresholded images
![alt text][image5]

### 3. Perspective transform
Transform image to birds-eye view. Using a straight lanes image is easy to find the destination points and source points, becase one lane will be vertical and parallel with another from birds-eye view
![alt text][image6]


### 4. Detect lane pixels
Use sliding window to search lane pixels
![alt text][image7]
Searching around previosly detected lane line and highline lane line area
![alt text][image8]

### 5. Compute the curvature and center offset
In this project, camera image has 720 relevant pixels in the y-dimension and roughly 600 relevant pixels in the x-dimension.Therefore, to convert from pixels to real-world meter measurements, I use:
* ym_per_pix = 30/720 
* xm_per_pix = 3.7/600 
![alt text][image9]

### 6. Building image pipeline
To remove shekiness, I average the current frame lines with the previous frame lines(13 frames). Besides, I implement sanity checks. If sanity checks s reveal that the lane lines are problematic for some reason, i will reset the algrithom and search from scratch using sliding window. Otherwise, i will search around previosly detected lane line.

## Videos
---
**Some results on test videos provided by Udacity:** 
* [regular](./output/regular.mp4) 
* [challenge](./output/challenge.mp4) 
* [harder](./output/harder.mp4) 

---
## Potential shortcomings
The image pipeline do a good job on regular test video provided for the project, which shows ideal situation with good road condition and good weather. However, the solution donot preform very well on the challenge video and even worse on the harder video. In the challenge video, the image pipeline can not detect the lane lines well when there was heavy shadow over the road from an overpass. In the harder video, these was strong sunshine whihc makes it difficult to detect the lane lines.

---
## Suggestions
To handle heavy shadow and avoid losing the lane lines, one possible solution is to develop stronger threshold image to reduce the negative effect of shadows. Besides, we can develop more sanity checks to filter bad lines, and use the pervious lines to tract the road.

