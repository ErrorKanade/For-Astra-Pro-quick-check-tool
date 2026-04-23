Astra Pro Multi-Stream Viewer (Python)这是一个基于 Python 的实时监控程序，专为 Orbbec Astra Pro 深度相机设计。该程序能够同步获取并展示 彩色 (RGB)、深度 (Depth)、红外 (IR) 数据流，并生成实时模拟点云 (PointCloud) 效果。
📸 功能特性多流同步展示：在同一窗口内通过四分屏实时显示四个数据流。
硬件兼容性优化：针对 Astra Pro 特有的 UVC RGB + OpenNI Depth 架构进行了适配。
镜像修正：代码内置了硬件镜像关闭指令，确保各数据流方向一致。
路径容错：自动切换工作目录至 Redist 文件夹，有效避免 Access Violation 内存报错。
🛠️ 环境要求硬件: Orbbec Astra Pro 深度相机 (建议接入 USB 3.0 接口)
操作系统: Windows 10/11Python: 3.10+ (需与 SDK 位数一致，建议 64-bit)
依赖库:Bashpip install numpy opencv-python openni

🚀 快速开始
1. SDK 准备由于本程序调用了底层 C++ 库，需要准备好 Orbbec 官方的 OpenNI 2.3 SDK。
确保以下文件夹结构存在：PlaintextRedist/
├── OpenNI2/
│   └── Drivers/ (包含 orbbec.dll 等)
├── OpenNI2.dll
└── ...
2. 配置路径在 test.py 中，根据实际存放位置修改 REDIST_PATH：PythonREDIST_PATH = r"C:\Your\Path\To\Win64-Release\tools\Redist"
3. 运行程序Bashpython test.py
4. 
🖥️ 窗口说明程序运行后将开启一个四分屏窗口，
布局如下：
左上 (RGB)右上 (Depth)调用 UVC 协议采集的彩色图像经过 BONE 伪彩色处理的深度图
左下 (IR)右下 (Simulated PC)实时红外散斑图基于深度梯度的伪彩色模拟点云
⚠️ 常见问题排查 (Troubleshooting)无法检测到 RGB 相机？Astra Pro 的彩色摄像头通常占用系统视频索引 0, 1 或 2。
若未显示，请尝试修改代码中的：cap_rgb = cv2.VideoCapture(2, cv2.CAP_DSHOW)。
出现 Access Violation 报错？这是因为 OpenNI 找不到驱动。请确保 os.chdir(REDIST_PATH) 指向的文件夹内包含 OpenNI2/Drivers 目录。
画面不对齐？Astra Pro 的 RGB 和 IR 镜头存在物理间距（视差）。
在近距离（< 80cm）拍摄时会有明显错位，建议在 1.5m 以外观察以获得最佳对应效果。
📜 许可证本项目采用 MIT License 许可。
