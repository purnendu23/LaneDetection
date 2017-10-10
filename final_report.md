# **Finding Lane Lines on the Road** 


[//]: # (Image References)


### Submission Files/Writeup

You're reading the writeup! and here is a link to my [project code](https://github.com/purnendu23/LaneDetection/blob/master/P1.ipynb) 

[html] ( https://github.com/purnendu23/LaneDetection/blob/master/P1.html )

---

### 1. Lane detection pipeline.

The lane detection pipeline consists of the following stages in order:

1. Filtering Colors
2. Generating gray scale image
3. Bluring the image
4. Getting the region of interest from the image
5. Canny edge detection
6. Drawing Hough lines
7. Return annotated image

Most of the methods here were provided in the earlier lessons. Therefore, I would go over only two methods which were important for solvng the problem completely:

* `draw_lines(img, lines, color=[255, 0, 0], thickness=5)`

The draw_lines method is called from the `hough_lines` method in the step six of the pipeline described above. The input to draw_lines is an empty image (`line_img = np.zeros((img.shape[0], img.shape[1], 3), dtype=np.uint8)`) and an array of line segments identified from the edge-image (output of canny edge detection method) by the `cv2.HoughLinesP` method.
The goal of this method was to draw the left and right side of the driving lane. However, there were multiple line segments detected on the left and right side of the lane. 
Here is the high level approach/algorithm followed in this method:
1. For all the lines:
    * calculate the slope m
    * if ( -.8 < m < -.5 ) then assign this line to the left side segments
    * if ( 0.5 < m < 0.8 ) then assign this line to the right side segments
2. For each left and right side points:
    * fit a line through the points (`np.polyfit(x,y,1)`) to get the _slope (m)_ and _y-intercept (b)_
    * Use the parameters to draw a line on each side
3. Return the image with lane-lines drawn on it.
    
* `filter_colors(image)`
This is a simple function which filters the white pixels and yellow pixels from the image and returns the combined image back.

As you go over the subsequent cells in the P1.ipynb file, everything is self explanatory. I have:

* Defined the helper functions
* Built the pipeline using the helper functions
* Tested the pipeline on a single image and subsequently on all test images.
* I then test the pipeline on test videos

### 2. Potential shortcomings in the current pipeline

* A possible shortcoming in the pipeline is updation rate. Sometimes the road curves really fast and the pipeline is not able to update the new lane line as fast as it should.

* The line which I draw is a straight line. That means, it is only going to fit the lanes-lines perfectly if it is a staright road. If the road is too curvy the method will definitely not work well.

* Changing conditions effect image quality
When weather conditions change during snow, rain or fog or when lighting changes because of shadows from trees, clouds, tunnels etc. it will be harder to distinguish edges.

* We are using a fixed region space to detect the lane lines. This will not work if the camera position is changed.

### 3. Possible improvements in the pipeline

* Adapt to image qulaity/ weather conditions:
We can use Canny Edge detection with adaptive thresholds which are dependent on characteristics of the image like brightness, contrast etc. A potential solution could be to switch to another color space.

* Images with different dimensions can be taken care of by using relative sizes for the mask instead of absolute pixel values.
