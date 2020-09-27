# Kali 配置

---

- 渗透脚本放在 /pentest
- 残留文件放在 /tmp/test
- 默认下所有命令走 proxychains4

---

# 1.配置基础环境

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
apt update

# 依赖
apt install -y gcc
apt install -y g++
apt install -y make
apt install -y vim git curl lrzsz wget unzip resolvconf p7zip
apt install -y apt-transport-https
apt install -y ca-certificates
apt install -y software-properties-common

# 换 DNS
echo "nameserver 223.5.5.5" > /etc/resolvconf/resolv.conf.d/head
resolvconf -u

# 安装中文字体
apt install -y xfonts-intl-chinese ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy

# /pentest 作为存放渗透工具的文件夹
# /tmp/test 作为存放临时文件的文件夹
mkdir /pentest
mkdir /tmp/test

# proxychains-ng
cd /tmp/test
# rz 一个 proxychains-ng.zip
unzip proxychains-ng.zip
cd proxychains-ng
./configure
make && make install
cp ./src/proxychains.conf /etc/proxychains.conf
cd .. && rm -rf proxychains-ng
vim /etc/proxychains.conf    # 改成你懂的

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

# 3.安全工具安装

```bash
cd /tmp/test

# Misc工具
gem install zsteg
apt install -y foremost lrzsz parallel owasp-mantra-ff
apt install -y rarcrack

# hashcat、7z2hashcat
cd /pentest
wget https://hashcat.net/files/hashcat-6.1.1.7z
wget https://raw.githubusercontent.com/philsmd/7z2hashcat/master/7z2hashcat.pl
7z x hashcat-6.1.1.7z && rm -rf hashcat-6.1.1.7z
cd hashcat-6.1.1 && chmod +x hashcat.bin && cp hashcat.bin hashcat
ln -s /pentest/hashcat-6.1.1/hashcat /usr/sbin/hashcat

# ncat
apt install ncat
update-alternatives --config nc
1

# powershell
apt install powershell
pwsh            # 启动
$PSVersionTable # 测试一下

# binwalk
cd /tmp/test
wget https://github.com/ReFirmLabs/binwalk/archive/master.zip
unzip master.zip
(cd binwalk-master && sudo python setup.py uninstall && sudo python setup.py install)

# sasquatch
cd /tmp/test
sudo apt-get install -y build-essential liblzma-dev liblzo2-dev zlib1g-dev
git clone https://github.com/devttys0/sasquatch
cd sasquatch
./build.sh

# unyaffs
cd /tmp/test
wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/unyaffs/unyaffs
mv unyaffs /usr/local/bin/
chmod +x /usr/local/bin/unyaffs
unyaffs

# ffuf
cd /tmp/test
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
