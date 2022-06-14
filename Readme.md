# **Charles Sim Wind**

*A short description of the project*

- Bilibili: [Charles](https://space.bilibili.com/10189857?spm_id_from=333.1007.0.0)
- Github主页：https://github.com/Charlesip

Charles Sim Wind是基于Arduino的开源项目，依赖Simhub软件运行。

![](https://i.imgur.com/Sqi1WMc.png)

**Charles Sim Wind的一些特性：**

- Type-C供电
- 支持2个风扇
- NanoV3.0主控

- 完全安静的PWM直接调速

- 无需飞线



## **前言：**

Nano主控受Simhub的直接支持，这个项目本质上是整合了引脚飞线与12V供电，所以并不会有定制的固件与硬件后续失去维护的问题，但是依然有一些注意事项。

首先是需要注意电压：

1. Type-C供电，需要**有12V电压QC协议的**的充电器，12V电压与QC协议缺一不可（QC2.0或者3.0都可以）
2. 注意充电器和风扇的功率匹配

例：手机充电器支持**12V2A的QC协议**，也就是有24W输出能力，那么我的风扇两个加起来就不能超过24W。

注意：可以不用过于纠结风扇的功率，Simhub可以软件限制风扇的输出能力。目前我的电源是24W，两个风扇是65W，在Simhub里面也能正常工作。



------



## **硬件构建指南**

**材料列表与价格**

| 名称          | 总数 |
| ------------- | ---- |
| NanoV3主控    | 1    |
| 12V诱骗模块   | 1    |
| 风扇&主控排针 | 若干 |
| PCB           | 1    |
| 3D打印外壳    | 1    |



**原理图与文件**

PCB的Gerber文件开源，原理图如下（回头再补，在家里的电脑上），外壳的3D文件也一并开源，可以自行打印。

- Gerber.zip
- SimWind.dwg
- SimWind.stl
- SimWind(2).stl



**12V供电**

12V供电用的是YZX的诱骗模块，支持QC和PD双协议诱骗，焊接前注意设置好电压，正负不要焊反。



**对于3D打印请注意：**

外壳面板固定使用外径3.5mm的m2预埋铜柱。

对于树脂材料请使用SImWInd.stl，这份的开孔是标准的3.25mm。

如果采用尼龙材料，请使用文件SimWInd(2).stl，这个文件的孔径是更大的3.7mm，因为尼龙熔融冷却之后会收缩。这种尺寸的孔径，大概率会收缩15~25%。



------



## **软件方面**

这里我将以第一次接触Simhub的立场，介绍让风扇能转起来的最简步骤，如果想实现更加完美的风扇效果，需要阅读SImhub官方的文档以及翻阅一些论坛，将会涉及到风扇的校准等等步骤。

![](https://www.simhubdash.com/wp-content/uploads/2017/09/gamehub-icon-small-text-1.png)

▲依赖Simhub运行，[点击此处跳转官网](https://www.simhubdash.com/)

![](https://i.imgur.com/JzrE2zJ.png)

▲初次运行需要安装[CH340驱动](https://www.wch.cn/download/ch341ser_exe.html)

![](https://i.imgur.com/V95NAl6.png)

▲初次使用Simhub的话建议选择多设备支持，后续加设备就可以直接识别

![](https://i.imgur.com/1ROiyLv.png)

▲链接设备等待片刻会读取到设备信息

![](https://i.imgur.com/cajtjjb.png)

▲启用设备支持，注意，Shakelt Motors和Shakelt Wind都能驱动风扇，但是二者同时控制频道会出现问题，Shakelt Wind是新出的功能，我还没有研究所以接下来以Shakelt Motors举例。（但是我认为Shakelt Wind单从名字上来看就应该是更好的解决方案，所以建议大家研究一下）

![](https://i.imgur.com/IfiazXc.png)

▲进入Shakelt Motors选项卡之后按图启用设备支持与频道（Channel）

![](https://i.imgur.com/KyivmCk.png)

▲启用频道之后可以进入Effects Profile选项卡对设备进行设置，这一页的设置主要按照个人喜好进行调整，唯一需要注意的：请确保音量开关是开启的

**注意**：

对于需要重新修改本设备固件的情况，请在编辑器中如下图设置

![](https://i.imgur.com/G90m49o.png)

