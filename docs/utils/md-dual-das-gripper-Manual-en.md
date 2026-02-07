[简体中文](./md-dual-das-gripper-Manual-zh.md) | English

# Data Collection Guide for Dual Hands V1.0

## Notes

**(1) During pairing, ensure the USB connection is secure. Use straps to minimize tension on the USB ports during collection. If the pairing indicator on the recording interface flickers or disappears, it indicates an unstable USB connection (refer to the fixation solution provided by Genrobot)**

**(2) After successful pairing, use the record button on the left-hand device to initiate recording operations.**  
**(3) During the actual data collection, please ensure that both devices are facing the same spot when starting the collection. Wait for 1 second in a stationary state before beginning the collection.**
---

## 1. How to Pair on the Interface

**(1) Connect both devices using a dual-ended USB cable.**


**(2) Turn on the pairing switch on both devices.**

<img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/main.jpg?v=1766653127" alt="Setting1" width="300" height="200">


**(3) Designate the left-hand device as the host. Long-press the pairing switch on the left-hand device and select "Left" on the pairing interface.**


**(4) Then, long-press the pairing switch on the right-hand device and select "Right" on its pairing interface.**


**(5) Upon successful connection, the pairing indicators for Left and Right should be displayed at the top of the recording interface on both devices, respectively.**

**(6) Finally, use the record button on the left-hand device to control the start and stop of data recording for both hands. The right-hand device is not controllable for this function.**

---

## 2. Recording Data to the SD Card

**(1) After recording data to the SD card, the bag names will distinguish between the host and client devices**

Host: host_eb208e5ece7fb883_20251226231342.mcap
Client: host_eb208e5ece7fb883_device_445aa23a732f5815_20251226231342.mcap

---

## 3. How to Process Dual-Hand Data Using Studio
Update in https://github.com/genrobot-ai/product-docs/blob/main/docs/md-productions-das-Matrix%20Studio%20Manual-en.md

## 4. Precautions for two-hand collection
1. Remain stationary for at least 3 seconds before collection.   
2. At the start and end of data collection, the left cameras of the two grippers should look at the same position as much as possible, with a larger overlapping range being better. When the commonly viewed object is in the distance, it is easier to fuse the coordinate systems of the two grippers.  
3. Excessive duration of a single packet will affect data processing speed, so the recording duration of each task should be controlled within 15-60 seconds as much as possible  
4. Avoid long-term occlusion of the field of view by the desktop/dynamic objects during the collection process   
5. The left camera field of view of the two devices should have as much texture as possible, and there should be other static objects besides the object to be grasped 