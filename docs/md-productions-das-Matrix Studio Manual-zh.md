# Matrix Studio 用户手册

简体中文 | [English](./md-productions-das-Matrix%20Studio%20Manual-en.md)

## 目录

1. 环境准备
2. 证书安装
3. Docker 镜像设置
4. Web 界面指南
5. 数据介绍
6. Q/A

## 1. 环境准备

### 系统要求

- **操作系统**: Linux
- **内存**: 最低 4GB RAM (推荐 8GB)
- **存储空间**: 10GB 可用空间

### 网络要求

- Web 界面需要 HTTPS 访问

## 2. 证书安装

### 分布指南

#### 2.1 下载证书文件

将证书下载到您的本地机器

```bash
wget https://huggingface.co/datasets/genrobot2025/cert/resolve/main/arnold.crt

```

#### 2.2 创建证书

```bash
sudo mkdir -p /usr/local/share/ca-certificates/extra
sudo cp arnold.crt /usr/local/share/ca-certificates/extra/
sudo update-ca-certificates
```

## 3. Docker 镜像设置

### 3.1 拉取 Docker 镜像

我们在 Docker hub 上发布镜像，您可以通过以下命令下载：

```bash
docker pull genrobot/matrix-studio:0.2.6 #latest version
```

### 3.2 获取启动脚本
脚本1： studio 启动脚本
```bash
wget https://huggingface.co/datasets/genrobot2025/studio/resolve/main/start_studio.sh

```
脚本2： 真值处理sdk启动脚本
```bash
wget https://huggingface.co/datasets/genrobot2025/studio/resolve/main/start_studio_sdk.sh

```

### 3.3 启动 Matrix Studio

#### 3.3.1 准备

1. 在您选择的任意位置创建一个 data 文件夹。该文件夹将用于存储您录制的 MCAP 文件。
2. 将 start_studio.sh 脚本文件放置在与数据文件夹相同的目录下。

![Data](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data.jpg?v=1763611603)

#### 3.3.2 启动 Studio

运行 bash start_studio.sh --help 查看所有配置选项.

```bash
bash start_studio.sh --help
```

![Help](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/help.jpg?v=1763611603)

##### Method 1: 本地主机模式 (默认)

```bash
bash start_studio.sh --image-name [docker_image]:[tag]
```

自动在 localhost 模式下运行
通过以下地址访问 Web 界面：

```bash
http://localhost:5500
```

此模式支持本地浏览器访问数据处理平台。

此模式允许您指定自定义的 Docker 镜像和标签。您也可以在 start_studio.sh 脚本中修改默认镜像。

##### Method 2: 方法 2: HTTPS 模式 (网络访问)

```bash
bash start_studio.sh --image-name [docker_image]:[tag] --server-ip [host_ip] --server-https true
```

1. 启用 HTTPS 启动后端服务。
2. 通过以下地址访问 Web 界面：

```bash
https://[host_ip]:5501
```

3. 此模式允许同一局域网内的其他计算机访问该平台。
4. 局域网内的任何计算机都可以使用指定的 IP 地址进行连接。

##### Method 3: 方法 3: 使用docker 内的真值算法
1. 进入容器：
```bash
bash start_studio_sdk.sh --image-name [docker_image]:[tag] 
```

该脚本将挂载data 路径下的文件到镜像的 /app/data路径下  

2. 运行vio处理脚本  
```bash
bash /app/scripts/process_mcap_inner.sh [input_mcap_path] --output-dir [output_dir] --device [version] -loop-closure-iterations 1
```
示例：  
```bash
bash /app/scripts/process_mcap_inner.sh /app/data/test.mcap --output-dir /app/data/output --device v2 -loop-closure-iterations 1
```
• --output-dir为可选参数，默认存到/app/data/output 路径下，保存对应转换后的结果及json文件  
• --device 为可选参数，默认v2  
• 结果分为处理后的mcap以及对应json文件，用户可通过json判断vio是否成功

##### 如果您想关闭 Studio:

```bash
docker stop matrix-studio
```

##### 如果需要删除数据库

1. 删除所有 mcap 数据
2. 进入 data 目录下：

```
sudo rm -rf .meta
```

## 4. Web 界面指南

### 4.1 用户登录

![Login](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/login.jpg?v=1763611603)

当您在计算机浏览器中打开 URL 时，需要输入用户名和密码。此信息将随您的订单确认信息一同发送给您。请联系我们的销售团队获取。

### 4.2 主界面

![Main Dashboard](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/studio_main_page2.jpg?v=1766652771)  
**核心功能模块:**  
• **Data Importer 可视化 ​** - 数据解析及可视化  
• **传感器标定** - 多源传感器参数校准  
• **真值生产** - 高质量标注和数据集生成

### 4.3 数据页面

数据页面是数据处理的主要界面，提供以下功能：  
**1. 显示本地数据目录中的所有 MCAP 数据，包括:**  
 • Token: 每个数据集的唯一标识符.  
 • FileName: 显示 MCAP 数据文件名。点击文件名可在 Monitor 中打开以进行数据可视化.  
 • VioState: 显示真值数据的处理状态.  
 • Action: 允许对单个或多个选定的数据集运行轨迹恢复算法.
![Data Page](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_page.jpg?v=1763611603)
**2. 运行 VIO 算法 (单个/批量) - 主要工作流:**  
• 选择一个或多个数据集.  
• 点击 "Batch Generate Trajectory" 按钮.
![Vio Task1](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/vio_task1.jpg?v=1763611603)
• 输入处理任务的名称.  
• (Optional) 选择是否使用 URDF 求解器 (开发中的功能)).  
• 选择设备类型（默认das gripper）
• 选择版本类型（可询问售后人员确认Das版本类型）
• 选择任务类型：single(单手) dual(双手)
• 点击 OK 开始真值数据处理.
![Vio Task2](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/vio_process.jpg?v=1768225144)
**3. 真值数据处理 ​**  
• 您可以通过 VioState 列监控进度，或在真值详情页面查看详细状态.
• 更多详细功能将通过 OTA 更新推出.


**4. 查看和处理数据:**  
• 从真值详情页面打开特定的数据可视化.  
• 处理后的数据保存在 ​data/output/[task_name]​​ 目录中.
![Task folder](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/task_folder.jpg?v=1763611603)
• 双手任务处理后的数据保存在 ​data/output/[task_name]​​ 目录中，以.merge.mcap 结尾
• 文件 ​vio_result.json​ 包含成功处理数据的路径.  
![Result](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/result.jpg?v=1763611603)

### 4.4 真值页面

真值页面主要显示处理后的真值数据，主要是轨迹数据。此页面支持以下功能:  
**1. 查看真值生成状态和详情::** 检查真值生成的状态和原因，以帮助识别和排查问题.  
**2. 在 Monitor 中可视化真值:**
点击 TruthValue 可在 Monitor 中打开数据可视化.
![GroundTruth](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/groundtruth.jpg?v=1763611603)

• 打开 Monitor 后，您可以通过 /robot0/vio/eef_pose 主题查看原始信息 (具体操作请参考第 4.5 节).  
• 如果使用了 URDF 求解器模式，您将看到 Franka 机械臂 (未来将支持自定义 URDF 上传) 及其末端执行器轨迹.

### 4.5 数据可视化功能

#### 4.5.1 主仪表板
![Importer Bag](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/studio_main_page.jpg?v=1766643934)  

![Upload Bag](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/studio_importer_page.jpg?v=1766643908)  
**功能:**  
• **打开本地文件** - 打开并将本地数据文件加载到系统中.  
• **Monitor** - 点击监控按钮以可视化传感器数据.  
​​

#### 4.5.2 Monitor 介绍

**1. 主题选择与数据类型配置:**
![topic](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/topic_selection.jpg?v=1763611604)
![topic](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_config.jpg?v=1763611604)
**功能:**  
• **​​ 主题显示类型选择** - 从文本、图像、图标、3D 模型和其他可视化格式中选择  
• **灵活布局调整 ​** - 向右或向下添加新面板、删除或重新定位面板  
• **​​​​ 按名称选择主题** - 根据主题名称过滤和选择数据流

**2. 3D 可视化面板:**

![3D panel](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/3d_panel.jpg?v=1763611604)
** 功能:**  
• **URDF 模型渲染 ​** - 显示和操作机器人 URDF 模型  
• **真值轨迹可视化** - 可视化参考轨迹和路径  
• **​ 可视化工具** - 视点控制和测量工具 ​​

**3. 数据包文件详情界面:**
![Bag detail](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/bag_detail.jpg?v=1763611603)  
** 功能:**  
• **​​MCAP 数据摘要 ​** - 通道列表、消息计数和持续时间统计信息  
• **​​ 主题时序** - 帧率分析及每个主题的时间戳可视化

## 5. 数据介绍

本节提供以 MCAP 格式记录的数据的详细文档，包括数据结构、主题列表、坐标系定义和数据转换工具.  
**1. 数据格式: MCAP​**  
系统使用 MCAP 文件格式作为所有记录的传感器数据和内部状态的主要格式. https://mcap.dev/  
**2. Topic 列表**  
主要主题介绍:

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

**3. 坐标系**  
T 系统在所有坐标系中遵循右手定则.  
坐标系定义:​​  
​• 原点: 中间摄像头 (camera0) 的光学中心.  
​• X 轴 (红色)​​: 沿摄像头光轴方向，即向前.  
​• Y 轴 (绿色)​: 垂直于 X 轴，指向左侧.  
​• Z 轴 (蓝色)​​: 垂直于 X-Y 平面，指向上方 (由右手定则确定).

![axis](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/data_axis.jpg?v=1763905297)

**4. Data Convert SDK**  
此工具包允许您将原生 MCAP 数据无缝转换为其他流行的研究和开发格式.

1. 解码 mcap 文件
2. 将 mcap 文件转换为 h5
3. 将真值结果 (vio_result.json 文件) 转换为 h5  
   Links: https://github.com/genrobot-ai/das-datakit

## 6. Q/A

1. Chrome 浏览器打开 Monitor，3d 界面显示失败.  
   解决方案：在浏览器中打开 chrome://flags ，搜索 webGL，将相关功能开启
   ![webgl](https://cdn.shopify.com/s/files/1/0777/8874/1847/files/chrome_webgl.jpg?v=1764301595)
