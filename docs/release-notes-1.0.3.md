# Sensor Sync Studio 1.0.3 发布说明

发布日期：2026-10-31
适用固件：Sensors-SYNC V3.1.0（协议 1.1）

## 本次变更

### 1. 移除 DEBUG 事件时间线面板

右侧栏不再单独展示 `$EVENT` 列表，界面更紧凑。固件事件仍按原有语义（紫色）记录在「原始 DEBUG 日志」中，`IMU_PORT` 事件改为驱动 IMU 模式状态显示。

### 2. 新增 IMU 端口模式状态

「IMU端口模式」面板顶部新增「当前模式」一行，实时显示固件上报值：

- `IMU 同步输出`（IMU_SYNC）
- `RTK NMEA 透传`（RTK_NMEA_PASS）
- `未读取`：未连接或尚未收到 `$GETIMUMODE` 回复

状态来源为 `$IMUMODE` 回复与 `$EVENT,...,IMU_PORT,...`，断开连接自动复位。

### 3. 新增「端口与相机设置」对话框

入口：「端口状态」面板右下角按钮。可在同一界面批量调整：

| 项目 | 取值范围 | 下发命令 |
|---|---|---|
| LIDAR1（UART1） | 4800–921600，九档 | `$SETBAUD,1,<rate>` |
| RTK（UART2） | 同上 | `$SETBAUD,2,<rate>` |
| LIDAR2（UART3） | 同上 | `$SETBAUD,3,<rate>` |
| DEBUG（UART4） | 同上 | `$SETBAUD,4,<rate>` |
| IMU（UART5） | 同上 | `$SETBAUD,5,<rate>` |
| 相机帧率（CAMERA） | 1–250 Hz | `$SETCAMFPS,<fps>` |

行为约定：

- 只下发与当前值不同的项，未改动的端口不会重复写 Flash。
- 所有改动汇总为一次确认提示，不会逐条弹窗。
- 修改 DEBUG 口（UART4）波特率后，会提示必须用新波特率重新连接。
- 下发结束后自动回读 `$GETBAUD` 与 `$GETCAMFPS`，主界面端口表随之更新。
- 「从设备读取」按钮可主动刷新当前值，且不会覆盖用户已手动修改的行。

### 4. 界面细节

- 「端口状态」表格可完整显示 CAMERA / LIDAR1 / LIDAR2 / IMU / RTK / DEBUG 六行，无需滚动。
- 默认窗口尺寸调整为 1500×1000。

## 兼容性

- 协议与 1.0.2 一致，未新增命令；仅改变界面组织方式。
- Ubuntu 20.04 包内置 Qt 6.2.4；Ubuntu 22.04 包依赖系统 Qt 6（`libqt6core6`、`qt6-qpa-plugins`）。
- Windows 为免安装 ZIP，内置 Qt/MinGW 运行时。

## 已知限制

- 相机触发频率、脉宽与四路相位仍需外部仪器实测，客户端只显示配置值与固件统计值。
- `$GETCONFIG`、`$GETPORTSTAT`、`$GETDEVICEINFO` 尚未在 V3.1.0 固件实现，相关界面字段保持「固件未提供」。
