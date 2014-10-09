## 简介 ##

在windows上安装docker时，一般到[https://github.com/boot2docker/windows-installer/releases](https://github.com/boot2docker/windows-installer/releases "")下载boot2docker.exe安装程序，但其自带的iso有以下局限：

1. boot2docker-vm 无法通过virtualbox和windows共享文件夹
2. 无法使用更多docker工具，比如fig等
3. boot2docker-vm启动后，不是中国大陆时区

而这个image将解决这些问题。

## 制作iso ##

`git clone` 后，请在当期目录下执行以下指令:

    # docker built -t qiankunli/boot2docker .
    # docker run --rm qiankunli/boot2docker > boot2docker.iso
    
然后，关闭boot2docker-vm，用生成的boot2docker.iso替换掉`<home dir>/.boot2docker`目录下的`boot2docker.iso`即可