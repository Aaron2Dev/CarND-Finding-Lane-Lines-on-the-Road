**Finding Lane Lines on the Road**

In this project I create a pipeline which identifies lanes in roadimages.
A example for a possible input image is shown below.

[//]: # (Image References)

[solidWhiteCurve]: ./solidWhiteCurve.jpg "solidWhiteCurve"
[gray]: ./gray.JPG "gray"
[masked]: ./masked.JPG "masked"
[canny]: ./canny.JPG "canny"
[RoI]: ./RoI.JPG "RoI"
[Hough_lines]: ./Hough_line.JPG "Hough_lines"
[weighted]: ./weighted.JPG "weighted"

![alt text](solidWhiteCurve)


---
**The Pipeline**

This Pipeline works for images, but I will apply it to videos also. It can recognize white and yellow lanes on the road.
The pipeline consist of the following steps:

1. Convert image to grayscale
![alt text](gray)
2. Define color masks
I define color masks in the color_mask() function. In order to get the yellow parts of the image, I convert from RGB to HSV.
In HSV space it`s easier than in RGB space to filter out the yellow parts of the image.
The thresholds for yellow were set to lower_yellow = [20, 100, 100] and upper_yellow=[40, 255, 255].

![alt text](masked)

3. Use the canny algorithm for edge detection
![alt text](canny)
4. Apply a Gaussian blurring
Its important to blur after the edge detection. The edge detection performs worse in a blurred image.

5. Define a Region of Interest (RoI)
![alt text](RoI)

6. Use Hough line detection Algorithm
![alt text](Hough_line)

7. Draw the lines in the initial input image
I modified the draw_lines function from the openCV Tutorial on Hough lines (https://docs.opencv.org/3.4.0/d9/db0/tutorial_hough_lines.html).

![alt text](weighted)


### 2. Shortcomings


One potential shortcoming would be the definition of the Region of Interest (RoI). in evry picture I used a constant RoI, which is fine for the given data.
For the case of more shifted lines on the road, one has to create a function for calculating the RoI.

Another shortcoming could be 


### 3. Possible improvements

A possible improvement would be to optimize the parameters for the Hough line Transformation. I see potential improvements in adjusting the min and max line gap. 

