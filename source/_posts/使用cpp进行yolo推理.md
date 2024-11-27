---
title: 使用cpp进行yolo推理
date: 2024-11-19 19:04:04
tags:
---
# 前置条件
* 已经安装并配置好opencv
* 具有一定c++知识

# 配置编译环境
## 下载 inference.cpp / inference.h  
这两个文件可通过 yolo官方的github地址进行下载 就不进行过多赘述了
## 修改编译指令
由于编译需要将main.cpp和inference.cpp和为一个可执行文件所以需要在编译指令的 **-g**后方添加上inference.cpp地址。

# 编辑main.cpp

## 引入头文件
```cpp
//cpp标准库
#include <iostream>
#include <vector>
#include <getopt.h>
//opencv库
#include <opencv2/opencv.hpp>

// yolo提供的推断头文件
#include "inference.h"
```
