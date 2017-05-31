# **Finding Lane Lines on the Road** 

## Writeup


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "Detect lanes raw 1"
[image2]: ./test_images_output/solidWhiteRightImproved.jpg "Detect lanes final 1"
[image3]: ./test_images_output/whiteCarLaneSwitch.jpg "Detect lanes raw 2"
[image4]: ./test_images_output/whiteCarLaneSwitchImproved.jpg "Detect lanes final 2"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur with kernel size of 5 to the images. After that, I found the canny edges in the images, and applied a mask to the wanted area. Finally, I found the Hough lines from the edges, and combined the resulted images containing only those lines with the original images. All of these operations were made using the helper functions.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by splitting information of the left and right lane, i.e. the slopes as well as the x and y coordinates. I then calculated for both left and right lines the average slope, the average/middle point, and from those the intercept _b_ (_y=kx+b_), and used those to calculate the two end points for both of the lanes. Those points were used to draw the lines.

Here are some example images of both the raw and the final versions of the lane detection. I didn't do the challenge video, because a `ValueError` was thrown, and I didn't know why.

![alt text][image1]

![alt text][image2]

![alt text][image3]

![alt text][image4]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is curvy. This implementation works well for finding straight lane lines, but somewhat falls apart when it tries to detect curvy lanes, especially on the final one-line implementation.

Another shortcoming is that this one-line implementation sometimes for an unknown reason (to me at least) fails to get data of the left and/or right lanes when run on videos. This results in empty lists, and therefore in `NaN` values (because of the handling of empty lists by `numpy.mean()`), and so causes problems. 


### 3. Suggest possible improvements to your pipeline

A possible improvement could be to split the drawn left and right lines into 2-4 parts, and connect them end-to-end. This would be practically the same as before on straight roads, but significantly better on curvy roads. However, it would be slower to calculate, which might make it impractical in some situations.

Another potential improvement could be to have the pevious values of the slope and the middle points of the lines to carry on to the next frame. In other words, the algorithm would "memorize" what the values were previously, and change them only a little, since they presumably don't change all that much between frames. Also, if an error would be thrown while calculating the new values, the old ones could be used instead without a problem. This would also decrease the amount of "wobbling" of the lines in the videos.
