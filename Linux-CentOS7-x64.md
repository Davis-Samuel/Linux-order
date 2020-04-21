# 修改字体

- ```java
  ls /lib/kbd/consolefonts | more 然后按下q停止刷新，开始选择字体
  setfont lat4-19
  su
  echo 'setfont lat4-19' >> /etc/bashrc  //放到etc/bashrc目录下，开机自启
  ```

# 设置开机登陆就是管理员：root密码修改+注销退出用户

```java
//在su的root管理员下
passwd root

//注销退出用户
exit
logout

//关机/重启  halt/reboot
```

# SSH管理服务

- 判断有没有ssh

  ```java
  rpm -qa | grep ssh
  ```

- 安装ssh

  ```java
  yum -y install openssh-server
  ```

- ssh配置

  ```Java
  //默认情况下ssh是不允许root登陆的，所以需要将此配置取消
  //1.打开ssh配置文件
  vi /etc/ssh/sshd_config
  //2.修改配置项
  倒数第三行的PermitRootLogin yes前面的#号删除
  i：开始编辑 保存退出： :wq！
  //3.重启ssh
  停止ssh：/bin/systemctl stop sshd.service
  查看ssh进程是否停止 ps -ef | grep ssh
  启动ssh：/bin/systemctl start sshd.service
  //4.相当于系统开启了一个ssh 的操作的通道，该通道默认占用端口为22端口，于是就可以在客户端上下载一个xshell的工具与Linux连接
  先看一下ip：ip addr
  //5.在Xshell中新建会话，主机填写虚拟机的地址。用户填root
  ```

# 防火墙的取消

- 查看防火墙是否存在：

  ```java
  firewall-cmd --state
  ```

- 停止防火墙：

  ```java
  systemctl stop firewalld.service
  ```

- 禁止防防火墙开机自启：

  ```java
  systemctl disable firewalld.service
  ```

- 删除iptables组件：

  ```Java
  yum -y remove iptables
  ```

- 禁用SELinux组件：

  ```java
   gcc//查看SELinux的状态：
  getenforce
  //打开配置文件
  vi /etc/selinux/config
  //修改配置项
  在SELINUX=enforcing修改为SELINUX=disabled
  //退出
  ：wq！
  //配置生效
  reboot
  ```

- 组件更新：

  ```Java
  在xshell中：yum -y update
  ```

- 配置依赖组件，为开发环境打组件基础,之后可以使用ifconfig：

  ```java
  yum -y install make g++ gcc libpcrecpp* libpcre3-dev libssl-dev autoconf automake libtool libncurses5-dev libaio.dev net-tools wget autoconf libaio-devel.x86_64 tree
  ```

# 时区和时间的配置(”5911“)

- 时区配置：

  ```Java
  1.tzselect
  2.选5
  3.选9
  4.选1
  5.选1
  ```

- 时间配置：

  ```java
  组件：yum -y install ntp ntpdate
  同步时间使用阿里的时间服务器：ntpdate -u ntp1.aliyun.com
  将配置写入硬盘，不必每次就要重重新设置：hwclock --systohc
  ```

# FTP文件传输

- 安装vsftpd组件：

  ```java
  yum -y install vsftpd
  ```

- 服务配置：

  ```java
  1.vi /etc/vsftpd/vsftpd.conf
  ```

  | 行数 | 配置项                                       | 描述                         |
  | ---- | -------------------------------------------- | ---------------------------- |
  | 12   | anonymous_enable=NO                          | 不允许匿名访问               |
  | 83   | ascii_upload_enable=YES                      | 允许上传ascii文件            |
  | 84   | ascii_download_enable=YES                    | 允许下载ascii文件            |
  | 86   | ftpd_banner=Welcome to : https://a.maorx.cn/ | 用户登陆的提示信息           |
  | 101  | chroot_local_user=YES                        | 只允许用户进行工作目录的访问 |
  | 102  | chroot_list_enable=YES                       | 允许进行工作目录的列表       |
  | 104  | chroot_list_file=/etc/vsftpd/chroot_list     | 定义授权用户列表配置文件路径 |
  | 末尾 | allow_writeable_chroot=YES                   | 【自己编写】允许文件的写入   |

- 密码配置：

  ```
  passwd ftp
  ```

- ftp列表文件：

  ```java
  vi /etc/vsftpd/chroot_list
  不需要配置:wq!
  ```

- 授权：

  ```java
  chmod -R 777 /var/ftp
  ```

- 授权变更，修改授权文件：

- ```java
  vi /etc/pam.d/vsftpd
  注释两行内容：第3，4行
  #auth       required    pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers onerr=succeed
  #auth       required    pam_shells.so
  
  ```

- ftp命令：

  | ftp启动      | systemctl start vsftpd.service   |
  | ------------ | -------------------------------- |
  | ftp关闭      | system stop vsftpd.service       |
  | 新启动p启动  | systemctl restart vsftpd.service |
  | 查看当前服务 | ps -ef \| grep ftp               |

- 开机自动启动：

  ```java
  systemctl enable vsftpd.service
  ```

  ![image-20200312124012447](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200312124012447.png)