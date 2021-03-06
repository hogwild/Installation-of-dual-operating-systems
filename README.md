# Two operating systems in one desktop
#### 简单记录一下在一台家用主机上安装 Windows 10 和 Ubuntu的过程。
因为是家用台式机，需要兼顾娱乐和学习工作，所以选择了一个简单有效的方法来实现双系统。
- 简单地说，本方案采用了2个硬盘，每个硬盘各安装一个操作系统，然后利用Grub2管理系统的启动引导。
- 安装中需要注意以下几点：
  - 应该先安装 Windows 10，再安装Ubuntu。这一次 Windows 10 安装在了磁盘1上，Ubuntu安装在了磁盘2上。
  - 在安装Ubuntu时，应该会有提示说检测到有windows manager， 这样的话 Grub2会自动将其添加到启动菜单里。shunxu
  - 在安装Ubuntu时，最好为/boot单独分割一个区(大小为200MB-500MB),用来安装Ubuntu的引导文件，即Grub2。
  - 此次 Ubuntu 的具体分区设置为： /boot： 200MB, /：大约180GB, swap: 16GB(和机器的内存数量差不多)。  
  - 上述Ubuntu分区在使用中遇到的情况：/boot设置的太小，使用一段时间后导致系统提示/boot分区空间不足，尝试了网上的一些方法，比如,sudo apt-get autoremove等，都未能解决这个问题。只能重装系统。目前看来，boot分区和/放在一起比较好，不需要另外再分区左boot。
#### 补充：修改Grub2的菜单中启动项的顺序
- grub2是由/etc/grub.d/目录下的文件名称顺序来决定启动项的顺序的。因此改变文件名排序就可以改变启动项排序了。
  - 若要将 Windows 10 的启动项放在 Ubuntu 前面，则需要将 30_os-prober 的文件名中的 30 改为 06～09之间的任何数字即可。
  
  For example:
  
      $sudo mv /etc/grub.d/30_os-prober /etc/grub.d/06_os-prober
      $sudo update-grub

#### 额外的情况：VPN无法上Google的原因及解决方案
- 安装完系统之后，在Ubuntu中设置了学校的VPN(vpn-ct.shanghai.nyu.edu)可以顺利访问BBC等网站，但就是不能访问google下属的网站，比如 www.google.com， facebook, youtube 等。分别ping google.com, ping google的主机IP，发现后者可以链接，但是前者却一直在变换，由此判断是DSN解析出了问题。于是，修改了 /etc/resolv.conf 将DNS 换成了8.8.8.8。问题解决。 [参考链接](http://www.yubosun.com/tech/ubntu-dns-reset.htm)
具体步骤：  
 1 在/etc/network/interfaces中最后增加一行：dns-nameservers 8.8.8.8  
 2 在/etc/resolvconf/resolv.conf.d/base中增加：nameserver 8.8.8.8  
 3 执行 resolvconf -u  
即可生效，并且重启之后也不会有影响。


