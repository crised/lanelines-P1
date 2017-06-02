# **Finding Lane Lines on the Road**

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./solidWhiteCurve.jpg "WhiteCurve"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale,
then I used the GaussianBlur function with `kernel_size=5`.

Later, I calculated the edges using Canny function, with a `low_threshold=50` and `high_threshold=150`.
Just like the values we used in the lessons.

Then in order to define a region of interest in the image, I created a `vertices` `numpy` array, describing
a polygon of 4 sides.

Using the region above described,

Then, I used `cv2.imwrite` to save testing image to the file system, using the image calculated from Hough's Lines algorithm.

Here is the output of one of them:

![White Curve][image1]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image:



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ...

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
