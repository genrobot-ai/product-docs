# DAS Controller Manual
# 1. Important Safety Information

## 1.1 Safety Instructions

Before first use, read this chapter thoroughly and follow all safety guidelines.  
For assistance: support@genrobot.ai.

### 1.1.1 Warning Sign Meaning

- **⚠️ Danger:** May cause serious injury, death, or major property damage.
- **⚠️ Warning:** May cause personal injury or equipment damage.
- **⚠️ Attention:** May result in device malfunction or data loss.
- **💡 Tip:** Helpful suggestions for better operation.

## 1.2 Liability & Restrictions

- Do not modify or alter the device.
- GENROBOT.AI is not responsible for issues caused by misuse, unauthorized changes, or operational errors.
- Using this device means you agree to all safety terms and assume full responsibility for its operation.
- The product is not intended for users under 18 years old.

## 1.3 Integrator & User Responsibilities

- Conduct a complete threat and risk assessment before deployment.
- Implement proper security protections based on assessment results.
- Ensure all hardware and software are installed and configured correctly.
- Do not disable or change safety measures without authorization.
- Comply with relevant laws, standards, and industry regulations.

## 1.4 Environmental Requirements

### 1.4.1 Operating Conditions

- Operating temperature: **0°C–40°C**
- Storage temperature: **-20°C–60°C**
- Humidity: **10–90% (non-condensing)**
- Protection rating: **IP52**

### 1.4.2 Environmental Precautions

- Avoid strong magnetic fields and prolonged direct sunlight.
- Keep away from heat sources and corrosive environments.
- Operate in a clean, dry, and well-ventilated area.

## 1.5 Operational Safety

### 1.5.1 Pre-operation Checks

- Ensure the device has no visible damage.
- Verify all cables are intact.
- Confirm the battery is charged.

### 1.5.2 Operating Guidelines

- Always operate within line of sight.
- Keep all body parts away from the device’s moving range.

### 1.5.3 Exception Handling

- Stop operation immediately if abnormalities occur.
- Do not disassemble or repair without authorization.
- Contact technical support for assistance.

# 2. Product Overview

## 2.1 Production Introduction
The DAS Controller is a homogeneous controller for the DAS Gripper. After users collect data and train models with the DAS Gripper, they can deploy these models using the DAS Controller.  
**Package List**  
	* DAS Controller × 1  
	* Replaceable Gripper Heads ×3
	* Type-C Data Cable × 1
	* Power Cable × 1
	* L-shaped Hex Key × 1   
	* M3 M3 Bolts

### 2.1.1 Structural Assembly
**Gripper Assembly**
![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/AssembleGripperHead.jpg?v=1763551432)
	* Universal Gripper: Suitable for most grasping tasks.  
	* Tactile Gripper: Suitable for tasks requiring precise force control.  
	* Soft Gripper: Provides better conformity.  
	
**Flange Assembly**  
	The end of the DAS Controller is pre-designed with mounting holes, and the side is reserved with three M3 threaded holes.    
	Connection and assembly require the use of a flange component. The design and fixation of the flange structural component (refer to the corresponding 3D model for specific dimensions) must be based on the mounting hole pattern at the end of the robotic arm or other manipulator.  
	When using the DAS Controller with a third-party robotic arm, an adapter flange needs to be installed. The installation steps are as follows:  
	* First, install the flange onto the end of the robotic arm.  
	* Then, install the DAS Controller onto the flange (requiring three M3 screws for fixation).  
	
![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/image_3287f03f-1448-44fe-aeff-f7f9c9e62b11.png?v=1766563875)

Parameters

![gripper](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/controller_cad.png?v=1766563863)

### 2.1.2 Electrical Connection
Use an XT30 series female connector to insert into the XT30 2+2 interface of the DAS Controller and connect to a 24V power supply. The power supply interface type is XT30 (PB).  
The communication and control interface uniformly uses a Type-C interface for communication.
### 2.1.3 Communication Connection
Connect the controller using a Type-C cable, with the other end (USB) connected to a PC.
If you prepare your own computer to connect with the data acquisition unit (Pika Sense), the computer software/hardware requirements are as follows:  

| Computer Configuration | Reference Parameters | 
|:------|:-------------|
| Operating System | Linux | 
| ROS Version | ROS1 |
## 2.1 SDK Usage Instructions
SDK Link: https://github.com/genrobot-ai/gen\_controller\_sdk\_release
### 2.1.1 Gripper Connection Configuration
Refer to the SDK's README for configuration.

### 2.1.2 Camera SDK Instructions
**1. Camera Node Functionality**  
The core function of the camera node is to capture image data from 3 cameras and publish this data to corresponding ROS Topics, providing visual input support for the gripper system.  
**2. Resolution Configuration**  
The camera supports multiple resolutions. The system will attempt to configure them in order of priority. Specific parameters are as follows:

| Resolution | Explanation | Typical Use Case | 
|:------|:-------------|:-------------|
| 1600×1296 | High Resolution (Default) | Fine manipulation, image processing 
| 640×480 | Standard Resolution | Real-time preview, low computational load scenarios

Set the resolution via parameters in the Launch file, formatted as a comma-separated string. Example:

```bash
xml
<!-- 单分辨率配置 --><arg name="camera_resolutions" default="1600x1296" />

```

### 2.1.3 Gripper SDK Instructions
The gripper system is a digital actuation system integrating drive control, position feedback, and pressure perception. It primarily consists of the following components:  
**1. System Components**  

| Component | Explanation | 
|:------|:-------------|
| Motor Driver | Receives distance commands and drives the gripper to perform open/close actions. | 
| Encoder | Provides real-time feedback on the gripper's opening/closing distance (unit: meters), ensuring control precision. | 
| Tactile Sensor | One on the left and one on the right, totaling 448 sensitive points, perceiving contact pressure between the gripper and objects. | 

**2. Core Features**  

- Communication Method：Bidirectional serial communication based on a custom DAS protocol.
- Data Update Frequency：Both encoder and tactile sensor data update at 50 Hz. 
- Control Precision: Millimeter-level distance control, meeting fine manipulation requirements.
- Operation Modes: Supports both single-gripper and dual-gripper working modes.
- Safety Protection: Supports safety operations such as emergency stop and motor disable.  

**3. Topic List**  
Published Topics:

| Topic name | Messasg type| Update Frequency | Explanation
|:------|:-------------|:-------------|:-------------|
| /tactile/left | std_msgs/Int8MultiArray | 50Hz | Single gripper left tactile sensor data.
| /tactile/right | std_msgs/Int8MultiArray | 50Hz | Single gripper right tactile sensor data.
| /encoder | std_msgs/Float32 | 50Hz | Single gripper encoder real-time position (unit: meters).
| /left_gripper/tactile/left | std_msgs/Int8MultiArray | 50Hz | Left gripper left tactile sensor data.
| /left_gripper/tactile/right | std_msgs/Int8MultiArray | 50Hz | Left gripper right tactile sensor data.
| /right_gripper/tactile/left | std_msgs/Int8MultiArray | 50Hz | Right gripper left tactile sensor data.
| /right_gripper/tactile/right | std_msgs/Int8MultiArray | 50Hz | Right gripper right tactile sensor data.
| /left_gripper/encoder | std_msgs/Float32 | 50HZ | Left gripper encoder real-time position (unit: meters).
| /right_gripper/encoder | std_msgs/Float32 | 50HZ | Right gripper encoder real-time position (unit: meters).

Subscribed Topics:

| Topic Name | Message Type | Update Frequency | Explanation
|:------|:-------------|:-------------|:-------------|
| /target_distance | std_msgs/Float32 | 50Hz | Single gripper target opening/closing distance (unit: m).
| /left\_gripper/target\_distance | std_msgs/Int8MultiArray | 50Hz | Left gripper target opening/closing distance (unit: m).
| /right\_gripper/target\_distance | std_msgs/Float32 | 50Hz | Right gripper target opening/closing distance (unit: m).）

