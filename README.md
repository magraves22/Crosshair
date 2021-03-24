# Crosshair - Computer Vision Based Aimbot

This project is meant to create a computer vision based aimbot and document the process of how it was created.

## Set Up:
This section is an attempt to describe and document the use of a static version of yolo-darknet including its dependencies. This readme will walk through the steps needed to run and compile darknet with OpenCV and CUDA support on Linux (specifically Ubuntu 18.04).

This process was done on Ubuntu 18.04 using a GTX1660 Super GPU.

### Notes: 
Please read through this readme in its entirety before beginning installation as this process is a massive headache that you will likely need to attempt multiple times. 

The best tutorial that I found for the installation process was [here](https://towardsdatascience.com/getting-your-machine-ready-to-use-yolov3-object-detector-on-ubuntu-18-04-185799ebc18d). This article does a good job of taking you through all of the steps required to install all of darknets dependencies, but some of the information was a little out of date. This was due in part to the fact that the darknet source code has changed sincec the article was published. to combat any changes in source code, I have downloaded a zip file of the most recent version of darknet as of 3-20-2021 and am including it along with its readme files.

## OpenCV: 
All of the information in [Adrian Rosebrock's Tutorial](https://www.pyimagesearch.com/2018/05/28/ubuntu-18-04-how-to-install-opencv/) worked flawlessly. This was actually the easiest part of the entire process. If you are running a different operating system.

## CUDA and cuDNN:
Note: When running any of the commands in this script you will need to replace cuda-10.1 with cuda-11.2

As pointed out in the how-to article [These](https://gist.github.com/Mahedi-61/2a2f1579d4271717d421065168ce6a73) instructions were very helpful. The version of darknet packaged with this explanation, however, does not support CUDA 10.1. I believe it would work with CUDA>=11.0, but I used 11.2.2 for this project. I skipped lines 34-41 in favor of downloading CUDA from the [NVIDIA website](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal) and runnung the installation commands that they provided. Additionally, I chose to manually download cuDNN from [here](https://developer.nvidia.com/rdp/cudnn-download) as you need to create an account with the website before being able to download and it just ended up being easier. Finally line 60 will need to be changed to read like this:

sudo cp -P cuda/include/cudnn*.h /usr/local/cuda-11.2/include

This has to do with a change between cuDNN 10 and cuDNN 11

## Training:
If you have made it this far this is the easy part and the training instructions in the darknet repo should have been easy enough to follow. This far I have trained 4 decently performing models that can be found in the weights folder. between training the regular and Tiny versions of Yolo I discovered the -map command. I will return to the regular yolo implementations to attempt to calculate their mAp scores.

## Initial Testing:
A first test on real video of CS:GO gameplay can be found [here](https://youtu.be/EPIVAnANO1I). As can be seen the model has some quirke but I believe that a number of those can be corrected by adjusting the threshold. It should also be noted that although the video quality looks poor, this is because yolo, scales the image to a 416x416 pixel grid to reduce computational requirements. If you would like to read up on the implementation of Yolo I would suggest starting [here](https://pjreddie.com/darknet/yolo/)

## Next Steps:
Next steps for this project include either finding some library to deploy darknet or converting the darknet model to tensorflow. This model will be wrapped in a python or c++ program to run on top of CS:GO.