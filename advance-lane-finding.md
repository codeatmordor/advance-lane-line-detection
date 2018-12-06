
**Project 2: Advanced Lane Finding Project**
** In project one we experimented with finding straight lanes using canny edge detection method, this project extends lane detection for curved lanes too. We have used perspective transformation and sliding window approach to draw lane lines. We have also computed curvature of lane lines.**

## Pipe-line Description 
- Caliberate Camera using chessboard images by identifying/drawing corners
- Undistort images
- Using color trasform , and use perspective transform to get birds-eye-view of lanes
- Identify rectangular shape in images as lane boundary
- Compute curvature of the lane 
- Output lane boundary and curvature and centre offset(vehicle position)


[//]: # (Image References)

[image1]: ./output_images/cam_cal/cam_cal_1.png "Caliberated1"
[image2]: ./output_images/cam_cal/cam_cal_2.png "Caliberated2"
[image3]: ./output_images/undistorted/Undis1.png "Undistorted1"
[image4]: ./output_images/undistorted/Undis2.png "Undistorted2"
[image5]: ./output_images/resul_bin_combined/res_bin1.png "Binary1"
[image6]: ./output_images/resul_bin_combined/res_bin2.png "Binary2"
[image7]: ./output_images/warped/warp1.png "Warped1"
[image8]: ./output_images/painted_lane.png "Lane Drawn"
[image9]: ./output_images/sliding_window/slide_win1.png "Slide Win1"
[image10]: ./output_images/sliding_window/slide_win2.png "Slide Win2"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The first step in the pipeline is to caliberate the camera.. Chessboard corners are identified and plotted. Open CV functions like findChessboardCorners(), drawChessboardCorners() and calibrateCamera() help us do this.
![alt text][image1]
![alt text][image2]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.
undistort() method is implemented in the code to achieve this.
![alt text][image3]
![alt text][image4]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

Gradient threshold and color threshold individually are applied and then  a binary combination of these two images to map out where either the color or gradient thresholds were met called the res_bin in the code.

![alt text][image5]
![alt text][image6]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.
Below values are used for perspective transform.warp_image() method is implemented in code.
src = np.float32([[588,450],[683,450],[1090,720],[200,720]])
dest = np.float32([[300,0],[900,0],[900,720],[300,720]])

![alt text][image7]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

search_around_poly() and fit_polynomial() methods are used for this.

![alt text][image9]
![alt text][image10]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

radius_and_offset() method is implemented to achieve this.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

 cv2.putText() is used in process_image method to write curvature and offset on result image.
![alt text][image8]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./video_output/project_video_output.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
