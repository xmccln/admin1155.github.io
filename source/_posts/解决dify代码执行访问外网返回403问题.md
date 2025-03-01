---
title: 解决dify代码执行访问外网返回403问题
date: 2025-03-01 15:19:15
tags:
  - 技术分享
---


## 解决dify代码执行访问外网返回403问题
![](https://pan.nmccl.cn.eu.org:5245/d/ali/pico/屏幕截图 2025-03-01 152342.png)


### 问题背景
在本地开发环境中能够正常运行的代码执行器，当部署到Dify平台时突然出现外网83端口访问失败的情况。通过Dify的架构日志追踪，我们发现核心问题出在平台的安全防护机制上。

```bash
# 查看SSRF代理容器日志
docker logs -f docker-ssrf_proxy-1
```

![](https://pan.nmccl.cn.eu.org:5245/d/ali/pico/屏幕截图 2025-03-01 152557.png)

### 技术原理分析
根据Dify官方文档，代码执行器(Sandbox)的网络流量默认会经过SSRF代理（Server-Side Request Forgery Proxy）。该代理基于Squid实现，通过预定义的安全规则防止潜在的SSRF攻击：

1. 默认仅放行80/443等标准端口
2. 采用白名单机制过滤非常规端口
3. 对非常规端口请求返回403状态码

这种安全策略导致本地调试时直连网络可用的83端口，在Dify环境中被代理层主动拦截。

### 解决方案实施
通过分析Squid配置文件，我们定位到代理规则定义文件：

`docker/ssrf_proxy/squid.conf.template`

```squid
# 原始安全规则配置
acl SSL_ports port 443
acl Safe_ports port 80      # http
acl Safe_ports port 443     # https
```

![](https://pan.nmccl.cn.eu.org:5245/d/ali/pico/屏幕截图 2025-03-01 153245.png)

新增83端口白名单规则：

```squid
acl SSL_ports port 83
acl Safe_ports port 83
```

> **配置说明**：同时添加至SSL_ports和Safe_ports可兼容HTTP/HTTPS场景

### 验证与生效
1. 重建SSRF代理容器
```bash
docker-compose up -d --build ssrf_proxy
```
1. 执行端口连通性测试
```python
import requests
response = requests.get("http://external-service:83")
assert response.status_code == 200
```

### 安全实践建议
1. 最小化开放原则：仅添加业务必需的端口
2. 环境隔离：生产环境建议通过环境变量管理白名单
3. 监控审计：开启Squid访问日志定期审查
```bash
tail -f /var/log/squid/access.log
```

### 技术总结
Dify通过SSRF代理构建了有效的网络安全边界，开发者需理解其白名单机制的工作原理。在遇到非常规端口访问需求时，应当：

1. 优先考虑使用标准端口
2. 必须开放非常规端口时，采用精准的ACL控制
3. 结合业务场景评估安全风险

该解决方案已通过Dify v0.3.5环境验证，适用于需要访问非标端口的AI应用开发场景。建议开发者在修改生产环境配置前，在测试环境充分验证网络策略变更的影响。