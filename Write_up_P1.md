**Finding Lane Lines on the Road**

In this project I create a pipeline which identifies lanes in roadimages.
A example for a possible input image is shown below.

[//]: # (Image References)
![alt text](solidWhiteCurve.jpg "solidWhiteCurve")


---
**The Pipeline**

This Pipeline works for images, but I will apply it to videos also. It can recognize white and yellow lanes on the road.
The pipeline consist of the following steps:

1. Convert image to grayscale.

![alt text](gray.JPG "gray")

2. Define color masks.
I define color masks in the color_mask() function. In order to get the yellow parts of the image, I convert from RGB to HSV.
In HSV space it`s easier than in RGB space to filter out the yellow parts of the image.
The thresholds for yellow were set to lower_yellow = [20, 100, 100] and upper_yellow=[40, 255, 255].

![alt text](masked.JPG "masked")

3. Use the canny algorithm for edge detection.

![alt text](canny.JPG "canny")

4. Apply a Gaussian blurring.
Its important to blur after the edge detection. The edge detection algorithm performs worse in a blurred image.

5. Define a Region of Interest (RoI).

![alt text](RoI.JPG "RoI")

6. Use Hough line detection Algorithm. I used the probabilistic Hough transformation. The output is a line in the form (x1,y1,x2,y2). (x1,y1) and (x2,y2) are the end points of the line.
These lines are the input for the draw_lines() function.

![alt text](Hough_line.JPG "Hough_lines")

7. Draw the lines in the initial input image.
I modified the draw_lines function from the openCV Tutorial on Hough lines. (https://docs.opencv.org/3.4.0/d9/db0/tutorial_hough_lines.html)
The draw_lines() function calls cv.line() with the argument cv2.LINE_AA, which specifies the type of the line.

![alt text](weighted.JPG "weighted")


### 2. Shortcomings


One potential shortcoming would be the definition of the Region of Interest (RoI). In every picture I used a constant RoI, which is fine for the given data.
For the case of different road images, one has to create a function for calculating the RoI.


### 3. Possible improvements

A possible improvement would be to optimize the parameters for the Hough line Transformation. I see potential improvements in adjusting the min and max line gap.
Also one could think of applying more color masks to the image.

