# **Finding Lane Lines on the Road** 


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps. 

1. Create a copy of the input image.

![org_img](https://user-images.githubusercontent.com/22439612/59164523-13bb7000-8adc-11e9-9a47-6968029ccdf6.png)

2. Convert the image into HLS Color Space (Choosing this color space rather than grayscale can help with detections of non-white lane lines). 

![hls_img](https://user-images.githubusercontent.com/22439612/59164538-52512a80-8adc-11e9-8576-9bc33e856931.png)

3. Normalize the hls image values.

![norm_img](https://user-images.githubusercontent.com/22439612/59164558-8f1d2180-8adc-11e9-86fd-931601f23a88.png)


4. Apply a Gaussian blurring filter or kernal size 5. (for avg effect)

![blur_img](https://user-images.githubusercontent.com/22439612/59164569-a3611e80-8adc-11e9-9fd0-79c8ede82fd2.png)

5. Apply a Canny edge detector.

![canny_img](https://user-images.githubusercontent.com/22439612/59164564-99d7b680-8adc-11e9-990a-fc9955f647b6.png)


6. Find the specific region of interst via cropping.
7. Apply a Hough transform on the cropped edge points image.
8. Use the returned Hough line list to actually generate a line image for the left and right lanes with a linear fit for each line group.
9. With the generated image of linear-fit left and right lane lines, we then must only combine the original input image with the generated lane line image.

![final_img](https://user-images.githubusercontent.com/22439612/59164575-a956ff80-8adc-11e9-8e00-aad48bfd54cb.png)

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
