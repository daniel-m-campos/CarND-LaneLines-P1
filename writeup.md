# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_images/solidYellowCurve_gray_gaus_blue.jpg "Gaussian Blur"
[image3]: ./test_images/solidYellowCurve_canny.jpg "Canny"
[image4]: ./test_images/solidYellowCurve_region.jpg "Region"
[image5]: ./test_images/solidYellowCurve_hough.jpg "Hough"
[image6]: ./test_images/solidYellowCurve_final.jpg "Final"
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:
1. Convert image to grayscale.
1. Apply Gaussian blur with kernel_size 5. 
![alt text][image2]
1. Run Canny edge detection using 50/150 low/high threshold respectively.
![alt text][image3]
1. Apply a region of interest mask using vertices `(0,imshape[0]),(450, 310), (490, 310),(imshape[1],imshape[0])`
![alt text][image4]
1. Find Hough lines using parameters `rho=1, theta=np.pi/180, threshold=35, min_line_len=5, max_line_gap=5`
![alt text][image5]
1. Extrapolate lines with similar slopes with absolute value greater than 0.5.
![alt text][image6]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by adding an `extrapolate` function that groups lines with similar slopes with absoluate value greater than 0.5 and then uses those lines to find an extrapolated line.

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the size of the image changes, the region of interest may not be well suited anymore.

Another shortcoming could be if the lane line separation changes, the hough line parameters may need to be re-tuned.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to standardized the images sizes before putting them into the pipeline. This may make the algorithm more robust to different image sizes.

Another potential improvement could be to find a way to fit parameters automatically.
