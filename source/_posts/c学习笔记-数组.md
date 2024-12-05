---
title: c学习笔记-数组
date: 2024-12-05 12:50:32
tags: []
---

# 一维数组的定义

## 定义方法

```c
变量类型 变量名[长度] 
```

## 存储结构

* 对应数组的连续空间，每一个单元因数据类型相同而大小相同

  ```c
  int a[10]
  ```



## 一维数组的初始化

* 定义数组时，对数组赋初始值

```c
int a[10] = {1,2,3,4,5,6,7,8,9,10}
```

* 静态数组的初始化

```c
static int b[5];
static int c[5] = {1.2.3.4.5};
```

* 动态数组的初始化

```c
auto int c[5];
```

* 如果对所有元素赋值数组长度可以省略

```c
int a[ ] = {1,2,3,4,5,6};
```

# 二维数组

```c
变量名[行下标][列下标]
```



# 一些轮子

* 冒泡排序

```c
int a[100],n = 0,temp,swapon = 1 ;
    FILE *fp;
    fp = fopen("/root/c/1.txt","r");
    while(fscanf(fp,"%d",&a[n++]) != EOF);//当fscanf函数读取到超出文本的数据则会返回EOF
    n--;//bugs 到最后会读取到EOF所以n自减以修复索引
    /** 冒泡排序优化版
    相比于传统冒泡排序时间复杂度大大降低，提高了效率（O(n-1)）
    */
    while(swapon){
        swapon = 0;//重置判断
        for(int i = 0 ; i<n;i++){
            if(a[n]>a[n+1]){
                temp = a[n];
                a[n] = a[n+1];
                swapon = 1;//如果有冒泡交换则修改swap
            };
        };
    };
    for(int i = 0 ; i< n;i++) printf("%d ",a[i]);
    fclose(fp); 
    
```



* 选择排序

```c
   // std::cout << "Hello, from poj!\n";
    int a[100],n = 0,temp,index=0 ;
    FILE *fp;
    fp = fopen("/root/c/1.txt","r");
    while(fscanf(fp,"%d",&a[n++]) != EOF);//当fscanf函数读取到超出文本的数据则会返回EOF
    n--;//bugs 到最后会读取到EOF所以n自减以修复索引
    /**选择排序 */
    for(int i = 0 ; i<n-1;i++){
        index = i;
        for(int j=i+1;j<n;j++ ){
            if(a[index] < a[j]) index = j;
        };
        if(index != i){
            temp = a[index];
            a[index] = a[i];
            a[i] = temp;
        };
    }
    for(int i = 0 ; i< n;i++) printf("%d ",a[i]);
    fclose(fp); 
```

