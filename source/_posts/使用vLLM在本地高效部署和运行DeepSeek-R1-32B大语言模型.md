---
title: 使用vLLM在本地高效部署和运行DeepSeek-R1-Distill-Qwen-32B大语言模型
date: 2025-01-31 18:48:25
tags:
---

# 使用vLLM在本地高效部署和运行DeepSeek-R1-Distill-Qwen-32B大语言模型

简介

本教程将指导您如何在本地环境中使用 vLLM 框架快速搭建并运行 DeepSeek-R1-32B 大语言模型。通过本教程，您可以实现以下目标：

* 安装必要的依赖环境

* 下载 DeepSeek-R1-32B 模型

* 配置 vLLM 环境

* 启动模型推理服务

* 进行基本的交互测试

---

前提条件

在开始之前，请确保您的环境满足以下要求：

1. 硬件要求：
   
   - CPU：支持 AVX2 指令集（大多数现代 CPU 都支持）
   - GPU：建议使用 NVIDIA 显卡（如 RTX 3090、A100 等），支持 CUDA 11.7 或更高版本
   - 内存：至少 64GB RAM（推荐 128GB 或以上）
   - 存储：至少 200GB 可用空间（用于存储模型文件）

2. 软件要求：
   
   - 操作系统：Linux（推荐 Ubuntu 22.04 或 macOS）
   - Python 版本：Python 3.8 或更高版本
   - CUDA 工具包：CUDA 11.7 或更高版本（仅限 GPU 加速）
   - Git：用于克隆代码仓库

---

步骤 1：安装依赖环境

1.1 安装 Python 和 pip

```bash
安装 Python 3.8+
sudo apt update && sudo apt install python3.8 python3.8-distutils python3-pip

验证安装
python3 --version
```

1.2 安装 CUDA 工具包（仅限 GPU 用户）

```bash
添加 CUDA 仓库
sudo apt-get update && sudo apt-get install -y wget
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-get update && sudo apt-get -y install cuda-11.7

验证安装
nvcc --version
```

1.3 安装其他依赖工具

```bash
安装基础依赖
sudo apt-get update && sudo apt-get install -y \
    build-essential \
    cmake \
    git \
    curl \
    unzip \
    aria2  # 用于加速下载大文件
```

---

步骤 2：下载 DeepSeek-R1-32B 模型

2.1 下载模型权重

DeepSeek-R1-32B 的模型权重较大（约 50GB），建议使用 `hfd` 或 `Hugging Face CLI` 进行下载。

# # 使用huggingface-cli安装

## 安装huggingface-cli

### 方法一：通过 pip 安装

```bash
pip install huggingface-cli
```

### 方法二：通过 conda 安装（推荐）

```bash
conda install -n base -c conda-forge huggingface-cli
```

### 验证安装

```bash
huggingface-cli --version
```

## 拉取模型

```bash
huggingface-cli download deepseek-ai/DeepSeek-R1-Distill-Qwen-32B
```



## 使用hfd下载（推荐）

### 下载安装hfd

```bash
apt install aria2c #hfd使用aria2下载模型，这条指令按照各种系统进行修改，或查阅百度/bing/aria2官方文档
wget https://hf-mirror.com/hfd/hfd.sh
chmod a+x hfd.sh
```

### 下载模型

```bash
./hfd.sh deepseek-ai/DeepSeek-R1-Distill-Qwen-32B
```

步骤 3：安装 vLLM 框架

3.1 克隆 vLLM 仓库

```bash
git clone https://github.com/vllm-project/vllm.git
cd vllm
```

3.2 安装依赖包

```bash
pip install -r requirements.txt
```

3.3 安装 vLLM

```bash
pip install .
```

---

步骤 4：配置模型推理环境

4. 1启动推理服务

```bash
vllm serve --model-path DeepSeek-R1-Distill-Qwen-32B --dtype float16 --num-workers 4 --listen localhost:8080
```

---

步骤 5：进行交互测试

5.1 使用命令行测试

```bash
curl -X POST http://localhost:8080/api/generate \
     -H "Content-Type: application/json" \
     -d '{
           "messages": [
             {"role": "user", "content": "你好！"}
         ]}'
```

5.2 使用 Python 脚本测试

创建一个 Python 文件 `test.py`：

```python
import requests

url = "http://localhost:8080/api/generate"
headers = {"Content-Type": "application/json"}

payload = {
    "messages": [
        {"role": "user", "content": "你好！"}
    ]
}

response = requests.post(url, headers=headers, json=payload)
print(response.json())
```

运行脚本：

```bash
python test.py
```

---

性能优化建议

5.1 使用量化技术

为了提高推理速度并减少显存占用，可以尝试使用量化技术。例如：

```bash
vllm serve --model-path DeepSeek-R1-Distill-Qwen-32B --quantization bitsandbytes-4bit --num-workers 4 --listen localhost:8080
```

5.2 调整工作线程数

根据您的 CPU 核心数调整 `--num-workers` 参数，以充分利用多核计算能力。

---

常见问题解答（FAQ）

Q1: 显存不足怎么办？

- 尝试降低批处理大小或使用更低精度（如 `int8` 或 `4bit` 量化）
- 确保模型路径正确，并且模型文件已正确解压

Q2: 下载模型速度太慢怎么办？

- 更换镜像源，或者使用网络加速器
- 尝试从镜像站点下载

Q3: 如何监控推理服务状态？

- 使用浏览器访问 `http://localhost:8080`
- 使用 `curl` 命令测试 API 响应

---

总结

通过本教程，您已经成功在本地环境中搭建并运行了 DeepSeek-R1-Distill-Qwen-32B 大语言模型。接下来，您可以根据实际需求进一步优化性能、扩展功能或集成到其他应用中。

如果需要更详细的文档或技术支持，请参考 或 。

祝您愉快地探索和使用大语言模型！
