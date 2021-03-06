作品名称：a simple game based on RT-Thread
===========================================

【背景描述】
-----------
    自己对操作系统比较感兴趣，有一次看了RT-Thread4.0的发布会。那个时候是考研的最后两个月，我还是决定参加了RT-Thread的学生培训。前六周的学习都只是把RTT工程师给的代码理解并自己运行了一遍，虽然体会到了RTT功能强大，但是自己对它的了解和掌握还是很基础，于是第七周做一个小作品来锻炼巩固自己学习的知识，经过考虑，就做了这样一个难度不是很大的小游戏，这也是刚出手机那个时代手机上的游戏。

【所用物料及实物图】
------------------ 
   #####  材料：一个stm32最小系统（带按键和led），oled显示屏，ST-link下载器和串口线（在淘宝店铺平衡小车之家都能买到）
   #####  实物图：
			 
			 菜单界面							   难度选择
 
			 
			 分数查看							   游戏界面
   #####  主控：STM32F103C8T6		
   #####  编译环境：Keil 5		
   #####  RT-Thread版本：4.0.0

【硬件设计】
-----------
    一个主控，一个按键（PA5），一个led（PA4），
    oled显示屏（IIC协议RST -> PB3, DC ->PA15, SCL->PB5,SDA->PB4）

【软件设计】
-----------
    thread1:显示菜单，选择难度，显示历史分数。根据邮箱接收的信息切换各状态；
    thread2:按键单击和双击的识别并发送到邮箱；
    thread3:游戏界面，动态显示障碍物，根据邮箱接收的信息动态显示飞机，检测是否碰撞，游戏结束时记录分数并显示；
    thread4:按键长按处理，将长按时间发送到邮箱。
    thread1,2和3,4两组不同时运行；（具体见代码，注释很详细）
    
【RT-Thread使用情况介绍】
-----------------------
    1、使用多个线程；
    2、线程中采用邮箱通信；
    3、按键处理和计分使用了定时器
    4、使用msh在线修改一些参数；
    5、通过RT_ASSERT快速的查错；
    6、使用rtt typedef的数据类型。
    
【项目难点介绍】
--------------
    1、各个线程的功能设计；
    2、动态显示障碍物，保证一定的帧率；
    3、障碍物的高低，空余的间隔控制要合理；
    4、飞机与障碍物的碰撞检测。
    5、每一部分都要注意效率，因为oled提供的api导致各生成图形都得描点，效率很低，要保证一定帧率，低于10帧人眼看着就很不适。
    
【收获】
--------  
    首先把前几周做的题目都复习了一下，然后这个游戏大概花了两个白天的时间做的，基本上熟悉了RT-Thread的一些基本函数，最重要的是对如何合理的设计各个线程，线程采用何种方式进行通信有了一定的自己的体会，在代码效率和可读性方面有了进一步的提升，一定程度上提升了自己的编程经验吧。也希望能看到其他同学精彩的设计。
    
【演示视频】
------------
[https://v.youku.com/v_show/id_XMzk5NjY1MTcwNA==.html](https://v.youku.com/v_show/id_XMzk5NjY1MTcwNA==.html)
    
