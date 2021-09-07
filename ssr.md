搭建SSR服务器
===
### 一键开启SSR  
bash <(curl -L -s https://raw.githubusercontent.com/hijkpw/scripts/master/centos_install_ssr.sh)

3. 如不能联网，则关闭防火墙（逐条输入）
service iptables restart
service iptables stop
chkconfig iptables off

加速ssr ：
破解版锐速安装一键更换内核脚本（vultr需先执行此脚本）
wget -N --no-check-certificate https://freed.ga/kernel/ruisu.sh && bash ruisu.sh
脚本执行过程中，请勿进行任何操作。待服务器重启后，重新连接安装锐速即可。
锐速安装脚本
wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh
若提示：The name of network interface is not eth0, please retry after changing the name.请使用备用脚本备用脚本：
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh
