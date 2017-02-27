#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "solidWhiteCurve"

![](./test_images/solidWhiteCurve_modified.jpg) 

---

### Reflection

###1. Describe your pipeline. 
My pipeline consisted of 5 steps:

* Convert the images to grayscale<br>
* Perform Gausian smoothing and apply Canny edge detection<br>
* Select region of interest and mask other areas of the image<br>
* Apply Hough Transform to detect lane lines<br>
* Superimpose the lane lines on the original image<br>

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

Calculated slope and center of each line. <br>
Then based on the slope, sort it into right or left lane line<br>
Calculate the average slope and the center of right and left lane<br>
Then using the Y coordinates, based on Region of Interest, figure out the X cordinates using the avg slope and center point of lane lines [equation used: (y-y') = M (x-x')]

The explaination of this equation: (y-y') = M (x-x') is as follows:<br>
y is equal with ymax and y' is equal with y_avg.<br>
As (xmax,ymax) and (x_avg,y_avg) are two points that are located in the same line. <br>
As a result, the line has the unique M and b.<br>

y=Mx+b,  b=y-Mx<br>
y'=Mx'+b,	b=y'-Mx'<br>
b=b, y-Mx=y'-Mx'<br>
(y-y') = M (x-x')<br>

Replacing xmax,x_avg,y_max,y-avg to this equation, I get the result below:<br>
ymax-y_avg=M(xmax-x_avg)<br>
xmax=x_avg-(y_avg-ymax)/slope_avg    <br>      

Then put above xmax into draw_lines function and calculate the xmax and xmin cordinates for both right and left sides.
 



###2. Identify potential shortcomings with your current pipeline


Potential shortcomings of my approach:

The region of interest in Image masking is static, hence it can only work in specific scenarios

Slope conditions used for detecting right and left lanes do not work in case of a curve in the road


###3. Suggest possible improvements to your pipeline

Possible improvements to my approach:

Make the image mask selection dynamic, so that it could work in different scenarios

Modify the slope conditions, so that they work with curve in the road
