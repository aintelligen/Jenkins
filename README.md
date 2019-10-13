# Jenkins

Jenkins 自动化部署

linux 操作

```shell
### ------
# 磁盘情况
df -hl
#
### ------
##### apt-get update && apt-get upgrade
apt-get update && apt-get upgrade
### ------

##### iptables file2ban
sudo iptables -F  #情况 iptables
sudo vi /etc/iptable.up.rules
### ------
*filter
# allow all connections
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# allow all traffic
-A OUTPUT -j ACCEPT
#allow http https
-A INPUT -p tcp --dport 443 -j ACCEPT
-A INPUT -p tcp --dport 80 -j ACCEPT
#allow ssh port login
-A INPUT -p -tcp -m state --state NEW --dport 39999 -j ACCEPT
#ping
-A INPUT -p -icmp -m icmp --icmp-type 8 -j ACCEPT
#log denied calls
-A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied:" --log-level 7

#drop incoming sensitive connections
-A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent--set
-A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent--update --seconds 60 --hitcount 150 -j DROP

# reject all other inbound
-A INPUT -j REJECT
-A FORWARD -j REJECT
COMMIT
### ------ 设置iptable 文件
iptables-restore < /etc/iptables.up.rules
#启功防火墙
ufw status
ufw enable
ufw status

### ------  mongodb
apt-get install mongodb
pgrep mongo -l
sudo service mongodb stop 　　sudo service mongodb start

### ------ 网络监控  https://www.cnblogs.com/voiphudong/p/3985779.html
apt-get install iftop
### ------安装最新版node
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt install npm

### ------ PM2
npm install pm2 -g
pm2 start server/server/.js --name LiveChat
# start restart reload delete

pm2 show LiveChat
### ------
### ------
### ------
### ------
### ------
### ------
### ------
### ------
### ------
### ------
### ------
```
