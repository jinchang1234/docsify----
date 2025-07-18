1.查看所有模组状态
bmsec getbi
------------------------------------------------------------
2.机器进入模组串口
sudo su

source ~/se_ctrl/sectr.sh

sectr_switch_uart 12

minicom -D /dev/ttyS1
--------------------------------------------------------
3.查看模组IP
fping -a -q -g 192.168.1.0/24

ifconfig

sudo su
                                                     
cat /sys/bus/i2c/devices/1-0017/board-ip                                                                 
------------------------------------------------------------
4.查看所有模组MCU版本和电源软件版本
bm_version |grep MCU

bmsec run all "bm_version"

sudo pmbus -d 0 -s 0x50 -j |grep 'output voltage
---------------------------------------------------------
5.MCU命令在线升级
scp sm7mini-mcu-v10-2023-09-26-20-36-00.bin linaro@192.168.1.10:~/.

ls

sudo su

mcu-util-aarch64 upgrade-full 1 0x17 sm7mini-mcu-v10-2023-09-26-20-36-00.bin
--------------------------------------------------------------------------------------------------------

bmsec ssh 11



核心板升级：
sudo su
systemctl status tftpd-hpa
ls -al /recovery/tftp/
cd /root/se6_ctrl/script

./core_run_command_bynet.sh "~/tftp_update/mk_bootscr.sh;sync" linaro linaro
./core_run_command_bynet.sh "sudo reboot now " linaro linaro

进串口：
sudo su
source ~/se6_ctrl/se6ctr.sh
se6ctr_switch_uart x
minicom -D /dev/ttyS2

You、:
ctrl+a z q 回车

You、:
看核心板MCU： ./core_run_command_bynet.sh "bm_version |grep MCU" linaro linaro

You、:
SDK日期： ./core_run_command_bynet.sh "uname -a" linaro linaro

