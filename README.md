#**Finding Lane Lines on the Road** 

---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road



[//]: # (Image References)

[image1]: ./initial_results/NormalizationAttempt.png "Normalization Attempt"
[image2]: ./tested_images/solidWhiteCurve.jpg "Result 1"
[image3]: ./tested_images/solidWhiteRight.jpg "Result 2"
[image4]: ./tested_images/solidYellowCurve.jpg "Result 3"
[image5]: ./tested_images/solidYellowCurve2.jpg "Result 4"
[image6]: ./tested_images/solidYellowLeft.jpg "Result 5"
[image7]: ./tested_images/whiteCarLaneSwitch.jpg "Result 6"
[image8]: ./initial_results/solidWhiteRight.jpg "Inital results"


---
### Running the program

Run the P1.ipynb 
### Reflection

###1. Describing the pipeline

My pipeline consisted of 5 steps. First, I converted the images to grayscale, applied a Gaussian blur to the image, and then used Canny edge detection on the image. I then defined a region of interest using defined vertices, and used Hough transform on the image. 
Initial Result:
![alt text][image8]

I attempted to normalize the image before converting it to grayscale but it didn't work as expected. Following is what it looked like: 
![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first calculating the slopes of the individual lines being drawn. I, through trial and error, found constants to threshold and filter out some of the lines. I, then averaged the remaining lines and used linear extrapolation to extend the line over the region of interest. The tested_images folder shows the following results:

![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]

The video results are stored as white.mp4, yellow.mp4, and extra.mp4

###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lines are perpendicular, the slope would become infinite. I have a try/except case to combat that. 

Another shortcoming could be surrounding lighting effects. This can be observed in the challenge video when the pipeline disappears from view. I tried combating this by normalizing the image first but wasn't able to execute it properly due to time. I will try revisiting this again afterwards.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to use the previous slope values for the lines and use those while predicting the future pipeline. This would prevent erratic jumping of the pipeline.

Another potential improvement could be to account for shadows and lightning changes through normalizing the image.
