## Project: Search and Sample Return

#### Email:sychaichangkun@gmail.com
#### Slack:@chaichangkun
---



**The goals / steps of this project are the following:**  

**Training / Calibration**  

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook).
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands.
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.  

[//]: # (Image References)

[image1]: ./sample.png
[image2]: ./sample2.png

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!
### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (either data you recorded or the test data provided). Add/modify functions to allow for color selection of obstacles and rock samples.

I have run, added and modified functions in the file. My dataset is recorded in folder ./my_dataset2.

The way to select obstacles, rocks and navigable area are as follows:
* Set color_threshold to be (160, 160, 160) as default which is the navigable area. (line 3-15 in color_threshold block)
* Set obstacle_threshold to be (0, 160, 0, 160, 0, 160) which means the whole picture is obstacle excluding the navigable area and the black area. That is the color of the obstacles.(line 17-30)
* Set rock_threshold to be (130, 180, 100,170,0,30) the as same way rock_threshold does.(line 32-44)

As is shown in the pic below, the obstacle is red and the navigable area is green.
![alt text][image1]


#### 2.Populate the process_image() function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap. Run process_image() on your test data using the moviepy functions provided to create video output of your result.
A video is created ./output/test_mapping.mp4

You can see the navigable terrain and obstacles are plot in the worldmap when the rover goes to anywhere.
![alt text][image2]

The process_image() does as follows:
* Use color theshold to detect obstacles, rocks and navigable area. (line 11-13)
* Convert there pictures into rover-centric and then into world coordinates. (line 16-18)
* Plot obstacles, rocks and navigable area on worldmap, in red, blue, green seperately. (line 24-37)


### Autonomous Navigation and Mapping

#### 1. Fill in the perception_step() (at the bottom of the perception.py script) and decision_step() (in decision.py) functions in the autonomous mapping scripts such that your rover can navigate and map autonomously. Explain how you did this in your writeup and discuss your results.

The way to autonomous mapping is much like process_image() does:
* Select the navigable, obstacle and rock area and their pixels (line 110-112)
* Convert the pixels into world coordinates. (line 122-130)
* Plot the coordinates with different color. (line 135-137)

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

1.I spent much time on map the navigable and obstacles onto the original map. The function pix_to_world cannot appropriately convert corrdinates and I modified the way to get yaw. Then it works.

2.I hope to add the pick function in decision.py but I have no idea how to send the 'pick' command.
To avoid being stuck, I followed Luqiang's method, adding a new variable to count the stoptime. If the stoptime exceeds a threshold, the rover will rotate clockwise.


3.The thesholded image should be displayed in the Roversim program, but I didn't see anything. After setting the Rover.vision_image to be 255 times of binary image, I could see the vision image on the bottom left.
