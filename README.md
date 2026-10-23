# SensorSyncStudio



## 1.2 Ubuntu 安装

在安装包所在目录打开终端，按照系统版本选择对应 DEB。推荐使用 apt 安装，因为 apt 会自动处理依赖。

sudo apt install ./gunda-sensor-sync-studio_1.0.1_amd64_ubuntu20.04.deb

sudo apt install ./gunda-sensor-sync-studio_1.0.1_amd64_ubuntu22.04.deb

也可以使用 dpkg。若提示缺少依赖，再执行 apt 修复。

sudo dpkg -i gunda-sensor-sync-studio_1.0.1_amd64_ubuntu22.04.deb

sudo apt-get install -f


安装完成后，可从应用菜单或 Ubuntu Dock 启动 GUNDA 多传感器同步器客户端，也可以在终端执行

sensor-sync-studio。安装脚本会在已登录的 GNOME 会话中尝试将应用加入收藏夹。

## 1.3 Ubuntu 串口权限

如果能看到 ttyUSB 或 ttyACM 设备但无法打开串口，请确认当前用户属于 dialout 组。

groups
sudo usermod -aG dialout "$USER"

修改用户组后必须注销并重新登录。仅关闭并重开客户端不足以刷新用户组权限。

## 1.4 Windows 启动

1. 将 Windows x64 ZIP 完整解压到本地文件夹。
2. 连接同步器 DEBUG USB 转串口。
3. 双击 sensor_sync_studio.exe。
4. 如果 Windows 显示安全提示，请核对文件来源和 SHA-256 后再运行。
Windows 版本为免安装包。不要只复制 EXE 文件，Qt DLL、platforms 和 imageformats 文件夹必须与 EXE
保持原有相对位置。

# 2 快速连接设备

5. 使用 USB 连接同步器 DEBUG 端口和电脑。
6. 启动客户端，展开右侧“串口与设备”区域。
7. 点击“刷新”，从列表选择 DEBUG 串口。Ubuntu 通常显示 ttyUSB0、ttyUSB1 或 ttyACM0；Windows
通常显示 COM3、COM4 等。
8. 波特率选择 115200。默认串口格式为 8 数据位、无校验、1 停止位、无流控。
9. 点击“连接”。底部状态栏显示“设备在线”和端口名称。
10. 等待客户端自动查询状态、波特率、相机频率、固件版本和 IMU 模式。
连接成功后，底部状态栏应显示固件和协议版本，例如“固件/协议：V3.1.0 / 1.1”。如果设备使用旧固件，
版本字段可能保持读取中或在日志中返回不支持命令。

## 2.1 识别正确的 DEBUG 端口

 断开设备，点击刷新并记录端口列表。
 重新连接设备，再次刷新。新增的 ttyUSB、ttyACM 或 COM 端口通常就是目标端口。
 若设备提供多个串口，使用系统设备信息或逐个连接确认 DEBUG 输出。
 连接后若日志持续出现 SRC、STATE、GNSS、UTC、LOCAL、Q 等状态行，说明 DEBUG 端口选择正确。

## 2.2 断开与重新连接

点击“断开”可安全关闭串口。更换设备、拔插 USB 或修改 DEBUG 波特率后，应先断开，再刷新端口列表并重新连接。

# 3. 保存日志

点击“保存日志”，选择 .log 或 .txt 文件。建议在复现问题前开启自动滚动，并在问题发生后立即保存。日
志最多保留 10000 行，较早内容会自动移除。

# 6. 常见问题


# 7 卸载

Ubuntu 版本：
sudo apt remove gunda-sensor-sync-studio

Windows 免安装版本不写入系统安装目录。退出客户端后删除解压文件夹即可。

