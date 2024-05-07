#  1. DiskGenius 磁盘管理工具



## 1. 对将C扩容



1. 右键C盘 选择扩容分区

![image-20240505175507097](assets/image-20240505175507097.png)





2. 选择将哪个盘的容量扩容到C盘，这边选择D盘

![image-20240505175554263](assets/image-20240505175554263.png)





3. 选择好需要扩容多大的空间给到C盘

![image-20240505175714298](assets/image-20240505175714298.png)



4. 等待关机重启后自动完成扩容





# 2. python 将 .py 文件打包成exe



1. 使用 pip命令安装   pyinstaller    

```shell
pip install pyinstaller
```

2. 将对应的 .py 文件打包成 exe   【这样构建会不仅有exe 文件 还会有一个 _internal  目录】

```shell
pyinstall your_script.py 
```

打包完成后会在同级目录下生成一个 dist 目录 ，构造的exe就在里面



使用这个命令构建的 exe 文件 将是只有一个exe 不会有 _internal 目录

```shell
pyinstall --onefile your_script.py 
简写 pyinstall -F your_script.py
```



