
整個文章大概是 1. 目的 2. 實驗環境 3. 程式執行 4. 結果  5. 結論

# Qt Mainmoil CUDA with ALPR

## 1. Purpose

Base on MOIL fisheye imaging, we hope to extend the MOIL application on ALPR( Automatic number-plate recognition )

<img src="lab/p001.jpg">
基於 MOIL 魚眼技術應用於 車牌辨識，以達到大角度同時多個車牌辨識

## 2. Testing environment

攝影機與車輛模型 車牌產生

One Raspberry Pi with a 220 degree fisheye camera, wirelessly connected to A PC running Ubuntu 18.04.


## 3. Software Running

### 3.1 Raspberry Pi Camera

The first step is to prepare a Raspberry Pi camera,

reference the repo,

https://github.com/yourskc/rpi_camera

check the IP address for later use.

```sh
ifconfig
```
enable the camera,

```sh
raspi-config
```

 then run the python script to start the streaming server

```sh
git clone https://github.com/yourskc/rpi_camera.git
cd rpi_camera
python rpi-camera.py
```



then you can enter the address in browser of another PC

> http://192.168.xx.xx:8000


### 3.2 Qt_Mainmoil_Cuda

We then run MOIL application qt_mainmoil_cuda  ( Repo : qt_mainmoil_cuda, it's a privtae

repository, please email me if you need the previledge )


We need to set the camera source from IP camera instead of the default USB camera, please

set the FORCE_CAMERA_USB to false in the mainwindow.cpp

<img src="programguide/p001.png">

Run the Qt Application, then enter the above address of the Raspberry Pi camera. for my case,

http://192.168.0.68:8000/stream.mjpg

<img src="programguide/p002.png">

Let's start record a video clip, press "Record" button to start/stop a recording

The recorded video should be a fisheye video, like this one

<a href="fisheye/220/moil_alpr_220.mp4">
<img src='fisheye/220/moil_alpr_220.jpg' width='300px'></a>

The above video clip can be loaded into MOIL application again,

<img src="snapshot/s00.jpg">

.

You can browse to any direction while playback the video clip.

We'll take some snapshots in the interested angles, and perform the Text recognition

in the next step.



### 3.3 AWS Rekognition for Text Recongnition

Since the ALPR is different with normal Text recongnition, the Fonts of license plate  

由於車牌字型與文件一般使用字型有所不同，自行訓練真實車牌 Model 需要大量影像樣本與時間，本實驗為快速驗證，後半部處理採用 AWS Rekognition 技術，可以得到較佳之辨識結果。

See the python program in the directory

modify the config file according to your AWS IAM keys.

Please reference to

xxxxx

cd AWS_rekog
python3





















設定

1. 影像來源
Raspberry Pi 4B+
220 degree camera

電腦設定

1. Conditional Compile
2. 設定影像來源


AWS rekognition

設定


結果


結論
