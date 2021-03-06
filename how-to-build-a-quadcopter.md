---
layout: post
title: How To Build A Quadcopter
comments: true
---

# how-to-build-a-quadcopter

飞行器的原理非常简单，只要产生足够的升力减去自重就可以起飞了，但是我们都知道螺旋桨旋转时会产生反扭力，因此一般会使用两个以上的螺旋桨反方向旋转\(直升机\)，这样就可以消除反扭力造成的影响。而四轴\(或以上\)的飞行器为了实现更多姿态会使用相邻两个方向相反，相对两个方向相同，如果要水平移动只需要让相对的两个螺旋桨加速，另外两个减速，是反扭力失衡，但总升力保持不变，这样飞行器就可以慢慢旋转了。

## 机架

我们上面提到，为了实现更多姿态控制我们通常会制作四轴以上的飞行器，以四轴为例一般会使用X形或者十字形，两种从外观上没什么区别，只是在飞行时前进方向\(即：头\)不太一样。理论上只要宽高相等，四个螺旋桨大打架就可以，你甚至可以自制机架，购买成品的话，比较成熟的方案是DJI大疆的F450，轴距是450mm，材料是工程塑料，为了简化布线F450机架自带了两块PCB主板，为了容易分辨飞行器升空以后的前后方向，机臂使用两种不同的颜色，因为白色与天空颜色对比不明显，我们一般建议选择红色和黑色。

每个机臂需要6颗M2.5\_6的螺丝与主板链接，4颗M3\_8螺丝用来固定电机，需要注意的是电机螺丝不要太长，否则可能会顶到电机定子的线圈，发生短路，损坏电机。

## 电机

如果玩过遥控飞机或者遥控汽车的人对电机应该不会陌生，电机一般分为有刷电机和无刷电机两种，有刷电机转子上带有线圈，通过电刷不断切换相位来产生磁场使转子旋转。而无刷电机则将线圈放到定子上，通过电调产生磁场使转子旋转。

为了产生更高的速度和力量我们通常会选择使用无刷电机，无刷电机相对有刷电机寿命更长，性能更稳定。

无刷电机型号目前没有一个统一的标准，比较通用的一种是内径标示法，即标示电机外转子内径，从一定程度上可以反映出电机的线圈直径和匝数。

一般我们会选择 2212或者2216电机等，其中前两位表示转子的直径，后两位表示转子的高度，简单来讲，前来两位越大，电机越肥，后面两位越大，电机越高。又高又大的电机功率就越大，耗电也越高。

一般电机会表示KV值，KV值是电机输入电压每提高1V电机空载转速提高的量。比如1400KV就表示在电机空载的情况下，加1V电压，转速为每分钟1400转，2V电压每分钟转速2800转，以此类推。同电机型号低KV值比高KV值的电机提供的扭力大，类似于汽车的1档虽然慢，但是爬坡更容易。但由于低KV值电机为了克服反扭力需要配大浆才能起飞，也就需要大机架，所以我们通常会选择800KV以上1400KV以下的电机。

国产电机品牌比较便宜，新西达，朗宇等是性价比比较高的电机品牌，比较适合新手。

## 电调

电调全称是电子调速器，针对电机结构不同分为有刷电子调速器和无刷电子调速器，它根据控制信号调节电机的转速。简单来讲就是将电池的直流电转换为三相交流电，并按照输入的指令调整供给电机的电压。实现电机转速可控。

## 主控

QQ飞控， APM

飞行控制板简称飞控，如果没有飞控板，四轴飞行器就会因为安装、外界干扰、零件之间的不一致型等原因形成飞行力量不平衡，后果就是左右、上下的胡乱翻滚，根本无法飞行，飞控的作用就是通过飞控板上的陀螺仪，对四轴飞行状态进行快速调整，如发现右边力量大，向左倾斜，那么就减弱右边电流输出，电机变慢，升力变小，达到平衡的状态。


购买飞控的时候老板会问你买X模式还是+模式，简单来说X模式要难飞一点，但动作更灵活。+模式要好飞一点，动作灵活差一点，如果飞控板安装错误，会剧烈的晃动，根本无法飞。常见的有KK、FF、玉兔、MMC等品牌，我购买的是MWC10 四轴飞控.

## 螺旋浆


同电机类似，桨也有如1045,7040等4位数字，前面2位代表桨的直径，也就是从桨的一头到另一头的长度，单位是英寸。后面两位数是指几何螺距，螺距原指螺纹上相邻两牙对应点之间的轴向距离，可以理解为螺丝转动一圈，前进的距离。而螺旋桨的螺距，是螺旋桨在固体介质内无摩擦旋转一周所前进的距离。简单来说可以理解为螺旋桨桨叶的“倾斜度”，螺距标称越大，倾斜度越大。桨长度和螺距越大，所需要的电机或发动机级别就越大，桨的长度越大，某种程度上能够保证飞机俯仰稳定性越高，螺距越大，飞行速度越快。


四轴飞行为了抵消螺旋桨的自旋，相隔的桨旋转方向是不一样的，所以需要正反桨。正反桨的风都向下吹。顺时针旋转的叫正浆、逆时针旋转的是反浆。安装的时候，一定记得无论正反桨，有字的一面是向上的。

## 遥控器，接收器

遥控器从几百到数千不等，常见品牌有国产天地飞，日本futaba等，根据所需通道和预算购买即可。通道就是遥控器控制的动作路数，比如遥控器只能控制四轴上下飞，那么就是1个通道。但四轴在控制过程中需要控制的动作路数有：上下、左右、前后、旋转，所以最低得4通道遥控器。

## 电池，充电器

由于同样的电池容量锂电最轻，起飞效率最高，所以电池一般使用锂聚合物电池，锂聚合物电池单片电压为3.7V，两片或三片串联得到的电压即为上面说到的7.4V或者11.1V。mah表示电池容量，如1000mah电池，即如果以1000ma放电，可持续放电1小时。如果以500mh放电，可以持续放电2小时。

在实际选购过程中电池后面有2S、3S、5C等字样，S代表锂电池的节数，锂电池1节标准电压为3.7v，那么3S电池，就是代表有3个3.7v电池在里面，电压为11.1v。C代表电池放电能力，这是普通锂电池和动力锂电池最重要区别，动力锂电池需要很大电流放电，这个放电能力就是C来表示。如1000mah电池标准为5c，那么用5x1000mah，得出电池可以以5000mh的电流强度放电。这很重要，如果用低C的电池，大电流放电，电池会迅速损坏，甚至自燃。与上面的C一样，多少C快充即快速充电的能力，如1000mah电池，2C快充，就代表可以用2000ma的电流来充电。千万不要图快冒然用大电流，超过规定参数充电，电池很容易损坏。


有了电池，充电器自然必不可少，一般选用平衡充。如3s电池，内部是3个锂电池，因为制造工艺原因，没办法保证每个电池完全一致，充电放电特性都有差异，电池串联的情况下，就容易造成某些放电过度或充电过度，充电不饱满等，所以解决办法是分别对内部单节电池充电，而平衡充则很好的解决了这个问题。

至于怎么配电池这与选择的电机、螺旋桨，想要的飞行时间相关。容量越大，c越高，s越多，电池越重；基本原理是用大桨，因为整体搭配下来功率高，自身升力大，为了保证可玩时间，可选高容量，高c，3s以上电池。常用的四轴电池为20C、3S电池。


