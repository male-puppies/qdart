### uboot升级

```sh
set ipaddr 192.168.1.1
set serverip 192.168.1.xx (tftpserver- Ipaddress)
tftpboot 0x42000000 <image name>
imgaddr=0x42000000 && source $imgaddr:script


set ipaddr 192.168.1.1
set serverip 192.168.1.180
tftpboot 0x42000000 nor-ipq807x_64-single_OK.img
imgaddr=0x42000000 && source $imgaddr:script
```

### 切换 FTM 模式

```sh
# ssh/telnet connected
/etc/init.d/qcmbr start

cd /lib/firmware/IPQ8074/ && {
   cp bdwlan.b292 bdwlan.bin;
   sync;
}
wifi down 
rmmod wifi_3_0 
rmmod wifi_2_0 
rmmod qca_ol 
insmod diagchar
insmod qca_ol testmode=1 
insmod wifi_3_0 
insmod wifi_2_0 
diag_socket_app -a 192.168.10.115 & #PC run QDART agent
/etc/init.d/ftm start 
ftm -n -dd & 
```

### 可修改wireless配置, 禁用wifi --- 缩短启动时间
