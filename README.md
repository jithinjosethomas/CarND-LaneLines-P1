# **Finding Lane Lines on the Road** 


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps. 

1. Create a copy of the input image.
2. Convert the image into HLS Color Space (Choosing this color space rather than grayscale can help with detections of non-white lane lines). 
3. Normalize the hls image values.
4. Apply a Gaussian blurring filter or kernal size 5. (for avg effect)
5. Apply a Canny edge detector.
6. Find the specific region of interst via cropping.
7. Apply a Hough transform on the cropped edge points image.
8. Use the returned Hough line list to actually generate a line image for the left and right lanes with a linear fit for each line group.
9. With the generated image of linear-fit left and right lane lines, we then must only combine the original input image with the generated lane line image.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
