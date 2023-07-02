## git的学习笔记

### 一、免密登录工具--SSH连接

1. 检查是否已经有SSH key （如果有，跳过这一步）

```bash
cd ~/.ssh
ls
```

	检查是否已经存在 id_rsa.pub 或 id_dsa.pub 文件，如果是第一次创建还会生成known_hosts文件，如果后续有所变动，则需要**修改**或删除该文件。

如果不是第一次使用，已经存在 id_rsa.pub 或 id_dsa.pub 文件。请执行下面的操作，清理原有 ssh 密钥。

```text
$ mkdir key_backup   
$ cp id_rsa* key_backup   
$ rm id_rsa*
```

2. 创建新的SSH key

```bash
ssh-keygen -t rsa -C "your_email@example.com"
```

-C 设置注释文字  -t指定密钥类型

创建过程提示输入两次密码，直接按回车

最后会有图案显示

3. 添加SSH key 到 github

拷贝 id_rsa.pub 文件的内容，在github的设置那一栏找到ssh选项，进行粘贴创建。

4. 验证是否成功

```text
ssh -T git@github.com
```

> 参考资料:
>
> [在github实现免密登录 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/481811078#:~:text=在 github 上添加 SSH key实现免密登录 ： 1 1、检查是否已经有,... 4 4、验证是否配置成功 ssh -T git%40github.com 成功的话如下所示 )
>
> 