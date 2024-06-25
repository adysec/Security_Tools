# Nessus

## 运行nessus.sh

```bash
sudo bash nessus.sh
```

## 手动安装

### 安装nessus

```bash
chattr -i -R /opt/nessus
apt update
apt -y install curl dpkg expect
systemctl stop nessusd.service
dpkg -i Nessus-latest-debian10_amd64.deb
systemctl restart nessusd.service
systemctl stop nessusd.service
/opt/nessus/sbin/nessuscli fix --set xmlrpc_listen_port=8834
/opt/nessus/sbin/nessuscli fix --set ui_theme=dark
/opt/nessus/sbin/nessuscli fix --set safe_checks=false
/opt/nessus/sbin/nessuscli fix --set backend_log_level=performance
/opt/nessus/sbin/nessuscli fix --set auto_update=false
/opt/nessus/sbin/nessuscli fix --set auto_update_ui=false
/opt/nessus/sbin/nessuscli fix --set disable_core_updates=true
/opt/nessus/sbin/nessuscli fix --set report_crashes=false
/opt/nessus/sbin/nessuscli fix --set send_telemetry=false
```

### 设置密码

```bash
cat > expect.tmp<<'EOF'
spawn /opt/nessus/sbin/nessuscli adduser admin
expect "Login password:"
send "adysec.com\r"
expect "Login password (again):"
send "adysec.com\r"
expect "*(can upload plugins, etc.)? (y/n)*"
send "y\r"
expect "*(the user can have an empty rules set)"
send "\r"
expect "Is that ok*"
send "y\r"
expect eof
EOF
expect -f expect.tmp
rm -rf expect.tmp
```

### 安装插件

```bash
curl -A Mozilla -o all-2.0.tar.gz --url 'https://plugins.nessus.org/v2/nessus.php?f=all-2.0.tar.gz&u=4e2abfd83a40e2012ebf6537ade2f207&p=29a34e24fc12d3f5fdfbb1ae948972c6'
/opt/nessus/sbin/nessuscli update all-2.0.tar.gz
vernum=$(curl https://plugins.nessus.org/v2/plugins.php 2> /dev/null)
cat > /opt/nessus/var/nessus/plugin_feed_info.inc <<EOF
PLUGIN_SET = "${vernum}";
PLUGIN_FEED = "ProfessionalFeed (Direct)";
PLUGIN_FEED_TRANSPORT = "Tenable Network Security Lightning";
EOF
chattr -i /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc
cp /opt/nessus/var/nessus/plugin_feed_info.inc /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc
chattr +i /opt/nessus/var/nessus/plugin_feed_info.inc
chattr +i -R /opt/nessus/lib/nessus/plugins
chattr -i /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc
chattr -i /opt/nessus/lib/nessus/plugins
systemctl restart nessusd.service
```

### 登录口令

```bash
https://localhost:8834/
username:admin
password:adysec.com
```