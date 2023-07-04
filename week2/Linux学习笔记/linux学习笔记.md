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