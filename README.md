# Raspberry-CM4-USB_Camera

<details>
<summary>参考链接</summary>
    
## ip查找及登录  
1. [使用触摸屏控制树莓派](https://www.waveshare.net/wiki/15.6inch_HDMI_LCD_(H)_(%E5%B8%A6%E5%A4%96%E5%A3%B3)#.E6.90.AD.E9.85.8D.E6.A0.91.E8.8E.93.E6.B4.BE.E4.BD.BF.E7.94.A8)  
只做5)、6)、7)步  
__先连接屏幕再打开树莓派电源__，与电脑连接到同一手机热点  
2. [使用nmap指令获取树莓派ip](https://www.waveshare.net/wiki/Raspberry_Pi_Documentation#.E4.BD.BF.E7.94.A8nmap.E6.8C.87.E4.BB.A4.E8.8E.B7.E5.8F.96)  
3. [ssh、putty&vnc登录](https://www.waveshare.net/wiki/Raspberry_Pi_Documentation#SSH.E7.99.BB.E5.BD.95)  
 VNC为可视化界面，但putty、命令行更流畅
4. [摄像头校验&MJPG-streamer启动](https://www.waveshare.net/wiki/Raspberry_Pi_Documentation#MJPG-streamer)
   __无需执行安装及下载__
   
</details>

## UGV小车使用
连接小车WIFI:`UGC`, `12345678`

进入`192.168.4.1`控制小车行进

## 树莓派ssh登录  
ID：`pi`

KEY：`raspberry`  
## ssh登录示例
### 1. 连接WIFI
[新建WIFI](#新建wifi) 或 [使用 test WIFI](#创建test-wifi)
- #### 新建WIFI
  打开手机热点或使用其他WIFI，切勿使用带有AP隔离的公共WIFI

   [使用触摸屏控制树莓派](https://www.waveshare.net/wiki/15.6inch_HDMI_LCD_(H)_(%E5%B8%A6%E5%A4%96%E5%A3%B3)#.E6.90.AD.E9.85.8D.E6.A0.91.E8.8E.93.E6.B4.BE.E4.BD.BF.E7.94.A8)

   只做5)、6)、7)步，_**先连接屏幕再打开树莓派电源**_

   __将电脑连接到同一手机热点__
- #### 创建test WIFI
  设置手机热点或WIFI名称为`test`，密码为`12345678` 若后续发现无法连接，设置为2.4G

   打开电源即可

### 2. 获得电脑IP地址

输入命令

    ipconfig
### 3. 找到结果中`无线局域网适配器 WLAN`

    无线局域网适配器 WLAN:
    
       连接特定的 DNS 后缀 . . . . . . . :
       本地链接 IPv6 地址. . . . . . . . : fe80::2170:b943:1c89:a074%16
       IPv4 地址 . . . . . . . . . . . . : 192.168.43.236
       子网掩码  . . . . . . . . . . . . : 255.255.255.0
       默认网关. . . . . . . . . . . . . : 192.168.43.1
IP 地址是`192.168.43.236`，则其他设备的地址将在这个`192.168.43.0/24`子网范围内（这涵盖`192.168.43.0`到`192.168.43.255`）  
### 4. 扫描设备
输入命令

    nmap -sn 192.168.43.0/24
例
   
    Starting Nmap 7.92 ( https://nmap.org ) at 2024-12-13 18:30 中国标准时间
    Nmap scan report for 192.168.43.1
    Host is up (0.0092s latency).
    MAC Address: AA:7D:12:D5:A1:C1 (Unknown)
    Nmap scan report for raspberrypi (192.168.43.43)
    Host is up (0.043s latency).
    MAC Address: D8:3A:DD:CC:F7:93 (Unknown)
    Nmap scan report for LAPTOP-K28L6V18 (192.168.43.236)
    Host is up.
    Nmap done: 256 IP addresses (3 hosts up) scanned in 2.66 seconds
其中`Nmap scan report for raspberrypi (192.168.43.43)`为所需IP
### 5. ssh连接
输入命令

    ssh pi@192.168.43.43
显示`pi@192.168.43.43's password:`  
输入密码

    raspberry
通常密码不可见
### 6. 启动推流
切换管理员权限

    sudo su
启动推流

    cd mjpg-streamer/mjpg-streamer-experimental/
    sh start.sh
本例对应source链接

    http://192.168.43.43:8080/?action=stream

[新建WIFI](#新建wifi) 或 [使用 test WIFI](#创建test-wifi)
