<p align="center">
    <img src="./assets/img/logo.png" width="30%">
</p>

<p align="center">
    <img src="https://img.shields.io/badge/Category-Fuzz List-red.svg">
    <img src="https://img.shields.io/github/last-commit/No-Github/AboutSecurity.svg?style=popout">
    <img src="https://img.shields.io/github/repo-size/No-Github/AboutSecurity?color=yellow">
</p>

[English](README.md) | 简体中文

---

* **简介** : 分享字典和 payload
* **定位** : ffffffff0x 团队军火库
* **更新时间** : 不定期
* **项目地址** : https://github.com/ffffffff0x/AboutSecurity

---

## Manual

* **[Dic](./Dic/README.md)**
    * Auth : 认证字典
        * 账号和密码。
    * Network : 网络
        * 排除的私有 IP 段、本地 IP 段、dns 服务器列表。
    * Port : 端口字典
        * 按照端口渗透的想法,将不同端口承载的服务可爆破点作为字典内容。
    * Regular : 规则字典
        * 各种规则、排列的字典整理。
    * Web : Web 字典
        * 顾名思义,在 web 渗透过程中出现的可爆破点作为字典内容。
* **Payload**
    * Burp
    * CORS
    * email
    * Format
    * HPP
    * LFI
    * OOB
    * SQL-Inj
    * SSI
    * XSS
    * XXE
* **VPS(不在维护这一部分，请使用 [f8x](https://github.com/ffffffff0x/f8x) 工具)**
    * [Debian~](./VPS/Debian~.md) - Debian 系基础设施配置。
    * [Kali](./VPS/Kali.md) - Kali 系统基础设施配置。
    * [RedHat~](./VPS/RedHat~.md) - RedHat 系基础设施配置。
* **[Checklist](./Checklist.zh-cn.md)** : 渗透测试过程中的检查项,杜绝少测、漏测的情况。
* **[CheatSheet](./CheatSheet.md)** : 渗透测试信息收集表,渗透测试时直接复制一副作为参考、信息记录、方便团队协作、出报告等。
* **[出报告专用](./出报告专用.md)**: 记录部分平常渗透测试遇到的案例,整理如下,出报告专用😁。
* **[行业名词](./行业名词.md)**

---

## 协作者&致谢

- [CONTRIBUTORS](./assets/CONTRIBUTORS.md)

---

## 免责声明&版权协议

- <sup>本项目采用 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.zh) 协议.</sup>
    - <sup>共享 — 在任何媒介以任何形式复制、发行本作品。</sup>
    - <sup>演绎 — 修改、转换或以本作品为基础进行创作在任何用途下，甚至商业目的。</sup>
    - <sup>署名 — 您必须给出适当的署名，提供指向本许可协议的链接，同时标明是否（对原始作品）作了修改。您可以用任何合理的方式来署名，但是不得以任何方式暗示许可人为您或您的使用背书。</sup>
    - <sup>相同方式共享 — 如果您再混合、转换或者基于本作品进行创作，您必须基于与原先许可协议相同的许可协议 分发您贡献的作品。</sup>
    - <sup>没有附加限制 — 您不得适用法律术语或者 技术措施 从而限制其他人做许可协议允许的事情。</sup>
- <sup>注: 本项目所有文件仅供学习和研究使用,请勿使用项目中的文件用于非法用途,任何人造成的任何负面影响,与本人无关.</sup>
- <sup>注: 下载这个资源库很可能会让你的反病毒软件报毒，请将项目路径列入白名单。在本项目中没有恶意文件，但是由于本地文件包含攻击的风险，不建议将这些文件存储在服务器或其他重要系统上.</sup>
