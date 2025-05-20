
# 皮肤URL链接使用指南

 SkinsRestorer插件支持通过图片URL链接加载自定义皮肤，这种方式可以直接使用网络图片资源而非其他玩家的皮肤数据。

 ## 皮肤有效性验证
 请确保链接直接指向有效的PNG格式皮肤文件。 若使用Imgur图床，链接必须以`.png`结尾。 有效皮肤链接示例：
```
 https://i.imgur.com/QuoWt6B.png
 ```
*注意：常见错误是复制了网页地址而非图片直链*

 参考示意图：

![有效皮肤格式示意图](http://pan.nmccl.cn.eu.org:5244/d/ali/pico/valid-format.png)


 ## Imgur上传教程
 ### 第一步：准备皮肤文件
 1. 获取`.png`格式的皮肤文件（可自建或下载现成素材）
 2. 推荐使用[官方皮肤设计指南](https://skinsrestorer.net/ )进行创作

 文件存储示例：
![皮肤文件存放示意图](http://pan.nmccl.cn.eu.org:5244/d/ali/pico/download-folder.png)

 ### 第二步：访问上传页面
 1. 打开 [Imgur上传页面](https://imgur.com/upload )
 2. 拖拽或选择本地皮肤文件上传

 上传界面示例：
![文件上传操作示意图](http://pan.nmccl.cn.eu.org:5244/d/ali/pico/upload-image.png)

 ### 第三步：获取直链地址
 1. 皮肤链接必须以`.png`结尾
 2. 右击已上传的图片选择「复制图像地址」
 3. 正确格式示例：`[https://i.imgur.com/abcdefgh.png ](https://i.imgur.com/abcdefgh.png )`

 链接获取示例：
![直链复制示意图](http://pan.nmccl.cn.eu.org:5244/d/ali/pico/copy-link.png)

 ## 应用皮肤指令
完成上传后，在游戏内执行：
 ```
/skin url "<复制的URL地址>"
 ```
*注意：必须使用英文双引号包裹链接*

 完成！现在即可通过图片链接使用自定义皮肤。