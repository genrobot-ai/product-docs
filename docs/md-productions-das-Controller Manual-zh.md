# DAS Controller 用户手册
简体中文 | [English](./md-productions-das-Controller%20Manual-en.md)
# 1. 重要安全信息

## 1.1 安全说明
首次使用前，请仔细阅读本章并遵守所有安全指南  
如需帮助，请联系：support@genrobot.ai  

### 1.1.1 警告标志含义
- **⚠️ 危险:** 可能导致严重伤害、死亡或重大财产损失.  
- **⚠️ 警告:** 可能导致人身伤害或设备损坏.  
- **⚠️ 注意:** 可能导致设备故障或数据丢失.  
- **💡 提示:** 有助于更好操作的建议.

## 1.2 责任与限制
- 请勿修改或改动设备.  
- GENROBOT.AI 不对因误用、未经授权的更改或操作错误引起的问题负责.  
- 使用本设备即表示您同意所有安全条款，并对其操作承担全部责任.  
- 本产品不适用于 18 岁以下的用户.

## 1.3 集成商与用户责任
- 部署前需进行完整的威胁和风险评估.  
- 根据评估结果实施适当的安全防护措施.  
- 确保所有硬件和软件均已正确安装和配置.  
- 未经授权不得禁用或更改安全措施.  
- 遵守相关法律、标准和行业法规.

## 1.4 环境要求

### 1.4.1 操作条件
- 工作温度: **0°C–40°C**  
- 存储温度: **-20°C–60°C**  
- 湿度: **10–90% (non-condensing)**  
- 防护等级: **IP52**

### 1.4.2 环境注意事项
- 避免强磁场和长时间阳光直射.  
- 远离热源和腐蚀性环境.  
- 在清洁、干燥、通风良好的区域操作.

## 1.5 操作安全

### 1.5.1 操作前检查
- 确保设备无可见损坏.  
- 检查所有线缆完好无损.
- 检查配套物品齐全  

### 1.5.2 操作指南
- 始终在视线范围内操作.    
- 使身体所有部位远离设备的运动范围.

### 1.5.3 异常处理
- 切勿修改或篡改设备.  
- 未经授权不得拆卸或维修.  
- 联系技术支持寻求帮助.

# 2. 产品概述

## 2.1 产品介绍
Das controller 是Das gripper 的同构控制器，用户通过Das gripper采集数据训练后，可使用das controller进行部署
**物品清单**  
	* DAS Controller × 1  
	* 可替换夹爪头 ×3  
	* type-c 数据线 × 1  
	* 供电线 × 1  
	* L 六角扳手   
	* M3 螺栓

### 2.1.1 结构组装
**夹爪组装**
![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/AssembleGripperHead.jpg?v=1763551432)
	* 通用夹爪: 适用于大多数抓取任务.  
	* 触觉夹爪: 适用于需要精确力控的任务.  
	* 软体夹爪：提供更好的贴合性.  
	
**法兰组装**  
	DAS Controller末端是预留了安装孔位,侧边预留3个M3螺纹孔，需要借助法兰件进行拼接组装，法兰结构件(具体尺寸参见相应三维模型)需要根据机械臂或其他操作器末端安装孔位进行设计其固定。  
	DAS Controller与第三方机械臂配合使用时需安装转接法兰。安装步骤如下：  
	* 先将法兰安装到机械臂的末端  
	*  再将DAS Controller与法兰安装（需要三颗M3螺钉固定）  
	
![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/image_3287f03f-1448-44fe-aeff-f7f9c9e62b11.png?v=1766563875)
具体参数
![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/controller_cad.png?v=1766563863)

### 2.1.2 电气连接
使用XT30系列母头插入DAS Controller的XT30 2+2接口并通24V电源，供电接口类型为XT30(PB)
通讯和控制接口统一使用Type-c接口进行通讯
### 2.1.3 通讯连接
Type-C线束连接controller，另一端USB连接至PC。
若自行准备电脑与采集器（Pika Sense）相连接，其电脑软/硬件需求如下：  

| 电脑配置 | 参考参数 | 
|:------|:-------------|
| 操作系统 | Linux | 
| ROS版本 | ROS1 |
## 2.1 SDK使用说明
SDK 地址：https://github.com/genrobot-ai/gen_controller_sdk_release

### 2.1.1 夹爪连接配置
可见SDK readme进行配置

### 2.1.2 相机SDK 说明
**1. 相机节点功能**  
相机节点核心功能是从 3 个摄像头采集图像数据，并将数据发布到对应的 ROS Topic，为夹爪系统提供视觉输入支持。  
**2. 分辨率配置**  
相机支持多种分辨率，系统会按优先级顺序尝试配置，具体参数如下：

| 分辨率 | 说明 | 典型用途 | 
|:------|:-------------|:-------------|
| 1600×1296 | 高分辨率（默认） | 精细操作、图像处理 
| 640×480 | 标准分辨率 | 实时预览、低计算负担场景

在 Launch 启动文件中通过参数设置分辨率，格式为逗号分隔的字符串，示例如下：

```bash
xml
<!-- 单分辨率配置 --><arg name="camera_resolutions" default="1600x1296" />

```

### 2.1.3 夹爪SDK 说明
夹爪系统是一套集驱动控制、位置反馈、压力感知于一体的数字化执行系统，主要由以下组件构成：  
**1. 系统组成**  

| 组件 | 说明 | 
|:------|:-------------|
| 电机驱动器 | 接收距离指令，驱动夹爪完成开合动作 | 
| 编码器 | 实时反馈夹爪开合距离（单位：米），保障控制精度 | 
| 触觉传感器 | 左右各1个，共448个敏感点，感知夹爪与物体的接触压力 | 

**2. 核心特性**  

- 通信方式：基于自定义DAS协议的双向串口通信  
- 数据更新频率：编码器、触觉传感器均为50HZ  
- 控制精度：毫米级距离控制，满足精细操作需求  
- 操作模式：支持单夹爪、双夹爪两种工作模式  
- 安全保护：支持紧急停止、电机禁用等安全操作  

**3. topic 列表**  
发布的topic:

| Topic 名称 | 消息类型 | 更新频率 | 说明
|:------|:-------------|:-------------|:-------------|
| /tactile/left | std_msgs/Int8MultiArray | 50Hz | 单爪左触觉传感器数据
| /tactile/right | std_msgs/Int8MultiArray | 50Hz | 单爪右触觉传感器数据场景
| /encoder | std_msgs/Float32 | 50Hz | 单爪编码器实时位置（单位：m）
| /left_gripper/tactile/left | std_msgs/Int8MultiArray | 50Hz | 左爪左触觉传感器数据
| /left_gripper/tactile/right | std_msgs/Int8MultiArray | 50Hz | 左爪右触觉传感器数据
| /right_gripper/tactile/left | std_msgs/Int8MultiArray | 50Hz | 右爪左触觉传感器数据
| /right_gripper/tactile/right | std_msgs/Int8MultiArray | 50Hz | 右爪右触觉传感器数据
| /left_gripper/encoder | std_msgs/Float32 | 50HZ | 左爪编码器实时位置（单位：m）
| /right_gripper/encoder | std_msgs/Float32 | 50HZ | 右爪编码器实时位置（单位：m）

订阅的topic:

| Topic 名称 | 消息类型 | 更新频率 | 说明
|:------|:-------------|:-------------|:-------------|
| /target_distance | std_msgs/Float32 | 50Hz | 单爪目标开合距离（单位：m）
| /left\_gripper/target\_distance | std_msgs/Int8MultiArray | 50Hz | 左爪右触觉传感器数据场景
| /right\_gripper/target\_distance | std_msgs/Float32 | 50Hz | 右爪编码器实时位置（单位：米）

