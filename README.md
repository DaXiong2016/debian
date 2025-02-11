# 关于这里
> 这是我对Debian系统使用、学习，做的一些笔记


## 设置目录
### 设置目录不可删除
```
chattr +i -RV movies
```

### 取消设置目录不可删除
```
chattr -i -RV movies
```

## grep search command
grep -Rwi /home/debian/Documents -e "grep"
@-R 递归子目录,w 查找对应的单词，i 不区分大小写

## apt查看已安装应用
apt list --installed
apt list --installed | grep virt*


## enable network
ip addr
dhclient enp3s0
ping qq.com

## show memory
free -m -h

## 仓库源
```
nano /etc/apt/sources.list
deb http://ftp.cn.debian.org/debian bookworm main
deb http://ftp.hk.debian.org/debian bookworm main 
deb https://repo.debiancn.org/ bookworm main
```

## install chrome
apt install google-chrome-stable

## 软件中心
aptitude install snapd
aptitude install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
aptitude install gnome-software-plugin-flatpak
reboot

PS:没卵用，卸载
sudo aptitude remove flatpak
sudo aptitude remove snapd -y

## update system
apt update && apt upgrade

## 将用户加入到root组
https://bashcommandnotfound.cn/article/linux-usermod-command

## 禁止自启动
sudo systemctl disable vboxadd.service

## 显示全部自启动的服务
systemctl list-unit-files --type=service | grep enabled

## 关机
poweroff
shutdown now


## 基础安装
su - root
apt install aptitude
sudo apt install git
sudo apt install nodejs
sudo apt install libuv1=1.40.0-2+deb11u1
sudo apt install npm
cd /data/ollama-webui-lite
npm install
npm run dev


@安装百度网盘
apt update && apt install baidunetdisk

@安装ftp工具
sudo apt install filezilla

## 用于连接smb
apt install cifs-utils

mkdir /mnt/smb-1
mount -t cifs //192.168.6.39/Root/storage/A114-DB0B /mnt/smb-1 -o username=user,vers=1.0
输入密码：user
或者：mount -t cifs //192.168.6.39/Root/storage/A114-DB0B /mnt/smb-1 -o username=user,password=user

## 依赖包，非必须
sudo apt install libcurl4=7.74.0-1.3+deb11u13
sudo apt install curl

## 安装nvm
### raw.githubusercontent.com无法访问需要修改hosts
nano /etc/hosts
### 185.199.108.133 raw.githubusercontent.com
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
source ~/.bashrc

nvm install node          # 最新版本
nvm install 14.15.1       # 指定版本
nvm use node              # 使用最新版本
nvm use 14.15.1           # 使用指定版本


## apt卸载命令
sudo apt-get remove package_name
或者：sudo apt autoremove python

## 本地安装命令
```
sudo apt install <filename>.deb
```
## 解压压缩包
```
tar -xvf filename.txz
```

## 进程查看命令
ps -ef | grep docker

## 故障：NO_PUBKEY 7EA0A9C3F273FCD8

### 解决
```
find / -name *.gpg
chmod a+r /usr/share/keyrings/docker-archive-keyring.gpg
```

## 万能安装，末尾为镜像名称
bash -c "$(curl -sSLf https://xy.ggbond.org/xy/docker_pull.sh)" -s xuyangbo/open-webui

*** ---  离线包安装方法 开始 ---***
## nodejs升级
参考：https://blog.csdn.net/Mr_Wang9264/article/details/140973079

tar -xf node-v18.12.1-linux-x64.tar.xz -C ./node-v18.12.1-linux-x64/
/home/debian/下载/node-v18.12.1-linux-x64/bin/node -v

## 映射目录
```

mv /home/debian/下载/node-v18.12.1-linux-x64 /data
ln -s /data/node-v18.12.1-linux-x64/bin/npm /usr/local/bin/npm
ln -s /data/node-v18.12.1-linux-x64/bin/node /usr/local/bin/node

```

## 修改环境变量
nano /etc/profile
## 底部增加
export NODE_HOME=/home/debian/下载/node-v18.12.1-linux-x64/bin
export PATH=$PATH:$NODE_HOME:/usr/local/bin/

## 刷新环境变量
source /etc/profile
node -v
npm -v

*** ---  离线包安装方法 结束 ***


## 安装Ollama并运行
'''
cd /home/debian/Downloads/
mkdir ./ollama
tar -zxvf ollama-linux-amd64.tgz -C ./ollama
mv ./ollama /data/ollama/bin
ln -s /data/ollama/bin/ollama /usr/local/bin/ollama

## start ollama
ollama serve

ollama run qwen2 #执行失败

ollama run gemma2:2b #执行成功
'''

***--- chrome begin ---***
## 解压chrome-linux.zip后，添加软连接
ln -s /home/debian/下载/chrome-linux /usr/local/bin/chrome

## 用普通用户执行命令
cd /usr/local/bin/chrome
./chrome --no-sandbox

或者：/usr/local/bin/chrome/chrome --no-sandbox
***--- chrome end ---***

***--- firefox黑屏处理 begin ---***
cd /home/debian/.mozilla/firefox
## 查找parentlock文件，然后执行删除
find / -name .parentlock
rm /home/debian/.mozilla/firefox/2e99sfi5.default-esr/.parentlock
***--- firefox黑屏处理 end ---***

## 查找安装包
sudo apt list | grep python

*** --- python升级 --- ***
sudo apt remove python2
## 安装指定版本
sudo apt install python3.11.2-1+b1



## 安装软件包
### install python3
```
python3 --version
```
### install nodejs
http://deb.nodesource.com/

```
ln -s /usr/bin/node /usr/local/bin/node
ln -s /usr/bin/npm /usr/local/bin/npm
```

npm config get registry
npm config set registry https://registry.npm.taobao.org
npm config set registry https://mirrors.cloud.tencent.com/npm/

find / -name ".npmrc"
nano /root/.npmrc

### install sublime-text
```
apt update && apt install sublime-text -y
```

### install xdman, 替代IDM的下载工具
```
cd /data/software
curl -L https://ghproxy.net/https://github.com/subhra74/xdm-experimental-binaries/releases/download/8.0.18-beta/xdman_gtk_8.0.18_amd64.deb -o xdman_gtk_8.0.18_amd64.deb
apt install ./xdman_gtk_8.0.18_amd64.deb
```

### install virtualbox
https://www.linuxtechi.com/how-to-install-virtualbox-on-debian/

apt install /data/virtualbox-7.0_7.0.20-163906~Debian~bookworm_amd64.deb

$ wget https://download.virtualbox.org/virtualbox/7.0.10/Oracle_VM_VirtualBox_Extension_Pack-7.0.10.vbox-extpack

$ sudo vboxmanage extpack install Oracle_VM_VirtualBox_Extension_Pack-7.0.10.vbox-extpack


### install aria2 download tools
[参考链接](https://blog.csdn.net/wudi1107/article/details/138410936)

```
sudo apt install aria2
sudo mkdir /etc/aria2
sudo touch /etc/aria2/aria2.session
sudo chmod 777 /etc/aria2/aria2.session
sudo nano /etc/aria2/aria2.conf
sudo aria2c --conf-path=/etc/aria2/aria2.conf
```
> 如果没有提示错误，按ctrl+c停止运行命令，转为后台运行： 
```
sudo aria2c --conf-path=/etc/aria2/aria2.conf -D
```

### download ed2k files
```
apt install amule
```

## remove softlink
https://www.cyberciti.biz/faq/linux-remove-delete-symbolic-softlink-command/
find /usr/local/bin/ -type l -iname "n*" -print
unlink /usr/local/bin/node
unlink /usr/local/bin/npm

## swap虚拟内存设置
- 通过dd生成一个文件--6G
```
dd if=/dev/zero of=/var/swap count=1024000 bs=6144
```
- 文件转换为 swap 格式
```
mkswap /var/swap
```
- 修改文件权限为600
```
chmod 600 /var/swap
```
- 挂在交换空间
```
swapon /var/swap
```

- 添加开机自启
```
echo '/var/swap swap defaults 0 0'>>/etc/fstab && mount -a
nano /etc/fstab
```

- 手工开启
```
swapon /var/swap
```

- 关闭
```
swapoff /var/swap
```


## install KVM
```
aptitude install virt-manager qemu-system libvirt-daemon-system qemu-utils
```


wifi:
3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    inet 192.168.43.203/24 brd 192.168.43.255 scope global dynamic noprefixroute wlp2s0
       valid_lft 3117sec preferred_lft 3117sec
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

```
nano /etc/network/interfaces
```
content:source /etc/network/interfaces.d/*

nano /etc/network/interfaces.d/br0


粘贴以下内容, wlp2s0 is wifi-name：
```
    auto br0
    iface br0 inet static
        address 192.168.43.203
        broadcast 192.168.43.255
        netmask 255.255.255.0
        gateway 255.255.255.254
        bridge_ports wlp2s0
        bridge_stp off
        bridge_waitport 0
        bridge_fd 0
```
或者

```
auto br0

iface br0 inet dhcp
bridge_ports wlp2s0
```

经实践，以上方法是错误的
只需要打开Network Connections应用，点击左下方加号，创建一个桥接，命名为br0即可

----

- size 60G
```
sudo virt-install --name win10vm --ram 4096 --vcpus=2 --disk path=/var/lib/libvirt/images/win10vm.qcow2,size=60 --os-type windows --os-variant win10 --cdrom /data/os/FirPE-V1.9.1.iso --network bridge=br0 --graphics vnc,listen=0.0.0.0 --noautoconsole
```

- 成功会显示，然后使用Virtual Machine Manager打开即可。
```
Starting install...
Allocating 'win10vm.qcow2'                                  | 8.1 MB  00:02 ... 
Creating domain...                                          |    0 B  00:00     
```
> 这样设置后虽然可以创建成功，虚拟机系统可以正常启动，但是连接不上网络

- 继续设置激活网络
```
virsh net-list --all
virsh net-autostart default
```


Domain is still running. Installation may be in progress.
You can reconnect to the console to complete the installation process.



## error:Dependency is not satisfiable: python3.10-minimal (= 3.10.4-3)
```
sudo apt-get update --fix-missing
sudo apt-get autoremove && sudo apt-get clean && sudo apt-get install -f
```

## error: xfce4-desktop, no wifi

> 安装网络管理工具,及图形工具
```
sudo apt install network-manager network-manager-gnome
```
- 启动网络管理工具

- [参考链接](https://cn.linux-console.net/?p=22364)
```
nmtui
```

- show
```
nmcli connection show
nmcli connection show --active
```

- connect wifi
```
nmcli connection up WIFI_323F
```


## mount ntfs-usb
- install
```
aptitude install ntfs-3g
```
- 使用首次挂载如下：
```
mount -t ntfs-3g /dev/sdd1 /mnt/usb/
```

- del
```
umount /mnt/usb/
```

- exfat则需要安装
```
aptitude install fuse-exfat exfat-utils
```

## 安装微信
```
cd /data/software
wget https://www.atzlinux.com/atzlinux/pool/main/a/atzlinux-archive-keyring/atzlinux-v12-archive-keyring_lastest_all.deb
apt -y install ./atzlinux-v12-archive-keyring_lastest_all.deb
apt update

apt show com.tencent.wechat
apt install com.tencent.wechat -y
```

## 安装esd系统后无法进入，报错0xc0000098
> 这是安装文件损坏导致的，使用md5sum对比其结果，重新拷贝文件安装即可。




