# WORK FLOW
End goal : do the training (retrain the custom data) and inference  on nano to detect the smoke and let ppl know where it's ther fire (simultaneously fire the alarm)and notify the firefighter cuz they have no tech to change the game



PATH1 : Digits[cloud platform ,kunetes] (make step by step tutorial)
- We use digits to do the training and test the inference on digits (30secs) [we use semantic segmation algortihm ,caffee model] we can change model or add layer
1. we put the Dataset from drone and we can distinguishh the sky and lrerrin
2.now we are trying feed the smoke data and label it to train and let it detect smoke in DIGITS(smoke and not smoke)60 pics

3.use the smoke data provided by researcher (solve label problem automatically,modify the layer text,come up with different scence for smoke) --label automatically and let ppl correct it manually create an UI(find a javascipt guy or snokel) 
Use motion_estimation to detect the smoke[to track smoke behavior] https://github.com/ross-abaco/rtp-motion-estimation/blob/master/demos/motion_estimation/motion_estimation_user_guide.md
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

ps.record how tousde kubernetes


# use DIGITS to train and run on Jeston nano (you can test your own data )
https://github.com/dusty-nv/jetson-inference
ps. download and extract the trained model snapshot to Jetson (snapshot is in job)
NET = snapshot folder , png = your own data
segnet-console north_firecam_720.png output_firetower.png --prototxt=$NET/deploy.prototxt --model=$NET/snapshot_iter_4522.caffemodel --labels=$NET/fpv-labels.txt --colors=$NET/fpv-deploy-colors.txt --input_blob=data --output_blob=score_fr
use custom dataset to train models in digits (you can also test inference on digits)

 記得操作的時候要show圖片的那格打勾，然後路徑選對

# data provided by researcher
http://hpwren.ucsd.edu/HWB/HPWREN-FIgLib/20180717-otay-om-s-mobo-c/
https://github.com/byungheon-jeong/HPWREN-data

# Data-preprocess : Label tool
snorkel : https://github.com/HazyResearch/snorkel


# plan
poster
powerpoint
pragma conference

