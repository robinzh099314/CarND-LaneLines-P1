# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/tmp_solidWhiteCurve.jpg "detect results"
[image2]: ./test_images_output/solidWhiteCurve.jpg "full length line on lane"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

### 1.1 My pipeline consisted of 9 steps. for the first two videos, it include steps :

#### Step1, from color to gray image
#### Step2, create mask image by setting only the front area for lane detection
#### Step3, blur image with filter to remove noises 
#### Step4, threshold the blur image to binary
#### Step5, detect edge by canny with the mask image
#### Step6, apply the Hough Transform for all lines
![alt text][image1]
 In order to draw a single line on the left and right lanes, I defined the left_right_lines() function for step7~9
#### Step7, mark the left and right lane area seperately by slope value
#### Step8, compute the average slope and center position for left and right lane
#### Step9, reconstruct the full length line for left and right land
#### Step10, memoize the sucessfule detection
#### Step11, compare current result with previous ones, if the difference is greater than presetted, using the previous value to draw
#### Step12, if fails in current frame, using the previous value to draw


![alt text][image2]

### 1.2. For the optional video, I add procedure for color, the left yellow line, threshold in HSL space, which remove the shadow from image, the right line area remains in gray space 

#### Step1, blur image with filter to remove noises 
#### Step2, from color RGB to HLS image
#### Step3, initilize the color range for yellow and gray
#### Step4, threshold the HLS and RGB image seperately for left and right line
#### Step5, create mask image by setting only the left/right front area for lane detection
#### Step6, detect edge by canny with the mask image
the other step is the same of previous from step6...


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when fail to detect the lane on image for several times continuedly, or the real value changed too much, it could lost tracking

Another shortcoming is the shadow and blobs on the road, the threshold value could not segmente lane road effectively, more refined strategy to get the the adaptive threshold value, such as in more small area, only detects in the lane line area from previous result


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to stable tracking, since the slope and position of lane are continues, large varience between two frames means error, save more past data in memory could useful for current frame verification during the failue

Another potential improvement could be to use the color information, I think the color information could be useful for future progress...

All code is available on [Github](https://github.com/robinzh099314/CarND-LaneLines-P1).