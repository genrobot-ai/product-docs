[简体中文](./md-dual-das-gripper-Manual-zh.md) | English

# Data Collection Guide for Dual Hands V1.0

## Notes

(1) During pairing, ensure the USB connection is secure. Use straps to minimize tension on the USB ports during collection. If the pairing indicator on the recording interface flickers or disappears, it indicates an unstable USB connection (refer to the fixation solution provided by Genrobot)  

(2) After successful pairing, use the record button on the left-hand device to initiate recording operations.  

(3) During the actual data collection, please ensure that both devices are facing the same spot when starting the collection. Wait for 1 second in a stationary state before beginning the collection.


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

---

## 4.Notes on Dual-Hand Collection
**(1) Pre-collection Stillness: Remain stationary​ for at least 3 seconds​ before starting data collection. This ensures a stable initial state.**    

**(2) Camera Alignment for Start/End:At the beginning and end of collection, the left camera​ of both grippers should be aimed at the same location, with the largest possible overlap​ in their fields of view .For easier fusion of the two grippers' coordinate systems, the common object​ of view should be distant. It is preferable for the shared visual object to be in the distance.**    


**(3) Task Duration: The recording duration for each task should ideally be controlled between 15 and 60 seconds. Excessively long packet durations can impact data processing speed.** 


**(4) Avoiding Obstructions: During collection, avoid the camera's field of view being obstructed​ by the desktop or dynamic objects for extended periods.** 


**(5) Scene Texture: The field of view of the left cameras on both devices should contain rich textures. Apart from the object being gripped, there should be other static objects​ in the scene.**  
