简体中文 | [English](./md-das-gripper-OTA-en.md)  

# 用户升级介绍
DAS-Gripper 支持升级端侧软件，分为升级APP和升级底层软件两部分。 
 
**APP升级**  
APP 升级将升级应用层代码  

**底层软件升级**  
底层软件升级将优化驱动、对齐等功能  

# 用户升级流程  
1. 按照先升级APP再升级底软的流程执行，若在升级APP时遇到异常，请及时联系售后
2. 确保整个升级流程设备电量充足（>50%）

---

## APP升级流程

1. 确保设备已成功连接WIFI  

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/WIFI.jpg?v=1766566053" alt="WIFI" width="300" height="200">  

2. 在设置界面找到“新版本检测”  

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Setting.jpg?v=1766565982" alt="新版本检测" width="300" height="200">

3. 点击进入“新版本检测”，系统会自动检测最新版本
   - 示例提示：  
     检测到新版本：0.0.36  
     当前版本：0.0.35  
     取消 | 确定  

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Version_Check.jpg?v=1766565986" alt="新版本检测2" width="300" height="200">  

4. 点击“开始下载”
   - 下载中显示进度
   - 下载完成后提示点击“确定”重启设备

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Update.jpg?v=1766565985" alt="update" width="300" height="200">  

5. 下载完成后进入更新确认界面
   - 提示信息：  
     升级包已下载完成  
     最新版本：0.0.36  
     当前版本：0.0.35  
     点击“确定”即可安装，安装完成后设备将自动重启. 

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Install.jpg?v=1766565952" alt="Install" width="300" height="200"> 

6. 点击“确定”后进入安装过程
   - 提示：正在安装更新，稍后设备会自动重启

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Restart.jpg?v=1766565970" alt="Restart" width="300" height="200">

7. 重启后进入“新版本检测”确认更新结果
   - 若成功：显示“当前已是最新版本 当前版本：0.0.36”
   - 若失败：可多次重试更新

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Last_Version.jpg?v=1766565973" alt="Last_Version" width="300" height="200">

---

## 底软升级流程

1. 下载最新的底软版本
   [Version update documentation](https://zcnma1sv5kma.feishu.cn/wiki/CKpbwye45iOlrckukIPc5hKCndh "查看固件版本更新文档")

2. 将最新版本下载到SD卡中

3. 将带有最新版本的SD卡插入设备

4. 进入设备设置界面找到“新版本检测”

   <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Setting.jpg?v=1766565982" alt="Setting" width="300" height="200">

5. 点击“新版本检测”
   - 提示：检测到新版本：full 6.0.0  
     当前版本：0.0.36  
     取消 | 确定

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/full_Version.jpg?v=1766565942" alt="full_Version" width="300" height="200">

6. 点击“确定”开始安装
   - 提示：正在安装更新，稍后设备会自动重启

      <img src="https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Restart.jpg?v=1766565970" alt="Restart" width="300" height="200">

7. 升级完成重启后，即可退出SD卡，可将SD中的底软版本删除
