## 1.项目名称：基于Arduino UNO开发板的童车倒车报警系统
## 开发环境：Arduino UNO开发板+HC-SR04模块+LCD1602+光敏电阻+蜂鸣器+LED灯+马达驱动器
项目描述：该项目主要利用Arduino软件编写HC-SR04（超声波模块）、LCD1602、蜂鸣器、LED灯、马达驱动器和光敏电阻的代码，将已完成的代码烧录到Arduino UNO开发板中，HC-SR04（超声波模块）会检测车后方的实时距离并显示在LCD1602屏幕上，当距离小于20厘米时，蜂鸣器、LED（红）灯、会发出警报并且由马达驱动器驱动的车轮也会停止转动以保证童车的安全。光敏电阻检测到亮度为暗时，自动打开车LED（白）灯。
<br>如图所示：
![](https://github.com/0000fine/1032303971-qq.com/blob/Photos/%E4%BB%BF%E7%9C%9F%E5%9B%BE.png) 



## 2.mysql服务设置远程连接 解决1251 client does not support ..问题
## 一、前期准备
1、虚拟机/物理机    mysql环境（非本机）
<br>2、本机 navicat软件（验证远程连接）
## 二 、mysql配置
1、在远程主机的本机   使用root用户连接mysql
<br>命令：mysql -u root -p
<br>备注 ： mysql -u 最高权限用户名 -p   再输入密码进入
<br>2、设置用户配置项
<br>(1) 查看用户信息
<br>select host,user,plugin,authentication_string from mysql.user;
<br>备注：host为 % 表示不限制ip   localhost表示本机使用    plugin非mysql_native_password 则需要修改密码
<br>(2)修改用户密码
<br>ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'newpassword'; 
<br>备注：更新一下用户的密码 root用户密码为newpassword



## 3.mysql数据库学习笔记
###数据库：
<br>RDBMS 关系数据库管理系统:     
    表（table）<br>    数据库（database）<br>    列（字段）<br>    行（记录）<br> 主键（唯一）<br>外键（关联两个表）<br>索引（目录）
<br>###基础命令：
<br>*create database 数据库名; 创建
<br>*drop database 数据库名； 删除
