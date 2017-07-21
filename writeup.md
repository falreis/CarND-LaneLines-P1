# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/whiteCarLaneSwitch.jpg "White Car Lane Switch"
[image2]: ./test_images_output/solidYellowLeft.jpg "Solid Yellow Left"
[image3]: ./test_images_output/solidWhiteRight.jpg "Solid White Right"
[image4]: ./test_images_output/solidWhiteCurve.jpg "Solid White Curve"
[image5]: ./test_images_output/solidYellowCurve.jpg "solid Yellow Curve"
[image6]: ./test_images_output/solidYellowCurve2.jpg "Solid Yellow Curve2"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. The steps I followed were:
1. Conversion of images to grayscale;
2. Application of Gaussian smoothing;
3. Definition of Canny parameters and aply to the image;
4. Drawing of a polygon in the image area to find the road lanes (region of interests);
5. Application of Hough Transform in the region of interest;
6. Extrapolation of the line segments returned by Hough transform to generate support lines (using linear regression - polyfit function);
7. Writing of the support lines (with transparency);

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to find the support lines.
The support lines was generated using linear regression of the line segments detected.
Firsty, I splitted the segments in two groups: The Left Lane and the Rigth Lane, using the slope of each segment.
Secondly, I rejected some segments. Segments wiht positive slope on the right lane or negative slope in the left lane were rejected. This small step had the goal to avoid noises.
Thirdly, I generate the support lines using python polyfit function.
Endly, I draw the lines and define a transparency mask.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road have closed curves. With the closed curves, it's possible that linear regression doesn't work well.
Another shortcoming could be identify small line segments in roads with lot of marks on asphalt.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use different methods to connect segments of lines that adpats on curves or any kind of situation. In this scenario, it's possible to use polinomial regression or 
Another potential improvement could be try to identify the lines with dynamic parameters that adapts on different images, from different camera positions in differents cars.
