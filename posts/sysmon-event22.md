# Sysmon Event ID 22 分析

## 事件描述

检测到 DNS Query：

```text
bxss.me
```

## 研判过程

1. 检查 Sysmon 配置
2. 分析 DNS 请求
3. 检查 Clash 流量

## 结论

属于正常代理行为触发的误报。
