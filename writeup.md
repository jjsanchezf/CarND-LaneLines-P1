# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./report_images_output/1-gray.jpg "Grayscale"
[image2]: ./report_images_output/2-normalized.jpg "Normalized"
[image3]: ./report_images_output/3-blur.jpg "Gausian Blur"
[image4]: ./report_images_output/4-canny_edges.jpg "Canny Edges"
[image5]: ./report_images_output/5-roi.jpg "Region of Interest"
[image6]: ./report_images_output/6-h_lines.jpg "Grayscale"
[image7]: ./report_images_output/7-final_img.jpg "Final Output"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
