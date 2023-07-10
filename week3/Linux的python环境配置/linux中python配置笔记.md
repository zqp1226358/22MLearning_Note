## Linux中python配置笔记

首先按照下面的笔记安装了anaconda  直接在home下

使用export PATH=/home/yourName/anaconda3/bin/:$PATH添加环境变量

[(182条消息) linux安装anaconda及配置pytorch环境_anaconda安装pytorch linux_Hydrion-Qlz的博客-CSDN博客](https://blog.csdn.net/qq_46311811/article/details/123524762)



在anaconda中创建了虚拟环境py38，python为3.8，cpu版本的pytorch

熟悉进入和退出的命令



其中遇到的一些问题：

- nvidia-smi  查看显卡的命令无效  感觉是没有安装相应的驱动
- 换源问题

```
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

```

使用了上面的源，conda确实快一点，但使用pip下载会慢一些，指定了源才快了很多，可能没有设置。

> pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.

[(182条消息) 解决pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool_禅心001的博客-CSDN博客](https://blog.csdn.net/woai8339/article/details/91351707)

pip 和 pip3的区别

- wsl2 vscode xhr fail 在vscode中**下载扩展失败**的问题

解决方案：设置自动更新时区

[(182条消息) vscode现在无法连接至扩展商店xhr failed_VoiceU的博客-CSDN博客](https://blog.csdn.net/Voiceu/article/details/114285691)

很玄学的感觉

> 另外提一点 在wsl2 中输入code . 启动了vscode  之前考虑在vscode连接wsl2  好像有点不大行  

- 在vscode使用jupyter  

要安装ipykernel  在vscode选对内核  成功运行