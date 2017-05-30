# **Finding Lane Lines on the Road** 

## Writeup


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur with kernel size of 5 to the images. After that, I found the canny edges in the images, and applied a mask to the wanted area. Finally, I found the Hough lines from the edges, and combined the resulted images containing only those lines with the original images. All of these operations were made using the helper functions.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by splitting information of the left and right lane, i.e. the slopes as well as the x and y coordinates. I then calculated for both left and right lines the average slope, the average/middle point, and from those the intercept _b_ (_y=kx+b_), and used those to calculate the two end points for both of the lanes. Those points were used to draw the lines.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
