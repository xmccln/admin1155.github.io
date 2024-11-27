---
title: alist文件上传_cpp
date: 2024-11-27 08:45:18
tags:["cpp",'轮子','alist','文件操作']
---

# alist文件上传_stream方式

参数介绍

* file_path **本地文件地址**
* token **alist的token地址**
* upload_path **上传到alist网盘的位置，需要带上文件名**
* alist_host **alist的host位置**

```cpp
int upload(const string& file_path, const string& token,string upload_path,const string& alist_host ) {
    

    httplib::Client cli(alist_host);
    //构造请求头
    httplib::Headers headers = {
        {"Authorization", token},
        {"File-Path", upload_path},
        {"As-Task", "true"},
        {"Content-Type", "application/octet-stream"}
    };

    // 读取文件内容到body
    ifstream file(file_path, ios::binary);
    if (!file) {
        cerr << "无法打开文件: " << file_path << endl;
        return 1;
    }

    string body((istreambuf_iterator<char>(file)), istreambuf_iterator<char>());

    headers.insert({"Content-Length", to_string(body.size())});

    auto res = cli.Put("/api/fs/put", headers, body, "application/octet-stream");
    // 解析相应
    if (res) {
        cout << "状态码: " << res->status << endl;
        cout << "响应内容: " << res->body << endl;
    } else {
        cerr << "上传失败，未收到响应。" << endl;
    }

    return 0;
}
```

