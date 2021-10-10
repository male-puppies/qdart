用之前 那个包直接写flash。 然后再进uboot 烧写这个包。 
set ipaddr 192.168.1.1
set serverip 192.168.1.xx (tftpserver- Ipaddress)
tftpboot 0x42000000 <image name>
imgaddr=0x42000000 && source $imgaddr:script


set ipaddr 192.168.1.1
set serverip 192.168.1.180
tftpboot 0x42000000 nor-ipq807x_64-single_OK.img
imgaddr=0x42000000 && source $imgaddr:script

/etc/init.d/qcmbr start

2、板子通过 telnet 进入控制台，执行如下命令进入产测状态 
   （1）首次运行板子需要执行如下 3 条命令 
  cd /lib/firmware/IPQ8074/ 
        cp bdwlan.b292 bdwlan.bin 
        sync   
   （2）wifi down 
rmmod wifi_3_0 
rmmod wifi_2_0 
rmmod qca_ol 
insmod qca_ol testmode=1 
insmod wifi_3_0 
insmod wifi_2_0 
diag_socket_app -a 192.168.200.180 &   （电脑的有线 IP 地址）   
/etc/init.d/ftm start 
ftm -n -dd & 
2、 运行完后有如下提示表示网口连接成功 


wifi down
rmmod wifi_3_0 
rmmod wifi_2_0 
rmmod qca_ol 
insmod qca_ol testmode=1 
insmod wifi_3_0 
insmod wifi_2_0 
diag_socket_app -a 192.168.100.123 &
/etc/init.d/ftm start 
ftm -n -dd & 


vim /etc/config/wireless 


i  修改。 esc ;    :wq