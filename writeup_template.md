# **Behavioral Cloning** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/autonomus_track_1.png "Autonomous Track 1"
[image2]: ./output-video/2019_05_28_05_45_17_868.jpg "Output Image"
[image3]: ./examples/nvidia.png "Nvidia Model Architecture"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* video.mp4 containing the recording of autonomous driving on the first track using my model
* writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code

First of all, the model is trained to generate the model.h5 file with the help of following command. model.py file contains the code to train the model.

python model.py

Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing:

python drive.py model.h5

After the car successfully steers through the track, the video of the driving behavior can be formed by producing various frames and saving that frames in the output-video folder, by executing the following command. The fourth argument, output-video, is the directory in which to save the images seen by the agent. If the directory already exists, it'll be overwritten.

python drive.py model.h5 output-video

After all the frames of the car driving in the simulator are saved in the output-video folder, the video can be made by combining all the frames with the use of following command. It creates a video based on images found in the output-video directory. The name of the video will be the name of the directory followed by '.mp4'.

python video.py output-video

Optionally, we can specify the FPS (frames per second) of the video. The default is 60 fps.

python video.py output-video --fps 48

![alt text][image1]

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

I have used a powerful network given by NVIDIA (model.py lines 47-71) suggested in the lectures. This architecture uses a normalization layer at the bottom using a Keras lambda layer followed by 5 convolution layers and 4 fully connected layers after that. I have also cropped the upper sky and trees portion from the images before feeding them into the network.

![alt text][image3]

#### 2. Attempts to reduce overfitting in the model

The model showed the cases of overfitting and the car got out of track so I have trained my model including dropout layer.(code line-63)

The model was trained and validated on different data sets (code line 43-44). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 75).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used data provided by Udacity and was able to have good results with autonomous driving of the car. The car is moving on the road in autonomous mode without deviating much towards the edges and recovering itself back to center when deviated. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

I used the NVIDIA network architecture provided in the Udacity lectures. As this architecture has already proven its worth before and was giving good results in my case too, I decided to go with it without any modifications.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my model had a low mean squared error on both the training and validation set. This implied that the model was working fine.

The final step was to run the simulator to see how well the car was driving around track one. There were some spots where the vehicle fell off the track when I was trying to feed whole data at once to train. To improve the driving behavior in these cases, I used generator to train my model in batches and with epochs=1.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to take decisions when the road is not visible to the camera.

The out-put images are avaialble here:
/output-video

The output Video is available here:
output-video.mp4

I have also tried to run simulator in my local machine and collected data,which are stored in /opt/data_csv. Images are stored in /opt/data_csv/images folder and csv file is stored at /opt/data_csv/data_csv.log.