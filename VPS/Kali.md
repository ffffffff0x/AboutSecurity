# Kali 配置

---

# 1.安装配置基础环境

```bash
# SSH
echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
systemctl start ssh
systemctl enable ssh
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t dsa -f /etc/ssh/ssh_host_rsa_key

# apt 换源
sudo tee /etc/apt/sources.list <<-'EOF'
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
EOF

# 依赖
apt install -y gcc g++ make vim git curl lrzsz wget unzip resolvconf
apt install -y apt-transport-https ca-certificates software-properties-common

# 换 DNS
echo "nameserver 223.5.5.5" > /etc/resolvconf/resolv.conf.d/head
resolvconf -u

# 安装中文字体
apt install -y xfonts-intl-chinese ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy

# /pentest 作为存放渗透工具的文件夹
# /tmp/test 作为存放临时文件的文件夹
mkdir /pentest
mkdir /tmp/test

# AboutSecurity
cd /
git clone https://github.com/ffffffff0x/AboutSecurity.git

# pip3
cd /tmp/test
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py

# go
cd /tmp/test
# rz 一个 go1.13.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.13.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
export GOROOT=/usr/local/go
export GOPATH=$HOME/Applications/Go
source $HOME/.profile
source ~/.bash_profile
go version
```

---

# 2.换源

```bash
# pip 换源
mkdir -p ~/.pip/
sudo tee ~/.pip/pip.conf <<-'EOF'
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
EOF

# docker 换源
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
EOF
sudo systemctl enable docker
sudo systemctl restart docker
sudo systemctl daemon-reload

# GO 换源
go env -w GO111MODULE=on
go env -w GOPROXY="https://goproxy.io,direct"
```

---

# 3.安装渗透工具

```bash
cd /tmp/test

# Misc工具
gem install zsteg
apt install -y foremost lrzsz parallel owasp-mantra-ff

# ncat
apt install ncat
update-alternatives --config nc
1

# powershell
apt install powershell
pwsh            # 启动
$PSVersionTable # 测试一下

# ffuf
wget https://github.com/ffuf/ffuf/releases/download/v1.1.0/ffuf_1.1.0_linux_amd64.tar.gz
tar -zxvf ffuf_1.1.0_linux_amd64.tar.gz
mv ffuf /usr/local/bin/
chmod +x /usr/local/bin/ffuf
ffuf -V

# oneforall
cd /pentest
git clone https://gitee.com/shmilylty/OneForAll.git
cd OneForAll/
python3 -m pip install -U pip setuptools wheel -i https://mirrors.aliyun.com/pypi/simple/
pip3 install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/
python3 oneforall.py --help

# ksubdomain
cd /tmp/test
apt install -y libpcap-dev

wget https://github.com/knownsec/ksubdomain/releases/download/v0.5.1/ksubdomain_linux.zip
unzip ksubdomain_linux.zip
mv ksubdomain /usr/local/bin/
chmod +x /usr/local/bin/ksubdomain
ksubdomain

# python模块
pip install PyJWT pyshark requests sqlparse threadpool urllib3 lxml pyzbar

# AWVS-13
docker pull secfa/docker-awvs
docker run -it -d -p 13443:3443 secfa/docker-awvs
    # 容器的相关信息
    # awvs13 username: admin@admin.com
    # awvs13 password: Admin123
    # AWVS版本：13.0.200217097
    # 浏览器访问：https://127.0.0.1:13443/ 即可
```
