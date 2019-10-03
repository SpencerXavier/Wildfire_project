# WORK FLOW
## End goal :

The Goal of this project is using [tensorflow 2.0.0 beta version]('https://www.tensorflow.org') and NVIDIA deep learning tools -- [DIGITS](https://github.com/NVIDIA/DIGITS),to Get Started training DNNs and deploying them into the edge computer that we can put inside the camera, which is [Jetson Nano/TX1/TX2/Xavier](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/), to  detect the smoke by itself. Once it detect the smoke, the alarm we set up inside the camera will notify the 911 department in time and prevent tragedy happening.


## Process :
This project is using two different path to implement it. The first Path is using deploy DIGITS in [kubernetes](https://kubernetes.io) combine the Semantic Segmentation with SegNet to do the training and deploy into Jetson Nano/TX1/TX2/Xavier. The following guide will help you go through the process step by step.

- Before we begin, we use the following commands to access into our Digits
     . kubectl get pod -n digits
     . kubectl exec -it -n digits digits(namespace) bash

1. Fisrt, we dig into what semantic segmantation is and download Aerial Drone Test Dataset.(we put the Dataset from drone and we can distinguishh the sky and terrain)
     1. [Semantic Segmentation with SegNet](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-dataset.md)
     2. [Downloading Aerial Drone Test Dataset](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-dataset.md#downloading-aerial-drone-dataset)
     3. while there are some slight difference in our data path:
     - Feature image folder: /home/digits/NVIDIA-Aerial-Drone-Dataset/FPV/SFWA/720p/images
     - Label image folder: /home/digits/NVIDIA-Aerial-Drone-Dataset/FPV/SFWA/720p/labels
     - Class labels: /home/digits/NVIDIA-Aerial-Drone-Dataset/FPV/SFWA/fpv-labels.txt
     - Color map file: /home/digits/NVIDIA-Aerial-Drone-Dataset/FPV/SFWA/fpv-training-colors.txt

2. Second, we generate pretrained FCN-Alexnet and Training FCN-Alexnet with DIGITS
     1. [Generating Pretrained FCN-Alexnet](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-pretrained.md)
     2. [training FCN-Alexnet with DIGITS](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-training.md)
     3. Remember to select the visualize image segmentation to image segmentation and click the bottom to show the visualization and statistics
     4. ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/1.png)
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/2.png)
        <img src="/Users/spencer/Desktop/UCSD-backtoschool/1.png"/>  

3. third, download and extract the trained model snapshot to Jetson (snapshot is in job folder)
     1. [FCN-Alexnet Patches for TensorRT](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-patches.md)
     2. [Running Segmentation Models on Jetson](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-console.md)
     3. Remember to change NET variable, NET = snapshot folder , png = your own data
segnet-console north_firecam_720.png output_firetower.png --prototxt=$NET/deploy.prototxt --                  model=$NET/snapshot_iter_4522.caffemodel --labels=$NET/fpv-labels.txt --colors=$NET/fpv-deploy-colors.txt --input_blob=data --    output_blob=score_fr


4. We use 60 [smoke images](https://github.com/aiformankind/wildfire-smoke-detection/tree/master/input/images) as our custom datas set to do the step 1-3 to train our network and test on DIGITS and Jetson.
     1. dataset : 
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/smoke_dataset-1.png)
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/smoke_dataset-2.png)
     2. model :
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/smoke_model.png)
     3. test data:
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/smoke_test-1.png)
        ![avatar](/Users/spencer/Desktop/UCSD-backtoschool/smoke_test-2.png)
       

5. We are trying to label the data provided by Hp-wren to repeat step 1-3 to train our network better which is still ongoing.
     1. [Data provides by Hpwren](http://hpwren.ucsd.edu/HWB/HPWREN-FIgLib/20180717-otay-om-s-mobo-c/) is now on this github page(https://github.com/byungheon-jeong/HPWREN-data)


PATH2 : KERAS (USE tensorflow 2.0) is still ongoing
- use keras to run it do the same thing



