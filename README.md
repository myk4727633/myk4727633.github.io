# git的安装与使用

# 前言：

`github`和`gitee`（码云）是目前来说使用最广泛的两个代码托管平台。目前将相同的电视节目源放到这两个平台，`github`上的就比较难访问，`gitee`国内使用速度比较快。节目源有时效性，需要经常更新节目源地址。使用git可以很方便地将修改后的节目源文本更新到`gitee`。

# 参考：

> - brew基础1：https://zhuanlan.zhihu.com/p/46239814
> - brew基础2：https://blog.csdn.net/fisherming/article/details/81334049
> - git官网：https://git-scm.com/
> - git文档：https://git-scm.com/book/zh/v2
> - https://www.jianshu.com/p/34d1d5fa4382
> - git入门：https://blog.csdn.net/ai1362425349/article/details/82119889
> - https://blog.csdn.net/codes_life/article/details/79231331?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase
> - git本地创建项目：https://www.jianshu.com/p/a9da5d0035e5

# 正文：

## 1.github中的相关操作：

### 1.1 fork：

将会完整地将项目文件复制一份到自己的仓库并单独存在，我们可以对该从仓库进行操作，并且不会对原仓库产生任何影响。

### 1.2 issue：

可以通过该选项进行提问，若是问题已解决或不想再提问，那么可以点击这个issue，点击`close issue`进行关闭问题。

关闭issue的权限，可以是提问的人、也可以是该项目的作者。

### 1.3 watch：

实际表示的意思是`关注`。在项目的右上角，可以通过点击设置是否收到当前项目的动态提醒、以及设置何时能收到提示等。默认当关注的仓库有更改时会提醒。

### 1.4 pull request：

当我们fork了一个仓库，并且对仓库进行了修改，我们认为该修改对原项目有帮助，那么就可以发起一个`pull request`，将我们的修改推送给原项目。

在我们fork的仓库中公有两个地方显示`pull request`字段，分别是仓库文件区的右上角和仓库名称的下方。点击右上角的`pull request` 将会跳转到下一页面，在该页面中显示我们进行的修改，再次确认即可提交；提交完成后，我们可以在仓库名的下方的菜单选项看到`pull request` 此时有了新变化，变成了1。项目作者同样会在这个位置看到推送请求，若是无问题，作者可以点击`merge pull request`选项，将该提交合并。

## 2.git相关：

需要先安装git，可以从官网下载对应的系统版本进行安装。

### 2.1 git的工作区域：

<img src="../../../../../../../Users/yongkangm/Desktop/教程/git的安装与使用/images/image-20201225094709868.png" alt="image-20201225094709868" style="zoom:50%;" />

> - Git 有三个区域，我们在本地工作区进行文件的新增或修改等操作，我们使用 `git add`命令,将文件添加到暂存区。当然我们仍可以对这些文件进行修改。
> - 最后，我们所有的操作都已经完成，并且认为不需要改动了，那么就可以使用`git commit`命令，将暂存区的内容提交到仓库。
> - `git status`命令可以查看文件的状态。

<img src="../../../../../../../Users/yongkangm/Desktop/教程/git的安装与使用/images/image-20201225095337431.png" alt="image-20201225095337431" style="zoom:50%;" />

### 2.2 用户信息：

安装完Git 之后，要做的第一件事就是设置你的用户名和邮件地址。这一点很重要，因为每一个Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改：

```sh
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

再次强调，如果使用了`--global`选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git都会使用那些信息。当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有`--global`选项的命令来配置。

可以通过下面命令，显示我们进行的配置信息以为所在位置：

```sh
 #--show-origin参数会显示具体路径
 git config --list --show-origin
```

### 2.3 初始仓库：

如果我们希望将本地的文件夹初始化为一个git仓库，可以使用下面命令：

```sh
#进入到仓库的根目录
cd test
#初始化test文件夹为仓库
git init
```

初始化命令并不会对已有文件进行删除，初始化完成后会生成一个隐藏文件夹`.git`，用于存储本地仓库信息。

### 2.4 提交文件到仓库：

- 在工作区创建一个文件：

  > 1.ls命令：查看到当前仓库下并没有文件
  >
  > 2.git status命令：检查文件状态，发现并没有文件需要提交

```sh
yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
$ ls

yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
$   git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
$ touch 1.txt

```

- 将新创建的文件添加到暂存区：

  > 1. git status命令：显示出一个文件（1.txt），状态为Untracked 。在git工具中该文件显示为红色。
  > 2. git add 文件名：将文件添加到暂存区
  > 3. git status命令：查看到一个文件（1.txt）。在git工具中该文件显示为绿色，表示该文件状态为正在追踪。

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $   git status
  On branch master
  
  No commits yet
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          1.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git add 1.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $   git status
  On branch master
  
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   1.txt
  
  ```

- 将暂存区的指定文件提交到仓库：

  > 1.git commit -m "注释信息"：将暂存区的文件提交到仓库
  >
  > 2.git status：表示当前暂存区中没有要提交的数据

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git commit -m "add 1.txt"
  [master (root-commit) 57d0500] add 1.txt
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 1.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  nothing to commit, working tree clean
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $
  ```

### 2.5 修改后的文件提交到仓库：

- 对指定文件进行修改，并查看文件状态：

  > 1.git status：查看到有一个文件修改后还没有提交。此时文件的状态为`modified`已修改状态。git工具中显示为红色。

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          modified:   1.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $
  ```

- 将指定文件添加到暂存区：

  > git status：文件状态虽然仍是`modified,`但是在git工具中已经显示为绿色

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git add 1.txt
  warning: LF will be replaced by CRLF in 1.txt.
  The file will have its original line endings in your working directory
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          modified:   1.txt
  
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $
  
  ```

- 将文件提交到仓库：

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git commit -m "update 1.txt"
  [master 1b6f500] update 1.txt
   1 file changed, 1 insertion(+)
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $
  
  ```

### 2.6 删除仓库中的文件：

- 删除工作区文件：

  > 1.rm -rf 文件名：删除指定的文件，也可以手动到文件夹中删除
  >
  > 2.git status：文件状态为`deleted`被删除状态

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ rm -rf 1.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          deleted:    1.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  ```

- 删除暂存区文件：

  > 1.git rm 文件名：从暂存区删除该文件
  >
  > 2.git status：文件状态变成绿色的`deleted`表示已被删除

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git rm 1.txt
  rm '1.txt'
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          deleted:    1.txt
  
  ```

- 提交到仓库：

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git commit -m "删除文件"
  [master cff21e8] 删除文件
   1 file changed, 1 deletion(-)
   delete mode 100644 1.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $ git status
  On branch master
  nothing to commit, working tree clean
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (master)
  $
  ```

### 2.7 git管理远程仓库：

#### 2.7.1 克隆远程仓库：

```sh
#创建指定文件夹并将远程项目克隆到文件夹
1.创建存放仓库的文件夹
mkdir test
2.进入到该文件夹
cd test
3.执行克隆命令
git clone 远程仓库地址
```

- 我在github上新创建了一个远程仓库：

  ```
  test
  ```

- 点击`code`，复制`https`连接地址：

  ```
  https://github.com/myk4727633/test.git
  ```

- 我在本地新创建一个文件夹`git`用于存放github克隆仓库

- 进入`git`文件夹执行clone命令：

  > 将会在当前位置克隆远程仓库，并且远程仓库名作为文件夹存在于当前位置。所以仓库位置为`git/test`

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git
  $ git clone https://github.com/myk4727633/test.git
  Cloning into 'test'...
  remote: Enumerating objects: 3, done.
  remote: Counting objects: 100% (3/3), done.
  remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
  Receiving objects: 100% (3/3), done.
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git
  $ ls
  test/
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git
  $ cd test
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ ls
  README.md
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $
  
  ```

#### 2.7.2 提交修改到远程仓库：

```sh
1.将修改后的文件添加到暂存区
git add 文件名
2.将暂存区文件提交到仓库
git commit -m "注释"
3.将本地仓库内容推送到远程仓库
git push
```

- 添加一个新文件到工作区：

  > 1.手动创建了一个新文件`2.txt`
  >
  > 2.查看状态，新创建的文件状态为未跟踪状态。显示为红色

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ ls
  2.txt  README.md
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ git status
  On branch main
  Your branch is up to date with 'origin/main'.
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          2.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  ```

- 将文件添加到暂存区：

  > 1.将`2.txt`添加到暂存区
  >
  > 2.文件状态为`new file`新创建的文件，颜色为绿色

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ git add 2.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ git status
  On branch main
  Your branch is up to date with 'origin/main'.
  
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          new file:   2.txt
  ```

  

- 提交暂存区文件的到本地仓库：

  > 1.将暂存区文件提交到本地仓库

  ```sh
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ git commit -m "add 2.txt"
  [main 4d8c664] add 2.txt
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 2.txt
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $ git status
  On branch main
  Your branch is ahead of 'origin/main' by 1 commit.
    (use "git push" to publish your local commits)
  
  nothing to commit, working tree clean
  
  yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
  $
  ```

- 将本地仓库推送到远程仓库：

  ```sh
  git push
  ```

  - 因为是首次进行推送到远程仓库，需要进行权限验证。需要我们登陆github进行验证。

  <img src="../../../../../../../Users/yongkangm/Desktop/教程/git的安装与使用/images/image-20201225112719444.png" alt="image-20201225112719444" style="zoom:50%;" />

  - 点击在浏览器中登陆，登陆成功后会跳出授权提示，点击认证：

    <img src="../../../../../../../Users/yongkangm/Desktop/教程/git的安装与使用/images/image-20201225112915759.png" alt="image-20201225112915759" style="zoom:50%;" />

  - 认证成功后，回到git工具，将会看到提交成功：

    ```sh
    yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
    $ git push
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 3 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 282 bytes | 141.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To https://github.com/myk4727633/test.git
       52ebf18..4d8c664  main -> main
    
    yongkangm@YONGKANGM248F MINGW64 ~/Desktop/git/test (main)
    $
    
    ```

  - 此时回到github的这个仓库，将会看到提交的信息已经同步过来了：

    <img src="../../../../../../../Users/yongkangm/Desktop/教程/git的安装与使用/images/image-20201225113217643.png" alt="image-20201225113217643" style="zoom:50%;" />

  - 遇到没权限的问题时：

    前面提到push是需要验证权限的，前面通过浏览器登录github的方式进行了授权，所以可以成功push。另一种方式是直接修改远程仓库地址，将用户名和密码添加到远程仓库地址即可：

    - 修改`.git/config`文件：

      ```sh
      #将下面的url修改成指定的
      [remote "origin"]
      	url = https://github.com/myk4727633/test.git
      #修改后的
      [remote "origin"]
      	url = https://用户名:密码@github.com/myk4727633/test.git
      ```

### 2.8 通过github page创建个人站点

创建成功后通过`https://用户名.github.io`进行访问。

```sh
#搭建过程
1.创建新仓库，仓库名必须是：用户名.github.io
2.创建新文件，index.html,作为网站首页
```



## 1.生成公钥文件：

```ssh
#这里的jmggwu@163.com为自己的邮箱
ssh-keygen -t rsa -C "jmggwu@163.com"
```

一路回车。

## 2.查看公钥文件：

```
cat ~/.ssh/id_rsa.pub
```

也可以使用访达的前往功能，手动打开`~/.ssh/id_rsa.pub`文件，复制内容。

## 3.添加公钥：

将上面复制到公钥内容添加到：设置-安全设置-ssh公钥。

<img src="https://i.loli.net/2020/06/26/Dy893bkrqW21oZM.png" alt="image-20200626190728611" style="zoom:50%;" />

## 4.克隆项目：

### 4.1 进入本地项目存放目录：

输入`cd`命令，然后将希望项目存放的文件夹拖入到终端，就会自动填充路径：

```
cd /Users/yongkangm/Documents/gitee/kang/zibo 
```

### 4.2 获取项目地址：

打开项目，点击克隆/下载，复制地址：

<img src="https://i.loli.net/2020/06/26/rv4O1go6MVLICqK.png" alt="image-20200626191222389" style="zoom:50%;" />

### 4.3 克隆项目：

终端输入：

```
#xxx即为上面复制的项目地址
git clone xxx
```

之后就会将项目克隆到本地。

## 5.更新项目：

每次提交都要进行下面的三步：

1.将所有都提交上去：

```
git add .
```

2.输入提交说明

```
git commit -m “输入提交说明”
#若不需要填写说明
git commit
```

3.选择提交分支

```
git push origin master
#若只有一个主分支
git push
```

到此项目就保存上去了。

