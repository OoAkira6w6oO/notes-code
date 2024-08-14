# Linux

## 入门

### Linux用在哪里

- 服务器运维
- 嵌入式开发
- 程序开发

### Linux的主要发行版

- CentOS / Redhat
- Ubuntu

### VMWare

- 实践中，如何验证CentOS配置完毕
  - 在CentOS中顺利打开终端
  - 可以ping到外面
- VMTools
  - 设置CentOS和电脑之间的共享文件夹
  - 保证CentOS可以共享电脑的剪切板
  - 共享位置：CentOS/mnt/hgfs【Host-Guest File System

### XShell5 / Xftp5

- 远程登录Linux用的 / 远程服务器传输文件用的
- Linux需要开启sshd服务
  - 监听外部命令
  - 保证安全性一般只开放22port

### 命令

| 命令            | 功能                                               |
| --------------- | -------------------------------------------------- |
| shutdown -h now | 立即关机                                           |
| shutdown -h 1   | 1分钟后关机                                        |
| shutdown -r now | 立即重启                                           |
| halt            | 关机                                               |
| reboot          | 重启                                               |
| sync            | 将内存数据同步到磁盘，关机和重启前都应使用sync命令 |
| man [cmd/ file] | 获得命令/配置文件的功能描述，获得帮助信息          |
| help [cmd]      | 获得shell内置命令的帮助信息                        |
|                 |                                                    |

## 用户 & 用户组

- 用户登录后，默认当前用户/home文件

### 基本命令

| 命令                                 | 功能                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| groupaddd [groupName]                | 添加组                                                       |
| groupdel [groupName]                 | 删除组                                                       |
| usermod -g [groupName] [userName]    | 修改用户组                                                   |
| useradd [userName]                   | 添加用户                                                     |
| useradd -d [newGroupName] [userName] | 创建用户&用户组<br />useradd不带任何参数会默认创建同名用户组 |
| useradd -g [groupName] [userName]    | 创建用户&分配至已有用户组                                    |
| passwd [userName]                    | 修改用户密码<br />- 简单密码被提示的话，重新输入可以强制设定<br />-仅root用户可以执行 |
| userdel [userName]                   | 删除用户，但保留用户home目录                                 |
| userdel -r [userName]                | 彻底删除用户                                                 |
| id [userName]                        | 查询用户信息<br />uid：用户id号<br/>gid：用户所在用户组的id号<br/>组：用户所在用户组 |
| su - [userName]                      | 切换用户                                                     |
| exit                                 | 取消切换用户，回到原来账户                                   |
| who am I / whoami                    | 确认当前用户                                                 |

### 相关文件管理

|              | 位置        | 信息                                                         |
| ------------ | ----------- | ------------------------------------------------------------ |
| 用户配置文件 | /etc/passwd | stuA:x :1002:1003::/home/stuA:/bin/bash<br />用户名：密码：用户ID：组ID：：家目录：对应的shell种类 |
| 组配置文件   | /etc/group  | groupB:x :1003:<br />组名：密码：组ID（标识符）：组内用户列表<br />最后一个参数被处理过，所以看不见 |
| 密码配置文件 | /etc/shadow | 口令、密码、登录相关信息，是一个加密文件                     |

## 运行级别

- 级别说明

  | 级别 | 信息           | 说明         |
  | ---- | -------------- | ------------ |
  | 0    | 关机           |              |
  | 1    | 单用户         | 找回丢失密码 |
  | 2    | 多用户、无网络 |              |
  | 3    | 多用户、有网路 | 最常用       |
  | 4    | 保留级别       |              |
  | 5    | 图形化界面     |              |
  | 6    | 重启           |              |

- 修改系统开机时的默认级别
  - /etc/inittab
- 指定运行级别
  - init [levelNumber]

## 文件目录操作

| 命令                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| pwd                                                          | 查看当前工作目录的绝对路径                                   |
| ls -a                                                        | 查看所有文件目录，包括隐藏文件                               |
| ls -l                                                        | 列表方式查看目录                                             |
| ls -al                                                       | 列表方式查看所有文件的文件目录 = ls -a + ls -l               |
| cd ~                                                         | 切换路径，到用户home目录                                     |
| cd /                                                         | 切换路径，到用户根目录                                       |
| cd ..                                                        | 切换路径，到上一级目录                                       |
| mkdir [dirName]                                              | 创建目录                                                     |
| mkdir -p [dir/dirName]                                       | 创建多级目录【parent                                         |
| rmdir [dirName]                                              | 删除空目录                                                   |
| rmdir -rf                                                    | 删除非空目录                                                 |
| touch [fileName1] [fileName2] [...]                          | 创建空文件                                                   |
| cp [sourceFile] [targetDir]                                  | 拷贝文件到指定目录                                           |
| cp -r [sourceDir] [targetDir]                                | 拷贝文件夹到文件夹                                           |
| \cp                                                          | 强制拷贝                                                     |
| rm [dir/file]                                                | 删除                                                         |
| rm -r                                                        | 递归删除文件夹                                               |
| rm -f                                                        | 强制删除                                                     |
| rm -rf                                                       | 强制递归删除文件夹                                           |
| mv [oldFileName] [newFileName]                               | 重命名文件                                                   |
| mv [file] [targetDir]                                        | 移动文件到指定文件夹                                         |
| >                                                            | 输出重定向（覆盖）<br />ls -l > file 就是将前面的结果输出到后面里<br />echo "test" > a.txt |
| >>                                                           | 追加，在尾部添加<br />把前者的输出内容追加到后者的最后<br />ls -al >> a.txt |
| cat [fileName]<br />cat -n [fileName]<br />cat [fileName] \| more | 只读查看文件【concatenate<br />查看并显示行号<br />查看并分页显示 |
| echo                                                         | 将内容输出到控制台<br />常用于输出环境变量                   |
| ¥PATH                                                        | 环境变量的路径                                               |
| head -n 5 [fileName]                                         | 查看文件头5行                                                |
| head [fileName]                                              | 查看文件头10行                                               |
| tail -n 5 [fileName]                                         | 查看文件末5行                                                |
| tail [fileName]                                              | 查看文件末10行                                               |
| tail -f [fileName]                                           | 实时追踪文档所有更新                                         |
| ln -s [file/name] [linkName]                                 | 软连接指令（类似快捷方式）<br/>存放了链接其他文件的路径<br/>应用特点：进入对应目录，但是不会改变pwd <br/>？如何删除软连接？rm -rf 链接名 |
| history 10                                                   | 显示最近使用过的10个指令                                     |
| history !10                                                  | 执行历史指令中的10号指令                                     |
| find [searchDir] [option] [targetFileName]<br />find /home -name hello.txt<br />find /opt -user userA<br />find /home -size +20M/-20M/20M<br />find /home -name a.txt<br />find /home -name *.txt | 查找文件                                                     |
| locate<br />updatedb<br />locate hello.txt                   | 查找文件，但不是遍历查找，而是建立了locate数据库去查找创建locate数据库<br />查找文件 |
| \|                                                           | 管道符号，表示将前面的命令的处理结果给后面的命令             |
| grep                                                         | 过滤查找                                                     |
| cat hello.txt \| grep -n yes<br />cat hello.txt \| grep -i yes | 在hello.txt中查找yes，并显示行号<br />+不区分大小写          |

## 时间日期指令

| 指令                      | 功能                  |
| ------------------------- | --------------------- |
| date                      | 显示当前时间          |
| date + %Y/m/d/H/M/S       | 显示当前年/月日时分秒 |
| date "+%Y-%m-%d %H:%M:%S" | 显示当前年月日时分秒  |
| date -s [dateTimeString]  | 设置当前系统时间      |
| cal                       | 显示当前日历情况      |
| cal 2020                  | 显示2020年日历        |

## 压缩&解压缩

| 指令                                                         | 功能                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| gzip                                                         | 压缩文件.gz【特点：压缩包和原文件只保存一个                  |
| gunzip                                                       | 解压缩.gz                                                    |
| zip<br />zip -r                                              | 压缩.zip<br />循环压缩文件夹                                 |
| unzip                                                        | 解压缩.zip                                                   |
| unzip -d [dir]                                               | 解压缩到指定dir.zip                                          |
| tar                                                          | 归档<br />-C 产生.tar打包文件<br />-v 显示详细信息<br />-f 指定压缩后的文件名<br />-z 打包同时压缩<br />-x 解包 |
| tar -zcvf a.tar.gz a1.txt a2.txt<br/><br/>tar -zcvf myhome.tar.gz /home<br/><br/>tar -zxvf a.tar.gz<br/><br/>tar -zxvf myhome.tar.gz -C /opt/tmp | tar和gz可以合并使用<br />将a1.txt和a2.txt打包压缩成a.tar.gz<br/><br/>将/home整个目录打包压缩成myhome.tar.gz<br/><br/>解压a.tar.gz到当前目录<br/><br/>解压myhome.tar.gz到/opt/tmp(要求目录必须存在)<br/> -C 选项的作用是：指定需要解压到的目录。 |

 gunzip | 解压缩.gz



