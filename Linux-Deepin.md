# Linux系统下的图片压缩

- ```
  sudo su #获取管理员权限 
  ```

  ```
  cd Desktop/pic #我的图片放在了桌面的pic文件夹下
  ```

  ```
   vim pic.sh #使用vim创建一个pic.sh文件
  ```

  ```
  find ./ -regex '.*\(jpg\|JPG\|png\|PNG\|jpeg\)' -size +50k -exec convert -resize 700x450 -quality 75 {} {} \; #这行代码的意思是将文件夹下的图片50K以上的都转换为原有图片质量的75%并设置尺寸为700x450
  ```

  ```
   esc->:wq  #按ESC然后输入:wq
  ```

  ```
   chmod +x pic.sh #给pic.sh加入权限 
  ```

  ```
  ./pic.sh #运行脚本后看一下文件夹下的图片变化
  ```

# VirtualBox更换分辨率界面

- 设备 → 安装增强功能
-  ![image-20200227125644487](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227125644487.png)
- sudo su
- ![image-20200227125738092](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227125738092.png)
- ![image-20200227125822379](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227125822379.png)



# 系统-软件升级

- ```
  1. sudo su  2. apt-get upgrade
  ```

# 安装plank(dock栏)

- ```
  //更新系统后在安装   sudo apt install plank
  ```

  

# 重启关机

- ```
  重启 reboot  关机poweroff
  ```

# 软件安装路径

- ```
  usr→share→application
  ```

- ![image-20200227150356701](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227150356701.png)

  application里面右键软件编辑，找到这里就是软件执行的路径，可以通过这个路径设置快捷键

# 配jdk

- ![image-20200227200123950](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227200123950.png)

  



# 配tomcat

- ![image-20200227201252155](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227201252155.png)

- ```
  在tomcat的bin目录下使用终端sudo su 然后再vim setclasspath.sh
  ```

- 启动与关闭tomcat![image-20200227201541767](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227201541767.png)

# 配mysql

- ![image-20200227205451296](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227205451296.png)

# 配navicate

- 见d盘未安装

# 配maven

- 环境变量配置：

  ![image-20200228123153564](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200228123153564.png)

  

- 仓库位置![image-20200227212919680](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227212919680.png)
- 阿里云镜像：![image-20200227213042633](C:\Users\91566\AppData\Roaming\Typora\typora-user-images\image-20200227213042633.png)

# 启动程序
- 用 ./   


# 其他

- https://www.bilibili.com/video/av84145183
