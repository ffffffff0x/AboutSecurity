# 网络设备默认口令 (Device_pass)

---

## Ruijie Networks

```
ruijie  ruijie
```

**锐捷 ap**
```
admin/ruijie  apdebug
```

---

## HUAWEI

**华为 RTSP**
```
admin       HuaWei123
```

**华为 switch**
```
huwei    huawei@1234
```

**Huawei ADSL2+**
```
admin/admin
```

**V200R003**
```
admin/admin
```

**V200R005C00-V200R005C20**
```
admin/Admin@huawei or admin
```

**V200R005C30-V300R003C10**
```
admin/Admin@huawei
```

**V300R019C00-latest**
```
admin/admin@huawei.com
```

### FusionCompute

**fusioncompute**

- 普通模式：admin/IaaS@PORTAL-CLOUD8!
- 三员分立模式：
    - 系统管理员：sysadmin/Sysadmin#
    - 安全管理员：secadmin/Secadmin#
    - 安全审计员：secauditor/Secauditor#
- 用户名：admin   密码：Admin@123
- 用户名：root    密码：Galax@8800
- 用户名：admin   密码：Huawei@CLOUD8!

**FusionManager**

- FusionManager 帐户
    - 用户名：admin 密码：Admin@123
    - 用户名：geadmin 密码：Admin@123
    - 说明： 使用该帐户登录 FusionManager 并跳转到 FusionCompute 后，拥有 FusionCompute 系统的所有管理和维护权限。使用其余帐户跳转到 FusionCompute 后，只能查看数据和修改告警阈值。

- FusionManager 节点操作系统帐户
    - 用户名：root 密码：Huawei@001
    - 不能直接使用 root 帐户登录。若需要使用 root 帐户，需先用 galaxmanager 帐户登录，然后执行 su - root 切换到 root 帐户。
- FusionManager 节点操作系统帐户（业务帐户）
    - 用户名：galaxmanager 密码：GalaxManager_2012
- FusionManager 访问数据库的帐户
    - 用户名：galaxmanager 密码：GalaxManager7!
- FusionManager 数据库的帐户
    - 用户名：cloudmgr 密码：Manager@123
- FusionManager 数据库默认的系统帐户
    - 用户名：sys 密码：System@123
- FusionCompute  主机的操作系统帐户
    - 用户名：root 密码：Huawei_123
    - 不能直接使用 root 帐户登录。若需要使用 root 帐户，需先用 gandalf 帐户登录，然后执行 su - root 切换到 root 帐户。
- 主机的操作系统帐户（业务帐户）
    - 用户名：gandalf 密码：Pwd8800_magic$
- VRM 节点的操作系统帐户
    - 用户名：root 密码：root
    - 不能直接使用 root 帐户登录。若需要使用 root 帐户，需先用 gandalf 帐户登录，然后执行 su - root 切换到 root 帐户。
- VRM 节点的操作系统帐户（业务帐户）
    - 用户名：gandalf 密码：Pwd8800_magic$
- FusionCompute 访问数据库的帐户
    - 用户名：galax 密码：SingleLOUD!1
- 管理节点 VNC 登录帐户
    - 用户名：root 密码：GalaX088
- FusionCompute 对健康检查工具的北向接口认证账户
    - 用户名：hchksysman 密码：HchkEnginE@456
- FusionCompute 对 FusionAccess 的北向接口认证账户
    - 用户名：vdisysman 密码：VdiEnginE@234
- FusionCompute 对内部的北向接口认证账户
    - 用户名：gesysman 密码：GeEnginE@123
- FusionStorage  FusionStorage Manager 节点操作系统帐户
    - 用户名：root 密码：UVP_2012lab
- FusionStorage Manager 节点操作系统的业务帐户
    - 用户名：dsware 密码：dsmHuawei@123
- FusionStorage 访问数据库的帐户
    - 用户名：omm 密码：ommHuawei@123
- 内部部件通讯帐户  FusionManager 对 FusionCompute 的内部通讯帐户
    - 用户名：GERest 密码：Rest@GE123
- FusionCompute 对 FusionManager 的内部通讯帐户
    - 用户名：gmsysman 密码：GMEnginE@123
- FusionManager 对 FusionStorage 的内部通讯帐户
    - 用户名：OmmRest 密码：Omm@1234
- FusionStorage 对 FusionManager 的内部通讯帐户
    - 用户名：gmadmin 密码：gmHuawei@123
- FusionManager 内部的通讯帐户
    - 用户名：GmUhmRest 密码：Rest@GmUhm123
- FusionCompute 内部的通讯帐户
    - 用户名：gesysman 密码：GeEnginE@123
- FusionStorage 对外提供的 Rest 接口帐户  FusionStorage 对其他 Rest 接口帐户提供的接口帐户
    - 用户名：admin 密码：Huawei@123
- FusionStorage 对健康检查工具提供的接口帐户
    - 用户名：healthycheckadmin 密码：hcHuawei@123
- FusionStorage 对 CLI 命令行界面提供的接口帐户
    - 用户名：cmdadmin 密码：cmdHuawei@123
- FusionStorage 对升级补丁提供的接口帐户
    - 用户名：upadmin 密码：upHuawei@123
- FusionStorage 预留的 Rest 接口帐户
    - 用户名：rsadmin 密码：rsHuawei@123
- FusionStorage 对 HA 机制提供的接口帐户
    - 用户名：haadmin 密码：haHuawei@123
- FusionStorage 对 OMM 内部模块提供的接口帐户
    - 用户名：systemman 密码：Admin@123
- FusionStorage 对 FusionCompute 提供的接口帐户
    - 用户名：geadmin 密码：geHuawei@123
- FusionManager 访问硬件设备的帐户  FusionManager 访问主机操作系统的帐户
    - 用户名：gandalf 密码：Pwd8800_magic$
- FusionManager 访问主机 BMC 的帐户
    - 用户名：uhmroot 密码：UhmRoot@2012
- FusionManager 访问机框的帐户
    - 用户名：uhmroot 密码：UhmRoot@2012
- FusionManager 访问存储设备的帐户
    - 用户名：uhmroot 密码：UhmRoot@2012
- FusionManager 访问交换机的帐户
    - 用户名：uhmroot 密码：UhmRoot@2012
- FTP 帐户  FusionCompute 下发 CNA、Tools 补丁到主机上的帐户
    - 用户名：ftppatchuser 密码：Patch_123
- 日志服务器 FTP 帐户
    - 用户名：cnalog 密码：1q2w3e~!
- 硬件设备帐户  E6000 服务器刀片 BMC 系统帐户
    - 用户名：root 密码：root
- E6000 服务器管理模块帐户
    - 用户名：root 密码：huaweiosta
- E9000 服务器刀片 BMC 系统帐户
    - 用户名：root 密码：Huawei12#$
- E9000 服务器管理模块帐户
    - 用户名：root 密码：Huawei12#$
- IP SAN 存储管理系统帐户
    - 用户名：admin 密码：Admin@storage

**FusionStorage Block**

- 软硬一体场景下操作系统帐户
    - 用户名：root 密码：Huawei@123

- FusionStorage Manager（FSM）节点操作系统帐户
    - 用户名：root 密码：IaaS@OS-CLOUD8!

- FSM 节点操作系统的业务帐户
    - 用户名：dsware 密码：IaaS@OS-CLOUD9!

- FusionStorage Block 访问数据库的帐户
    - 用户名：omm 密码：IaaS@DATABASE-PublicCLOUD9!

- FSM 节点操作系统上独立运行数据库的帐户
    - 用户名：ommdba 密码：IaaS@OS-FSBDBACLOUD8!

- FSM 节点数据库的管理员帐户
    - 用户名：ommdba 密码：IaaS@DATABASE-CLOUD8!

- FSM 节点操作系统的软件管理帐户
    - 用户名：omm 密码：IaaS@OS-FSBCLOUD8!

- FusionStorage Block 对外提供的 Rest 接口帐户
    - FusionStorage Block 对 FusionManager 的内部通讯帐户
        - 用户名：gmadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对其他 Rest 接口帐户提供的接口帐户
        - 用户名：admin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 eSight 提供的接口帐户
        - 用户名：cmdadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 CLI 命令行界面提供的接口帐户
        - 用户名：cmdadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对升级补丁提供的接口帐户
        - 用户名：upadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 FusionCare 提供的接口帐户
        - 用户名：pmiadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 HA 机制提供的接口帐户
        - 用户名：haadmin 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 OMM 内部模块提供的接口帐户
        - 用户名：systemman 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 FusionCube 管理系统提供的接口帐户
        - 用户名：fc2Rest 密码：IaaS@PORTAL-CLOUD9!
    - FusionStorage Block 对 vCenter 提供的接口帐户
        - 用户名：vnadmin 密码：vnIaaS@PORTAL-CLOUD9!
    - FSM 节点操作系统 grub 帐户  FSM 节点操作系统 grub 引导程序的帐户
        - 密码：IaaS@OS-FSBGRUB8!

- FSM 节点 FTP 帐户
    - FusionStorage Block 用于元数据备份的 FTP 帐户
        - 用户名：metadata_backup 密码：IaaS@SERVICE-CLOUD9!
    - FusionStorage Block 用于 FusionCare 进行信息收集的帐户
        - 用户名：pmi 密码：IaaS@SERVICE-CLOUD9!
    - FusionStorage Block 用于脚本进行信息收集的 FTP 帐户
        - 用户名：ops_tool 密码：IaaS@SERVICE-CLOUD9!
    - FusionStorage Block 用于微服务安装的 FTP 帐户
        - 用户名：install 密码：IaaS@SERVICE-CLOUD9!
    - FusionStorage Block 用于 OMM 组件进行升级包获取的 FTP 帐户
        - 用户名：omm_ftpserver 密码：IaaS@SERVICE-CLOUD9!

- FusionStorage Block 自助维护平台
    - 用户名：admin 密码：IaaS@PORTAL-CLOUD8!

---

## hikvision

```
admin  初始密码一般设为 12345 123456  888888  admin
admin/Admin@123
```

---

## ZTE

```
admin/admin
```

## 3Com

```
admin/admin
```

---

## Linksys

```
admin/admin
```

---

## Belkin

```
admin/admin
```

---

## 思科

```
admin/123456
用户名:admin   密码:cisco
```

---

## FUJI XEROX

**FUJI XEROX 打印机**
```
11111 x-admin
```

---

## RICOH

**RICOH 打印机**
```
supervisor 密码为空
```

---

## juniper

```
用户名:netscreen   密码:netscreen
```

---

## Netgear

```
admin/password
```

---

## US Robotics

```
root/letmein
```

---

## Arris

```
admin/password
```

---

## Netcomm

```
admin/password
```

---

## Synology

```
admin  123456
admin/Admin
```

## ASUS

```
admin/admin
```

## BenQ

```
admin/admin
```

## D-Link

```
admin/admin
```
