

# Bionic_Spider_Servo_Robot

本项目完成于2024年2月24日，不再更新。

This project was completed on February 24, 2024, and will no longer be updated.

## 项目简介
这是一个基于STM32F103C8T6的八自由度舵机蜘蛛机器人项目，具备**蓝牙无线遥控**和**OLED显示屏表情切换**功能。机器人采用仿生蜘蛛结构，通过8个舵机实现多方向移动、姿态调整，并可通过手机APP发送指令切换OLED屏幕上的趣味表情，适合机器人爱好者学习STM32硬件控制、蓝牙通信和嵌入式开发。


## 项目文件框架说明（Bionic_Spider_Servo_Robot）

```plaintext
Bionic_Spider_Servo_Robot/
├── DebugConfig/               
├── Hardware/                  # 硬件驱动目录
│   ├── LED.c/h    
│   ├── Key.c/h 
│   ├── OLED.c/h               # OLED显示屏（SSD1306）
│   ├── PWM.c/h        
│   ├── Servo.c/h          	   # 舵机封装
│   └── Serial.c/h             # 蓝牙模块（HC-05/06）
├── Library/                   # 通用库目录
├── Start/                     # 启动文件目录
│   └── startup_stm32f10x_md.s # STM32F103C8T6启动汇编文件
├── System/                    # 系统核心配置目录
│   ├── sys.c/h                # 系统初始化
│   └── Delay.c/h              # 精准延时
├── User/                      # 应用逻辑目录（项目核心功能实现）
│   ├── main.c/h               # 主程序入口（表情、初始化外设、循环处理指令、状态管理）
│   └── stm32f10x_it.c/h       # 中断处理（未使用）
├── stl/                       # 机械结构3D模型目录
├── Project.uvoptx             # Keil uVision项目配置文件
├── Project.uvprojx            # Keil uVision项目工程文件
├── README.md                  # 项目说明文档
└── keilkill.bat               # 编译缓存清理脚本
```


## 功能特性
- **八自由度运动**：8个舵机分别控制蜘蛛的8条腿，实现前进、后退、转向等运动。
- **蓝牙遥控**：通过HC-05/HC-06蓝牙模块与手机APP通信，支持自定义控制指令
- **OLED表情显示**：128×64 OLED屏幕可切换多种预设表情（如开心、愤怒、疑惑等）


## 硬件清单
| 部件名称               | 数量 | 说明                                  |
|------------------------|------|---------------------------------------|
| STM32F103C8T6开发板    | 1    | 主控制器，提供PWM、USART、I2C等接口    |
| SG90     | 8    | 驱动器              |
| HC-05/HC-06蓝牙模块    | 1    | 实现与手机的无线通信                  |
| SSD1306 OLED显示屏 | 1    | 显示表情、调试信息                    |
| 舵机驱动电源（5V/2A以上） | 1    | 为舵机单独供电      |
| 蜘蛛机器人结构件       | 1套  | 3D打印制作 |
| 杜邦线、面包板         | 若干 | 电路连接                              |


## 硬件接线图
### STM32F103C8T6与外设连接
- **舵机控制**：STM32的`PA0、1、2、3、6、7`与`PB0、1`脚输出PWM信号，分别连接8个舵机的信号端（舵机电源接外部5V电源，GND与STM32共地）。
- **蓝牙模块**：HC-05的`TX`接STM32的`USART1_RX（PA10）`，`RX`接STM32的`USART1_TX（PA9）`，`VCC`接5V，`GND`接GND。
- **OLED显示屏**：SSD1306的`SDA`接STM32的`PB7`，`SCL`接`PB6`，`VCC`接3.3V，`GND`接GND。


## 软件环境
- 开发工具：Keil uVision
- 依赖库：
  - STM32标准外设库
  - SSD1306 OLED驱动库


## 固件编译与烧录
1. **项目导入**：将仓库代码导入Keil uVision，配置芯片型号为`STM32F103C8T6`。
2. **编译设置**：选择编译目标为`Debug`或`Release`，点击“Build”生成二进制文件（.hex或.bin）。
3. **烧录固件**：使用ST-Link/Daplink/Jlink，将固件烧录到STM32开发板。


## 蓝牙遥控操作
1. **手机APP选择**：下载“蓝牙串口助手”类APP
2. **蓝牙配对**：打开手机蓝牙，连接名为“HC-05”的设备（默认密码`1234`或`0000`）。
3. **发送控制指令**


## OLED表情显示配置
预设表情存储在`main.c`文件中，每个表情为128×64像素的点阵数据。若需自定义表情，可使用**OLED点阵生成工具**（如“取模软件”）生成点阵数组，替换对应表情的数组即可。


## 注意事项
1. **电源隔离**：舵机必须使用独立电源供电，否则会因电流过大导致STM32复位或损坏。
2. **舵机角度范围**：调试时需确认每个舵机的最大转动角度，避免机械结构卡死。
3. **蓝牙配对**：若蓝牙模块无法连接，可尝试重置模块。
4. **OLED初始化**：若屏幕无显示，检查I2C引脚接线和地址。


## 贡献与扩展
欢迎提交PR扩展功能，如：
- 增加如避障、自动巡航等多模式运动。
- 优化蓝牙通信协议。
- 扩展更多OLED表情或显示传感器数据。

# Bionic_Spider_Servo_Robot

## Project Overview  
This is an 8-Degree of Freedom (DOF) servo spider robot project based on the STM32F103C8T6, featuring **Bluetooth wireless control** and **OLED display expression switching**. The robot adopts a bionic spider structure, using 8 servos to achieve multi-directional movement and posture adjustment. It can also switch between fun expressions on the OLED screen via commands sent from a mobile app, making it suitable for robotics enthusiasts to learn STM32 hardware control, Bluetooth communication, and embedded development.


## Project File Structure (Bionic_Spider_Servo_Robot)  
```plaintext
Bionic_Spider_Servo_Robot/
├── DebugConfig/               
├── Hardware/                  # Hardware driver directory
│   ├── LED.c/h    
│   ├── Key.c/h 
│   ├── OLED.c/h               # OLED display (SSD1306)
│   ├── PWM.c/h        
│   ├── Servo.c/h              # Servo encapsulation
│   └── Serial.c/h             # Bluetooth module (HC-05/06)
├── Library/                   # General library directory
├── Start/                     # Startup file directory
│   └── startup_stm32f10x_md.s # STM32F103C8T6 startup assembly file
├── System/                    # System core configuration directory
│   ├── sys.c/h                # System initialization
│   └── Delay.c/h              # Precise delay
├── User/                      # Application logic directory (core project functions)
│   ├── main.c/h               # Main program entry (expressions, peripheral init, command loop, status management)
│   └── stm32f10x_it.c/h       # Interrupt handling (not used)
├── stl/                       # 3D models for mechanical structure
├── Project.uvoptx             # Keil uVision project configuration file
├── Project.uvprojx            # Keil uVision project engineering file
├── README.md                  # Project documentation
└── keilkill.bat               # Compilation cache cleaning script
```


## Features  
- **8-DOF Movement**: 8 servos control the robot’s 8 legs separately, enabling movement such as forward, backward, and turning.  
- **Bluetooth Control**: Communicates with a mobile app via the HC-05/HC-06 Bluetooth module, supporting customizable control commands.  
- **OLED Expression Display**: A 128×64 OLED screen can switch between multiple preset expressions (e.g., happy, angry, confused).  


## Hardware List  

| Component Name               | Quantity | Description                                  |
| ---------------------------- | -------- | -------------------------------------------- |
| STM32F103C8T6 Development Board | 1        | Main controller with PWM, USART, I2C interfaces |
| SG90 Servo                   | 8        | Actuator for leg movement                    |
| HC-05/HC-06 Bluetooth Module | 1        | Enables wireless communication with mobile phones |
| SSD1306 OLED Display         | 1        | Displays expressions and debugging information |
| Servo Driver Power Supply    | 1        | Powers servos independently (5V/2A or higher) |
| Spider Robot Mechanical Kit  | 1 set    | 3D-printed structural parts                  |
| Dupont Wires, Breadboard     | Several  | For circuit connections                      |


## Hardware Wiring Diagram  

### STM32F103C8T6 Connection to Peripherals  
- **Servo Control**: The `PA0, 1, 2, 3, 6, 7` and `PB0, 1` pins of the STM32 output PWM signals, which connect to the signal pins of the 8 servos respectively. (Servos are powered by an external 5V power supply; their GND must share a common ground with the STM32.)  
- **Bluetooth Module**: The `TX` pin of HC-05 connects to `USART1_RX (PA10)` of the STM32, and its `RX` pin connects to `USART1_TX (PA9)` of the STM32. `VCC` connects to 5V, and `GND` connects to ground.  
- **OLED Display**: The `SDA` pin of the SSD1306 connects to `PB7` of the STM32, and its `SCL` pin connects to `PB6` of the STM32. `VCC` connects to 3.3V, and `GND` connects to ground.  


## Software Environment  
- Development Tool: Keil uVision  
- Dependent Libraries:  
  - STM32 Standard Peripheral Library  
  - SSD1306 OLED Driver Library  


## Firmware Compilation and Flashing  
1. **Project Import**: Import the repository code into Keil uVision, and set the chip model to `STM32F103C8T6`.  
2. **Compilation Settings**: Select the compilation target (`Debug` or `Release`), then click "Build" to generate a binary file (.hex or .bin).  
3. **Firmware Flashing**: Use an ST-Link/Daplink/Jlink to flash the firmware onto the STM32 development board.  


## Bluetooth Remote Control Operation  
1. **Mobile App Selection**: Download a "Bluetooth Serial Assistant" app.  
2. **Bluetooth Pairing**: Enable Bluetooth on your phone, and connect to the device named "HC-05" (default password: `1234` or `0000`).  
3. **Send Control Commands**: Send predefined commands via the app to control the robot’s movement or switch OLED expressions.  


## OLED Expression Display Configuration  
Preset expressions are stored in the `main.c` file, with each expression represented as 128×64 pixel dot matrix data. To customize an expression:  
1. Use an **OLED dot matrix generation tool** (e.g., "Modulation Software") to create a dot matrix array.  
2. Replace the array of the target expression with the newly generated one.  


## Notes  
1. **Power Isolation**: Servos must be powered by an independent power supply. Using the STM32’s power directly may cause the STM32 to reset or be damaged due to excessive current.  
2. **Servo Angle Range**: Confirm the maximum rotation angle of each servo during debugging to avoid mechanical jamming.  
3. **Bluetooth Pairing**: If the Bluetooth module fails to connect, try resetting the module.  
4. **OLED Initialization**: If the screen shows no content, check the I2C pin wiring and the OLED’s address.  


## Contributions and Extensions  
PRs for feature expansion are welcome, such as:  
- Adding multi-mode movements (e.g., obstacle avoidance, autonomous cruising).  
- Optimizing the Bluetooth communication protocol.  
- Expanding more OLED expressions or displaying sensor data.  

