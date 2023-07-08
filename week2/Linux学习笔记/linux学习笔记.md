## Linux安装

参考文章：

[Windows10/11 三步安装wsl2 Ubuntu20.04（任意盘） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/466001838)

https://www.bilibili.com/read/cv8144655





其中遇到的错误：

WslRegisterDistribution failed with error: 0x80370102 Error: 0x80370102 ????

解决方案：

https://blog.csdn.net/weixin_45930223/article/details/128955798

管理员方式启动 powershell，并运行：

- bcdedit /enum | findstr -i hypervisorlaunchtype
  如果此处看到hypervisorlaunchtype Off，则输入

- bcdedit /set hypervisorlaunchtype Auto

回想起本科期间操作系统课设时安装的hls，也是类似错误，与电信宽带Neetkeeper有冲突。



最后解决完报错，成功在D盘上安装了Linux系统





### Linux 学习笔记

如果提示符的最后一个字符是“#”, 而不是“$”, 那么这个终端会话就有超级用户权限。

我们需要学习的第一件事（除了打字之外）是如何在 Linux 文件系统中跳转。 在这一章节中，我们将介绍以下命令：

> - pwd — 打印出当前工作目录名
> - cd — 更改目录
> - ls — 列出目录内容

> - cp — 复制文件和目录
> - mv — 移动/重命名文件和目录
> - mkdir — 创建目录
> - rm — 删除文件和目录
> - ln — 创建硬链接和符号链接

这五个命令属于最常使用的 Linux 命令之列。它们用来操作文件和目录。



 I/O 重定向。”I/O”代表输入/输出， 通过这个工具，你可以重定向命令的输入输出，命令的输入来自文件，而输出也存到文件。 也可以把多个命令连接起来组成一个强大的命令管道。为了炫耀这个工具，我们将叙述 以下命令：

> - cat － 连接文件
> - sort － 排序文本行
> - uniq － 报道或省略重复行
> - grep － 打印匹配行
> - wc － 打印文件中换行符，字，和字节个数
> - head － 输出文件第一部分
> - tail - 输出文件最后一部分



其他命令详见文档

[第二十四章：编译程序 · The Linux Command Line 中文版 · 看云 (kancloud.cn)](https://www.kancloud.cn/thinkphp/linux-command-line/39455)

