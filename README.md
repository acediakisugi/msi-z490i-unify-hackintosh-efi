# msi-z490i-unify-hackintosh-efi
🖥 MSI MEG Z490I UNIFY + Intel i9-10850k + AMD RX6900 XT

## 配置 Hardware List
 规格     | 详细信息
 ---------|--------
 主板 Motherboard | 微星 MSI MEG Z490i Unify MS-7C77
 处理器 CPU       | 英特尔 Intel Core i9-10850K 3.6-5.3Ghz
 显卡 Graphic     | 公版 AMD Radeon RX 6900 XT 8GB
 内存 Memory      | 宏碁 Acer DDR4 4000MHz 32GB 16GBx2
 硬盘 M.2 NVME    | 西数 WD_BLACK SN730 M.2 NVME 512GB
 无线网卡 WiFi     | 博通 Broadcom BCM943602CS 白苹果原拆
 有线网卡 Ethernet | 瑞昱 Realtek RTL8125B 板载
 声卡 Audio        | 瑞昱 Realtek ALC S1220A 板载

## 系统安装
    #### 0. 安装前请自行用GenSMBIOS替换MLB、ROM、SystemSerialNumber、SystemUUID。

1. config.plist和config-z490i.plist中的配置除了'HideAuxiliary'项其他完全一样
   	- ###### config.plist关闭了'HideAuxiliary'
   	- ###### config-z490i.plist开启了'HideAuxiliary'
   config.plist可用于系统安装和reset nvram，安装完成和reset nvram后将config-z490i.plist改名回config.plist日常使用，隐藏多余启动项后较为简洁。

2. 用Hackintool修复睡眠项到0/0标绿。

3. 安装完进入系统后需用OpenCore Legacy Patcher 1.4.2进行Post-Install Root Patch方可启用博通无线网卡。


## 从MacOS 14.4.1 Sonoma开始支持
1. 修复曾经免驱的博通网卡
	- ###### 添加IOSkywalkFamily.kext V1.1.0和IO80211FamilyLegacy.kext V1.0.0修复曾经免驱的博通无线网卡。

2. 修复系统版本OTA更新
	- ###### 添加RestrictEvents.kext驱动和boot-args String 'revpatch=sbvmm'修复系统版本OTA更新功能。

3. 修复百度网盘闪退
	- ###### 添加boot-args String 'ipc_control_port_options=0'和csr-active-config '7F0A0000'修复百度网盘闪退问题。

4. 修复虚拟机无法开启
	- ###### 添加AMFIPass.kext和boot-args String '-amfipassbeta'修复虚拟机无法开启问题。
 
## 日常功能使用测试
1. 核显加速
	- ###### 解码正常，支持缓冲帧。

2. 核显输出
	- ###### 板载DP和TypeC支持输出4K60Hz，板载HDMI支持输出4K30Hz，支持3口同时输出，均带音频通道。

3. 独显输出
	- ###### 公版RX6900XT offset 降频至 2550Mhz 1.10V
	- ###### 风扇策略≤45°停转，≥60°启转。4口支持同时输出带音频通道4K60HZ
	- ###### 公版显卡TypeC口MacOS下只支持声音和音频，不可传输数据。Windows下支持声音、音频和数据传输。

5. 有线网卡
	- ###### 2.5Gbps全速率正常

6. 无线网卡
	- ###### MacOS下1300Mbps全速率正常。
	- ###### Windows下默认驱动867Mbps，打最新Windows驱动后1300Mbps。

7. 蓝牙正常
	- ###### 此前MacOS13时遇到睡眠唤醒后蓝牙进程占用过高，目前MacOS14仍待观察。

8. 雷电三接口
	- ###### 支持TypeC全速率传输，但雷电网桥不可用。雷电协议的显卡/声卡拓展坞未测试

9. USB口定制
	- ###### 内置 USB 2.0 (接BCM943602CS蓝牙线单通道)；
	- ###### 前置 TypeC 2.0 & 3.0；
	- ###### 前置 TypeA USB 2.0 & 3.0；
	- ###### 后置 TpyeC 2.0 & 3.0 (同雷电口)；
	- ###### 后置黑口 USB 2.0；
	- ###### 后置蓝口 USB 3.0；
	- ###### 后置红口 USB 3.0。

10. 苹果生态功能
	- ###### i. 隔空投送双向正常。
	- ###### ii. 睡眠正常(BIOS开启PCI/USB设备唤醒可键鼠唤醒)，无法深睡，会不定时由苹果子自带系统服务唤醒几秒后又睡。
	- ###### iii. 通用控制键鼠跨屏连接正常(在同一局域网测试)，无法连接时可关闭两台设备通用控制功能，再次开启。
	- ###### iv. 在Mac上将iPhone用作网络摄像头“连续互通相机”，FaceTime或使用直播软件时可开启，系统自发唤起。
	- ###### v. 随航功能(将iPad用作Mac的第二台显示器)因作者没有iPad无法测试，理论上正常。



## 其他未详尽有待补充
