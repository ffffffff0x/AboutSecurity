# RedHat system infrastructure configuration.

---

# Basic installation (基本配置)

```bash
# EPEL
curl -o /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
rm -f /var/run/yum.pid
yum clean all && yum makecache

yum groupinstall -y "Development Tools"
yum install -y yum-utils
yum install -y vim make gcc gcc-c++ curl git lrzsz wget unzip openssl-devel p7zip
yum install -y kernel-devel
yum install -y dnf telnet tree gdb
yum update

# Proxychains-ng
cd /tmp/test
# rz upload a proxychains-ng.zip
unzip proxychains-ng.zip
cd proxychains-ng-master
./configure
make && make install
cp ./src/proxychains.conf /etc/proxychains.conf
cd .. && rm -rf proxychains-ng
vim /etc/proxychains.conf    # Change it to your proxy.

# Python
rm -f /var/run/yum.pid
yum install -y python36 python36-devel
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py
yum install -y python-pip
yum install -y python-devel
yum install -y python3-devel
pip install --upgrade pip

# Docker
rm -f /var/run/yum.pid

yum install -y yum-utils device-mapper-persistent-data lvm2
wget -O /etc/yum.repos.d/docker-ce.repo https://download.docker.com/linux/centos/docker-ce.repo
sed -i 's+download.docker.com+mirrors.tuna.tsinghua.edu.cn/docker-ce+' /etc/yum.repos.d/docker-ce.repo
yum makecache fast
yum install -y docker

systemctl start docker
systemctl enable docker

# Docker-compose
proxychains4 bash
wget "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -O /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

---

# Change mirrors (换源)

> If your service does not go through any firewall, you know, this step is not needed

```bash
# pip
mkdir -p ~/.pip/
tee ~/.pip/pip.conf <<-'EOF'
[global]
index-url = https://mirrors.aliyun.com/pypi/simple/

[install]
trusted-host=mirrors.aliyun.com
EOF

# Docker
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
EOF
systemctl restart docker
systemctl daemon-reload
```

---

# bash-insulter

> Install or skip according to your preference🤣

```bash
git clone https://github.com/No-Github/bash-insulter.git bash-insulter
cp bash-insulter/src/bash.command-not-found /etc/
chmod 777 /etc/bash.command-not-found
source /etc/bash.command-not-found
```

```vim
vim /etc/bashrc

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
