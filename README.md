# 🚜 MineSLAM：非煤矿井危险征兆智能巡检无人车

该项目来源于国家重点研发计划项目：**《地下非煤矿山危险征兆智能巡检关键技术及装备2021YFC3001302》** 子课题。**MineSLAM** 是一套面向非煤矿井复杂地下环境的智能巡检机器人系统，搭载 **LIO-SAM激光惯性里程计系统**，结合**多传感器融合**和透水、地压、有毒气体传感器，用于识别潜在危险征兆，实现无人化自主巡检，提高矿井安全管理效率。

该项目与**山东黄金集团**展开合作，以山东莱州焦家金矿为示范矿区完成应用示范及验收工作。

该系统以 **自研履带式无人车** 为平台，适用于狭窄、不平整、无GPS信号的地下矿井环境，具备高鲁棒性的实时定位与智能识别能力。

---

## 🎯 项目目标

- 🔍 基于 LIO-SAM 实现高精度实时定位与建图（SLAM）
- 🎥 融合双目相机进行井下视觉感知与危险征兆检测
- 🧭 自主路径规划与导航能力，支持远程控制与自动回传
- 💡 支持后期集成有毒气体检测、电磁透水法等多种监测方式

---

## 🔧 技术栈 & 传感器配置

| 模块            | 工具 / 设备                                |
|-----------------|--------------------------------------------|
| SLAM            | LIO-SAM（基于激光 + 惯性里程计融合）       |
| 主控            | 域控制器（NVIDIA Jetson / x86 工控机）     |
| 激光雷达        | 16线机械式雷达（Velodyne / Robosense）     |
| IMU             | TL740D（瑞芬 IMU）                         |
| 摄像头          | 双目相机（支持立体视觉和深度估计）         |
| 危险检测传感器  | 电磁法透水探头（非SLAM部分）               |
| 气体传感器      | 有毒有害气体检测模块（非SLAM部分）         |

---

## 📁 项目结构

```bash
MineSLAM/
├── lio_sam_config/     # LIO-SAM 的配置文件（.yaml、.launch）
├── sensor_config/      # 激光雷达、IMU、相机等驱动参数
├── scripts/            # 一些启动脚本或工具脚本
├── maps/               # 保存的地图和运行数据包
├── docs/               # 文档、流程图、调试记录
├── .gitignore
├── LICENSE
├── CONTRIBUTING.md
└── README.md
```

### 🚀 快速开始 | Quick Start

> 以下为项目主要功能模块的启动流程与说明（基于 ROS Noetic + LIO-SAM + 实际传感器）

#### 1️⃣ 环境依赖

请确保你已安装以下依赖：

- Ubuntu 20.04 + ROS Noetic
- [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
- CMake / catkin_tools
- Velodyne 驱动（适配 16线激光雷达）
- TL740D IMU 驱动
- 双目相机驱动（如 ZED SDK / ROS 包）

#### 2️⃣ 初始化 ROS 工作空间

```bash
mkdir -p ~/mine_slam_ws/src
cd ~/mine_slam_ws/src
catkin_init_workspace
```
#### 3️⃣ 克隆项目并编译
```bash
cd ~/mine_slam_ws/src
git clone https://github.com/yourusername/MineSLAM.git
cd ..
catkin_make
source devel/setup.bash
```
#### 4️⃣ 启动 LIO-SAM SLAM 系统
```bash
roslaunch lio_sam run.launch
```
