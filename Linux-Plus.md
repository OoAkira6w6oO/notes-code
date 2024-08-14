## Linux的文件目录

- 采用tree目录结构，只有一个根目录
- 在Linux中一切均为文件
  - 指令文件
    - /bin 常用指令
    - /sbin 超级用户指令
  - 日志文件
    - /lost+found 非法关机后存放的某些文件
    - /var
      - var其实是variable的缩写，存放动态可变文件
      - 日志 / 打印 / 邮件 / lock等
  - 设备文件
    - /dev 管理设备CPU、Disk等
    - /media 媒体设备
    - /etc 配置文件
  - 系统文件
    - /proc 内核相关
    - /sys 系统
    - /srv 服务
  - 文件管理
    - /mnt 挂载，让用户临时挂载别的文件系统
    - /opt 安装文件
    - /usr/local 通过编译源码的方式安装的程序
    - /usr 用户安装的软件
  - 其他
    - /home 用户
    - /lib 动态库
    - /root 根用户
    - /selinux 安全子系统
    - /tmp 临时文件夹
    - /boot 启动

## VMWare

- 虚拟机，用来安装Linux
- 通过VMWare创建虚拟机空间 => 在虚拟机空尽安装CentOS系统文件
- bios配置
  - 处理器个数
  - 网络连接方式
    - 桥连接：给Linux系统分配一个相同网段下的IP，Linux可以和和网络下其他系统通信，但是可能出现IP地址冲突
    - NAT模式：主机会有2个IP地址，Linux和其中一个位于同一网段。外部网段无法找到Linux，Linux可以找到外部其他网段。
      - NAT（网络地址转换，Network Address Translation）是一种常用的网络连接方式。
      - 使用NAT模式时，虚拟机会通过主机（即运行虚拟机的物理计算机）的网络连接来访问外部网络。
    - 主机模式：Linux是独立主机，无法访问外网
  - CD/DVD中指向CentOS.iso
  - Linux的分区
    - boot 200M
      - 挂载点，Linux启动时需要的引导文件 
    - swap 2048M
      - 交换分区，系统内存不够时可以用swap暂时替代内存
      - 分区太大会导致性能下降
      - 物理内存的1.5～2倍
    - root
  - kdump
    - 内核崩溃转存储机制，会占用一部分内存

## CentOS

| 命令    | 功能           |
| ------- | -------------- |
| ip addr | 查看本机IP地址 |

## 找到Linux中root密码

- 思路：使用单用户模式，此时不需要密码就可以登录
- 步骤
  - 启动
  - 引导时按下enter
  - 新界面，输入e
  - 新界面，选择kernel
  - 输入e
  - 输入 “空格 1”
  - 输入 b
