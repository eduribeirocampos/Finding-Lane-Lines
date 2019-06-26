[//]: # (Image References)

[image1]: ./test_images/pipeline_1.jpg "pipeline summary" 
[image2]:./test_images/pipeline_2.jpg  "pipeline correction" 
[image3]: ./test_images/solidWhiteCurve.jpg "Initial image" 
[image4]: ./test_images/Schematic_extended_lines.jpg "Draw lines strategie" 
[image5]: ./test_images/Single_lines.jpg "Draw lines result" 

[image6]: ./test_images/Formula_1.jpg 
[image7]: ./test_images/Formula_2.jpg 
[image8]: ./test_images/Formula_3.jpg 
[image9]: ./test_images/Formula_4.jpg 



# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

This project was created in order to reach the goals from the Udacity Self driving car Nanodegree program.

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)

### 1. Describing the pipeline:.

My pipeline consisted of 6 steps:

**Step 1:**  I converted the images to grayscale.

**Step 2:**  I have applied a gaussian blur in the gray image (from step 1 result).

**Step 3:**  It was used the tool canny edges detection (from step 2 result).

**Step 4:**  I defined a mask area to keep only the lane lines (from step 3 result).

**Step 5:**  It was created a empty picture and it was added lines using the picture obtained on step 4 as reference.

**Step 6:**  And finally  it was overlaid the result from step 5 to original picture.

In the next picture is possible to see the result of each step.

![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by a new a function named "draw_Extended_lines".

The strategie was use the for loop to added the coordinate points for each line inside a list,
and after calculate de average for each coordinate point to create the lines.
To sort the information between left line and right line the Slope of the line was used

The schematic picture below show the strategie:

![alt text][image4]


The result of this strategy could be saw in the next picture:

![alt text][image5]

To accomplish the goals of this project, it was required extend the lines along the lane proposing new limits for both sides (left and right).

Here , using an analytic geometry concept it was created a matrix to define the equation for each line. Where:

![alt text][image6]

To figure out the lower point. it was fixed the Y coordinate with the limite of the image size, And it was calculated the X coordinate. The equation below was used for both lines:

![alt text][image7]

The upper point for both lines is the intersection point of them. where the variables X is isolated and the equations are combined. ( L = left line and R = right line)

**X coordinate for upper point:**

![alt text][image7]

**Y coordinate for upper point:**

starting from the known coordinate X_upper,using the equation from line 1, it was found the Y_upper 

![alt text][image8]

So after the function "draw_Extended_lines" already created , it was necessary create a new function named "hough_Extended_lines" where the new criteria to create lines was applied.


For the official Pipeline the Steps 5 and 6 was replaced by the new one.

The next picture show the final result.

 ![alt text][image2]

## general information about the parameter and some variables:

**Gaussian Blur Kernel:** Gaussian Blur Kernel:  It was used 5x5 - others values was set, but without  any gain.

**low_threshold / high_threshold:** Used (50/150), low values show a inconsistent results . High values was not good because sometimes, the algorithm was not able tho recognize the lines. Both observation was made when the algorithm run with the videos.

**Vertices for Masked edges:** Coordinates created in order to isolate the lane lines.

**rho,theta,threshold,min_line_len,max_line_gap:**  the values were combined to generate a solid result regard the lane line identification during  the time of the video test.

using the library ` moviepy.editor`and the function `VideoFileClip `,it was applied the pipeline in the 2 input videos.

The final result could be checked in the next 2 files:

* [solidWhiteRight.mp4](./test_videos_output/solidWhiteRight.mp4) 
* [solidYellowLeft.mp4](./test_videos_output/solidYellowLeft.mp4) 

For more details see the code file [P1.ipyng](./P1.ipyng) 






