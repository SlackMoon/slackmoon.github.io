[Windows_and_AD Fundamentals.md](https://github.com/user-attachments/files/27369984/Windows_and_AD.Fundamentals.md)
# Windows 与 Active Directory 基础

课程：Cyber Security 101  
模块：Module 3 Windows and AD Fundamentals

---

# 模块概览

本笔记主要包含：

- Windows MMC 管理控制台
- 常见 `.msc` 管理工具
- Active Directory 基础
- 组策略管理
- Living Off The Land（LOLBAS）技术
- PowerShell 域管理命令

---

# Microsoft Management Console（MMC）

Windows 中大量管理工具都以：

```powershell
*.msc
```

形式存在。

这些文件本质上是：

# Microsoft 管理控制台（MMC）组件

通常通过：

```powershell
Win + R
```

输入：

```powershell
dsa.msc
```

或：

```powershell
gpmc.msc
```

进行启动。

---

# 枚举系统中的 MSC 管理工具

列出系统中的所有 `.msc` 文件：

```powershell
dir C:\Windows\System32\*.msc
```

作用：

- 枚举当前系统存在的管理控制台
- 识别系统可用管理组件
- 安全排查时识别管理工具

---

# 常见 Windows 管理控制台

---

## Computer Management

启动：

```powershell
compmgmt.msc
```

作用：

- 打开“计算机管理”
- 集成多个 Windows 管理模块

常用组件：

---

## Event Viewer（事件查看器）

启动：

```powershell
eventvwr.msc
```

作用：

- 查看 Windows 日志
- 安全事件分析
- Sysmon 日志分析
- 蓝队排查
- 威胁狩猎

重点日志位置：

- Windows Logs
- Security
- System
- Application

蓝队重点：

- 登录日志
- 权限提升
- PowerShell 执行
- Sysmon 告警

---

## Task Scheduler（任务计划程序）

启动：

```powershell
taskschd.msc
```

作用：

- 查看计划任务
- 创建自动化任务
- 排查持久化
- 分析恶意任务

安全场景：

- 木马持久化
- 定时恶意脚本
- LOLBin 调用链
- 横向移动后的持久化

蓝队重点：

- 可疑计划任务
- 隐藏任务
- PowerShell 定时执行

---

# Group Policy（组策略）

---

## 本地组策略编辑器

启动：

```powershell
gpedit.msc
```

作用：

- 管理本地组策略
- Windows 安全加固
- 系统行为配置

常见配置：

- USB 禁用
- PowerShell 限制
- Windows Defender 配置
- 用户权限控制

---

## 本地安全策略

启动：

```powershell
secpol.msc
```

作用：

- 管理本地安全策略
- 配置审计
- 配置密码策略
- 配置权限

重点内容：

- 密码复杂度
- 账户锁定策略
- 登录审计
- 用户权限分配

---

# Living Off The Land（LOLBAS）

[官方项目](https://lolbas-project.github.io/)

---

## 什么是 Living Off The Land


> [!NOTE] Living Off The Land
> 攻击者利用Windows 自带合法程序完成攻击行为，这些程序被称为LOLBin（Living Off The Land Binary）

---

## 为什么攻击者喜欢 LOLBin

优势：

- 不需要上传恶意程序
- 更容易绕过杀毒软件
- 更容易绕过 EDR
- 更像正常管理员行为

---

## 常见 LOLBin

| 程序 | 作用 |
|---|---|
| powershell.exe | 执行脚本 |
| certutil.exe | 下载文件 / 编码 |
| mshta.exe | 执行 HTA |
| rundll32.exe | 执行 DLL |
| regsvr32.exe | 执行脚本 |
| schtasks.exe | 创建计划任务 |
| wmic.exe | 远程管理 |

---

## 蓝队重点监控

重点关注：

- 异常 PowerShell
- LOLBin 网络连接
- 可疑父子进程
- Sysmon Event ID 1
- 编码下载行为
- 计划任务创建

---

# Active Directory 基础

---

## Active Directory Users and Computers

启动：

```powershell
dsa.msc
```

作用：

- 打开 AD 用户和计算机
- 管理域用户
- 管理计算机
- 管理 OU
- 管理安全组

常见操作：

- 创建用户
- 禁用用户
- 重置密码
- 管理计算机对象
- 权限委派

---

## Organizational Units（OU）

OU：

# 组织单位

作用：

- 分类管理用户和计算机
- 应用组策略
- 权限隔离

示例结构：

```text
corp.local
├── Servers
├── Workstations
├── IT
└── HR
```

---

## Security Groups（安全组）

安全组用于：

- 权限控制
- 访问控制
- 管理用户权限

常见安全组：

| 组名 | 作用 |
|---|---|
| Domain Admins | 域管理员 |
| Enterprise Admins | 企业管理员 |
| Remote Desktop Users | RDP 登录 |
| Backup Operators | 备份权限 |

---

## Group Policy Management

启动：

```powershell
gpmc.msc
```

作用：

- 打开组策略管理控制台
- 管理域 GPO
- 链接组策略
- 配置安全策略

常见用途：

- 密码策略
- RDP 限制
- Defender 配置
- 审计策略
- PowerShell 日志

---

## Active Directory 密码管理

---

### 重置用户密码

命令：

```powershell
Set-ADAccountPassword alice -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password')
```

作用：

- 重置用户 `alice` 的密码
- 安全输入新密码

---

### 强制用户下次登录修改密码

命令：

```powershell
Set-ADUser -Identity alice -ChangePasswordAtLogon $true
```

作用：

- 用户下次登录必须修改密码

---

## 蓝队安全关注点

重点监控：

- 非授权密码重置
- 域管理员组变更
- 异常 GPO 修改
- 可疑计划任务
- LOLBin 滥用
- PowerShell 横向移动

重点日志：

| 日志 | 含义 |
|---|---|
| Event ID 4624 | 登录事件 |
| Event ID 4724 | 密码重置 |
| Event ID 4732 | 用户加入高权限组 |
| Sysmon Event ID 1 | 进程创建 |

---
## 重点总结

- `.msc` 是 Windows 管理控制台
- `dsa.msc` 用于管理 Active Directory
- `gpmc.msc` 用于管理组策略
- LOLBin 是攻击者常用合法程序
- PowerShell 可直接管理 AD
- 蓝队需要重点监控管理行为与策略变更

---
