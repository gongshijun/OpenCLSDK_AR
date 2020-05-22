<!--
 * @Description: Copyright(c) All rights reserved.
 * @Company: YUSUR
 * @Author: Shijun Gong
 * @Date: 2020-05-18 15:22:23
 * @LastEditors: Shijun Gong
 * @LastEditTime: 2020-05-22 15:16:52
--> 
# OpenCL 介绍
OpenCL （全称Open Computing Language，开放运算语言）是第一个面向
异构系统通用目的并行编程的开放式、免费标准。也是一个统一的编程环境，便于
软件开发人员为高性能计算服务器、桌面计算系统、手持设备编写高效轻便的代码，
而且广泛适用于多核处理器（CPU）、Cell类型架构以及数字信号处理器（DSP）
等其他并行处理器，在游戏、娱乐、科研、医疗等各种灵越都有广阔的发展前景。

OpenCL最初由苹果公司开发，拥有其商标权，并在于AMD，IBM，Intel和NVIDIA
技术团队的合作之下初步完善。随后，苹果公司将这一草案提交至Khronos Group。

2008年6月的WWDC大会上，苹果提出了OpenCL规范，旨在提供一个通用的开放API，
在此基础上开发GPU通用计算软件。随后，Khronos Group宣布成立GPU通用计算开
放行业标准工作组，以苹果的提案为基础创立OpenCL行业规范。5个月后的2008年
11月18日，该工作组完成了OpenCL 1.0规范的技术细节。2010年6月14日，
OpenCL 1.1 发布。2011年11月15日，OpenCL 1.2 发布。2013年11月19日，
OpenCL 2.0发布。

### 版本历史
#### OpenCL 1.0
OpenCL 1.0主要由一个并行计算API和一种针对此类计算的编程语言组成，此外还特别定义了：
1、C99编程语言并行扩展子集;
2、适用于各种类型异构处理器的坐标数据和基于任务并行计算API;
3、基于IEEE 754标准的数字条件;
4、与OpenGL、OpenGL ES和其他图形类API高效互通。

#### OpenCL 1.1
Khronos Group2010年6月15日宣布，OpenCL通用计算标准的1.1版本已经发放，开发者可以免费下载，并依照新标准开始进行编程。
OpenCL 1.1标准向下兼容1.0版，提供了更多的新功能，并对性能进行了改善。主要新特性包括：
- 支持新数据类型，如3维矢量和新增图像格式。
- 支持处理多Host指令以及跨设备Buffer处理。
- Buffer区域操作，包括对1D、2D、3D三角形区域的读、写和拷贝操作。
- 改进驱动和控制指令执行的事件应用。
- 增加OpenCL内建C功能。
- 通过链接OpenCL和OpenGL事件，高效共享图像和Buffer，改进与OpenGL的互操作性。

OpenCL标准由Khronos Group的OpenCL工作组制定，完全开放，任何开发者都可免费使用。OpenCL工作组成员包括（英文首字母排序）：3DLABS、动视暴雪、AMD、苹果、ARM、Broadcom、CodePlay、EA、爱立信、飞思卡尔、富士通、通用电气、GraphicRemedy、HI、IBM、Intel、Imagination Technologies、美国Los Alamos国家实验室、摩托罗拉、Movidia、诺基亚、NVIDIA、Petapath、QNX、高通、RapidMind、三星、Seaweed、S3、意法半导体、Takumi、德州仪器、东芝和Vivante。

#### OpenCL 2.0
Khronos Group2013年11月19日宣布了OpenCL通用计算标准的2.0版本特性，其中对共享虚拟内存的支持是一大亮点（此前NVIDIA发布了CUDA 6规范也同样支持共享虚拟内存，但目前仅限Kepler和Maxwell架构的N卡。此外，AMD的GCN架构显卡同样支持。AMD的Kaveri APU支持HSA异构计算和hUMA统一物理寻址，较虚拟共享更加先进。）
1、共享虚拟内存
主机和设备内核可以直接共享复杂的、包含指针的数据结构，大大提高编程灵活性，避免冗余的数据转移。
2、动态并行
设备内核可以在无需主机交互的情况下进行内核排队，实现灵活的工作调度，避免数据转移，大大减轻主处理器的负担。
3、通用内存空间
无需指定地址空间名称即可为引数(argument)编写函数，不用再为程序里的每一个地址空间名称编写函数。
4、图像
改进图像支持，包括sRGB、3D，内核可以读写同一图像。
5、C11原子操作
新的C11原子和同步操作子集，分配在同一工作组内
6、Pipes
以FIFO格式组织数据的内存对象，可以直接读写，数据结构可简单编程、高度优化。
7、安卓可安装客户端驱动扩展
安卓系统上可将OpenCL作为共享对象进行载入。

### 存储体系
OpenCL包含四层的存储体系：

1. 全局存储（global memory）：所有PE共享，具有最高的访问延迟；
2. 只读存储（read-only memory）：只有主机端cpu具有写权限，设备端只能访问，通常比较小，延迟比较低；
3. 本地存储（local memory）：设备端PE共享；
4. PE私有存储（per-element private memory）：registers

在实现OpenCL标准时，不需要所有设备实现所有level的存储体系。此外，介于不同level存储体系之间的数据一致性也是比较宽松的。同时，设备端可以或者不实现与主机端cpu之间的数据共享，OpenCL 提供了专门的API实现不同主机端与设备端的数据读写。

# OpenCL详细介绍
OpenCL尤其适合在那些新兴的将一般的并行计算算法与图形渲染流程结合的图形交互式应用中扮演着一个越来越重要角色。

## OpenCL 1.0
OpenCL标准：
1. 支持数据和任务级的并行程序模型
2. 采用ISO C99子集扩展
3. 基于IEEE 754标准的数字条件
4. 与OpenGL、OpenGL ES和其他图形类API高效互通。

### OpenCL结构
OpenCL是一个开放的异构计算编程行业标准，该平台可以包括CPU、GPU、以及其他离散的计算设备。OpenCL是一个并行编程框架，包括编程语言、API、库、以及一个支持软件开发的运行时系统。例如，通过OpenCL，程序员可以通过写通用的程序，就能够在GPU上运行，而不需要将他们的算法映射成3D图形API像OpenGL或者DirectX那样。

#### 平台模型
#### 执行模型
#### 编程模型
#### OpenCL框架 