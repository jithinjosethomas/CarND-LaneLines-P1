# **Finding Lane Lines on the Road** 

### Overview

The goal of the project is to come up with a lane finding pipeline using OpenCV and Python. The pipeline will be tested on the sample images and videos provided by Udacity Self Driving Car Nanodegree Program.

### Reflection

### 1. Describe your pipeline.

My pipeline consisted of the following steps. 

**Create a copy of the original image**
This will be used in processing onto line overlay image (weighted image)

![org_img](https://user-images.githubusercontent.com/22439612/59167104-838e2280-8afd-11e9-9324-c7007a09f00c.png)

**Convert the image into HLS Color Space** 
This color space will help with detections of non-white lane lines. 

![hls_img](https://user-images.githubusercontent.com/22439612/59167110-8ab53080-8afd-11e9-8ac3-27ecba4ebb9c.png)

**Normalize the hls image values**

![norm_img](https://user-images.githubusercontent.com/22439612/59167116-9274d500-8afd-11e9-8768-d5385800095b.png)



**Gaussian blurring filter**
Kernal size is 5. It is for averaging effect, smoothens out smaller edges.

![blur_img](https://user-images.githubusercontent.com/22439612/59167125-99034c80-8afd-11e9-8150-54b776c6e192.png)


**Canny edge detector on the blurred image**
Focus on strong contrasting boundaries, low threshold of 50 and a high threshold of 150

![canny_img](https://user-images.githubusercontent.com/22439612/59167135-9ef92d80-8afd-11e9-94cc-6c488b2e6cf5.png)


**Find the Region of interst via cropping** 
I defined a left and right trapezoidal Region Of Interest (ROI) based on the image size. Since that the front facing camera is mounted in a fix position, we supposed here that the lane lines will always appear in the same region of the image.


**Apply a Hough transform on the cropped edge points image**
To find the lines in the image

**Compute Lines**
Use the returned Hough line list to actually generate a line image for the left and right lanes with a linear fit for each line group. 

**Weighted Image**
With the generated image of linear-fit left and right lane lines, we then must only combine the original input image with the generated lane line image. 

![final_img](https://user-images.githubusercontent.com/22439612/59167140-a3bde180-8afd-11e9-986a-7ccfc20da264.png)

**Generating Linear-fit Left and Right Lane Lines**

It was a challenge to determine which lines belong to the left or right group. I used a simple trick to group them. The line belongs to the left group if the slope is negative. If the slope is positive, it must belong to the right group. The lines without sufficient extreme slope that is less than 0.5 are discarded. For extrapolating the grouped lines, I used the top y value as the middle of the image and the bottom y value as bottom of the image. Now the challenge was to find the corresponding x values. I used numpy's poly1d function for obtaining the top and bottom x values. These (x, y) pairs were the beginning and end of the line segments that could then be drawn.

### 2. Identify potential shortcomings with your current pipeline

So the current pipeline functions satisfactorily because of the following assumption

1. The camera always has the same position with respect to the road
2. There is always a visible white or yellow line on the road
3. We don't have any vehicle in front of us
4. We consider highway scenario with good weather conditions (good lighting with no shadows)

If any of the above assumptions are violated, the pipeline will perform badly.

Also the straight lines do not work when there are curves on the road.


### 3. Suggest possible improvements to your pipeline

1. Update the ROI mask dynamically
2. Use the information from previous frames to smoothen the lines that we trace on the road and take corrective steps, for egs, if the new line computed at frame N deviates disproportionately from the mean of line slopes and intercepts we computed from frames [0, N-1], we can use the information to correct it and avoid any abrupt errors (jitters).

