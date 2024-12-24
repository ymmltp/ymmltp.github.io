---
title: python
date: 2023-08-24 15:56:10
tags: 学无止境
---

# Python

## 模块

### 打包工具

`cx_Freeze` ：[cx_Freeze使用方法](https://www.diaoyc.cn/archives/python%E4%BD%BF%E7%94%A8cxfreeze%E6%89%93%E5%8C%85fastapi%E9%A1%B9%E7%9B%AE%E7%9A%84%E6%96%B9%E6%B3%95%E4%BB%A5%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98#post-content)
`pyinstaller`：[pyinstaller打包讲解](https://blog.csdn.net/qq_39621009/article/details/122308590)

```python
 pyinstaller --hidden-import -F tmp.py
```

### 环境搭建

```python
## 新建环境
python.exe -m venv yolo_env  (yolo_env所在路径是当前路径,而不是使用的python.exe的路径)
## 启动
yolo_env\Scripts\activate 

## 创建Jupyter环境
## 使用绝对路径的python.exe
C:\Users\1382919\AppData\Local\Programs\Python\Python310\yolo_env\Scripts\python.exe -m ipykernel install --user --name=yolo_env --display-name "Python 3.10 (yolo_env)"
```

### cmd运行Python脚本

```
.\Scripts\python.exe filepath
```

### 各镜像网站

[清华](https://pypi.tuna.tsinghua.edu.cn/simple)
[阿里云](https://mirrors.aliyun.com/pypi/simple/)
[中国科技大学](http://pypi.mirrors.ustc.edu.cn/simple/)
