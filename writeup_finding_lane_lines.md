# **Finding Lane Lines on the Road** 

## This project uses computer vision base approach to find lane lines on the Road

### Using openCV and numpy as tools to develop an algorithm that identifies and marks the lane lines. 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
My Pipeline consist of following Algorithm stages 
#### 1 Grey Scale : 
we will work with grey scale images as lane lines can have Yellow or white colors. 
#### 2 Gaussian Blur
To enhance edges Low pass filter everything else with Gaussian filter.
#### 3 Canny Edge detector
Canny Edge detector with Low and High thresholds 1:3 is used. Followed by filering out some noise by setting ROI, roughly around center of Image is identified as horizon and we do not look at edges beyond horizon, to refine the output of Canny Edge detector to a meaning full lane devider lines.
#### 4 Houges Line transform 
After we have significanltly filtered the Canny edges we use houghs tranform to find the liles in the Image. 
#### 5 Drawing Lane lines 
Drawing function was developed in 2 iterations : Iteration 1 simple CV2.line function, then this was improve to flold all the lane line segments idetified into one lane line. The merge and extrapolation was done by finding the Slope of the line and combining points with equal slope on to one line. 
Linear Coefficient Polygon is then Fittet that minimizes the error giving us one Lane boundary. 




![alt text][image1]

[//]: # (Image References)

[image1]: ./test_images_output/output_gray_scale.jpg "Grayscale"

### 2. Identify potential shortcomings with your current pipeline

Since this Approach is CV based overall image ligting can significantly affect accuracy of detections. 
ROI selected for horizon filtering will have to adjusted as per the Camera properties (FOV, Mount point, mounting angel etc)



### 3. Suggest possible improvements to your pipeline
Possible improvements could be : 
1. For sloving lighting issue : 
   a. Use RCCB color space so images are more brighter with night vision. 
   b. pre-process the image to enhance the avg brightness. 
   c. use a DL based approcah by labeling and Training images and them inferencing the lane lines using trained network. 
2. For ROI issue making ROI bounding box a function of camera parameters will help reduce the errors. 
3. Possible to do some perf optimization. 


