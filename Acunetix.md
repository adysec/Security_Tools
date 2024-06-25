# Acunetix

### 修改 /etc/hosts

```bash
127.0.0.1  erp.acunetix.com
127.0.0.1  erp.acunetix.com.
::1  erp.acunetix.com
::1  erp.acunetix.com.
192.178.49.174  telemetry.invicti.com
192.178.49.174  telemetry.invicti.com.
2607:f8b0:402a:80a::200e  telemetry.invicti.com
2607:f8b0:402a:80a::200e  telemetry.invicti.com.
```

### 安装acunetix

```bash
sudo bash acunetix.sh
```

### 停止服务

```bash
sudo systemctl stop acunetix
```

### 替换wvsc文件

```bash
sudo cp wvsc /home/acunetix/.acunetix/v_240427095/scanner/wvsc
sudo chown acunetix:acunetix /home/acunetix/.acunetix/v_240427095/scanner/wvsc
sudo chmod +x /home/acunetix/.acunetix/v_240427095/scanner/wvsc
```

### 添加证书

```bash
sudo rm /home/acunetix/.acunetix/data/license/*
sudo cp license_info.json /home/acunetix/.acunetix/data/license/
sudo cp wa_data.dat /home/acunetix/.acunetix/data/license/
sudo chown acunetix:acunetix /home/acunetix/.acunetix/data/license/license_info.json
sudo chown acunetix:acunetix /home/acunetix/.acunetix/data/license/wa_data.dat
sudo chmod 444 /home/acunetix/.acunetix/data/license/license_info.json
sudo chmod 444 /home/acunetix/.acunetix/data/license/wa_data.dat
sudo chattr +i /home/acunetix/.acunetix/data/license/license_info.json
sudo chattr +i /home/acunetix/.acunetix/data/license/wa_data.dat
```

### 重启acunetix

```bash
sudo systemctl start acunetix
```