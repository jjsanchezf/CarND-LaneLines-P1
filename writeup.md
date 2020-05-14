# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./report_images_output/1-gray.jpg "Grayscale"
[image2]: ./report_images_output/2-normalized.jpg "Normalized"
[image3]: ./report_images_output/3-blur.jpg "Gausian Blur"
[image4]: ./report_images_output/4-canny_edges.jpg "Canny Edges"
[image5]: ./report_images_output/5-roi.jpg "Region of Interest"
[image6]: ./report_images_output/6-h_lines.jpg "h_lines"
[image7]: ./report_images_output/6-h_lines.jpg "h_lines"
[image8]: ./report_images_output/7-final_img.jpg "Final Output"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
#### Pipeline Steps

My pipeline consisted of 9 steps.

1. Create a copy of the input image for processing into a line overlay image.
2. Convert the image into Grayscale.![alt text][image1]
3. Normalize the image values once in Grayscale.![alt text][image2]
4. Apply a Gaussian Blurr filter with a kernel size = 5. This smoothes out the edges, making the small edges less detectable, and therefore making the edge detection process more robust.![alt text][image3]
5. Apply a Canny Edge Detection filter with a low threshold of 50 and a high threshold of 110.![alt text][image4]
6. Crop the resulting image down to a specific Region of Interest. The region chosen maximizes the removal of points above the horizon, and to the left and right of the vehicle.![alt text][image5]
7. the Hough Transform is then applied to the Region of Interest. Here the shorter lines (< 40 px) are ignored. The rest of the detected lines are set to be merged over a gap distance of 25 px.![alt text][image6]
8. The resulting Hough Line List is then used to generate 2 lines, each representing the bondaries of the Lane on the left and right side of the car. The function `left_right_line` is explained in more detail below.![alt text][image7]
9. The resulting image obtained from the pipeline is then combined with the original image.![alt text][image8]

#### Generating Left and Right Lane Lines

The first step in line processing is to determine which lines belong on the left group and which belong to the group on the right. This is accomplished by calculating the slope of each line. According to the image perspective, if the slope is negative, the line belongs to the left group, otherwise, if the slope is positive, the line belongs to the right group. It is asumed that the car trevels on a parallel path to the line. this asumptions allows us to eliminate any line which do not have a sufficient  slope to be a close match to lane line geometry (any slope with an absolute value below 0.5).

The second step is to extrapolate the grouped lines into a single representative line for each group. To generate such lines it is assumed that they extend towards the rear of the car and beyond the horizon, this assumption allows us to use the lower and upper limit of the Region of interest as the starting and ending point of the lines, thus minimizing the complexity of the problem to just finding the correct "X" values for each point of each line segment.

In order to find the correct x values for each point, a function `f(y) = x` is needed. such function should be a linear fit to the point data given by each group. This is performed by using numpy's [polyfit](https://docs.scipy.org/doc/numpy/reference/generated/numpy.polyfit.html) and [poly1d](https://docs.scipy.org/doc/numpy/reference/generated/numpy.poly1d.html) operations to generate a linear function that matched the two input spaces (x and y). With these linear polynomial functions, its is possible then to calculate the corresponding "X" values for the previously defined "Y" values. The resulting (x, y) pairs are the beginning and end of the line segments.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
