# Problems
记录一下平时遇到的问题和解决方案

2018.03.20
树莓派开机自启的问题，在rc.local里设置了自启后，上电无法自启程序，但是重启可以自启。
查看了系统log日志，发现应该是网络初始化还没完成时就执行了程序，在程序里加了一个sleep()函数，解决。
/etc/rc.local 设置开机自启如/home/pi/boot.x，在exit(0)之上
boot.x里
cd /home/pi/NetBeansProjects/Dx203SystemWatchDog/dist
sudo java -jar Dx203SystemWatchDog.jar > /dev/null &
最后&是让程序能在单独的命令行里执行，然后> /dev/null是输出都扔到空洞里
