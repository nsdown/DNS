# DNS
PandaDNS

更好的上网,远离邪恶

#原理
过去一段时间里大多数人利用hosts来访问被封锁的网站,但是hosts文件需要常常更新,所以本人建立了此项目,利用bind9实现相同的效果.

简单来说,当你上网访问某些被封锁的网站,DNS将返回一个可以访问的IP.这样你就能正常上网啦.

#优点
较hosts来说,用户只要改个DNS即可省去频繁更新hosts文件的烦恼.

#缺点
1.信任问题,DNS服务器既可以返回正确的IP,也可以返回错误的IP,如恶意劫持域名,甚至利用DNS指向钓鱼网站.

2.服务器必须位于国内,但是考虑到国内环境,如果DNS服务做的众人皆知,恐怕离查水表不远了,如HelloDNS.

#那么...
那么,希望通过本项目,建立一个又一个的DNS节点~~~~

#PandaDNS环境
centos6.7

bind-9.8.2-0.37.rc1.el6_7.5.x86_64

#快速搭建DNS
1.yum install bind -y

2.替换服务器目录文件 /etc/named.conf 为本项目 根目录的同名文件

3.替换服务器目录文件 /etc/named.rfc1912.zones 为本项目 目录 named.rfc1912.zones 下 named.rfc1912.zones文件

4.把本项目 目录 named 下所有文件上传至服务器目录 /var/named/ 下

5.启动: service named start

#DNS服务器安全
配置防火墙防止DDos攻击及放大攻击

iptables -A INPUT -p udp --dport 53 -m recent --set --name dnslimit

iptables -A INPUT -p udp --dport 53 -m recent --update --seconds 60 --hitcount 11 --name dnslimit -j DROP

service iptables save


#参考书籍
linux服务范例速查大全 刘丽霞 邱晓华 编著  清华大学出版社 第一版

linux网络服务配置详解 何世晓 编著 清华大学出版社  第一版

#参考途径
www.baidu.com

www.google.com
