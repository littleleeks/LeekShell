# LeekShell C2 Server — 发布包

LeekShell 是一套面向授权安全测试与红队演练场景的远程管理框架。
控制端为无依赖单文件可执行程序，内置全部 Agent 模板（PE / ELF / Shellcode），
无需安装 Python 或其他运行时，上传即可运行。

> ⚠️ **仅限授权测试与教学研究使用。** 未经授权访问他人系统属违法行为，
> 使用者须自行承担全部法律责任。

---

## 文件清单

| 文件 | 说明 |
|------|------|
| `c2_server.exe` | Windows 控制端（x86_64，PyInstaller 单文件） |
| `c2_server_linux` | Linux 控制端（x86_64，PyInstaller 单文件） |
| `config.example.yaml` | 示例配置（请复制为 config.yaml 后修改） |
| `README.md` | 本说明 |

Agent 模板（TCP/WSS EXE、DLL、Linux ELF、Shellcode 等）已内置在控制端中，
通过 Web 界面 `/api/generate` 动态生成，无需额外部署。

---

## 快速开始

### Windows

```bat
c2_server.exe
```

### Linux

```bash
chmod +x c2_server_linux
./c2_server_linux
```

首次启动会自动生成 `config.yaml`（带注释的默认配置）与自签名 TLS 证书，
并拉起三个监听通道：

- **TCP 加密通道**（默认 `4444`）
- **WSS 加密通道**（默认 `8443`，可伪装 HTTPS）
- **Web 管理界面**（默认 `8445`）

浏览器访问 `http://<服务器IP>:8445` 即可登录控制台。

---

## 配置说明

所有参数同时支持：**命令行参数 > 环境变量 > config.yaml > 默认值**。

```bash
c2_server --help          # 查看全部可覆盖参数
c2_server -c my.yaml      # 指定配置文件
c2_server --web-port 9000 # 覆盖 Web 端口
c2_server --wss-auto-cert # 自动生成自签名证书
```

典型 `config.yaml`：

```yaml
auth:
  login_user: admin
  login_pass: <your-layer2-password>
  preauth_user: operator
  preauth_pass: <your-layer1-password>
server_host: <your-server-ip>      # Payload 默认回连地址
tcp_listener:
  port: 4444
web:
  host: 0.0.0.0
  https: false
  port: 8445
wss_listener:
  port: 8443
  auto_cert: true
auto_listeners:
- protocol: tcp
  port: 4444
- protocol: wss
  port: 8443
```

---

## 生成 Agent

登录 Web 控制台 → **GENERATE** → 填入服务器地址与端口 → 选择形态：

| 形态 | 说明 |
|------|------|
| TCP EXE | Windows 可执行程序，TCP 加密通道 |
| TCP DLL | Windows 动态库，`rundll32 <dll>,Start` 启动 |
| WSS EXE | Windows 可执行程序，WSS(HTTPS) 加密通道 |
| WSS DLL | Windows 动态库，WSS 通道 |
| ELF x86_64 | Linux 可执行程序 |
| Shellcode TCP / WSS | 无 PE 头的裸壳代码，可注入内存执行 |

生成后部署到目标主机运行，约 20~40 秒后上线（内置沙箱检测与延迟上线）。

---

## 默认口令

| 层级 | 用户 | 密码 |
|------|------|------|
| 第一层（企业伪装登录） | `operator` | `changeme` |
| 第二层（C2 控制台） | `admin` | `leekshell2026` |

> 生产环境请务必通过命令行参数或 config.yaml 修改以上默认口令。

---

## 免责声明

本软件仅供授权安全测试、教学研究使用，请勿用于任何非法用途。
使用者须自行承担使用本软件产生的全部法律责任。
