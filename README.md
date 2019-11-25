一键脚本安装ShadowsocksR + bbr
---
1.1  首先购买一个国外的VPS，例如[谷歌云](https://cloud.google.com/)平台免费一年可以试试哦！   

2.1  以谷歌云为例，用VISA卡注册完以后，创建VM实例，选择asia-east1，台湾的速度快、延迟小，选v1核，1.7G的那个微型机器，选默认的debian9，防火墙允许HTTP/HTTPS流量，等待创建loading；   

2.2  右边找到VPC网络，创建防火墙规则，名称随意，目标选择“网络中的所有实例”，来源IP地址范围填“0.0.0.0/0”，协议和端口勾选你需要用的协议，例如tcp:6666，当然也可以选择全部允许，比较省事，其他默认就行；   

2.3  进入VPC网络->外部IP地址->保留静态地址，名字小写字母随意，区域选择你选服务器的区域asia-east1，附加到你的VM实例中；   

2.4  进入VM实例，点SSH，在浏览器窗口中打开，用谷歌浏览器进行SSH连接；   

2.5  以debian9为例；   

      sudo -i进入root模式，敲入apt-get install git   
      git clone https://github.com/Minghaovcc/SSR.git  
      chmod +x shadowsocks-all.sh   
      ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
      
      wget -N --no-check-certificate https://raw.githubusercontent.com/CecilWu/SSR-Chinese/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
      

   输入你的想设置的ssr密码，选择端口号（例如6666），然后一路回车，选默认的就好，等待创建loading；   
    
   开启BBR加速（因为debian9最新的是4.9以上内核，默认集成了BBR）；   
   
      echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
      echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
      sysctl -p
   装上后可以敲入lsmod | grep bbr，显示bbr就行     
    
2.6  下载使用[SSR客户端](https://github.com/Minghaovcc/SSR/blob/master/Client/ShadowsocksR-win-4.9.0.zip)，填写刚才的SSR的IP，密码；  
