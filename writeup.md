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

Here is the output of one of images:

![White Curve][image1]

For the video images, I used the lane marking on the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

- Primarily by adding a `m`, the slope of the given line. So each of the lines is described as: `m, x1, y1, x2, y2`

- Then I sorted the lane lines, by using `m`, so my first idea is to split the array in two. The first half will likely correspond to the `left` lane,
consequently the second line to the `right` lane. Usually, left lanes lines will have negative slope, while right lanes positive slope.

- I calculated a `split` value, by calculating the biggest gradient/differential in the array of lines.

- Later on, I implemented a helper method called `extreme_points`. Again, I used the magic of sorting, this time by `x1`.
In the left lane case, I picked the most left point, then I found the most right point to draw a line. Inversely, in the right lane case,
it calculated the most right point, then picked the most left one to draw a line.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when point of the lanes are confused.
I spent most of the time dealing with this fact. Problem with `draw_lines` is that sometime it draw lines connecting left and right lanes.
To avoid this error, I forced the method to only draw lines that had similar slopes.

Another shortcoming is that lines are oscillating a bit.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use Supervided Learning, humanly marking the lanes in the target value.

Another potential improvement could be to use Reinforcement Learning, rewarding the car when it's inside the lanes, and punishing it when it trespasses them.
