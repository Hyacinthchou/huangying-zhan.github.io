---
layout: post
title:  "ZED Stereo Camera Setup and Practice on Jetson TK1"
date:   2016-08-23
categories: Technical
tags: [Jetson TK1, ZED Camera]
---

### Summary

As the name given, ZED Stereo Camera(ZED) is a stereo camera produced by [Steteolabs](https://www.stereolabs.com/). Basically, ZED is able to capture high-resolution pictures and depth perception. For details, please refer to the official website. In this article, the installation and a simple practice example of ZED is provided. Again, all the produces are based on Ubuntu 14.04.

### Contents

1. [Setup of ZED on TK1](#Setup of ZED camera)
2. [Capture picture and depth map](#Capture picture and depth map)

___
<a name = "Setup of ZED camera"></a>
### Part 1. Setup of ZED camera

The installation of ZED on TK1 is actually quite straightforward. The [official instruction: TK1 & ZED](https://www.stereolabs.com/blog/index.php/2015/09/24/getting-started-with-jetson-tk1-and-zed/) is well written. Just follow the steps and everything should be done. Here is a quick summary for all steps. 

*Requirement: (refer to [here](https://huangying-zhan.github.io/2016/08/15/Caffe-installation-and-practice-on-Jetson-TK1.html#title4))*

* CUDA 6.5 R.21
* openCV4tegra 2.4.10

Now, let's start setup the ZED camera!

1. Enable USB3.0
	
    ZED Camera requires a USB3.0 port. TK1 has only one USB3.0 port. Make good use of it~

    ```
    sudo vi /boot/extlinux/extlinux.conf
    # Replace ‘usb_port_owner_info=0‘ by ‘usb_port_owner_info=2‘.
    # Save and exit (*:wq*)
    ```

2. Download and install ZED SDK for Jetson

	Visit [ZED download page](https://www.stereolabs.com/developers/#download_anchor) and download ZED SDK for Jetson, which is a *.run* file
    
    ```
    chmod +x ZED_SDK_JTK1_v*.run
	./ZED_SDK_JTK1_v*.run
    # Accept the statement and follow installation instruction.
    ```

	Now, ZED SDK should be installed and there are many interesting demos. The SDK is installed at `/usr/local/zed` by default. However, before running these examples, you might encounter a problem, there is only one USB port on TK1. It is not enought for your keyboard, mouse, and ZED. Unless you have a USB3.0 hub, you need [remote control](https://huangying-zhan.github.io/2016/09/13/Linux-cheat-sheet.html#Remote) TK1 from your computer. 

<br></br>
___

<a name="Capture picture and depth map"></a>
### Part 2. Capture picture and depth map

#### 2.1. Summary
To study ZED, we can learn from it's [blog examples](https://www.stereolabs.com/blog/) or study the [Github examples](https://github.com/stereolabs). Basically, the examples are the same, blog examples provide more detailed explanations but some parts of the code are quite outdated. The reason is that ZED released Ver.1.0 and made some changes. The blog examples were written before Ver.1.0. Nevertheless, Github examples provide update codes. In summary, study both at the same time should be more efficient. 

#### 2.2. Hello World
Before jumping to the later content. A simple ["Hello-world" example](https://www.stereolabs.com/blog/index.php/2015/07/15/hello-world/) is suggested to be implemented by yourself first. Follow the instruction and build a Hello-World program. However, as I mentioned before, the blog examples are quite outdated. Please use this [main_hello_world.cpp](/home/jzhan/github/huangying-zhan.github.io/public/post_resource/Technical/ZED_stereo_camera_setup_and_practice_on_Jetson_TK1/main_hello_world.cpp) and [CMakeLists.txt](/home/jzhan/github/huangying-zhan.github.io/public/post_resource/Technical/ZED_stereo_camera_setup_and_practice_on_Jetson_TK1/CMakeLists.txt) to build the program. Remember to rename *main_hello_world.cpp* to *main.cpp*.

#### 2.3. Capture pictures and depth maps
Suppose you have built your `Hello World`. In this part, we will see a simple modification based on a ZED's [OpenCV example](https://github.com/stereolabs/zed-opencv). The ultimate goal is to capture RGB pictures and their corresponding depth map from time to time. First, let's have a taste on the original example.

```
cp /usr/local/zed/sample/cpu/with\ OpenCV ~/Desktop/zed_capture #copy and rename the example to desktop
cd $zed_capture # For simplicity, $zed_capture represents the full directory of /zed_capture
mkdir build
cd build
cmake ..
make # If you can see "Linking CXX executable "ZED with OpenCV" ", the program is built sucessfully
./ZED\ with\ OpenCV
```

Play around with the program first. Then, download and rename [main_capture.cpp](/home/jzhan/github/huangying-zhan.github.io/public/post_resource/Technical/ZED_stereo_camera_setup_and_practice_on_Jetson_TK1/main_capture.cpp) as *main.cpp*.
Now, replace the original *main.cpp* by this new *main.cpp* and build the program again.

```
cd $zed_capture/build
make
./ZED\ with\ OpenCV
```

This program allows you to save images, disparity images and depth maps from time totime. However, there are some settings you can modify in the *main.cpp*. Please refer to *main setup parameters* at the beginning of the code. After modification, you have to build the program again.



### Reference


[official blog: TK1 & ZED](https://www.stereolabs.com/blog/index.php/2015/09/24/getting-started-with-jetson-tk1-and-zed/)    