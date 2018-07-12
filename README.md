## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./output_images/distortion_correction.png "Distortion Correction"
[image2]: ./output_images/undistort.png "Undistorted"
[image3]: ./output_images/binary.png "Binary Example"
[image4]: ./output_images/warped.png "Warp Example"
[image5]: ./output_images/color_fit_lines.png "Fit Visual"
[image6]: ./output_images/output.png "Output"
[video1]: ./project_video_output.mp4 "Video"

---

### Camera Calibration

#### 1. How I computed the camera matrix and distortion coefficients.

The code for this step is contained in the second code cell of the IPython notebook located in [Advanced-Lane-Lines.ipynb](./Advanced-Lane-Lines.ipynb).

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing pipeline on single frames.

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image1]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

Apply distortion correction to the original image based on the camera calibration matrix and the distortion factor.
![alt text][image2]

#### 2. How I used color transforms, gradients or other methods to create a thresholded binary image.

I used a combination of color and gradient thresholds to generate a binary image in the fourth cell. Here's an example of my output for this step.

![alt text][image3]

#### 3. How I performed a perspective transform and provide an example of a transformed image.

The code for my perspective transform is in the sixth code cell of the IPython notebook. I chose the hardcode the source and destination points in the following manner:

```python
offset = 200

src = np.float32([[590, 445], [690, 445], [1050, 675], [230, 675]])  

dst = np.float32([[offset, 0], [img_size[0] - offset, 0], [img_size[0] - offset, img_size[1]], [offset, img_size[1]]])

```

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][image4]

#### 4. How I identified lane-line pixels and fit their positions with a polynomial?

The lane boundary can be found by fitting to a second order polynomial after separating the left and right lane line pixels. Here is an example of my result on a test image:

![alt text][image5]

#### 5. How I calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in the seventh cell.

#### 6. Provide an example image of the result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in the eighth cell. Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### Here's a link to my [video result](./project_video_output.mp4)!
