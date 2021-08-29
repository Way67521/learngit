# Git 学习笔记

### Git 工作原理 / 流程

![](https://pic2.zhimg.com/80/v2-3bc9d5f2c49a713c776e69676d7d56c5_1440w.jpg)



Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库

### 安装 Git

download：https://github.com/git-for-windows/git/releases/download/v2.33.0.windows.2/Git-2.33.0.2-64-bit.exe

安装完后如图所示

![image-20210828235648929.png](https://files.alexhchu.com/2021/08/29/33673146a12ae.png)

在桌面或者文件夹中右键点击 Git Bash 打开操作窗口

![批注 2021-08-29 000049.png](https://files.alexhchu.com/2021/08/29/bca83384ce7ee.png)

安装完成后，还需要最后一步设置，在命令行输入如下：

```text

git config --global user.name "Way67521" 

git config --global user.email "example@XXX.com"

```

注意：

因为Git是分布式版本控制系统，所以需要填写用户名和邮箱作为一个标识。

git config --global 参数，有了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然你也可以对某个仓库指定的不同的用户名和邮箱。

### 使用 Git

#### 创建版本库

什么是版本库？版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都

能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。

所以创建一个版本库也非常简单，如D盘下下新建一个learngit版本库。

* git init

通过命令 git init 把这个目录变成git可以管理的仓库

![批注 2021-08-29 004521.png](https://files.alexhchu.com/2021/08/29/b875eb9276433.png)

这时候你当前learngit目录下会多了一个.git的目录，这个目录是Git来跟踪管理版本的，没事千万不要手动乱改这个目录里面的文件，否则，会把git仓库给破坏了。

#### 把文件添加到版本库

首先要明确下，所有的版本控制系统，只能跟踪文本文件的改动，比如txt文件，网页，所有程序的代码等，Git也不列外，版本控制系统可以告诉你每次的改动，但是图片，视频这些二进制文件，虽能也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是知道图片从1kb变成2kb，但是到底改了啥，版本控制也不知道。

* git status

我在版本库learngit目录下新建一个记事本文件 readme.md 内容如下：learn git，使用 git status 命令查看文件状态。

![批注 2021-08-29 011736.png](https://files.alexhchu.com/2021/08/29/e00c8f434161b.png)

如图所示，会显示新增的文件。

* git add [文件名]

  使用命令 git add readme.md 或者 git add . 添加到暂存区里面去。如下：

![批注 2021-08-29 012028.png](https://files.alexhchu.com/2021/08/29/28d0908a5b232.png)

* git commit

用命令 git commit -m "---提交注释---"告诉Git，把文件提交到仓库。

![批注 2021-08-29 012515.png](https://files.alexhchu.com/2021/08/29/189b7d9f7327e.png)

至此，我们已经提交了一个readme.md文件了，我们下面可以通过命令 git status 来查看是否还有文件未提交，如下：

![批注 2021-08-29 012713.png](https://files.alexhchu.com/2021/08/29/80af90eb50709.png)

说明没有任何文件未提交，但是我现在继续来改下readme.md内容，比如我在下面添加一行 git commit！内容，继续使用git status来查看下结果，如下：

![image.png](https://files.alexhchu.com/2021/08/29/e62b7d10bb20b.png)

上面的命令告诉我们 readme.md文件已被修改，但是未被提交的修改。

* git diff

接下来我想看下readme.md文件到底改了什么内容，如何查看呢？可以使用如下命令：git diff readme.md 如下：

![1630229455471.png](https://files.alexhchu.com/2021/08/29/b8df4dd27a9e5.png)

如上可以看到，readme.md文件内容已经被修改过。

知道了对readme.md文件做了什么修改后，我们可以放心的提交到仓库了，提交修改和提交文件是一样的2步(第一步是git add 第二步是：git commit)。

#### 版本回退

如上，我们已经学会了修改文件，现在我继续对readme.md文件进行修改，再增加一行

* git log

现在我已经对readme.md文件做了三次修改了，那么我现在想查看下历史记录，如何查呢？我们现在可以使用命令 git log 演示如下所示：

![1630243082345.png](https://files.alexhchu.com/2021/08/29/74867ba15ec59.png)

git log 命令显示从最近到最远的显示日志，我们可以看到最近三次提交。

现在我想使用版本回退操作，我想把当前的版本回退到上一个版本，要使用什么命令呢？可以使用如下2种命令，第一种是：git reset --hard HEAD^ 那么如果要回

退到上上个版本只需把HEAD^ 改成 HEAD^^ 以此类推。那如果要回退到前100个版本的话，使用上面的方法肯定不方便，我们可以使用下面的简便命令操作：git 

reset --hard HEAD~100 即可。未回退之前的readme.md内容如下：

![1630243279018.png](https://files.alexhchu.com/2021/08/29/e2787172fbd52.png)

如果想回退到上一个版本的命令如下操作：

![1630243409797.png](https://files.alexhchu.com/2021/08/29/c26657cd48e22.png)

再来查看下 readme.md内容如下：通过命令cat readme.md查看

![1630243489053.png](https://files.alexhchu.com/2021/08/29/fc843ba871f3e.png)

可以看到，内容已经回退到上一个版本了。我们可以继续使用git log 来查看下历史记录信息，如下：

![1630243540870.png](https://files.alexhchu.com/2021/08/29/bb0383a1845c5.png)

我们看到 git log 内容我们没有看到了，但是现在我想回退到最新的版本，如：有 git log的内容要如何恢复呢？我们可以通过版本号回退，使用命令方法如下：

git reset --hard 版本号 ，但是现在的问题假如我已经关掉过一次命令行或者有git log内容的版本号我并不知道呢？要如何知道 git log 内容的版本号呢？可以通过

如下命令即可获取到版本号：git reflog 演示如下：

![1630243745734.png](https://files.alexhchu.com/2021/08/29/7c0fc0bfa3846.png)

通过上面的显示我们可以知道，包含内容 git log 的版本号是 e3aeacc.我们现在可以命令 git reset --hard e3aeacc来恢复了。演示如下：



可以看到 目前已经是最新的版本了。

#### 理解工作区与暂存区的区别

工作区：就是你在电脑上看到的目录，比如目录下learngit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。

版本库(Repository)：工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我

们自动创建了第一个分支master,以及指向master的一个指针HEAD。

我们前面说过使用Git提交文件到版本库有两步：

第一步：是使用 git add 把文件添加进去，实际上就是把文件添加到暂存区。

第二步：使用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支上。

我们继续使用demo来演示下：

我们在readme.md再添加一行内容为 demo 演示！，接着在目录下新建一个文件为test.md内容为 test，我们先用命令 git status来查看下状态，如下：

![1630244479168.png](https://files.alexhchu.com/2021/08/29/fcd566dfe1dac.png)

现在我们先使用git add 命令把2个文件都添加到暂存区中，再使用git status来查看下状态，如下：

![1630245309715.png](https://files.alexhchu.com/2021/08/29/17aca95ee8b7b.png)

接着我们可以使用git commit一次性提交到分支上，如下：

![1630245388637.png](https://files.alexhchu.com/2021/08/29/9e6f5d2737b50.png)

#### Git撤销修改和删除文件操作

* 撤销修改

比如我现在在readme.md文件里面增加一行内容为 ---撤销修改---，我们先通过命令查看如下：

在我未提交之前，我发现添加---撤销修改---内容有误，所以我得马上恢复以前的版本，现在我可以有如下几种方法可以做修改：

第一：如果我知道要删掉那些内容的话，直接手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。

第二：我可以按以前的方法直接恢复到上一个版本。使用 git reset --hard HEAD^

但是现在我不想使用上面的2种方法，我想直接想使用撤销命令该如何操作呢？首先在做撤销之前，我们可以先用 git status 查看下当前的状态。如下所示：

![1630245659962.png](https://files.alexhchu.com/2021/08/29/2475418ef9265.png)

可以发现，Git会告诉你，git restore file 可以丢弃工作区的修改，如下命令：git restore readme.md,如下所示：

![1630245817081.png](https://files.alexhchu.com/2021/08/29/46af925bd1bf0.png)

* 删除文件

假如我现在版本库learngit目录添加一个文件rm.md,然后提交。如下：

![1630246581513.png](https://files.alexhchu.com/2021/08/29/68efaa2c63d09.png)

如上：一般情况下，可以直接在文件目录中把文件删了，或者使用如上rm命令：rm rm.md ，如果我想彻底从版本库中删掉了此文件的话，可以再执行commit命

令提交掉，现在目录是这样的，

![1630246614753.png](https://files.alexhchu.com/2021/08/29/6244f01cd57e5.png)

只要没有commit之前，如果我想在版本库中恢复此文件如何操作呢？可以使用如下命令 git restore rm.md，如下所示：

![1630246730480.png](https://files.alexhchu.com/2021/08/29/26b41af532e0e.png)

再来看看我们learngit目录，恢复了被删除的文件 rm.md，如下所示：

![1630246730480.png](https://files.alexhchu.com/2021/08/29/26b41af532e0e.png)

#### 远程仓库

在了解之前，先注册github账号，由于你的本地Git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置：

第一步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果有的话，直接跳过此如下

命令，如果没有的话，打开命令行，输入如下命令：ssh-keygen -t rsa -C "ga3372186@gmail.com"。

![1630247630173.png](https://files.alexhchu.com/2021/08/29/98984e11e07b9.png)

![1630247661205.png](https://files.alexhchu.com/2021/08/29/7672bad6ad35f.png)

id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第二步：登录github,打开” settings”中的SSH Keys页面，然后点击“Add SSH Key”,填上任意title，在Key文本框里黏贴id_rsa.pub文件的内容。

![1630248395388.png](https://files.alexhchu.com/2021/08/29/1c311554dfb0b.png)

点击 Add Key，你就应该可以看到已经添加的key。

![1630248488540.png](https://files.alexhchu.com/2021/08/29/eeb88b9a73d70.png)

* 如何添加远程库

现在的情景是：我们已经在本地创建了一个Git仓库后，又想在github创建一个Git仓库，并且希望这两个仓库进行远程同步，这样github的仓库可以作为备份，又

可以其他人通过该仓库来协作。首先，登录github上，然后在右上角找到“create a new repo”创建一个新的仓库。如下：

![1630248570991.png](https://files.alexhchu.com/2021/08/29/8970e9024fad9.png)

在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

![1630248638100.png](https://files.alexhchu.com/2021/08/29/4a649a697a264.png)

目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库

的内容推送到GitHub仓库。

 git remote add origin https://github.com/Way67521/learngit.git

git remote add origin [自己的远程仓库地址] ----本地仓库与之关联

git push -u origin master---推送到远程仓库master分支

把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支main 推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了 –u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支

和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。推送成功后，可以立刻在github页面中看到远程库的内容已经和本地一模一样了

![1630249533827.png](https://files.alexhchu.com/2021/08/29/e01781cd3147c.png)

![1630249619853.png](https://files.alexhchu.com/2021/08/29/0ba9d2d2525dd.png)



从现在起，只要本地作了提交，就可以通过如下命令：

git push origin master

把本地master分支的最新修改推送到github上了，现在你就拥有了真正的分布式版本库了。

#### 如何从远程库克隆

在远程库创建一个新项目testclone，下一步是使用命令git clone克隆一个本地库了。如下所示：

![1630250041626.png](https://files.alexhchu.com/2021/08/29/7f08b2a5d06d2.png)

* git clone

git clone https://github.com/Way67521/testclone.git

接着在我本地目录下生成testclone目录了，并clone 远程代码如下所示：

![1630250803898.png](https://files.alexhchu.com/2021/08/29/b4e354d1c26e0.png)

#### 分支管理

在版本回填退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分

支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。首先，我们来创建dev分支，

然后切换到dev分支上。如下操作：

![1630251081814.png](https://files.alexhchu.com/2021/08/29/7e9fe2dad8f79.png)

* git branch dev

* git checkout dev

git branch查看分支，会列出所有的分支，当前分支前面会添加一个星号。

可以使用 git checkout -b [分支名] 代替上面两条命令。然后我们在dev分支上继续做demo，比如我们现在在readme.md再增加一行 git checkout -b dev

 ![1630252032745.png](https://files.alexhchu.com/2021/08/29/a10b6dcae57e0.png)

现在dev分支工作已完成，现在我们切换到主分支master上，继续查看readme.md内容如下：

![1630252095017.png](https://files.alexhchu.com/2021/08/29/01c6f55c86d94.png)

现在我们可以把dev分支上的内容合并到分支master上了，可以在master分支上，使用如下命令 git merge dev 如下所示：

![1630252227513.png](https://files.alexhchu.com/2021/08/29/6dc331674327b.png)

git merge命令用于合并指定分支到当前分支上，合并后，再查看readme.md内容，可以看到，和dev分支最新提交的是完全一样的。

注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

合并完成后，我们可以接着删除dev分支了，操作如下：

![1630252379122.png](https://files.alexhchu.com/2021/08/29/df5f68910ac67.png)

总结创建与合并分支命令如下：

查看分支：git branch

创建分支：git branch [分支名]

切换分支：git checkout [分支名]

创建+切换分支：git checkout –b [分支名]

合并某分支到当前分支：git merge [分支名]

删除分支：git branch –d [分支名]

如何解决冲突？

下面我们还是一步一步来，先新建一个新分支，比如名字叫 test，在readme.md添加一行内容 test branch，然后提交，如下所示:

![1630252657641.png](https://files.alexhchu.com/2021/08/29/a68294e006435.png)

同样，我们现在切换到master分支上来，也在最后一行添加内容，内容为 master branch，如下所示：

![1630253011033.png](https://files.alexhchu.com/2021/08/30/c416584e5f364.png)

现在我们需要在master分支上来合并test，如下操作：

![1630253089362.png](https://files.alexhchu.com/2021/08/30/2ebcba1f03dbd.png)

发现产生了冲突，git status 查看状态，cat README.md 查看冲突后的内容

![1630253269866.png](https://files.alexhchu.com/2021/08/30/5c4e73d0ebd6a.png)

Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中<<<HEAD是指主分支修改的内容，>>>>>test是指test上修改的内容

冲突的内容：

![1630253405565.png](https://files.alexhchu.com/2021/08/30/d2c9fa6a98680.png)

修改成和主干上一致的内容后如下后保存：

![1630253576315.png](https://files.alexhchu.com/2021/08/30/1079643678aee.png)

