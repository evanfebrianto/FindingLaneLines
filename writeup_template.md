# **Finding Lane Lines on the Road** 

## Description

### This program is used to detect land lines using standard openCV library such as canny edge detection as well as Hough lines transformation. By implementing region of interest on top of that, you are able to eliminate unnecessary information on the image.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/slopes_distribution.png "Slopes Distribution"
[image2]: ./test_images_output/solidWhiteCurve.jpg "Output Example"
[image3]: ./test_images_output/all_images.png "All Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. Below are the details:
* Converting image from 3 color spaces to grayscale
* Applying Gaussian Blur with kernel size = 5
* Applying canny edge detection with 1:3 threshold ratio
* Defining vertices for region of interest masking
* Applying Hough line transformation inside the region of interest

After putting all the pipelines together, I was able to detect the lane lines inside the region of interest. However, the goal of this project is to draw a single line on the left and right lanes.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by extrapolating the lines. I separated the left and right lanes based on their slopes. Then I grouped them in two different categories in which the linear regression equation will be generated by calling np.polyfit()

The image below shows the slopes distribution in one image. Right lane will have a positive slope starting from 0.5 while the left lane has a negative slope starting from -0.5. Therefore, any values in between will be ignored.

![alt text][image1]

Once the draw_lines() is modified, I run back the pipelines on the input image and below is the result.

![alt text][image2]

If I put all the input images together, it will look like this

![alt text][image3]

After applying the pipelines to the video input, I managed to get satifying results on the solidWhiteRight.mp4 and solidYellowLeft.mp4. However, I am still struggling on how to optimize the pipeline so that it works for the challenge.mp4 as well


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane is not straight as my extrapolated formula is using a linear regression.

Another shortcoming could be if the slope range is -0.5 to 0.5 then it will be negleted. Every video footage may have different slope value so that putting a hardcoded threshold seems not the best way to achieve the goal.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to to use curve fitting lane instead of linear regression.

Another potential improvement could be to use filtering algorithm to remove some noise inside the region of interest instead of using a hardcoded slope range threshold.
