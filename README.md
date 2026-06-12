# LeekShell

> 轻量化、全自研C2——红队的新选择 | 实测卡巴斯基优选版+EDR双双失明

[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-blue)](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-blue)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://img.shields.io/badge/Python-3.8%2B-blue)
[![C++](https://img.shields.io/badge/C%2B%2B-17-orange)](https://img.shields.io/badge/C%2B%2B-17-orange)
[![License](https://img.shields.io/badge/License-Research%20Only-red)](https://img.shields.io/badge/License-Research%20Only-red)

**LeekShell** 是一款完全自研的轻量级C2框架，采用 **Python + C++** 架构，舍弃部分冗余功能，以换取更高隐蔽性与可控性。

市面上的Cobalt Strike、Sliver、Havoc，特征库已被安全厂商翻了个底朝天。即使魔改profile、二次开发beacon，面对杀软以及EDR也比较乏力。于是，这款完全自研的C2框架——**LeekShell（第一版）** 应运而生。

> **源码不公开的原因**：作者个人在国内，本工具仅供学习研究及合法授权使用。不公开源码是为了避免被恶意利用，保护作者及使用者的安全。

---

## 📌 目录

- [免杀能力实测](#-免杀能力实测)
- [使用指南](#-使用指南)
- [快速开始](#-快速开始)
- [为什么自研新的C2？](#-为什么自研新的c2)
- [免责声明](#-免责声明)

---

## 🛡️ 免杀能力实测

| 安全产品 | 版本 | 测试结果 |
|---------|------|----------|
| **卡巴斯基优选版** (Kaspersky Premium) | 2026.06 最新特征库 | ✅ 上线成功，命令执行成功，全程无弹窗无拦截 |
| **卡巴斯基端点检测与响应** (Kaspersky EDR) | 2026.06 最新特征库 | ✅ 上线成功，执行 `whoami`、`ipconfig`、`tasklist` 等命令回显正常，EDR控制台无任何高危告警 |

> 测试环境：Windows 10 21H2，卡巴斯基全部更新至2026年6月最新特征库。

---
### Kaspersky Premium：

<img width="1632" height="729" alt="685dcf87c5b1500adab5562360a6fee7" src="https://github.com/user-attachments/assets/fcc81702-67dd-4148-a5a6-53629b88ad1b" />
<img width="948" height="600" alt="68f7b7478ec5e56997106f8b54a6995c" src="https://github.com/user-attachments/assets/b6ce0559-1a9a-4b43-82e0-9ef369eed655" />
<img width="1842" height="699" alt="faa35c805c5de2bb197c677b2e0f5879" src="https://github.com/user-attachments/assets/cb1da435-3cf4-46a7-a1c3-4d6d19779f11" />

### Kaspersky EDR：
<img width="1515" height="584" alt="cd6c9a2c1af8bccb52b423ff72e3f9e3" src="https://github.com/user-attachments/assets/8fcfd9f9-23c9-459d-bcdd-d29ee0c45d29" />
<img width="951" height="570" alt="1fc2d9fd40f87a0c053d907b3dadc03a" src="https://github.com/user-attachments/assets/79c485c6-aec2-4027-a4a6-467a8470deda" />
<img width="1803" height="795" alt="413a43c3df8bea4d6b42d58f16a4ddec" src="https://github.com/user-attachments/assets/223122fb-8f89-4cf8-a61c-691dfba42c82" />



## 📖 使用指南

### ⚠️ 强烈建议

将生成的 **exe** 转为 **Shellcode**，并使用**自定义加载器**加载执行。

**为什么？**  
因为工具使用人数增多后，`exe` 的静态特征可能会被安全软件标记。转为 Shellcode 并配合自己的加载器，可以大幅提升免杀效果。

**不用担心**  
作者会**每周重构并发布新版本**，持续更新，对抗特征库升级。

---

## 🚀 快速开始

### 1. Server端部署

直接启动LeekShell.exe     
从浏览器访问控制台（默认）：`http://127.0.0.1:4433`

### 2. 独立监听设置（以80端口为例）

找到 `Listeners` → 填写端口号 → 点击 `Add`，即可添加新监听。

### 3. Payload 生成

填写服务端的IP以及监听的端口号，点击**生成**。  
浏览器会自动下载一个生成好的 **EXE文件**。

### 4. 实际运行效果

> 目前版本仅支持执行命令，隐蔽性较好。  
> （截图略，读者可自行测试验证）

---

## 🤔 为什么自研新的C2？

### 现状痛点

| C2框架 | 问题 |
|--------|------|
| **Cobalt Strike** | 特征库被撸烂，哪怕换了stageless、做了sleep mask，流量和行为模式仍有强特征 |
| **Sliver** | 开源但代码公开，商业EDR可以针对性做检测规则 |
| **其他小众C2** | 功能残缺，稳定性差，免杀基本靠第三方Loader，操作链路冗长 |

### 红队对C2的核心需求

- **上线稳定**：不挑网络环境
- **流量隐蔽**：端口、通信协议可自由定制
- **免杀**：至少能扛住主流EDR（尤其是卡巴斯基这类重武器）的静态+动态检测
- **功能够用**：执行命令、文件上传下载、进程管理、内存执行等基础能力不能少

**LeekShell 就是奔着这几条去的。**

> 当然，免杀永远是猫鼠游戏。测试时卡巴斯基没杀，不代表以后不会杀。这也是我建立交流群的原因——**免杀有时效性，需要你们的反馈来持续迭代**。

---



## ⚠️ 免责声明

1. **合法使用**：LeekShell 仅限用于**授权的安全测试、渗透测试、红队演练、攻防竞赛**等合法场景。使用者必须确保已获得目标系统的**书面授权**，并遵守所在国家及地区的法律法规（包括但不限于《中华人民共和国网络安全法》《数据安全法》）。
2. **禁止恶意行为**：严禁将 LeekShell 用于任何**未授权的入侵、窃取数据、破坏系统、勒索、恶意控制**等非法活动。因使用者违反法律法规或滥用工具所引发的一切法律责任，**均由使用者自行承担，与作者无关**。
3. **技术交流**：本文及群内分享的内容仅作为**网络安全技术研究与交流**之用。作者不鼓励、不支持任何形式的黑产或恶意攻击行为。
4. **工具风险**：LeekShell 作为自研工具，可能存在未知 Bug 或安全缺陷。使用者应自行评估风险，并在隔离环境中测试。作者不对因使用本工具造成的任何直接或间接损失负责。
5. **保留权利**：作者保留随时停止共享、更新或修改 LeekShell 的权利。本文所述功能及免杀效果均为特定环境的测试结果，不承诺在其他环境中长期有效。

**请务必在下载、使用前仔细阅读本声明。如不同意，请立即停止使用并删除相关文件。**

---

## 📄 License

本项目仅限学习研究及合法授权使用，严禁商业用途或非法传播。

---

## 更新日志

2026/6/12  ---  新增Symantec绕过；程序EXE格式转换；新增图标
