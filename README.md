# Problems
记录一下平时遇到的问题和解决方案

### 树莓派开机自启问题<br>
树莓派开机自启的问题，在rc.local里设置了自启后，上电无法自启程序，但是重启可以自启。<br>
查看了系统log日志，发现应该是网络初始化还没完成时就执行了程序，在程序里加了一个sleep()函数，解决。<br>
/etc/rc.local 设置开机自启如/home/pi/boot.x，在exit(0)之上<br>
boot.x里<br>
cd /home/pi/NetBeansProjects/Dx203SystemWatchDog/dist<br>
sudo java -jar Dx203SystemWatchDog.jar > /dev/null &<br>
最后&是让程序能在单独的命令行里执行，然后> /dev/null是输出都扔到空洞里<br>

### 树莓派查看系统日志指令问题<br>
树莓派查看系统日志指令<br>
cat  /var/log/syslog  //打印日志<br>
cat  /var/log/dmesg  //显示启动信息<br>
树莓派后台运行程序的方法：在控制台命令的最后加上‘&’。 <br>
dmesg //显示树莓派最近发生的事情 <br>

### 路由器各种无线模式问题<br>
1. 访问点 (AP)该模式下路由器的无线网卡就像一个”无线HUB”，负责建立无线路由器和电脑之间的数据链路（相当于无形的网线）。正常情况下，家用的无线路由器的无线连接都默认工作在此模式下。<br>
2. 客户端 (Client)像笔记本电脑上的无线网卡那样工作，仅连接其它的无线网络，而不发射自己的无线网络信号。对于无线路由器来说，这种模式相当于启用了一个无线的WAN口，且下面的电脑只能通过有线方式接到此设备。<b>该模式下无线路由器仍然提供DHCP及NAT功能，内部四个LAN口组成的单独IP地址段局域网，通过无线路由器上自己的网关，连上外部主网络。</b><br>
3. 客户端网桥 (Client Bridge)和“客户端”模式一样，相当于启用了一个无线的WAN口，且下面的电脑只能通过有线方式接到此设备。不过，内部的LAN口组成的局域网和连接上的无线网段处于相同的IP地址段。<font color=red>内部的DHCP请求也会被转发到主无线网络上。</font><br>
4. AdhocAdhoc有个形象的比喻，就像是将两台电脑之间直接找根网线连起来，只不过在这里这根网线是个无线的。最常见的使用adhoc连接的设备多数是一些手持游戏机。该模式在无线路由器上使用的场合比较罕见。<br>
5. 中继 (Repeater)顾名思义，中继就是一边是接受信号，一边又发射自己的无线信号。在这种模式下无线路由器以无线网卡客户身份接入主AP，然后再以新增虚拟界面(Virtual Interfaces)来为客户端提供无线接入。该模式的最大意义在于可以解决无线信号受到距离或者障碍物的影响不能传输到更远的问题。这种模式下无线路由器仍然提供DHCP及NAT功能，<b>即所有的内部LAN口以及无线客户接入组成的是一个单独的局域网网段。</b><br>
6. 中继桥接 (Repeater Bridge)和”中继”模式一样，可以解决无线信号受到距离或者障碍物的影响不能传输到更远的问题。不过，接入到该无线路由器上的电脑终端，是和主无线网网络处在相同的IP地址段。<b>内部的DHCP请求，也会被转发到主无线网络上。</b><br>
<br>
也就是说，只要有bridge这个词，基本就相当于他没有自己单独的局域网网段，所以如果你需要还有自己单独的局域网网段的话，需要以中继的模式连接。<br>

### 500 internal server error at GetResponse()<br>
To get the error from the web server, add a try catch and catch a WebException. A WebException has a property called Response which is a HttpResponse.

### C++读取多行不定数字
    #include<sstream>
    // 先把一行数据用geline读到str里
    while(getline(cin, str)) {
        vector<int> line;
        if (str.size() == 0) break;
        // 把一行数据转化为istringstream，会自动切分
        istringstream ist(str);
        while (ist >> num) {
            line.push_back(num);
        }
        input.push_back(line);
    }

