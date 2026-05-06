
---
# 常用命令记录
---
## 1.查看系统相关
**查看当前系统中的所有环境变量:**
```powershell
C:\Users\YANG>set
ALLUSERSPROFILE=C:\ProgramData
APPDATA=C:\Users\YANG\AppData\Roaming
CATALINA_HOME=E:\Security\Web\Java\Tomcat\apache-tomcat-10.1.47
CLASSPATH=.;E:\Security\Web\Java\Tomcat\apache-tomcat-10.1.47\lib\servlet-api.jar
......
```
**确定当前操作系统版本：**
```powershell
C:\Users\YANG>ver
Microsoft Windows [版本 10.0.26200.7840]
```
**查看完整系统信息:**
```powershell
C:\Users\YANG>systeminfo
主机名:             DANYUE
OS 名称:            Microsoft Windows 11 专业版
OS 版本:            10.0.26200 暂缺 Build 26200
OS 制造商:          Microsoft Corporation
OS 配置:            独立工作站
OS 构建类型:        Multiprocessor Free
......
```
---
## 2.网络相关命令
**查看本机网络接口的基础 IP 配置:**
```powershell
ipoconfig
```
**查看本机全部网络详细信息，包括 MAC、DNS、DHCP 等配置:**
```powershell
ipconfig /all
```
**测试本机与目标主机之间的网络连通性与延迟:**
```powershell
ping target_name
```
**追踪数据包到目标主机经过的网络路径:**
```powershell
tracert target_name
```
**使用指定 DNS 服务器解析域名对应的 IP 地址:**
```powershell
nslookup example.com 1.1.1.1
```
**查看 netstat 命令的帮助信息与参数说明。**
```powershell
netstat -h
```
**查看当前所有网络连接、监听端口及对应进程和程序:**
```powershell
netstat -anob
```
---
## 3.文件和磁盘管理命令
**查看当前目录中的文件和文件夹:**
```powershell
dir
```

**显示当前目录中的全部文件，包括隐藏文件:**
```powershell
dir /a
```

**递归显示当前目录及所有子目录中的文件:**
```powershell
dir /s
```

**以树状结构显示当前目录层级:**
```powershell
tree
```

**切换到指定目录:**
```powershell
cd target_directory
```

**返回上一级目录:**
```powershell
cd ..
```

**创建新的目录:**
```powershell
mkdir directory_name
```

**删除指定空目录:**
```powershell
rmdir directory_name
```

**查看文本文件内容:**
```powershell
type target_file
```

**复制文件并生成新文件:**
```powershell
copy fileA fileB
```

**移动文件到指定目录:**
```powershell
move fileA Path
```

**删除指定文件:**
```powershell
del
```

**删除文件，作用与 del 相同:**
```powershell
erase
```
---
## 4.任务和进程管理

**查看当前系统正在运行的全部进程:**
```powershell
tasklist
```

**查看tasklist命令帮助:**
```powershell
tasklist /?
```

**过滤显示指定名称的进程:**
```powershell
tasklist /FI "imagename eq sshd.exe"
```

**根据进程 PID 强制结束指定进程:**
```powershell
taskkill /PID target_pid
```
---