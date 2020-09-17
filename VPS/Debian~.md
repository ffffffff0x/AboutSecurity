# Debian 系配置

---

# Net
```bash
nano /etc/network/interfaces

auto enp7s0
iface enp7s0 inet static
address 10.0.208.222
netmask 255.255.240.0
gateway 10.0.208.1
dns-nameservers 10.0.208.1
```
```bash
systemctl restart networking.service
```
```vim
vim /etc/resolv.conf
nameserver 8.8.8.8
```

# SSH
```bash
apt update
apt install -y ssh
```
```bash
echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
service ssh restart
systemctl enable ssh
```

# apt
**Ubuntu apt 换源**
```vim
sudo tee /etc/apt/sources.list <<-'EOF'

deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
EOF
```

**Debain apt 换源**
```vim
sudo tee /etc/apt/sources.list <<-'EOF'

# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
EOF
```

**Kali apt 换源**
```vim
sudo tee /etc/apt/sources.list <<-'EOF'
deb http://http.kali.org/kali kali-rolling main non-free contrib

# 清华源
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

# 官方源
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib

# 中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

# 浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
EOF
```

# base
```bash
rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

apt update

rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

apt install -y gcc g++ make vim git curl lrzsz wget unzip resolvconf
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
apt update

echo "nameserver 114.114.114.114" > /etc/resolvconf/resolv.conf.d/head
resolvconf -u
```

# proxychains
```bash
rz

unzip proxychains-ng.zip
cd proxychains-ng-master
./configure
make && make install
cp ./src/proxychains.conf /etc/proxychains.conf
cd .. && rm -rf proxychains-ng
vim /etc/proxychains.conf
```

# python
```bash
rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

apt install -y python
```
```bash
proxychains4 bash
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py

# 或

apt-get install -y python-pip
```

```bash
mkdir -p ~/.pip/
sudo tee ~/.pip/pip.conf <<-'EOF'
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
EOF

pip install pyinstaller
```

# docker
```bash
rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

apt remove docker docker-engine docker.io
sudo apt-get install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  software-properties-common \
  gnupg

curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
echo 'deb https://download.docker.com/linux/debian stretch stable'> /etc/apt/sources.list.d/docker.list
apt update
apt install -y docker-ce

docker version
sudo systemctl start docker
```
```bash
proxychains4 bash
wget https://github.com/docker/compose/releases/download/1.25.5/docker-compose-Linux-x86_64
mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://rf7ead45.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
sudo systemctl enable docker

docker-compose version
```

# bash-insulter
```bash
git clone https://github.com/No-Github/bash-insulter.git bash-insulter
cp bash-insulter/src/bash.command-not-found /etc/
chmod 777 /etc/bash.command-not-found
source /etc/bash.command-not-found
```

```vim
vim /etc/bash.bashrc

. /etc/bash.command-not-found
echo "$(tput cuf 10) $(tput setab 1)FBI WARNING$(tput sgr 0)"
echo ""
echo "Federal Law provides severe civil and criminal penalties for
the unauthorized reproduction, distribution, or exhibition of
copyrighted motion pictures (Title 17, United States Code,
Sections 501 and 508). The Federal Bureau of Investigation
investigates allegations of criminal copyright infringement"
echo "$(tput cuf 5) (Title 17, United States Code, Section 506)."
```
