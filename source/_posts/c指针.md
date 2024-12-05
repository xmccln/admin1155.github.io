---
title: c指针笔记
date: 2024-11-28 13:00:56
tags: ['c','指针']
---



# 文件指针读写

## 打开文件

```c
FILE = fopen(file_path);
```

* 如果未能打开则FILE将会是NULL

## 文件内容读取

  

## 文件是否读取完成的判断

  ```c
  feof(FILE)
  ```

  * 文件读完则返回0
  * 文件未读完则返回1

# 一些轮子

* 使用指针转化a,b的位置

```c
void swap(int *a,int *b){
    int temp;
    temp = *a;
    *a = *b;
    *b = *a;
}
```

* 判断文件是否成功打开

  ```c
   if ((fp = fopen("/home/xmccln/c/class/data1.txt", "rw")) == NULL) 
  ```

* 判断是否为瑞年

  ```c
  int IslEAP(int years){
    if(years%400 !=0 || (years%100 !=0 && years%4 == 0)){
      return 0;}
      return 1;
  }
  ```

  