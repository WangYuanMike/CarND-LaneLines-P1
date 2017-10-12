# **Finding Lane Lines on the Road** 


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

My pipeline is a function called lane_finding_pipeline(), which consists of 9 steps:

1) Convert the input image to gray scale
2) Apply Gaussian smoothing
3) Highlight edges by canny edge detector
4) Apply an image mask to filter out edges which are not in the masked region
5) Run Hough transform to get line segments
6) Compute lane lines
7) Apply image mask once more to exclude the part of lane lines which are not in the masked region
8) Merge lane lines and the input image to form the output image
9) Return output image and most intermidiate images 


In order to draw a single line on the left and right lanes, I created a new function called draw_lane_lines(). Basically I followed the hints in the Note of function draw_lines(), namely throught computing slope of each line segments, I seperated them into two classes, left lane line and right lane line. Then I exclude the outliers by comparing a slope threshold. By printing out the slopes of each line segments, I found that most valid ones are in the interval of [0.5, 0.95], which became my slope threshold. Plus I futher exclude outliers by comparing their distance to the mean. The rest of the funciton is quite straight forward. 


I kept the draw_lines() function for printint out Hough line segments, which is helpful for me to check the process of the image processing.


For handling the challenge video, I get one image snapshot of the video and save it in the test_image directory with name challenge.jpg, through which I found out the shape, channel, and other properties of this video. I added some branch and parameters to make function draw_lines(), draw_lane_lines(), and the pipeline function be able to handle the 4 channel high resolution image/video to some extent.


The output of pipeline cell should explain the whole image processing procedure quite clearly.


### 2. Identify potential shortcomings with your current pipeline


One shortcoming is that lane lines shake more frequently than the ones in the examples/P1_example.mp4.

Another shortcoming is that I did not handle the challenge video perfectly, which means occasionally the lane lines I draw would be away from the real lane lines too much.

The third shortcoming is that all parameters are set by me manually according to the test images, namely they are not self-adpative to different images in the video, although the lane line part does not change frequently in the test video.


### 3. Suggest possible improvements to your pipeline


A possible improvement would be to find out a way to adjust parameter according to image change dynamically. I am curious about how to adjust parameters effectively, even in a manual manner.

Another potential improvement could be to implement a better outlier exclusion algorithm.

The program architecture could be optimized as well, e.g. introducing OO might be useful to handle more image cases, and some redundant part in draw_lines() and draw_lane_lines() could be merged somehow.
