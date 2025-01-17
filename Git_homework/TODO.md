# Git 作业
1. 用 Vim MarkDown 写一份自己对于 Git 的学习笔记
2. 将笔记 PR 到[]()
## 一：首先是创建一个仓库

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit 
```

 然后变为可管理的仓库

```plain
$ git init
```

接着创建文件，步骤如下： 1  编写文件

​                                               2   添加到仓库

```
$ git add readme.txt
```

3  提交（添加和提交的区别。提交是将添加的所有文件全部提交到仓库中）

```plain
$ git commit -m "wrote a file"
```

注意：添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m <message>`，完成。

### 二：时光穿梭机

###      1提交修改

1首先，修改原来txt文件上面的内容

2用下面的指令查看git仓库的状态：

```plain
$ git status
```

注意：这个只能看出仓库被改了，但不知道改的内容是什么
若要查看修改的内容，我们可以用以下指令

```plain
$ git diff readme.txt 
```

修改完之后，也要提交修改。步骤和提交文件是一样的过程

#### 注意：

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

###     2关于如何查看历代版本：

​        `git log`命令显示从最近到最远的提交日志，（如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数）

```
$ git log --pretty=oneline
```

前面表示的数字是版本号。

###     3回退到以前的版本

1.   关于版本的表示：  本版本是HEAD

   上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

2. 回退例子：

   ```plain
   $ git reset --hard HEAD^
   ```

​        以上代码表示回退到上个版本， 为了表示严谨，我们可以再看一下txt文本的内容

```plain
$ cat readme.txt
```

3. 我们还可以去到未来，找到之前的版本号

   ```plain
   $ git reset --hard 1094a
   ```

​       这里的1094是前面那一串的前几个数字，不用输全，电脑会自动搜索

4. 找不到版本号，怎么办，可以查看之前的命令

   Git提供了一个命令`git reflog`用来记录你的每一次命令

   从输出可知，`append GPL`的commit id是`1094adb`

   ### 3 工作区和暂存区

   从输出可知，`append GPL`的commit id是`1094adb`

   ### 4 管理修改：

   有俩种方法:1. 第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

   ​                    2. 第一次修改 -> `git add` ->git commit-> 第二次修改 -> `git add` -> `git commit

###      5 撤销修改：

`git checkout -- file`可以丢弃工作区的修改

​         命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

​     一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

​     一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态

###       6 删除文件 

我们通常采用文件管理器的方法或者以下:

```plain
$ rm test.txt
```

并且`git commit`现在，文件就从版本库中被删除了.

## 三 远程仓库 

####     1 添加sskey：用 config 查看sskey所存在的文件路径，用cat查看

![image-20250114150201459](C:\Users\包华贺\AppData\Roaming\Typora\typora-user-images\image-20250114150201459.png)

成功后如图所示

####      2 简单介绍：

你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步

Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库

GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的`learngit`仓库下运行命令：

```plain
$ git remote add origin git@github.com:october1314520/learngit.git
```

远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库

​    3 推送 :

下一步，就可以把本地库的所有内容推送到远程库上：

```plain
$ git push -u origin master
```

注意;于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

## 四:分支管理

##### 1创建和合并分支

自己理解：类似于c语言中的链条，控制指针指向来控制分支

首先，我们创建`dev`分支，然后切换到`dev`分支：

```plain
$ git checkout -b dev
```

`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```plain
$ git branch dev
$ git checkout dev
```

然后，用`git branch`命令查看当前分支

```plain
$ git branch
* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

然后，我们就可以在`dev`分支上正常提交，比如对`readme.txt`做个修改，加上一行

然后提交：

```plain
$ git add readme.txt 
$ git commit -m "branch test"
[dev b17d20e] branch test
 1 file changed, 1 insertion(+)
```

在，`dev`分支的工作完成，我们就可以切换回`master`分支：

```plain
$ git checkout master
Switched to branch 'master'
```

切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：
以上关于分支的例子：分支不影响主干。分支可合并回主干

我们把`dev`分支的工作成果合并到`master`分支上：

```plain
$ git merge dev
```

`git merge`命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。

注意：新的`git switch`命令，比`git checkout`要更容易理解。

#### 2冲突： master改了 dev也改了 ，合并可能会存在冲突

`git status`也可以告诉我们冲突的文件，我们可以直接查看readme.txt的内容：

it用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容

```plain
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```

带参数的`git log`也可以看到分支的合并情况

最后，删除`feature1`分支：

```plain
$ git branch -d feature1
```

#### 三 分支管理策略

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`：

```plain
$ git merge --no-ff -m "merge with no-ff" dev
```

并后，我们用`git log`看看分支历史

#### 四  bug分支

幸好，Git还提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

```plain
$ git stash
```

你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支`issue-101`来修复它

首先确定要在哪个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支：

复完成后，切换到`master`分支，并完成合并，最后删除`issue-101`分支：

#### 五 Feature分支

销毁失败。Git友情提醒，`feature-vulcan`分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的`-D`参数。。

现在我们强行删除：

```plain
$ git branch -D feature-vulcan
```

#### 六 多人协作

你从远程仓库克隆时，实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支

## 四 标签管理

在Git中打标签非常简单，首先，切换到需要打标签的分支上：

```plain
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
```

然后，敲命令`git tag <name>`就可以打一个新标签：

```plain
$ git tag v1.0
```



以用命令`git tag`查看所有标签：

默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了

方说要对`add merge`这次提交打标签，它对应的commit id是`f52c633`，敲入命令：

```plain
$ git tag v0.9 f52c633
```

如果标签打错了，也可以删除：

```plain
$ git tag -d v0.1
```

## 九 使用GitHub

你可以访问它的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：

```plain
git clone git@github.com:michaelliao/bootstrap.git
```

如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。

# PR：
