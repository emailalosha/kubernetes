# Linux basics
***

## To start and stop services
    systemctl stop/start/enable/disable firewalld
    systemctl stop/start/enable/disable NetworkManager
    systemctl enable/start/stop docker

## Content of /etc/resolv.conf
    nameserver 192.168.0.1
    
## Content of /etc/sysconfig/network
```
NETWORKING=yes
GATEWAY=192.168.0.1
HOSTNAME=raining-lab-3.reed.com
```

## Content of /etc/sysconfig/network-scripts/ifcfg-ens33
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
#BOOTPROTO=dhcp
BOOTPROTO=static
#DEFROUTE=yes
#IPV4_FAILURE_FATAL=no
#IPV6INIT=yes
#IPV6_AUTOCONF=yes
#IPV6_DEFROUTE=yes
#IPV6_FAILURE_FATAL=no
#IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=d36c8161-5a3c-4549-a1e3-c9798a2e6c5b
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.0.123
GATEWAY=192.168.0.1
NETMASK=255.255.255.0
```

## To add a user - jenkins, group wll be same as username
        useradd jenkins 

## Reset password of a user - jenkins
        passwd jenkins 
        
## To add a user - jenkins into group - docker
        usermod -a -G docker jenkins

> How to make sure bridge network works fine in VM Workstation

        Open VM workstation -- Edit -- Virtual Network Editor -- click on change settings (right below)
        -- within VMnet Information -- select bridge to -- the wireless adapter
        
## How to check wireless adapter is getting used..

        
![Untitled](https://user-images.githubusercontent.com/63675131/165819921-a6286cc4-fd1e-4ca5-9266-e0e42bc47c17.png)

## Pre-req software on linux host

```
yum install net-tools -y
yum install wget -y
```


