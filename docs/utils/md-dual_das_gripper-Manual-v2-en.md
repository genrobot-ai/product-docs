# Guide to Bimanual Data Acquisition V2.0

Data Acquisition of the two-handed device is mainly carried out through wireless frequency band pairing.

## Precautions

**（1）After each power-on, manually set the device to left or right gripper and click the Confirm Configuration button**  
**（2）When multiple devices are placed together, ensure that the frequency bands and synchronization words of every two devices are the same to avoid frequency interference**  
**（3）After the confirmation configuration button turns gray, return to the main interface and check for the left or right hand icon on the page. Once pairing is successful, recording can be initiated**  
**（4）During actual data acquisition, please ensure that both devices are looking at the same position when starting the acquisition, remain stationary for 1 second, and then start the movement to ensure that the initialization is complete**  
**（5）If the two devices have not been connected, it is recommended to switch the frequency band and synchronization word. If it still doesn't work, restart once and then reconnect**


## 1.1. How to pair on the interface

**（1）Long press to turn on the pairing switch of the two devices**  

<img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/dual_hand_setiing.png?v=1770445671" alt="Setting1" width="300" height="200">

**（2）Enter the pairing page**  

<img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/dual_hand_wifi.webp?v=1770445640" alt="Setting2" width="300" height="200">

**（3）Use the device in the left hand as the master device, select the frequency band, sync word, and left gripper, click Confirm Configuration, and wait for the icon to turn gray**  

**（4）Long press the pairing switch on the right-hand device, select the same frequency band and synchronization word as the left-hand device, choose the right gripper, click Confirm Configuration, and wait for the icon to turn gray**  

**（5）After successful connection, the pairing identifiers for left and right should be displayed respectively above the recording interface of the two devices**  

**（6）After successful pairing, only the recording button on the left-hand device can control the recording and termination of data acquisition for both hands, while the right-hand device is only controlled by the left-hand device**  

## 2. 2. Record data to SD card

After recording data to the SD card, the bag name will distinguish between the master and slave devices:  
Host：DAS-Gripper_20260127193045_left_leader_00000000.mcap  
Client：DAS-Gripper_20260127193045_right_follower_00000000.mcap  

## 3.How to use studio to process two-handed data
1. studio Manual
Update in https://github.com/genrobot-ai/product-docs/blob/main/docs/md-productions-das-Matrix%20Studio%20Manual-en.md

## 4. Precautions for two-hand collection
1. Remain stationary for at least 3 seconds before collection.   
2. At the start and end of data collection, the left cameras of the two grippers should look at the same position as much as possible, with a larger overlapping range being better. When the commonly viewed object is in the distance, it is easier to fuse the coordinate systems of the two grippers.  
3. Excessive duration of a single packet will affect data processing speed, so the recording duration of each task should be controlled within 15-60 seconds as much as possible  
4. Avoid long-term occlusion of the field of view by the desktop/dynamic objects during the collection process   
5. The left camera field of view of the two devices should have as much texture as possible, and there should be other static objects besides the object to be grasped 


