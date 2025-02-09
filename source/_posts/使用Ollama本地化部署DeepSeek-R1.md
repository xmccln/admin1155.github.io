---
title: 使用Ollama本地化部署DeepSeek-R1
date: 2025-02-09 16:48:53
tags:
---

# 使用Ollama本地化部署DeepSeek-R1

Ollama是一个开源的本地化大模型部署工具，旨在简化大型语言模型（LLM）的安装、运行和管理。它支持多种模型架构，并提供与OpenAI兼容的API接口，帮助开发者和企业快速搭建私有化AI服务。

### 核心特点：

- **轻量化部署**：支持在本地设备上运行模型，无需依赖云端服务
- **多模型支持**：兼容LLaMA、DeepSeek等多种开源模型
- **高效管理**：提供命令行工具，方便下载、加载和切换模型
- **跨平台支持**：支持Windows、macOS和Linux系统

![Ollama界面](https://picx.zhimg.com/v2-63ade8da26a11da59b9b892ca03913eb_1440w.jpg)

---

## 2. DeepSeek-R1简介

DeepSeek-R1是由深度求索（DeepSeek）公司开发的高性能AI推理模型，专注于数学、代码和自然语言推理任务。

### 核心优势：

- **强化学习驱动**：通过强化学习技术显著提升推理能力，仅需少量标注数据即可高效训练
- **长链推理（CoT）**：支持多步骤逻辑推理，能够逐步分解复杂问题并解决
- **模型蒸馏**：支持将推理能力迁移到更小型的模型中，适合资源有限的场景
- **开源生态**：遵循MIT开源协议，允许用户自由使用、修改和商用

DeepSeek-R1在多个基准测试中表现优异，性能对标OpenAI的o1正式版，同时具有更高的性价比。

![DeepSeekR1模型](https://pic1.zhimg.com/v2-8fdb5a2c9a3ab07abe8e49c65afaa520_1440w.jpg)

---

## 3. 使用Ollama部署DeepSeek-R1

### 3.1 安装Ollama

**下载Ollama**：

- 官网：[https://ollama.com/](https://ollama.com/)
- Github：https://github.com/ollama/ollama

**安装与验证**：
在终端中运行以下命令验证安装：

```bash
ollama --version
```

成功输出示例：

```
admin@Mac-miniM4 ~ % ollama --version
ollama version is 0.5.7
```

---

### 3.2 下载DeepSeek-R1模型

**模型获取**：
Ollama已支持DeepSeek-R1，模型地址：[deepseek-r1](https://ollama.com/library/deepseek-r1)。

**下载模型**：
根据显存选择合适的模型版本（如macmini m4 16G可流畅支持7B），运行以下命令下载模型：

```bash
ollama pull deepseek-r1:1.5b
```

**运行模型**：
启动DeepSeek-R1模型：

```bash
ollama run deepseek-r1:1.5b
```

成功运行后，终端将进入交互式终端（REPL），可以输入问题进行测试。

示例对话：

```
>>> 你好，介绍一下你自己
您好！我是由中国的深度求索（DeepSeek）公司开发的智能助手DeepSeek-R1。如您有任何任何问题，我会尽我所能为您提供帮助。
```

---

## 4. 部署Open-WebUI增强交互体验

通过Open-WebUI与Ollama结合，可以显著提升交互体验。Open-WebUI支持多种功能，包括文档知识库问答、对话流管理等复杂需求。

### 4.1 下载Open-WebUI

使用Docker部署Open-WebUI：

```bash
docker pull ghcr.io/open-webui/open-webui:main
```

### 4.2 启动Open-WebUI

```bash
mkdir /Users/admin/program/docker/instance/open-webui/data
cd /Users/admin/program/docker/instance/open-webui
docker run -d -p 3000:8080 -v $PWD/data:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
```

启动完成后，通过浏览器访问Open-WebUI：[http://localhost:3000](http://localhost:3000)

### 4.3 配置Ollama地址

进入Open-WebUI设置页面：

1. 点击右上角的设置图标
2. 进入“模型”选项卡
3. 点击“添加模型”，选择“Ollama”
4. 输入Ollama地址（默认为[http://localhost:11434）](http://localhost:11434%EF%BC%89)

### 4.4 测试功能

在Open-WebUI中，可以体验以下功能：

- **智能客服**：输入“如何安装Ollama？”
- **内容创作**：输入“为DeepSeek写一篇入门指南”
- **编程辅助**：输入“用Java实现快速排序”
- **教育辅助**：输入“解释牛顿第二定律”

![OpenWebUI界面](https://pic2.zhimg.com/v2-5a4e2ce67d21685532c3a53ba9a647ef_1440w.jpg)

---

## 总结

通过Ollama部署DeepSeek-R1，并结合Open-WebUI进行交互，用户可以快速搭建本地化AI服务，享受高性能模型带来的便捷体验。无论是开发测试还是企业应用，这种本地化部署方案都提供了高性价比的选择。

部分引用[使用Ollama本地化部署DeepSeek - 知乎](https://zhuanlan.zhihu.com/p/20924220892)
