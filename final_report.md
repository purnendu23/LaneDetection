# **Finding Lane Lines on the Road** 


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"


### Submission Files/Writeup

You're reading the writeup! and here is a link to my [project code](https://github.com/purnendu23/LaneDetection/blob/master/P1.ipynb)

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
    


### 2. Potential shortcomings in the current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Possible improvements in the pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
