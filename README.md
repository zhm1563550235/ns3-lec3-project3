# Ns3学习第三次报告ns3-lec3-project3
##Logging系统
1.在脚本中定义和启动组件

```
NS_LOG_COMPONENT_DEFINE ("ns3-lec3-project3"); 
LogComponentEnable("ns3-lec3-project3",LOG_LEVEL_ALL); 
```
2.在命令行中启动记录组件：

``$ export NS_LOG=UdpEchoClientApplication=level_all``

3.运行脚本文件ns3-lec3-project3.cc。在ns3-lec3-project3.cc中启动UdpEchoClientApplication记录组件，并记录下所有的日志消息，结果如下所示：
 ![](http://i1.piimg.com/567571/dbee33472c351570.png)
 ![](http://i1.piimg.com/567571/55171e900fdb1eb6.png)

##Tracing系统
###ASCII Tracing：以ASCII格式的信息输出
1.声明一个AsciiTraceHelper对象

  ``AsciiTraceHelper ascii;``
  
2.激活Ascii Tracing，并输出文件为***.tr

  ```
  pointToPoint.EnableAsciiAll (ascii.CreateFileStream("ns3-lec3-project3.tr"));  
  phy1.EnableAscii (ascii.CreateFileStream("ns3-lec3-project3_wifi.tr"), ap1Devices.Get (0));
  ```
  
###PCAP Tracing:输出为pcap文件，可通过wireshark，TcpDump查看
   ```
    pointToPoint.EnablePcapAll ("ns3-lec3-project3");
    phy1.EnablePcap ("ns3-lec3-project3", ap2Devices.Get (0));
   ``` 
    
###在ns3-lec3-project3.cc中同时使用这两种方式可以得到以下文件。

![](http://i1.piimg.com/567571/ca2cef565fe1760b.png)
![](http://i1.piimg.com/567571/df2a99eef929104f.png)

##PyViz（仿真拓扑变化）
1.PyViz安装依赖包

  ``$ sudo apt-get install python-dev python-pygraphviz python-kiwi python-pygoocanvas python-gnome2 python-gnomedesktop（已经被包含在python-rsvg中） python-rsvg``
  
  可以测试一下，如果在Ubuntu的/NS3_install/ns-allinone-3.24.1/ns-3.24.1$ 目录下使用如下命令进行测试：./waf
  如果出现以下结果：
  
  ![](http://i1.piimg.com/567571/436855e5c68eb1a3.png)
  即如果visualizer模块已被编译，那么可以直接进入后续步骤。如果visualizer在Modules not built目录下，那么还需要下载pyviz软件包，解压后放在/NS3_install/ns-allinone-3.24.1目录下，再需重新编译如下命令：
  ```
  $ ./waf clean
  $ ./waf --build-profile=optimized --enable-examples --enable-tests configure
  ```
  网上大多数的案例教程都没有该步骤，我的Ubuntu中的visualizer 模块就没有被build。然后重新下载pyviz软件包并编译，这一步花费的时间较长，然后就可以使用pyviz工具了。
  
2.PyViz使用前准备
  在程序中包含：
  ```
  CommandLine cmd;
  cmd.Prase (argc,argv);
  ```
3.PyViz使用
  在运行脚本的语句后面加入参数 –vis。结果如下所示：
  ![](http://i1.piimg.com/567571/e244f4f99a6b3f83.png)
  
##Wireshark工具
1.Wireshark的下载安装

 ```
 $ sudo apt-get update
 $ sudo apt-get install wireshark
 ```
 2.Wireshark的使用
 
  ```
  $ wireshark
  ```
  ![](http://i2.piimg.com/567571/f3eac59193fa0d71.png)
  
  然后，使用wireshark工具读取.pcap文件
  ![](http://i2.piimg.com/567571/6c249515db76b916.png)
  ![](http://i2.piimg.com/567571/3c27f859edb05ee0.png)
  ![](http://i2.piimg.com/567571/1e03902fc0b99bfb.png)
  
