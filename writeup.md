# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./others/step1.png "Step.1"
[image2]: ./others/step2.png "Step.2"
[image3]: ./others/step3.png "Step.3"
[image4]: ./others/step4.png "Step.4"
[image5]: ./others/step5.png "Step.5"
[image6]: ./others/step6.png "Step.6"
[image7]: ./others/step7.png "Step.7"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps. 

Step.1

I resized so that the input image size is 960 x 540.

This is to prevent mask area and lane line from being dependent on image size.

Actually, the given "challenge.mp4" was 1280 x 720 in size different from other images, and good results were not obtained unless the size was aligned.

![alt text][image1]

Step.2

A color mask was applied to detect only white lane lines and yellow lane lines.

In "challenge.mp 4", unless this processing is applied, textures other than the lane lines are detected as a line, and a good result cannot be obtained.

![alt text][image2]

Step.3

I converted the images to grayscale.

![alt text][image3]

Step.4

I applied Gaussian filter.

![alt text][image4]

Step.5

I applied Canny edge detection.

![alt text][image5]

Step.6

I masked unnecessary areas of the image.

![alt text][image6]

Step.7

I applying Hough transform for detecting straight lines.

![alt text][image7]

In Step.7, in order to draw a single line on the left and right lanes, I modified the draw_lines() function.

First, I separated line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.

Then, I found straight lines fitting each of the left and right segments using linear regression.

In addition, when the line segment is not found, or when the linear regression is not performed properly, drawing of the straight line is not performed.

### 2. Identify potential shortcomings with your current pipeline

Sometimes lane lines may not be detected.

Especially it cannot be detected in the scene where the brightness of the road changes like "challenge.mp 4".

Also, if there are multiple lane lines on either side, they cannot be separated and detected.

### 3. Suggest possible improvements to your pipeline

In order to detect lane lines more robustly, Canny's edge detection and Hough transform parameters could be more optimized.

This time I optimized the parameters with human's hands, but using deep learning may have obtained more optimal parameters.

Alternatively, although these parameters are always fixed, it may be considered to dynamically change according to the shooting situation of the image or the area of the image.

In addition, in order to suppress the influence of luminance fluctuation of the image, it may be good to apply a high pass filter or the like.

And, in order to separate multiple lane lines, cluster analysis may be used.
