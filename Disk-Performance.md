# debuging
#check disk iops performance
dd if=/dev/random of=./test bs=1M count=200
dd if=/dev/random of=./test bs=1k count=200000
dd if=/dev/random of=./test bs=10M count=20

#install sar package
#check kernel
uname -a
#check OS
cat /etc/os-release
#check load avarage
uptime
#check cpu
cat /proc/cpuinfo
#check memory
cat /proc/meminfo
#check system process
top
##############
#work with sar
#sar interval count =>  sar 1 10
#use sar to check cpu load to check iowait
sar 1
#-b block device, -d disk , -n network
sar -b -d 1
sar -n TCP 1
#check used port
ss -lntpo
#check io process with iotop
iotop
#if you know that which process have io you can search the process with this command
ps aux | grep -i dd
ps auxf | less
#now test again with sar
sar 1
#test hard disk iops
dd if=/dev/random of=./test bs=1M count=200
dd if=/dev/random of=./test bs=1k count=200000
dd if=/dev/random of=./test bs=10M count=20
