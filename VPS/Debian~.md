# Debian system infrastructure configuration.

---

# Basic installation (基本配置)

```bash
# Ubuntu apt mirror
tee /etc/apt/sources.list <<-'EOF'

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

# Debain apt mirror
tee /etc/apt/sources.list <<-'EOF'

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

rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

# SSH
apt update
apt install -y ssh

echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
service ssh restart
systemctl enable ssh

# python
apt install -y python
wget https://bootstrap.pypa.io/get-pip.py
python2 get-pip.py
python3 get-pip.py
python2 -m pip install --upgrade pip
apt-get install -y python-dev
apt-get install -y python3-dev
apt-get install -y python-pip
apt-get install -y python3-pip

# 安装依赖 (install dependence)
apt install -y gcc g++
apt install -y make
apt install -y vim git curl lrzsz wget unzip resolvconf p7zip
apt install -y apt-transport-https
apt install -y ca-certificates
apt install -y software-properties-common
apt install -y kernel-devel
apt update

# Change DNS
echo "nameserver 223.5.5.5" > /etc/resolvconf/resolv.conf.d/head
resolvconf -u

# proxychains
cd /tmp/
# rz upload a proxychains-ng.zip
unzip proxychains-ng.zip
cd proxychains-ng-master
./configure
make && make install
cp ./src/proxychains.conf /etc/proxychains.conf
cd .. && rm -rf proxychains-ng
vim /etc/proxychains.conf    # Change it to your proxy.

# docker
rm -rf /var/cache/apt/archives/lock
rm -rf /var/lib/dpkg/lock-frontend
rm -rf /var/lib/dpkg/lock
rm /var/lib/dpkg/lock
rm /var/lib/apt/lists/lock

apt remove docker docker-engine docker.io
apt-get install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  software-properties-common \
  gnupg

curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | apt-key add -
echo 'deb https://download.docker.com/linux/debian stretch stable'> /etc/apt/sources.list.d/docker.list
apt update
apt install -y docker-ce

docker version
systemctl start docker
systemctl enable docker

# docker-compose
wget https://github.com/docker/compose/releases/download/1.25.5/docker-compose-Linux-x86_64
mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

docker-compose version
```

---

# Change mirrors (换源)

> If your service does not go through any firewall, you know, this step is not needed

```bash
# pip
mkdir -p ~/.pip/
tee ~/.pip/pip.conf <<-'EOF'
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
EOF

# Docker
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

---

# bash-insulter

> Install or skip according to your preference🤣

```bash
cd /tmp/test
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
