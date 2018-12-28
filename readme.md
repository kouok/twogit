# Git配置多个SSH-Key

现在我电脑想要两个git账号，一个是github的，一个是gitee的，那么不管之前是否是安装了任一个，都需要按照以下步骤进行：

### 背景

当有多个git账号时，比如：

a. 一个gitee，用于公司内部的工作开发；
b. 一个github，用于自己进行一些开发活动；

### 解决方法
1. 生成一个公司用的SSH-Key

`$ ssh-keygen -t rsa -C 'xxxxx@company.com' -f ~/.ssh/gitee_id_rsa`

2. 生成一个github用的SSH-Key

`$ ssh-keygen -t rsa -C 'xxxxx@qq.com' -f ~/.ssh/github_id_rsa`

在 ~/.ssh 目录下新建一个config文件，添加如下内容（其中Host和HostName填写git服务器的域名，IdentityFile指定私钥的路径）
```
# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitee_id_rsa
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_id_rsa
```

4. 用ssh命令分别测试（最好在ssh目录下测试）

目录一般为`C:\Users\KOUOK\.ssh`

```
$ ssh -T git@gitee.com
$ ssh -T git@github.com
```
成功的话会返回如下内容:

`Hi kouok! You've successfully authenticated, but GitHub does not provide shell access.`

5. 假设没有成功，而是报如下错误，那是因为没有在github和gitee中添加ssh keys

`Permission denied (publickey).` 

6. 则需要在github和gitee的设置中添加ssh  keys

github中添加：找到`github_id_rsa.pub`打开，复制里面的所有代码到github的ssh keys中

gitee中添加：找到`gitee_id_rsa.pub`打开，复制里面的所有代码到gitee的ssh keys中

然后再测试！

### 如何分别提交到不同的远程服务器中（指定提交到github还是gitee）

1. 场景1-线上到线下：已经从线上clone到了线下，那么就已经将本地与线上进行了关联，这时可以直接像平常那样提交
2. 场景2-线下到线上：也就是在本地创建文件夹，然后新增文件再推送到服务器，步骤同github之前的，如下：

```
a、在本地新建一个文件夹，命名为项目名字（注意：不要项目中嵌套项目）
b、`git init` 初始化本地文件夹为一个github项目库
c、`git add .` 新增
d、`git commit -m "注释"`  提交到暂存区
e、接下来就是将本地的与线上的库进行关联：所以到线上去新建一个一模一样名字的远程库
f、`git remote add origin 远程库地址`：比如`git remote add origin https://github.com/kouok/web14-gitbash.git`
将本地的与线上的进行管理
g、`git push -u origin master`  将线下的同步到线上去。
f。后面的增删改查等操作全部都与第一个场景一样了。
```