# 成功使用VScode连接研究室服务器过程记录

时间：2020-02-06

版本信息：本机WIN10家庭版1909；VSC1.41.1，目标服务器是UBUNTU18.04.03LTS(使用`lsb_release -a`查看)

插件信息：`Remote Development`

------

步骤如下：

1. 先确保WIN10的openSSH功能开启

2. 打开powershell输入命令ssh-keygen生成本机对应的公钥和密钥，命令提示默认回车即可

3. 通过xshell建立ssh连接后输入`vi ~/.ssh/authorized_keys`准备输入公钥信息

4. 本机打开刚才新建的公钥存储文件，后面是`id_rsa.pub`，用记事本打开，复制全部粘贴到xshell打开的`authorized_keys`中，用`wq`保存关闭

5. 设置服务器允许基于密钥认证的方式登录（需要超级用户权限），输入`sudo vim /etc/ssh/sshd_config`，用`/Pub`快速定位，修改其中的`PubkeyAuthentication`为`yes`，我的情况是前面有个#，删掉它使之成为正文而不是批注

6. 打开VSC，安装`Remote Development`插件，重启后左侧工具栏最下方出现远程电脑图标，点击它，顶部远程资源管理器旁边下拉选中`SSH Targets`，点击下面一栏`SSH TARGETS`的添加按钮，弹出输入ssh命令的悬浮窗，输入常规的ssh命令，回车后选择更新第一个`\config`用户配置文件，回车

7. 此时右下角会提示添加内容到了config文件中，打开查看内容，适当补充，最后应该是这个样子的:

```    
Host 服务器ip

  HostName 服务器ip

  User 用户名

  Port 端口

  ForwardAgent yes
```

8. 保存后重启VSC，左下角出现`SSH:服务器IP`表示可以使用了，点击`文件`-`打开文件夹`选择服务器上的文件夹使用

----

主要参考：

1. <https://zhuanlan.zhihu.com/p/86637316>

2. <https://zhuanlan.zhihu.com/p/76562181>

3. <https://blog.csdn.net/whbing1471/article/details/52074390>
