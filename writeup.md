# **Finding Lane Lines on the Road** 

## Writeup

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of following steps:

* Make a copy of an image to not affect initial image array
* Converted the images to grayscale
* Apply blur to supress noize
* Apply Canny edge detection to find edges of objects
* Apply region of interrest mask to ignore edges outside this region
* Apply Hough transform to find lines in region from previous step
* Draw lines on initial image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function:
* I ignore lines that has angle less than 20 degrees to horizont to exclude horizontal lines (a few of them appeared on car hood because of blur)
* I saved slope, intersect and length of each line. If slope is less than zero - it's left line, if greater than zero - right line
* I found average slope and intercept for left and right lines separately with respect of each line length (so longer lines make more impact)
* Draw left and right line on image from image bottom coordinate to visible apex

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Grayed image](https://github.com/debuggio/Udacity-SDC-FindingLaneLines/tree/master/test_images_output/gray_solidWhiteCurve.jpg)
![Canny image](https://github.com/debuggio/Udacity-SDC-FindingLaneLines/tree/master/test_images_output/edges_solidWhiteCurve.jpg)
![Image with region of interrest](https://github.com/debuggio/Udacity-SDC-FindingLaneLines/tree/master/test_images_output/masked_solidWhiteCurve.jpg)
![After hough transformation](https://github.com/debuggio/Udacity-SDC-FindingLaneLines/tree/master/test_images_output/hough_solidWhiteCurve.jpg)
![Result](https://github.com/debuggio/Udacity-SDC-FindingLaneLines/tree/master/test_images_output/solidWhiteCurve.jpg)


### 2. Identify potential shortcomings with your current pipeline

A potential shortcoming would be what would happen when on bright sun, white lines could be almost the same color as road itself, so it would be hard to identify them.

Another potential improvement could be to curve lines on turns, to better understand future path

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to preserve previous condition could help to stay on road if it's hard to identify what's next

Another potential improvement could be to change region of interest based on direction and move it left or right (also change it's form) it if car makes a turn
