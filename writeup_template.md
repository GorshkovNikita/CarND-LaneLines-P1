# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[result_image]: ./test_images_output/solidWhiteCurve.jpg "Result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of following steps. First, I converted the images to grayscale, then I applied gaussian filter to blur image in order to get rid of some noise. Next, I ran Canny algoritm to detect edges on blurred image. At this point I have a binary image, where pixels with value 0 aren't edges, and pixels with value 255 are edges.

In order to draw a single line on the left and right lanes, I didn't modify the draw_lines() function because I think the only purpose of this function is, well, to draw lines and not to compute average line. So, I decided to split the image with detected edges in two parts (left and right) using region_of_interest function. This way I can make sure, that all edges that belong to the right (left) lane are on the right (left) part. Next, for each part, I found hough lines, and then I approximated this lines with numpy.polyfit function. Finally, I used coefficients of approximated line to draw final lines on the source image using draw_lines function.

![Result][result_image]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when it is dark outside and it is quite difficult to detect edges using Canny algorithm. 

Another shortcoming could be when there is a lot of snow on the road, and it is almost impossible to detect lanes, because they are under snow.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use polyfit function with higher degree of polynomial to detect curved lines. 

Another potential improvement could be to 
