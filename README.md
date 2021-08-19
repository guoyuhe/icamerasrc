# icamerasrc

This repository supports MIPI cameras through the IPU6/IPU6EP on Intel Tigerlake/Alderlake platforms. There are 4 repositories that provide the complete setup:

* https://github.com/intel/ipu6-drivers - kernel drivers for the IPU and sensors
    * branch for Intel Tigerlake: master, branch for Intel Alderlake: ccg_plat_adlp
* https://github.com/intel/ipu6-camera-hal - HAL for processing of images in userspace
    * branch for Intel Tigerlake: master, branch for Intel Alderlake: ccg_plat_adlp
* https://github.com/intel/ipu6-camera-bins - IPU firmware and proprietary image processing libraries
    * branch for Intel Tigerlake: master, branch for Intel Alderlake: [ccg_plat_adlp](https://github.com/intel/ipu6-camera-bins/tree/ccg_plat_adlp)
* https://github.com/intel/icamerasrc (branch:icamerasrc_slim_api) - Gstreamer src plugin


## Content of this repository:
* gstreamer src plugin 'icamerasrc'

## Build instructions:
* Prerequisites: ipu6-camera-bins and ipu6-camera-hal installed 
* Prerequisites: libdrm-dev

```
 export CHROME_SLIM_CAMHAL=ON
 export STRIP_VIRTUAL_CHANNEL_CAMHAL=ON

 ./autogen.sh 
 make
 sudo make install
```
 
## Pipeline examples
* Testpattern generator (no sensor)
```
sudo -E gst-launch-1.0 icamerasrc device-name=tpg_ipu6 ! video/x-raw,format=YUY2,width=1280,height=720 ! videoconvert ! xvimagesink
```

* Sensor ov01a1s
```
sudo -E gst-launch-1.0 icamerasrc device-name=ov01a1s-uf ! video/x-raw,format=YUY2,width=1280,height=720 ! videoconvert ! xvimagesink
```

* Sensor hm11b1
```
sudo -E gst-launch-1.0 icamerasrc device-name=hm11b1-uf ! video/x-raw,format=YUY2,width=1280,height=720 ! videoconvert ! xvimagesink
```

* Sensor ov8856
```
sudo -E gst-launch-1.0 icamerasrc device-name=ov8856-wf ! video/x-raw,format=YUY2,width=1280,height=720 ! videoconvert ! ximagesink
```