#**Finding Lane Lines on the Road**
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


1. The pipeline
---

1. turned image to hsv

![title](test_images/figure_1.png)

2. filtered it with white only

![title](test_images/figure_2.png)

3. applied gaussian blur

![title](test_images/figure_3.png)

4. applied canny edge detection

![title](test_images/figure_4.png)

5. defined region of interest

![title](test_images/figure_5.png)

6. setup hough lines & laid them over

![title](test_images/figure_6.png)

7. extrapolated lines in draw_lines

    8. got the slope and length of each line
    9. separated lines into right and left based on slope being negative or positive
    10. if slope was between 0.4 and -0.4, meaning too shallow, the line was discarded
    11. if the slope's absolute value was greater than 0.9 it was also discarded
    12. added x's and y's and slopes and lengths to it's own list
    13. calculated a weighted slope based on the length of the line
    14. calculated the change in percentage of the previous slope with current slop
    15. if previous slope was great than 1.5 percent for either lane, it was discarded
    16. then took the remaining x's in the right and left lane and ran a polynomial fit
    17. then averaged out the current x's with the previous x's so the transition is smoother
    18. then showed the line
    19. if any of the parameters failed, the previously cached line was shown

    ![title](test_images/figure_7.png)

Potential shortcomings
---

- it will definitely not work with the challenge currently
- it does not work for rain and dust
- it does not work well with curved roads
- it does not work so well when there are a lot of different color marked lanes
- it does not work when there are no lanes in the road (dirt road, etc.)
- it does not work well on hills or any sort of severe vertical curverature
- it does not work well at night (it's dark)
- it does not work well when light is shining right at the vehicle
- it does not work well when other vehicles, cars, bikes, people are covering the lanes.

Possible improvements in the future
---

- use EKF or particle filtering instead
- use RANSAC to make better guesses of lane lines
- multi-dimensional poly fit for curved lines, currently only linear approx.
- find better hough line parameters
- use IR camera for night time lane detection
- use multiple cameras to get a better sense of where the lanes are
