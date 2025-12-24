# Matrix Studio User Manual

[简体中文](./md-productions-das-Matrix%20Studio%20Manual-zh.md) | English

## Table of Contents

1. Prerequisites
2. Certificate Installation
3. Docker Image Setup
4. Web Interface Guide
5. Data Introduction
6. Troubleshooting

## 1. Prerequisites

### System Requirements

- **Operating System**: Linux
- **Docker**
- **Memory**: Minimum 4GB RAM (8GB recommended)
- **Storage**: 2GB available space

### Network Requirements

- HTTPS access required for web interface

## 2. Certificate Installation

### Step-by-Step Guide

#### 2.1 Download Certificate File

Download the certificate file to your local machine.

```bash
wget https://huggingface.co/datasets/genrobot2025/cert/resolve/main/arnold.crt

```

#### 2.2 Create Certificate

```bash
sudo mkdir -p /usr/local/share/ca-certificates/extra
sudo cp arnold.crt /usr/local/share/ca-certificates/extra/
sudo update-ca-certificates
```

## 3. Docker Image Setup

### 3.1 Pull Docker Image

We publish

```bash
docker pull genrobot/matrix-studio:0.2.5 #latest version
```

### 3.2 Get start scripts

```bash
wget https://huggingface.co/datasets/genrobot2025/studio/resolve/main/start_studio.sh

```

### 3.3 Launch Studio

#### 3.3.1 Prerequisites

1. Create a data directory in any location of your choice. This directory will store your recorded MCAP files.
2. Place the start_studio.sh script file in the same directory as the data folder.

![Data](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data.jpg?v=1763611603)

#### 3.3.2 Starting the Studio

Run bash start_studio.sh --help to view all configuration options.

```bash
bash start_studio.sh --help
```

![Help](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/help.jpg?v=1763611603)

##### Method 1: Localhost Mode (Default)

```bash
bash start_studio.sh --image-name [docker_image]:[tag]
```

Automatically runs in localhost mode  
Access the web interface at:

```bash
http://localhost:5500
```

This mode supports local browser access to the data processing platform

This mode allows you to specify a custom Docker image and tag. You can also modify the default image in the start_studio.sh script

##### Method 2: HTTPS Mode (Network Access)

```bash
bash start_studio.sh --image-name [docker_image]:[tag] --server-ip [host_ip] --server-https true
```

1. Starts the backend with HTTPS enabled
2. Access the web interface at:

```bash
https://[host_ip]:5501
```

3. This mode allows other computers on the same network to access the platform
4. Any computer on the network can connect using the specified IP address

##### If you want to close studio:

```bash
docker stop matrix-studio
```

## 4. Web Interface Guide

### 4.1 User Login

![Login](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/login.jpg?v=1763611603)

When you open the URL in your computer browser, you will need to enter a username and password. This information will be sent to you along with your order confirmation. Please contact our sales team to obtain your credentials.

### 4.2 Main Dashboard

![Main Dashboard](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/Home_board.jpg?v=1763611603)
**Core Functional Modules:**  
• **Data Viz Visualization** - Data exploration and interactive chart analysis  
• **Sensor Calibration** - Multi-source sensor parameter calibration
• **Ground Truth Production** - High-quality annotation and dataset

### 4.3 Data Page

The Data Page is the main interface for data processing, offering the following functionalities:  
**1. Display all MCAP data in local data directory including:**  
 • Token: A unique identifier for each dataset.  
 • FileName: Shows the MCAP data filename. Clicking on it opens the Monitor for data visualization.  
 • VioState: Displays the processing status of the ground truth.  
 • Action: Allows running the VIO trajectory recovery algorithm on single or multiple selected datasets.
![Data Page](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_page.jpg?v=1763611603)
**2. Run VIO Algorithm (Single/Batch)​​ - The main workflow:**  
• Select one or multiple datasets.  
• Click the "Batch Generate Trajectory" button.
![Vio Task1](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/vio_task1.jpg?v=1763611603)
• Enter a name for the processing task.  
• (Optional) Choose whether to use the URDF Solver (Feature under development).  
• Click OK to start the ground truth processing.
![Vio Task2](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/create_vio_task.jpg?v=1763611603)
**3. GroundTruth Processing**  
• You can monitor the progress via the ​VioState​ column or check the detailed status on the ​GroundTruth Details Page.
• More detailed features will be rolled out via ​OTA updates.

**4. View & handle datas:**  
• Open the specific data visualization from the ​GroundTruth Details Page.  
• The processed data is saved in the **data/output/[task_name]** directory.
![Task folder](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/task_folder.jpg?v=1763611603)
• The file **vio_result.json** contains the paths to the successfully processed data.  
![Result](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/result.jpg?v=1763611603)

### 4.4 GroundTruth Page

The GroundTruth Page primarily displays the processed ground truth data, which mainly consists of trajectory data. This page supports the following functionalities:  
**1. View Ground Truth Generation Status & Details:** Check the status and reasons for ground truth generation to help identify and troubleshoot issues.  
**2. Visualize ground truth in Monitor:**
Click on the TruthValue to open the Monitor for data visualization.
![GroundTruth](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/groundtruth.jpg?v=1763611603)

• After opening the Monitor, you can view the original information via the ‘/robot0/vio/eef_pose’ topic (for specific operations, refer to section 4.5).  
• In the 3D Panel, you can select the ‘robot trajectory’ to view the recovered trajectory ground truth.  
• If the URDF Solver mode was used, you will see the Franka robot arm (with future support for custom URDF uploads) and its end-effector trajectory.

### 4.5 Data viz Features

#### 4.5.1 Main Dashboard

![Upload Bag](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/upload_mcap.jpg?v=1763611603)
**Functional:**  
• **Open Local Files** - Open and load local data files into the system.  
• **Monitor** - Click monitor buttion to visualize sensor data.  
​​

#### 4.5.2 Monitor Intruction

**1. Topic Selection & Data Type Configuration:**
![topic](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/topic_selection.jpg?v=1763611604)
![topic](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_config.jpg?v=1763611604)
**Functional:**  
• **​​Topic Display Type Selection** - Choose from text, image, icon, 3D model, and other visualization formats  
• **Flexible Layout Adjustment​** - Add new panels to the right or bottom, delete, or reposition them  
• **​​​​Topic Selection by Name​​** - Filter and select data streams based on their topic name

**2. 3D Visualization Panel:**

![3D panel](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/3d_panel.jpg?v=1763611604)
**Functional:**  
• **URDF Model Rendering** - Display and manipulate robot URDF models  
• **Ground Truth Trajectory Visualization** - Visualize reference trajectories and paths  
• **Visualization Tools** - Viewpoint Control & Measurement Tools ​​

**3. Bag File Detail Interface:**
![Bag detail](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/bag_detail.jpg?v=1763611603)  
**Functional:**  
• **​​MCAP Data Summary​​​** - Channel lists, message counts, and duration statistics  
• **​​Topic Timing​​​** - Frame rate analysis with timestamp visualization per topic

## 5. Data Intruction

This section provides detailed documentation for the data recorded in the MCAP format, including the data structure, topic list, coordinate frame definitions, and data conversion tools.  
**1. Data Format: MCAP**  
The system utilizes the ​MCAP​ file format as the primary container for all recorded sensor data and internal states. https://mcap.dev/  
**2. Topic List**  
Main topic intruction:

| Topic                                | Description                          | Frequency |
| :----------------------------------- | :----------------------------------- | :-------- |
| `/robot0/sensor/camera0/compressed`  | mid cam image stream H.264 encoder   | 30 Hz     |
| `/robot0/sensor/camera1/compressed`  | left cam image stream H.264 encoder  | 30 Hz     |
| `/robot0/sensor/camera2/compressed`  | right cam image stream H.264 encoder | 30 Hz     |
| `/robot0/sensor/imu`                 | IMU info                             | 200 Hz    |
| `/robot0/sensor/magnetic_encoder`    | gripper distace（m）                 | 50 Hz     |
| `/robot0/vio/eef_pose`               | vio eef pose                         | 30 Hz     |
| `/robot0/sim/robot_info`             | urdf robot info: eef pose,joints     | 30 Hz     |
| `/robot0/sensor/camera0/camera_info` | calibration info                     | 30 Hz     |
| `/robot0/sensor/tactile_left`        | tactile info                         | 50 Hz     |
| `/robot0/sensor/tactile_right`       | tactile info                         | 50 Hz     |

**3. Coordinate Frames**  
The system adheres to the ​right-hand rule​ convention for all coordinate frames.  
Frame Definition:​​  
​• Origin: Optical center of the middle camera (camera0).  
​• X-axis (Red)​: Points along the camera's optical axis, i.e., ​forward.  
​• Y-axis (Green)​: Perpendicular to the X-axis, pointing to the ​left.  
​• Z-axis (Blue)​: Perpendicular to the X-Y plane, pointing ​upward​ (as determined by the right-hand rule).

![axis](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_axis.jpg?v=1763905297)

**4. Data Convert SDK**  
This toolkit allows you to seamlessly convert the native MCAP data into other popular research and development formats.

1. decode mcap files
2. convert mcap files to h5
3. convert groundtruth result(vio_result.json files) to h5  
   Links: https://github.com/genrobot-ai/das-datakit

## 6. Troubleshooting

1. The 3D interface fails to display when opening Monitor in the Chrome browser.  
   Solution:​ Open chrome://flagsin the browser, search for "webGL", and enable the related features.  
   ![webgl](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/chrome_webgl.jpg?v=1764301595)
