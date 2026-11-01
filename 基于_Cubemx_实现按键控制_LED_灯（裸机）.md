# 基于 Cubemx 实现按键控制 LED 灯（裸机）

# 实验目的

1. 验证开发环境
2. 检验基于 Cubemx 搭建 STM32 裸机开发的能力
3. 理解按键的电路原理
4. 理解 LED 灯的电路原理

## **准备过程中遇到问题一定要先参考后面的Q&A**

# 学习资料

> **前几节平行基础课，已经确认熟悉的内容可以根据自己情况进行跳过**
> （这些优秀的外部链接很适合从全方位角度去科普理解基础知识，作为前置知识补充，如果有不熟悉的内容建议全部看完，然后再去看我们最后面的手把手教学，才能达到最好的学习效果！）

## 理解GPIO原理和编程（内容较多，如果这块有一定基础可以跳过，直接看后面零基础小白手把手实操）

[28 GPIO Pin and GPIO Port](https://twd6onxsxva.feishu.cn/docx/FfaRdKF65olq4PxtMX6c45UwnKf)

[29 GPIO幕后的工作原理](https://twd6onxsxva.feishu.cn/docx/GIzMdqRexoU32Kxoe6Pcz2b3nY7)

[30 GPIO输入模式下的高阻抗](https://twd6onxsxva.feishu.cn/docx/Qbf9dv6oWoRt8PxteDScMBprn7c)

[31 GPIO输入模式下的上下拉](https://twd6onxsxva.feishu.cn/docx/IKdQdzTAKog4BzxwyxdcJhWhnuc)

[32 开漏输出](https://twd6onxsxva.feishu.cn/docx/Iev4dfDqlo79rQxwzPYcy8Mpn9z)

[33 开漏输出（I2C）](https://twd6onxsxva.feishu.cn/docx/VkdtdUdWQo16LLx8WXqcKlvhnTc)

[34 推挽输出](https://twd6onxsxva.feishu.cn/docx/Oq6hdvdmfoH6u8xKbf0cj0ksnxb)

[35 浮空输入引脚可能会导致漏电流](https://twd6onxsxva.feishu.cn/docx/BBf8dy2PJoL5DixibgHcyDP1n6f)

[36 GPIO编程架构解析](https://twd6onxsxva.feishu.cn/docx/UtdGdaoe3oFmbYx0XXFceW3knRg)

[37 STM32F411CEU6核心板上的GPIO Port和Pin](https://twd6onxsxva.feishu.cn/docx/LEfFd1J5mopQPBxzkxRcc35knxc)

[38 GPIO Moder Register](https://twd6onxsxva.feishu.cn/docx/Gq6Id1QMNo9yWTxSQ6icODuHn2g)

[39 GPIO引脚的输入配置](https://twd6onxsxva.feishu.cn/docx/EzFzdNymAoZczGxFB0ncv48jnXg)

[40 GPIO 引脚的输出配置](https://twd6onxsxva.feishu.cn/docx/OGf3dkOT7orSUJxKxQ9cWWMmnWe)

[41 开漏输出配置](https://twd6onxsxva.feishu.cn/docx/QPEgdhPddo8qkzxQSREcILwVndg)

[42 输出模式下的输入驱动电路](https://twd6onxsxva.feishu.cn/docx/LAk8dAFndovEoLxaLuUcbIjgnLe)

[43 GPIO的复用功能配置](https://twd6onxsxva.feishu.cn/docx/Tck3dxwi5oPVYyxkXBAcYAYDnKc)

[44 GPIO输出类型寄存器](https://twd6onxsxva.feishu.cn/docx/Q277dAahPocddNxgUKJc6X7Pnbe)

[45 GPIO速度寄存器](https://twd6onxsxva.feishu.cn/docx/Bl0hd7X0moSOg7xPQ3mcmLdSnpd)

[46 GPIO上下拉寄存器](https://twd6onxsxva.feishu.cn/docx/MtvWdv8kpoynZwxyTLBc8M50n3d)

[47 GPIO输入数据寄存器](https://twd6onxsxva.feishu.cn/docx/CDWodUUOeoYsP6xhrAFcLDR8neb?from=from_copylink)

[48 GPIO输出数据寄存器](https://twd6onxsxva.feishu.cn/docx/YUUHdgQCsoTfB9xdZ6hczr5Hn1E?from=from_copylink)

## 时钟理解

[【STM32】超清晰STM32时钟树动画讲解_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ph4y1e7Ey/?vd_source=9aa8b5f39d390182510fb79554840e31)（外部链接不用实操，理解原理即可）

## 按键电路工作原理

[【小白也看的懂的按键输入原理】 ](https://www.bilibili.com/video/BV1LP411h7ND/?share_source=copy_web&vd_source=15bad2bcd085cfc0439f4c8d50ecb9b5)（外部链接不用实操，理解原理即可）

## LED 控制原理

##  WeAct 开发板资料

https://github.com/WeActStudio/WeActStudio.MiniSTM32F4x1

https://gitee.com/WeAct-TC/WeActStudio.MiniSTM32F4x1

![b25d058a674bded703b1922e12a129ef.jpg](assets/17.jpg)

![8fe506a18998524dcf87536114c8fded.jpg](assets/1.jpg)

![image.png](assets/15.png)

![d31f7e8892a3a339f3eb7abff13a8cb6.jpg](assets/16.jpg)

## 实现按键控制 LED

[【第 4 集 按键控制小灯 GPIO 输入】 ](https://www.bilibili.com/video/BV1Z84y157dx/?share_source=copy_web&vd_source=15bad2bcd085cfc0439f4c8d50ecb9b5)

## [Jlink介绍和使用](https://twd6onxsxva.feishu.cn/docx/YG4FdvNH8oJVelxvAGDciqGgnCk?from=from_copylink)

## 零基础小白手把手实操（有经验的同学可以不看视频直接操作）

### **7.1. 硬件环境确认(5mins）**

录制文件：https://meeting.tencent.com/crm/lv9BZRb464

密码：XCKX

### **7.2. 软件环境确认(5mins）**

录制文件：https://meeting.tencent.com/crm/NQDZL7yJ15

密码：YRHA

### **7.3. 下载开发板资料和讲解（13mins）**

录制文件：https://meeting.tencent.com/crm/NoqMPxPa79

密码：ES6K

录制文件：https://meeting.tencent.com/crm/2k0qMEGYff

密码：ZJF6

录制文件：https://meeting.tencent.com/crm/NQDZoQ8Xd5

密码：QKFC

### **7.4. 查看电路原理图（电源|复位）（7mins）**

录制文件：https://meeting.tencent.com/crm/K07pXoQrc8

密码：NP8X

### **7.5. 查看电路原理图（LED灯|按键）（6mins）**

录制文件：https://meeting.tencent.com/crm/l7QkWVX8bf

密码：ZYKQ

### **7.6. 通过Cubemx配置单片机裸机运行环境（10mins）**

录制文件：https://meeting.tencent.com/crm/NQDZZz5p4c

密码：63I4

[06_LED.7z](assets/06_LED.7z)

> 链接: https://pan.baidu.com/s/1-I5susOooPepevY2JxwYkA?pwd=hzah 提取码: hzah 

### **7.7. 控制LED进行闪烁**

#### 7.7.1 下载配置**（1mins）**

录制文件：https://meeting.tencent.com/crm/ldgBBVaYba

密码：ZFJJ

#### 7.7.2 编写LED控制代码和延时，让它闪烁**（7mins）**

录制文件：https://meeting.tencent.com/crm/l5XGQX5Zce

密码：WTAW

[06_LED_V1.7z](assets/06_LED_V1.7z)

> 链接: https://pan.baidu.com/s/1Id3bgTSqy98uFE3K6uRkrQ?pwd=n9y2 提取码: n9y2 

#### 7.7.3 编写按键读取代码，让按键控制LED亮灭**（4mins）**

录制文件：https://meeting.tencent.com/crm/NgY3rzdz5a

密码：PPAE

[06_LED_V2.7z](assets/06_LED_V2.7z)

> 链接: https://pan.baidu.com/s/1EMPbj6M6ZP59z_2wDiyXZg?pwd=fv8h 提取码: fv8h 

# 实验内容

1. 用 STM32CubeMX 实现基于 STM32F411CEU6 开发板（WeAct Studio）的按键控制 LED 灯闪烁的工程。

（**若没有此开发板，先用自己身边的开发板快速开始**）

1. 已掌握 git 的同学，将本次作业上传 git 分支为：LED_Initial

还没掌握的同学，观看这节课：[2_Git和Gitee基础使用教程](https://twd6onxsxva.feishu.cn/docx/TI0KdKluJocukhxwv42cU1DinDf)

1. 后面我们每个作业代码都新建一个单独的分支，然后上传，最终是一个仓库，多个分支

> （比如这节平行基础课我们点亮完led，就上传git，后续可以作为我们做其他的基础工程，这样不用每次重复配置）

> 注：CubeMx 创建 Keil-MDK 工程时，绝对路径不允许带中文字符，否则工程生成有问题

1. 参与对本节课的课件质量进行反馈 https://www.wjx.cn/vm/wFz6Ccx.aspx

开发板若还没买，请快速下单：

 通用开发板：[item.taobao.com](https://item.taobao.com/item.htm?id=594670660262&spm=a1z10.1-c.w4004-21792748727.3.25f678f2xWEvJf&skuId=4275490085468) （平行作业需要，抓紧买）

> 2024.9.4 更新：**可以直接购买焊好 Flash 和排针版本**

![image.png](assets/8.png)

### 参考代码讲解

_对于零基础小白同学：这里的参考代码对于零基础小白同学可能难度较大，可做完前面的“7.零基础小白手把手实操”后直接开始下一节课，这里的参考代码看一看就行，等后面按键全部做完了，再回头来看亦可。_

<video src="assets/06裸机按键讲解_V1.mp4" controls width="100%"></video>

[06_Project.7z](assets/06_Project.7z)

> 链接: https://pan.baidu.com/s/1XQ8g1nxb4IcoMYWanjvBSg?pwd=es6t 提取码: es6t 

# 面试知识预习

### **C 语言运算符**

**运算符的优先级要熟悉**

1. 逗号运算符最后的结果是最后一位，如

x =(a=2,b=3,a+b)

结果为 5

1. 理解下列运算

a=5,b=10;

a=b++;

printf("%d,%d", a, b);

//结果是 10，11

1. a++的具体运算过程为：

int temp=a;

a=a+1;

return temp;

1. ++a 的具体运算过程为：

a=a+1;

return a;

# Q&A

### 问题 1：如何了解 Led 和按键硬件原理？

答 1：

![7b93bc245088e18b7bce6fbaedf0280.png](assets/7.png)

对于按键，我们这里可以看出，当按键按下时，右边接地，所以当按键按下时，我们的读取电平为低，并且由于外面没有上拉电阻，我们软件内部需要将该 Pin 的上拉电阻使能。

![06adac492015d72190b84578759d3c9.png](assets/6.png)

对于 Led，左边是 3V3，那么为了使 Led 点亮，Led 右边电压应该为 0，让二极管产生压降。  所以 PC13 输出低电平时，Led 点亮。

### 问题 2：当 CubeMx 不小心配置时钟超频了并下载进去，后续下载器无法识别芯片，如何解决？

因为超频，所以导致代码无法正常运行，此时我们需要按下开发板的 Boot0，重新上电，让 MCU 从内部 ROM（系统存储器）中启动，就可以识别到 MCU。

[10_STM32烧录某固件后提示识别不到芯片原理与解释](https://twd6onxsxva.feishu.cn/docx/MZMAdvxM3oXu9IxjtR9cSCGOnye)

### 问题 3：配置 GPIO 时的内部上下拉电阻，不太清晰

> 1. 设置为推挽输出模式，是否需要配置上拉下拉电阻，不太清晰
> ### 答：上下拉电阻的一大作用就是提供默认电平，不配置的话就是悬空，输出随机值
> 如果是开漏模式，配置上拉才能输出高电平
> 但是如果是推挽模式，我们初始化时一般已经会给一个默认电平，所以不需要配置，具体配置与否的区别，可以看下面列的表格
> 1. 然后按键配置输入模式的时候，外部没有上下拉电阻，配置成浮空输入实验现象也是正常的，这是为什么呢？
> 答：跟推挽模式的上下拉电阻同理，提供默认电平，不然引脚悬空的时候读取的电平是不确定的

![image.png](assets/3.png)

**GPIO 的管脚选用不同的模式并搭配上下拉电阻的实际输出表，所有搭配列举出来，更明确：**

![66ad5916835547e38f830182e67018f.png](assets/12.png)

### 问题 4：有的板子能带电烧录有的不能。有的能带电调试有的就不能，这种原因是因为电压不稳吗

答：不是，是因为有些调试器，它需要你输入一个参考电压，比如你看 Jlink 它有个管脚是 Vref，它要根据你的输入的参考电压（比如 MCU 电源电压 3.3V）来估计你的 TTL 电平范围。举例：如果你是 3.3V 的电源电压输入到 Vref，那你的 TTL 的高电平可能就是 2.6 到 3.3V（举例而已），如果你是 5V 的电源电压输入到 Vref，那你的 TTL 电平可能就是 4.3V 到 5V。

### 问题 5：下载完程序后程序不会自动运行

![be14a0b77f8c043b7815b9fd7d09b85.png](assets/5.png)

### **问题 6：CubeMX 的使用问题**

> ** **使用 CUBEMX 配置硬件在正常开发流程中会经常用到吗？是只在测试某个单元的时候使用？还是整个项目周期都会使用？感觉 CUBEMX 生成的代码结构和自己代码结构有些出入，实际使用起来有点乱。
> 答：根据个人和项目的情况，这个没有绝对的答案，仅仅是实现路径的差别而已。
> 关于 Cubemx 本质上是什么：
> Cubemx 只是一个通过选项选择来将它背后的一套已经验证过 HAL 库的初始化代码拼凑出来给你用的工具。
> 个人层面来讲：
> Cubemx 在项目开发前期（硬件选型确定后），移植操作系统，开发 BSP 程序时，用 Cubemx 可以节约片上外设初始化，Freertos 移植的时间。但是手工移植和初始化这些外设也不是不行，如果你能逐步移植和初始化（你理解每一步做什么，而不是去网上 Copy）到你正确想要的状态，那最好不过。
> 项目层面上来讲：
> Cubemx 能够加快最开始的 BSP 和操作系统甚至文件系统移植的速度，但是其在一定程度上也让用户容易忽略具体的初始化过程，（比如，在初始化串口和 DMA 时，可能它初始化的 DMA 模式是 Normal，但是用户可能默认以为它是 cycle），这增加了一点点的项目细节风险，但对于其提供的便利性来说无可厚非。因此，对于 Cubemx 的使用，既然要其速度，那我们也要配备相应检测手段，来确保这个工具是按照我们的目标运行的。如果要了解 Cubemx 具体如何操作了我们的项目，就要去我们后面作业中提到的，使用 VScode 差异对比，系统 System View 里去观察最终外设状态情况，来确保 Cubemx 是按照我们的意图在执行初始化。
> 另外，Cubemx 的工程代码生成是基于芯片厂商的角度来思考的，它把 OS 归于了中间件，我们的课程是依照项目角度来看的，所以把 RTOS 分到了 OS 层面。
> 市场上来讲，目前越来越多的公司使用 Cubemx，但大部分是在做 BSP 和系统移植时直接用 Cubemx 生成好初始化，后期就不再操作 Cubemx 了。

### 问题 7：老师，RTOS为什么会出现？

> 很早之前，在单片机开发工作中，其实并没有什么操作系统，因为我们单片机的项目并不复杂，小项目通过几个常规的任务不停去查询，然后配合一些中断（异常）来响应突发事件就够了。
> 但是随着系统应用（功能）的不断迭代和增加、修改，会发现，裸机的任何一个模块的代码的修改都很容易对其他模块产生干扰，模块彼此之间的干涉很严重。修改需要非常小心，尤其当需要配置的中断/异常越来越多的时候，就会发现非常难改，难度几何级上升。
> 所以这时候，裸机的开发工程师们，想出了一些类似于protothreads这类的事件驱动型的框架。但是在真实的项目中，可能有很多常规任务（轮询）和需要及时处理的事件，一旦有改动，干涉的代码就会非常多。
> 所以出现了RTOS这种兼容常规任务轮询和异常事件及响应兼顾的框架。本身RTOS中的各种IPC（消息队列，信号量，邮箱。。。）本质上都是全局变量，但是RTOS提供了这些API，同时提供了经过高手优化的临界区保护等手段，确保了这些API的安全。程序员使用这些API，可以大大简化程序员的操作，降低了大家开发复杂系统的难度。
> 另外，RTOS拥有的这一切好处并不是凭空得来的，代价是损失了CPU的计算资源，因为CPU需要再任务之间不停地切换（出栈入栈，上下文保存），这些都是浪费时间的，所以RTOS有个很重要的评价指标，就是RTOS自身任务切换会用掉CPU多少个指令时间。
> 再者，RTOS对使用者也有要求，比如说tick用多少合适，如果时间太短，那很大部分时间都用在栈切换上了，时间太长，任务轮询的时间刻度就变大了，无法得到及时响应。
> 总之，在裸机和RTOS之间，没有绝对的谁好谁坏。如果一个人裸机做的很厉害，能够有效规避任务修改对其他任务执行/响应产生的干涉，那肯定没问题。这就好比你跟用C++的人说，我用C结构体也能做出C++类的效果一样，以前用汇编的老前辈大拿也会说C语言没有汇编高效，都是一个道理，只能说各有各的好。
> 但是，从整个项目生命周期的角度来看，老板肯定不同意用汇编来做项目，这让后面的人根本没法维护；同样，如果用了RTOS，那后面项目在后期维护时，可以招会RTOS的人来快速上手维护。

### 问题 8：GPIO的几种模式

![image.png](assets/2.png)

### 问题 9 ：疑问：就是目前基本上都是用的国产芯片来实现产品，故没有cubemax这样的软件方便，就是基本用到的标准库，这样是否会有影响到不熟悉代码（用标准库的时候就不会操作了），后续会有通过标准库的讲解吗，还是其实通过cubemx也能不影响后续

> 先看下**问题6**中对cubemx使用的解答，工作中其实不太会使用这种图形化界面，各种外设配置定下后改动的机会也较少
> 那我们为什么要使用cubemx？因为我们每一个实验都会有比较多的配置，一是为了方便我们每个实验快速配置快速开发，抓住重点
> 二是方便我们的讲解，图形化界面非常直观精炼，基本能做到一看就懂，就跟玩游戏时各种参数设置一样
> 但是享受了这种方便之后，我们也需要有回归底层的能力，不光说是cubemx（他只是完成一个配置，实际上你很容易能找到它生成的对应代码），还包括像不管是HAL库，标准库。我们常说，敢用别人的库，你就必须得有随时能深入底层，深入寄存器去debug的能力，因为即使别人的库再经过验证，层层封装下来还是有可能出现意想不到的问题
> 所以cubemx，hal库，加快平常开发速度，我们要用；但是真正遇到问题，随时深入底层debug的能力，我们也要有
> ### **那具体怎么培养这种深入底层的能力？**
> 一是深入了解arm内核原理（调试技巧课中原理部分都会涉及）
> 二是跟着我们课程中故意设置的一些常见踩坑点，一步步深入底层，通过手把手视频来培养这种技巧和意识（手把手视频中，能够完整体会到老师当时的整个思考和判断过程）

### 问题10：Keil显示问题：

![1733409909463.png](assets/13.png)

### 问题11：Debug模式配置的问题

如下配置：

![image.png](assets/4.png)

每个配置的含义：

![476a1f3766f17cd90268d9670c9f0e7.png](assets/11.png)

参考链接：

[3_基于Cubemx搭建FreeRTOS开发环境](https://twd6onxsxva.feishu.cn/docx/YxeRdXVzwo6YqhxqNVacu0a2nQ9?from=from_copylink)

[10_STM32烧录某固件后提示识别不到芯片原理与解释](https://twd6onxsxva.feishu.cn/docx/MZMAdvxM3oXu9IxjtR9cSCGOnye?from=from_copylink)

### 问题12. Jlink下载失败怎么办？

1.确认下开发板上的USB-Type-C接口有没有接线。
2.先按下Boot0，然后再按下reset，然后再先松开reset，再松开boot0，看能不能查找到。
3.咨询下jlink的店家，他们家应该有专用的jlink驱动程序，试试。
4.截图一下你的jlink驱动版本。
5.看下设备管理器里面是否有jlink，右键jlink driver然后看看设备属性，截图。
6.用万用表测量下开发板上的vcc引脚是多少V，3.3引脚是多少v
7.cubemx这里要配置为serial wire

![](assets/14.jpg)

![](assets/9.jpg)

### 问题13. 编译时提示：Default Compiler Version 5' which is not available

![414aaac2034a6293015f01ac5cb8f99.png](assets/10.png)

https://blog.csdn.net/qcmyqcmy/article/details/125814461

可以参考下这个链接

### 问题14. 每一次作业都新建分支上传，那最后master放什么？

Master是要到系统集成阶段才用，快速就业路线前期不包括系统集成，来不及。

# 本节参考（学习完后再查看）

[06【参考】基于Cubemx实现按键控制LED（裸机）](https://twd6onxsxva.feishu.cn/docx/PTi0d7qVboMtcuxiie2cpiYInUf)
