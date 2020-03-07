# 迷宫算法-问题描述

![](./assets/2020-02-29-14-12-22.png)


* 0代表路 1代表墙
* 从左上角走到右下角
* 使用广度优先算法求出最段路径


## 思路步骤 

* 初始状态 
![](./assets/2020-02-29-14-22-56.png)  

* 探索第一个点（0，0）  
![](./assets/2020-02-29-14-23-25.png)

* 探索第二个点(1,0)   
![](./assets/2020-02-29-14-24-25.png)

* ...

* 最终状态  
![](./assets/2020-02-29-14-25-03.png)


> 2个退出条件，1、到达终点，2、发现不了新的点。

