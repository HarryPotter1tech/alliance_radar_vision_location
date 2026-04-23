# RADAR Vision Location

## 1. 当前文件结构

项目是典型 C++ 工程，核心目录如下：

```text
.
├── CMakeLists.txt                # 构建入口，生成可执行文件 RADAR-H
├── config.yaml                   # 运行参数配置（相机、地图、赛场信息）
├── config/
│   ├── config.hpp                # 配置加载接口声明
│   └── config.cpp                # YAML 配置解析实现
├── data/
│   ├── CameraData/               # 相机参数数据结构
│   ├── GameData/                 # 比赛状态/阵营/版本数据结构
│   ├── MapData/                  # 地图配置数据结构
│   └── UtilityData/              # 工具类数据结构（含 AABB 数据定义）
├── src/
│   ├── Mainloop/main.cpp         # 程序主入口
│   ├── Camera/                   # 相机驱动封装（OpenCV）
│   ├── Map/                      # OBJ 地图加载与三角面提取
│   ├── Utility/Ray/              # AABB 相关几何工具
│   ├── Location/                 # 定位模块（当前基础框架）
│   └── Recognition/              # 识别模块（当前基础框架）
├── include/
│   └── tiny_obj_loader.h         # OBJ 加载头文件
├── scripts/
│   └── install-git-hooks.sh      # 辅助脚本
└── Dockerfile.dev                # 开发容器环境
```

## 2. 当前已实现功能

### 2.1 YAML 配置加载

- 在启动阶段读取 `config.yaml`。
- 解析相机参数：设备号、分辨率、亮度、对比度、饱和度、色调、曝光。
- 解析相机内参：焦距、传感器尺寸。
- 解析相机物理位姿：位置 + 欧拉角（roll/pitch/yaw）转旋转矩阵。
- 解析地图参数：地图名、OBJ 文件路径、BIN 文件路径。
- 解析比赛参数：阵营、状态、运行版本（test/release）。

### 2.2 相机驱动封装

- 基于 OpenCV 的 `cv::VideoCapture`。
- 支持实际摄像头设备输入（deviceID）。
- 支持本地视频文件输入（用于 test 模式）。
- 支持将配置参数写入采集对象（亮度、曝光等）。

### 2.3 地图加载与三角面构建

- 基于 tinyobjloader 加载 OBJ 地图。
- 读取顶点数据并生成三角面集合。
- 提供顶点列表和三角面列表接口，为后续几何计算提供输入。

### 2.4 AABB 初始化

- 对每个三角面计算最小包围盒（AABB）
- 输出每个 AABB 的最小点/最大点。

## 3. 程序入口与运行流程

程序入口是 `src/Mainloop/main.cpp`，主流程如下：

1. 初始化配置数据对象（相机、地图、比赛状态）。
2. 调用配置加载函数读取 `config.yaml`。
3. 根据版本字段区分 test/release 模式（当前都会创建相机驱动对象）。
4. 创建地图对象并加载 OBJ 地图。
5. 提取三角面并构建 AABB。
6. 初始化成功后正常退出（当前阶段是基础流程连通验证）。

可执行文件名：`RADAR-H`

## 4. 环境配置

### 4.1 系统依赖

建议 Ubuntu 22.04，最小依赖如下：

```bash
sudo apt-get update
sudo apt-get install -y \
	build-essential \
	cmake \
	libopencv-dev \
	libeigen3-dev \
	libyaml-cpp-dev \
	pkg-config
```

### 4.2 Docker 构建与运行（推荐）

```bash
docker build -f Dockerfile.dev -t radar-dev .
docker run --rm -it -v "$PWD":/RADAR-LOCATION-CAMERA radar-dev
```

容器内执行：

```bash
cd /RADAR-LOCATION-CAMERA
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j

cd build
./RADAR-H
```

注意：当前配置加载使用相对路径 `../config.yaml`，建议从 `build/` 目录启动程序。

