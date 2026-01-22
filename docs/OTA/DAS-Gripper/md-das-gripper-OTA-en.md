[简体中文](./md-das-gripper-OTA-zh.md) | English  
# User Upgrade Introduction
DAS-Gripper supports upgrading its edge-side software, which is divided into two parts: upgrading the APP and upgrading the underlying software  

[Version update documentation](https://zcnma1sv5kma.feishu.cn/wiki/CKpbwye45iOlrckukIPc5hKCndh "查看固件版本更新文档")
 
**APP Upgrade**  
The APP upgrade will update the application-layer code.

**Underlying Software Upgrade**  
he underlying software upgrade will optimize drivers, alignment functions, and more. 

# User Upgrade Process

Strictly follow the process: upgrade the APP first, then upgrade the underlying firmware.

Ensure that the device has sufficient battery power throughout the upgrade process (around 50%).

---

## APP Upgrade Process

1. Ensure the device is successfully connected to Wi-Fi.

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/WIFI.jpg?v=1766566053" alt="WIFI" width="300" height="200">

2. In the Settings interface, find "Version Check".

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Settings1.jpg?v=1766645554" alt="Setting1" width="300" height="200">

3. Click "Version Check". The system will automatically detect the latest version.
   - Example prompt:  
     New version detected: 0.0.36  
     Current version: 0.0.35  
     Cancel | Update

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Version_Check1.jpg?v=1766645522" alt="Version_Check1" width="300" height="200">

4. Click "Start download".
   - Progress is displayed during download.
   - After download is complete, a prompt will appear to click "OK" to restart the device.

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Update1.jpg?v=1766645549" alt="Update1" width="300" height="200">

5. After the download is complete, enter the update confirmation interface.
   - Prompt message:  
     Upgrade package download completed.  
     Latest version: 0.0.36  
     Current version: 0.0.35  
     Click "Update" to install. The device will automatically restart after installation.

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Install1.jpg?v=1766645562" alt="Install1" width="300" height="200">

6. Click "Update" to begin the installation process.
   - Prompt: Installing update, the device will automatically restart shortly.

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Restart1.jpg?v=1766645562" alt="Restart1" width="300" height="200">

7. After restarting, go to "Version Check" to confirm the update result.
   - If successful: Display "You are on the latest version. Current version: 0.0.36".
   - If failed: Retry the update multiple times.

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Last_Version1.jpg?v=1766645555" alt="Last_Version1" width="300" height="200">

---

## Underlying Firmware Upgrade Process

> Note: **Perform the underlying firmware upgrade only after the APP upgrade is complete.**

1. Download the latest underlying firmware version.
   - Select the latest underlying firmware version.
   [Version update documentation](https://zcnma1sv5kma.feishu.cn/wiki/CKpbwye45iOlrckukIPc5hKCndh "查看固件版本更新文档")

2. Download the latest version to an SD card.

3. Insert the SD card with the latest version into the device.

4. In the device Settings interface, find "Version Check".

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Settings1.jpg?v=1766645554" alt="Setting1" width="300" height="200">

5. Click "Version Check".
   - Prompt: New version detected: full 6.0.0  
     Current version: 0.0.36  
     Cancel | OK

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Full_Version1.jpg?v=1766645557" alt="Full_Version1" width="300" height="200">

6. Click "Update" to start the installation.
   - Prompt: Installing update, the device will automatically restart shortly.

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Restart1.jpg?v=1766645562" alt="Update" width="300" height="200">

7. After the upgrade is complete and the device has restarted, you can remove the SD card.