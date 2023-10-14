# L298N module
* L298N module uses 2 pins to control each motor; 2 motors maximium
* pin VIN and GND on the board accept 4.5V-36V external power supply
* connect pin IN1, IN2, IN3, IN4 to pin 2,3,4,5 on Arduino
* connect pin EN1, EN2 to pin 9,10 (with analog mode) on Arduino; or without EN1, EN2 with jumper in place
* connect pin +5V, GND to pin Vcc and GND on Arduino to power it up (it requires 12V maximium voltage connects to VIN)
* if the input voltage over 12V connecting to the VIN, it will burn the on-board bec, so remove the jumper before connection; and power up the l298n by using the +5V pin 

# Notice
1、共地问题
L298N 通常需要使用单片机提供 PWM 信号作为输入调速信号，具体怎么实现的懂电路的同学可以把原理图找来看看，虽然有很多版本，但是基本都是大同小异。
做软件的同学需要注意的是：PWM 的占空比与电压之间的换算关系，
另外有一条最需要注意的就是PWM 不能直接控制电机转动！！！！！！！！！别把PWM直接接电机！！！！！

原因分析：
通常这种行为是用 Arduino 板子时出现的，因为这东西可以 USB 供电，所以很多人直接在线调试，调个GPIO（小灯）还可以，但是调电机的时候用电池给L298N供电。

共地要求单片机的地（GND）和电机（motors，任意1根线，非必要）、L298N 的GND、直流电源（GND）是同一个。

现象

当不满足上述条件时可能出现的现象（自己遇到过的）：

（1）电机不转；

（2）输出端口电压 0V；

（3）电笔或其他导体（包括手）触碰输出端子，电机转动（可能是静电导致）。

解决方案：

自己想办法使两个共地吧，不要简单地把两个GND连在一起~！

2、功率不足
有些人可能了解共地的重要性，但是明明线连的都对，为什么电机还是不转呢？

出现原因

这时候你就要考虑整体功率不足的问题了，因为L298N本身需要一定的电能（忘记在哪看到的），所以在驱动电机的时候，5V电压根本带不动电机，表面 5V 的电压，电流可能远不达标。

现象：

出现这种问题的通常是因为单片机供电 5V 左右就可以了，而L298N也可以5V供电，为了方便，当然是单电源双用，这时会出现以下现象（自己遇到过的）：

（1）电机不转；

（2）带负载时电机输出端子电压很小；

（3）卸掉负载电机后电压正常；

（4）指示灯（L1,L2,L3,L4）按程序正常闪烁。

解决方案：

选取12V电源，对L298N和单片机供电，单片机如果需要5V的话，还需要接一个稳压模块或自己做降压（不推荐，烧过一块板子，伤心）。


# Block Description
* Use the first block to initialize the module
* Use the second block in while loop to repeatedly request for data
* Use the third and fourth block the calculate the roll and pitch angle respectively

# Release Logs
* V0.0.1  Basic functions completed.
