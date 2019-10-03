# WORK FLOW
## End goal :

The Goal of this project is using [tensorflow 2.0.0 beta version]('https://www.tensorflow.org') and NVIDIA deep learning tools -- [DIGITS](https://github.com/NVIDIA/DIGITS),to Get Started training DNNs and deploying them into the edge computer that we can put inside the camera, which is [Jetson Nano/TX1/TX2/Xavier](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/), to  detect the smoke by itself. Once it detect the smoke, the alarm we set up inside the camera will notify the 911 department in time and prevent tragedy happening.


## Process :
This project is using two different path to implement it. The first Path is using deploy DIGITS in [kubernetes](https://kubernetes.io) combine the Semantic Segmentation with SegNet to do the training and deploy into Jetson Nano/TX1/TX2/Xavier. The following guide will help you go through the process step by step.

1. Fisrt, we dig into what semantic segmantation is and download Aerial Drone Test Dataset.
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

3. Last, download and extract the trained model snapshot to Jetson (snapshot is in job folder)
     1. [FCN-Alexnet Patches for TensorRT](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-patches.md)
     2. [Running Segmentation Models on Jetson](https://github.com/dusty-nv/jetson-inference/blob/master/docs/segnet-console.md)
     3. NET = snapshot folder , png = your own data
segnet-console north_firecam_720.png output_firetower.png --prototxt=$NET/deploy.prototxt --                  model=$NET/snapshot_iter_4522.caffemodel --labels=$NET/fpv-labels.txt --colors=$NET/fpv-deploy-colors.txt --input_blob=data --    output_blob=score_fr




PATH1 : Digits[cloud platform ,kunetes] (make step by step tutorial)
- We use digits to do the training and test the inference on digits (30secs) [we use semantic segmation algortihm ,caffee model] we can change model or add layer
1. we put the Dataset from drone and we can distinguishh the sky and lrerrin
2.now we are trying feed the smoke data and label it to train and let it detect smoke in DIGITS(smoke and not smoke)60 pics

3.use the smoke data provided by researcher (solve label problem automatically,modify the layer text,come up with different scence for smoke) --label automatically and let ppl correct it manually create an UI(find a javascipt guy or snokel) 
Use motion_estimation to detect the smoke[to track smoke behavior] 
https://github.com/ross-abaco/rtp-motion-estimation/blob/master/demos/motion_estimation/motion_estimation_user_guide.md
https://github.com/ross-abaco/rtp-motion-estimation
https://developer.ridgerun.com/wiki/index.php?title=Xavier/JetPack_4.1/Components/VisionWorks

4.run the motion vector algorithm to see moving smoke and observe their behavior(addoition annotation see if it's from fire based on weather,wind) and different and find the distance on smoke (joseph)

5. run the model on jeston nano(edge device) to do inference(2 mins)

6.Data simulation :fresh information to continue on progress in simulation (time line) live training like 氣象播報


------------------
PATH2 : KERAS (USE tensorflow 2.0)
- use keras to run it do the same thing

PATH3 : UC Berkeley;s algorithm 
-build a container and storage place and use UC Berkeley;s algorithm 


# kubernetes backend monitor
https://grafana.nautilus.optiputer.net/d/85a562078cdf77779eaa1add43ccec1f/k8s-compute-resources-namespace-w-variable-averaging?orgId=1&refresh=10s&var-datasource=prometheus&var-namespace=wifire&var-avg=30m

Pod 是 Kubernetes 的最小工作单元。每个 Pod 包含一个或多个容器。Pod 中的容器会作为一个整体被 Master 调度到一个 Node 上运行。
Cluster 是计算、存储和网络资源的集合，Kubernetes 利用这些资源运行各种基于容器的应用。
Master 是 Cluster 的大脑，它的主要职责是调度，即决定将应用放在哪里运行。Master 运行 Linux 操作系统，可以是物理机或者虚拟机。为了实现高可用，可以运行多个 Master。
node 的职责是运行容器应用。Node 由 Master 管理，Node 负责监控并汇报容器的状态，并根据 Master 的要求管理容器的生命周期。Node 运行在 Linux 操作系统，可以是物理机或者是虚拟机。


ps.record how to use kubernetes
ps.  #Copy /tmp/foo local file to /tmp/bar in a remote pod in a specific container
     kubectl cp /tmp/foo <some-pod>:/tmp/bar -c <specific-container>
ps.kubectl cp ~/Desktop/1  digits-66cd96f7c6-kzfkr:/home/digits  



# use DIGITS to train and run on Jeston nano (you can test your own data )
https://github.com/dusty-nv/jetson-inference


use custom dataset to train models in digits (you can also test inference on digits)


 
 
# data provided by researcher
http://hpwren.ucsd.edu/HWB/HPWREN-FIgLib/20180717-otay-om-s-mobo-c/
https://github.com/byungheon-jeong/HPWREN-data

# Data-preprocess : Label tool
snorkel : https://github.com/HazyResearch/snorkel


# plan
poster
powerpoint
pragma conference


# waymo for large data sets
https://waymo.com/open

