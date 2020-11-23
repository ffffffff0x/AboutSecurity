# RedHat system infrastructure configuration.

---

# Basic installation

```bash
rm -f /var/run/yum.pid

yum clean all
yum makecache

rm -f /var/run/yum.pid

yum groupinstall -y "Development Tools"
yum install -y yum-utils
yum install -y vim make gcc gcc-c++ curl git lrzsz wget unzip openssl-devel epel-release p7zip
yum update
```

---

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

---

# python

```bash
rm -f /var/run/yum.pid

yum install -y python36 python36-devel

proxychains4 bash

wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py

# or

yum install python-pip

# Change mirrors
mkdir -p ~/.pip/
sudo tee ~/.pip/pip.conf <<-'EOF'
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
EOF
```

---

# docker

```bash
rm -f /var/run/yum.pid

yum install -y yum-utils device-mapper-persistent-data lvm2
wget -O /etc/yum.repos.d/docker-ce.repo https://download.docker.com/linux/centos/docker-ce.repo
sed -i 's+download.docker.com+mirrors.tuna.tsinghua.edu.cn/docker-ce+' /etc/yum.repos.d/docker-ce.repo
yum makecache fast
yum install -y docker

sudo systemctl start docker
```

```bash
proxychains4 bash
sudo wget "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -O /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
EOF
sudo systemctl enable docker
sudo systemctl restart docker
sudo systemctl daemon-reload
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
