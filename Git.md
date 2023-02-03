# Git基本操作

### 1.设置用户名称和email地址

##### ①.打开Git Bash

##### ②.设置用户信息

```
git config --global user.name "xxx"		//xxx为用户名
```

```
git config --global user.email "xxx@xxx"		//xxx@xxx为邮箱
```

##### ③.查看配置信息

```
git config --global user.name
```

```
git cinfig --global user.email
```



### 2.常用指令配置别名

##### ①.在用户目录下(例:C:\Users\22357)打开Git Bash创建.bashrc文件

```
touch .bashrc
```

##### ②.编辑.bashrc文件，输入以下配置

```
#用于输出git提交日志
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
#用于输出当前目录所有文件及基本信息
alias ll='ls -al'
```

##### ③运行.bashrc文件

```
source ~/.bashrc
```



### 3.文件修改会存在的几个状态

|              仓库(repository)               |      暂存区(index)       |         工作区(workspace)          |
| :-----------------------------------------: | :----------------------: | :--------------------------------: |
| 修改进入仓库就变成一次提交记录<==git commit | 已暂存(staged)<==git add | 未暂存(unstaged) <==修改已有的文件 |
|                                             |                          | 未跟踪(untracked)<==新创建一个文件 |



### 4.文件基本操作

##### ①获取本地仓库

```
git init		//当目录出现.git隐藏文件的时候即创建成功
```

##### ②.查看文件状态

```
git status
```

##### ③.工作区 ==>暂存区

```
git add xxx		//xxx为文件名 xxx=.时为添加所有文件
```

##### ④.暂存区 ==>本地仓库

```
git commit -m "message"		//message为备注信息
```

##### ⑤.查看提交日志（记录）

```
git log --options
	--options:
		--all 查看所有分支
		--pretty=oneline 将提交信息显示为一行
		--abbrev-commit 使得输出的commitId更简短
		--graph 以图的形式显示
```

##### ⑥.版本回退

```
git reset --hard commitID		//回退至commitID版本，commitID（提交记录）可以使用git log查看
```

##### ⑦.记录历史操作

```
git reflog
```



### 5.忽略文件

创建.gitignore文件，其中配置忽略文件，下面给出实例：

```
# 所有以.a 结尾的文件讲被忽略(递归)
*.a
# 不管其他规则怎样,强制不忽略  lib.a
!lib.a
# 只忽略 文件 TODO (注意这里是文件)
/TODO
# 忽略 build文件夹下所有内容(递归) 这里是文件夹
build/
# 忽略 doc 目录下以 *.txt 结尾的文件 (不递归)
doc/*.txt
# 忽略 doc 目录下以 *.pdf 结尾的文件 (递归)
doc/**/*.pdf
```



# 分支

概念：几乎所有的版本控制系统都以某种形式支持分支。使用分支意味你可以把你的工作从开发主线上分离开来进行重大的Bug修改，开发新的功能，以免影响开发主线

### 1.分支基本操作

##### ①.查看本地分支

```
git branch
```

##### ②.查看本地分支

```
git branch 分支名
```

##### ③切换分支

head指向谁谁就是当前分支

```
git checkout 分支名		
```

```
git checkout -b 分支名		//切换到一个不存在的分支（创建并切换）
```

##### ④合并分支

一般是将其他分支合并到master上面

```
git merge 分支名称		//将其他分支合并到当前分支
```



##### ⑤删除分支

不能删除当前分支，只能删除其他分支

```
git branch -d xxx	//删除分支时，需要做各种检查
```

```
git branch -D xxx	//不做任何检查，强制删除
```



### 2.冲突

不同分支修改了相同文件，合并时此文件产生的分歧，需要手动解决，步骤如下：

##### 解决冲突

##### ①处理文件中冲突的地方

##### ②将解决完冲突的文件加入暂存区

##### ③提交到仓库



### 3.开发中分支使用原则和流程

一般有如下分支使用原则与流程

##### ①master(生产)分支

线上分支，主分支，中小规模项目作为线上运行的应用对应的分支

##### ②develop(开发)分支

是master创建的分支，作为开发部门的主要开发分支，阶段开发结束后，是需要合并到master分支上

##### ③feature/xxx分支

从develop创建的分支，一般是同期并行开发，分支上的研发任务完成后合并到develop分支上

##### ④hotfix/xxx分支

从master派生的分支，一般为线上bug修复使用，修复完成后需要合并到master、test、develop分支

##### ⑤其他分支

test分支（用于代码测试）、pre分支（预上线分支）等等



# Git远程仓库

### 1.创建远程仓库



### 2.配置SSH公钥

##### ①生成SSH公钥

```
ssh-keygen -t rsa		//生成SSH公钥
```

不断回车，若公钥已经存在，则自动覆盖

我的笔记本密钥

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDV3E0TA90tJFUfzS3BpV4+BPlxMgryCFJXgb/FVSHSMOMwvPzknfr9TA6hm64AHQEzCgFhkR8tILBp8wZkSA2mB/jRaJRbTHL+XAv92dm2wCYey5eWX4q2Hwfrv73x+h5RMnVkRefhs9KTV0q1ZVixqE9K0c5stXpdd0B9DRu5BKb73gNw2KwYOdnY1OGecAtD5ZvkI/5JroBJItDdEgwWydQ7OejjKsCvGYHYlFy6rp/QdmPWBsg4Ik6oWY4kKG5PcTq1iOu1eosKrAZQzJlwUfuPm5do4bl1doFBFNfKyn+0bETl2nqp2l0UplxtrYdUo1t9z8hzFEvGuvWfa2/hlTR5JQAAKFwcMfDMNvI+IK1PaWpu7g6/5fa7mXxpokRS3zX4ca+M5IQGTynS0s1z6BEnWw1KS+GBtz4oqThpDT5oV0+5QIoWi1x3wahNh/jnYA+gJc0sZuorGk5iZc5ifq8BIRhd56RiPWuKutKnPgddvYpGSwHrdZlU56rN6VE= 22357@DESKTOP-EH53ON4

```

##### ②Gitee设置账户共公钥

```
cat ~/.ssh/id_rsa.pub		//获取公钥
```

##### ③在gitee上粘贴公钥

##### ④验证是否添加成功

```
ssh -T git@gitee.com		//输入yes
```



### 3.本地绑定远程仓库

##### ①在创建的仓库中复制ssh地址

##### ②绑定远程仓库

```
git remote add origin ssh地址 	//绑定远程仓库,origin为远程仓库名
```

##### ③查看远程仓库是否添加成功

```
git remote
```

##### ④删除指定远程仓库

```
git remote rm origin
```



### 4.代码推送至远程仓库

##### ①若关联当前分支和远程分支，可以省略分支名和远端分支名

```
git push [-f] [--set-upstream] [远程名称[本地分支名][:远程分支名]]
//-f 强制覆盖远程仓库
//--set-upstream 推送到远端的同时建立起和远端分支的关联关系
```

```
git push --set-upstream origin master:master	//设置本地分支和远程分支
git branch -vv	//查看本地分支和远程仓库分支的信息
git push	//设置完成后直接push
```

##### ②若远程分支名和本地分支名相同，则可以只写本地分支

```
git push origin master
```



### 5.从远程仓库克隆

如果有一个远端仓库，我们可以直接clone到本地 

```
git clone <仓库路径> [本地目录]
```



### 6.从远程仓库中抓取和拉取

远程分支和本地分支一样，我们可以进行merge操作，只是需要先把远端仓库里的更新都下载到本地，再进行操作

##### ①抓取命令：将仓库里面的更新都抓取到本地，不会进行合并。但是不指定远端名和分支名，则抓取所有并更新当前分支

```
git fetch [remote name][branch name]
```

##### ②拉取指令：将远端仓库的修改拉到本地并进行合并，等同于fetch+merge。如果不指定远端名和分支名，则抓取所有并更新当前分支

```
git pull [remote name][branch name]
```



### 七.推送远程仓库冲突

在一段时间里，A,B用户修改了同一文件夹的同一位置，此时会发生合并冲突。

场景：A用户先提交远端，B用户也需要提交远端，B推送远端会发生错误

解决方法：故需要先拉取远程仓库，会提示冲突文件，经过修改冲突后，才能推送到远程



















































































































































































































































































































