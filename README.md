# Two operating systems in one desktop
#### 简单记录一下在一台家用主机上安装 Windows 10 和 Ubuntu的过程。
因为是家用台式机，需要兼顾娱乐和学习工作，所以选择了一个简单有效的方法来实现双系统。
- 简单地说，本方案采用了2个硬盘，每个硬盘各安装一个操作系统，然后利用Grub2管理系统的启动引导。
- 安装中需要注意以下几点：
  - 应该先安装 Windows 10，再安装Ubuntu。这一次 Windows 10 安装在了磁盘1上，Ubuntu安装在了磁盘2上。
  - 在安装Ubuntu时，应该会有提示说检测到有windows manager， 这样的话 Grub2会自动将其添加到启动菜单里。
  - 在安装Ubuntu时，最好为/boot单独分割一个区(大小为200MB-500MB),用来安装Ubuntu的引导文件，即Grub2。
  - 此次 Ubuntu 的具体分区设置为： /boot： 200MB, /：大约180GB, swap: 16GB(和机器的内存数量差不多)。


