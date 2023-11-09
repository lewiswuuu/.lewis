# tmux

## 默认快捷键

==ctrl + b为prefix==

### session

```shell
tmux rename-session -t old_session_name new_session_name	# 修改session名
```

### window

```shell	
tmux rename-window -t target_window_index new_window_name	# 修改window名
```

## 自定义快捷键

==**alt + a为prefix**==

### session

```shell
alt + s			# 创建session
prefix + s		# 关闭session
prefix + r		# 修改session名称
prefix + L		# 列出所有session
alt + N			# 切换为下一个session
alt + P			# 切换为上一个session
```

### window

```shell
alt + w					# 创建window
prefix + w				# 关闭window
alt + 数字	   		   # 切换到数字对应的window
alt + p/n				# 切换到上一个/下一个window
alt + shift + 数字	   # 将当前的pane转移到对应数字的window
prefix + t				# 修改window名称
```

### pane

```shell
prefix + k/j/h/l		# 在上/下/左/右 创建pane
prefix + p				# kill pane
alt + b					# break pane
alt + k/j/h/l			# 向上/下/左/右 切换pane
prefix + 数字			   # 切换到数字对应的pane
alt + 空格			   # pane自动布局
```

# Git常用命令

## git config 

```shell
# 设置用户信息
git config --global user.name "xxx"			# 用户名
git config --global user.email "xxx@xxx"	# 用户邮箱
git config --global core.editor	"vim"		# 默认编辑器

# 查看配置信息
git config --global user.name
git config --global user.email
```

## git add

```shell
git add 文件名			# 将文件从工作区添加到缓存区
git add .			  # 将所有文件从工作区添加到缓存区
```

## git commit

```shell
git commit -m "commit message"		# 暂存区->本地仓库
git commit -am "commit message" = git add . + git commit -m "commit message"
```

## git status

查看状态

## git reset

```shell
git reset --hard <commitID>		# 版本回退
```

## git log

```shell
git log --all --abbrev-commit --graph --pretty=oneline		# 查看日志
# --all:显示所有分支	--abbrev-commit:精简显示commitID	--graph:以图的形式显示		--pretty=oneline:将提交信息显示为一行

git reflog		# 查看回退后的日志
```

## git branch

```shell
git branch			# 查看分支
git branch -d(D) <分支名>		# 删除(强制删除)分支
git branch -vv		# 查看分支,包括本地分支与远程分支的关联关系
git branch -m(M) main	# 重命名(强制重命名)当前分支为main
git branch -a			# 查看所有分支(包括远程非主分支)
```

## git checkout

```shell
git checkout -b <分支名>		# 新建分支并切换到该分支
git checkout <分支名>			# 切换分支
```

## git merge

```shell
git merge <分支名>			# 合并分支(首先切换到目标分支)
```

## git remote

```shell
git remote			# 查看远程仓库
git remote -v		# 查看远程仓库及路径
git remote add <远程仓库名(一般为origin)> <远程仓库地址>		# 关联本地仓库和远程仓库
git remote --set-url <远程仓库名(一般为origin)> <远程仓库地址>	# 设置远程仓库地址(一般为修改远程仓库地址用)
git remote rm <远程仓库名(一般为origin)>		# 移除远程仓库路径

git remote add upstream <远程仓库地址>		# 添加上游代码库
```

## git clone

```shell
git clone <远程仓库路径> [本地仓库名]		# 从远程仓库clone到本地(本地仓库不指定则与远程仓库名相同)
git clone -b 分支名 <远程仓库路径> [本地仓库名]	# 指定要clone的分支
```

## git push

```shell
git push [-f] [--set-upstream] [仓库路径(一般为origin)] [本地分支名(一般为master):远程分支名(一般为master)]	
# 将本地仓库推送至远程仓库	其中:-f(--force):强制推送    --set-upstream:将本地仓库与远程仓库关联(如果本地仓库与远程仓库已经关联,下次推送直接git push就可以)

git push -u origin master	# 如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push

git push --all origin		# 推送所有分支

git push -f origin local_branch:remote_brance	# 将本地分支(local_branch)推送到远程仓库的对应分支(remote_branch)
```

## git fetch

```shell
git fetch [远程仓库名] [分支名]		# 从远程仓库拉取更新到本地仓库,但是没有合并,故一般还需要git merge
```

## git pull

```shell
git pull = git fetch + git merge
```

## git tag

```shell
git tag		# 查看标签
```

## git stash

```shell
git stash save "Stashing local changes before merge(暂存信息)"
// 将本地修改暂存，就可以继续git pull了
git stash   # 功能同git stash save,只不过没有后面的注释

git stash apply  # 将之前暂存的修改重新应用到工作目录(一般是git pull后)
git stash pop  # 将之前暂存的修改重新应用到工作目录，和apply的差别在于，apply之后记录里还有，pop之后记录里没有了
git stash list  # 查看所有暂存的修改
git stash clear  # 清空所有暂存记录
```

## 本地Git和GitHub绑定

在push到GitHub前需先将Git和GitHub绑定:

1. 生成ssh key

   ```shell
   ssh-keygen -t rsa
   ```

   私钥和id_rsa和公钥默认生成在以下目录:

   - Linux:~/.ssh
   - Mac:~/.ssh
   - Windows:C\user\username\\.ssh

2. 把公钥id_rsa.pub的内容添加到GitHub的SSH and GPG Keys中，绑定完成后可通过`ssh -T git@github.com`测试

## git fatal:unable to access ...:Recv failure Connection was reset问题解决

```shell
git config --global --unset http.proxy
git config --global --unset https.proxy
```

[方法二](https://blog.csdn.net/m0_63230155/article/details/132070860)

# ssh

## ssh-keygen

```
ssh-keygen -t rsa -C "your_comment_here"

-C:指定自定义备注信息
-t选项:rsa(默认) dsa(已被认为不安全,不推荐) ecdsa ed25519
```



# vim常用命令

## vim自定义快捷键

```shell
S			# 保存
Q			# 退出
R			# 使更改的vimrc生效
空格 + 回车	 # 取消查找高亮

ctrl + i	# 光标移动到行尾
ctrl + n	# 光标移动到行首

# 分屏
sl			# 往右分屏
sh			# 往左分屏
sj			# 往下分屏
sk			# 网上分屏

空格 + l	   # 切到右边窗口
空格 + h	   # 切到左边窗口
空格 + j	   # 切到下边窗口
空格 + k	   # 切到上边窗口

↑/↓			# 改变上下分屏大小
←/→			# 改变左右分屏大小

sv			# 改为垂直分屏
sh			# 改为横向分屏

# 标签
tk			# 打开标签(上边)
th			# 打开标签(左边)
tl			# 打开标签(右边)
```



```shell
# <operation> <motion>

# operation
c			# 更改
d			# 删除(剪切)
y			# 复制


cw						# 更改当前词
ciw(change in word)		# 在词中更改当前词
ci"						# 更改""中的所有内容
di"
yi"

This is vim: the best editor out there.
fv				# find v
df:				# 删除:之前的内容
yf:
cf:

d$				# 删除当前光标到行尾的内容

:split			# 上下分屏
:vsplit(vs)		# 左右分屏

I		# 行首插入
A		# 行尾插入

G		# 到最后一行

# visual模式下 
选中多行	:normal Imy-wallpaper-
:normal A.png

# visual block  选中多行 + I   # 同时插入多行

e		# 打开文件

:r		# 从文件中读取内容并插入到当前编辑的文件中
!		# 执行bash命令
```

```shell
:vs		# 垂直分屏, ctrl + w l 光标右移, :e 打开
```

```c
// 导航与编辑
i			- 插前
a			- 附后
hjkl		- 左下上右
o			- 新增下一行
O			- 新增上一行

G			- 到最后一行
gg			- 到第一行
yy			- 复制当前行
dd			- 删除当前行
.			- 重复前次操作
u			- 撤销前次操作
ctrl+r		- 恢复前次操作
dw			- 删除单词
cw			- 改变单词
w			- 下个单词首部
e			- 下个单词尾部
b			- 上个单词首部

// 搜索、替换
/			- 搜索
:%s/旧/新/g  - 全局替换
yw			- 复制单词
p			- 粘贴
ci{			- 删除{}里的内容
ctrl+v		- 可视化块
shift+v		- 可视化行

e			- 在文件中打开另一文件
w			- 保存
w a.c	  	- 打开新文件(文件名为a.c)
```

## vimrc常用配置

```
syntax on		- 开启语法高亮。
set ts=4		- 设置制表符的宽度为4个空格。这样，当用户按下Tab键时，将插入四个空格而不是制表符。
set expandtab	- 将制表符自动转换为空格。这个选项指定，当用户插入制表符时，Vim会自动将其转换为一定数量的空格，从而确保不同编辑器中的代码缩进看起来一致。
set autoindent	- 开启自动缩进。这个选项指定，当用户按下回车键时，Vim会自动缩进到当前行的缩进级别，从而让代码更加整齐。
set number		- 显示行号。这个选项指定，Vim会在每一行的左侧显示行号，从而方便用户在代码中进行定位和调试。
```

## 按字符、单词和标记移动

```
h	- 向左移动光标
j	- 向下移动光标
k	- 向上移动光标
l	- 向右移动光标

b	- 移动到单词的开头
B	- 移动到标记的开头
w	- 移动到下一个单词的开头
W	- 移动到下一个标记的开头
e	- 移动到单词末尾
E	- 移动到标记末尾
```

## 按行移动

```
按第0行(零)移动	- 跳到行的开头
$				- 跳到行尾
^				- 跳转到行的第一个(非空白)字符
#G/#gg/:#		- 移动到指定的行号(用行号替换#)
```

## 按屏幕移动

```
ctrl+b	- 向后移动一个全屏
ctrl+f	- 向前移动一个全屏
ctrl+d	- 向前移动1/2屏幕
ctrl+u	- 向后移动1/2屏幕
ctrl+e	- 向下移动屏幕一行(不移动光标)
ctrl+y	- 向上移动屏幕一列(不移动鼠标)
ctrl+o	- 向后移动跳转历史
ctrl+i	- 向前移动跳转历史

H		- 移至屏幕顶部(H=高)
M		- 移至屏幕中部(M=中)
L		- 移至屏幕底部(L=低)
```

## 插入文本

```
i	- 切换到光标前的插入模式
I	- 在行首插入文本
a	- 切换到光标后的插入模式
A	- 在行末尾插入文本
o	- 在当前行下方打开新行
O	- 在当前行上方打开新行
ea	- 在单词末尾插入文本
Esc	- 退出插入模式
:	- 切换到命令模式
```

## 编辑文本

```
r		- 替换单个字符(并返回到命令模式)
cc		- 替换整行(删除该行并移动到插入模式)
C/c$	- 从光标替换到行尾
cw		- 从光标更换到单词结尾
s		- 删除字符(并移动到输入模式)
J		- 将下面的行合并到当前行，中间留有空格
gJ		- 合并将下面的行移到当前行，其间没有空格
u		- undo
ctrl+r	- redo
.		- 重复上一命令
```

## 剪切、复制和粘贴

```
yy	- 复制整行
#yy	- 复制指定行数
dd	- 剪切(删除)整行
#dd	- 剪切指定的行数
p	- 粘贴在光标之后
P	- 粘贴在光标之前
```

## 在文件中搜索

```
*			- 跳转到当前单词的下一个实例
#			- 跳转到当前单词的上一个实例
/pattern	- 向前搜索指定的模式
?pattern	- 向后搜索指定的模式
n			- 沿相同方向重复搜索
N			- 沿相反方向重复搜索
```

## 保存和退出文件

```
:w					- 保存文件但保持打开
:wq					- 保存并关闭文件
:q					- 退出
:q!					- 退出而不保存更改
shift+zz			- 保存文件并退出
:w new_file_name	- 以新名称保存文件并继续编辑原始文件
:sav				- 以新名称保存文件并继续编辑新副本
:w! sudo tee%		- 使用sudo和tee命令写出文件
:e new_file_name	- 编辑新文件
```

## 标记文本(视觉模式)

```
v		- 使用字符模式选择文本
V		- 使用行模式选择行
ctrl+v	- 使用块模式选择文本
启用其中一种模式后，使用导航键选择所需的文本。

o		- 从所选文本的一端移动到另一端
aw		- 选择单词
ab		- 选择带有()
aB的块   - 选择带有{}的块
at		- 使用<>选择块
ib		- 使用()
iB选择内部块	- 使用{}选择内部块
it		- 使用<>选择内部块
```

## 视觉命令

```
y	- 拖动(复制)标记文本
d	- 删除(剪切)标记文本
p	- 粘贴光标后的文本
u	- 将市场文本更改为小写
U	- 将市场文本更改为大写
```

## 替换

```
:s/old/new			- 替换第一个匹配到的词
:%s/old/new/g		- 替换所有(/g可不加)(加i标志可忽略大小写,如/gi)
```

# UEFI

```shell
build -a X64 -p edk2/MdeModulePkg/MdeModulePkg.dsc -m edk2/MdeModulePkg/Application/HelloWorld/HelloWorld.inf -t GCC5 -b DEBUG
```



# Windows常用cmd命令

## 查看电脑连接过的所有WiFi及密码

```
netsh wlan show profiles
netsh wlan show profile name="WiFi名称" key=clear
```

## 查看IP地址

```
ipconfig
ipconfig /all
```

## 查看外网地址

```
curl -L ip.tool.lu
```

## 检测当前电脑系统的磁盘文件

```
chkdsk				- 检测
chkdsk /r			- 修复
chkdsk				- 检测所有硬盘
```

## 通过ping来检测当前网络或者VPS 服务器有没有发生网络故障

```
ping IP地址
ping IP地址 -t	- 持续检测
```

## 远程桌面控制器

```
mstsc
```

## 打开电脑的性能监测

```
perfmon.msc
```

## 查看当前电脑上所有的用户

```
net user
net user 用户名 /del	- 删除用户
```

## 扫描系统

```
sfc /scannow
```

## 定时关机

```
shutdown /s /t 定时关机的时间(s)
shutdown /s /t 300	- 300s定时关机
shutdown /a			- 取消定时关机任务
```

# Linux常用命令

```shell
neofetch
ps -aux
ps -ef
	-a 显示所有用户的进程，不仅仅是当前用户的进程。
	-u 以用户为主的格式显示进程信息。
	-x 显示没有控制终端的进程。
	
	-e 显示所有进程，包括没有控制终端的进程。
	-f 完整格式显示进程信息。
netstat -nltp	
netstat -anp
	-a 显示所有(显示所有socket)
	-n 参数指定以数字形式显示IP地址和端口号，而不是以名称形式显示。
	-l 参数指定只显示正在监听的连接。
	-t 参数指定只显示TCP连接，而不显示UDP连接。
	-p 参数指定显示与网络连接关联的进程（程序）信息。
	-u 显示UDP协议传输的socket信息
	
echo $$  # 查看当前进程id
```

## Linux基础命令

### Linux的目录结构

![image-20221027214128453](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011337.png)

- `/`，根目录是最顶级的目录了
- Linux只有一个顶级目录：`/`
- 路径描述的层次关系同样适用`/`来表示
- /home/itheima/a.txt，表示根目录下的home文件夹内有itheima文件夹，内有a.txt

### ls命令

功能：列出文件夹信息

语法：`ls [-l -h -a] [参数]`

- 参数：被查看的文件夹，不提供参数，表示查看当前工作目录
- -l，以列表形式查看
- -h，配合-l，以更加人性化的方式显示文件大小
- -a，显示隐藏文件

**隐藏文件、文件夹**

在Linux中以`.`开头的，均是隐藏的。

默认不显示出来，需要`-a`选项才可查看到。

### pwd命令

功能：展示当前工作目录

语法：`pwd`

### cd命令

功能：切换工作目录

语法：`cd [目标目录]`

参数：目标目录，要切换去的地方，不提供默认切换到`当前登录用户HOME目录`

### HOME目录

每一个用户在Linux系统中都有自己的专属工作目录，称之为HOME目录。

- 普通用户的HOME目录，默认在：`/home/用户名`

- root用户的HOME目录，在：`/root`



FinalShell登陆终端后，默认的工作目录就是用户的HOME目录

#### 相对路径、绝对路径

- 相对路径，==非==`/`开头的称之为相对路径

  相对路径表示以`当前目录`作为起点，去描述路径，如`test/a.txt`，表示当前工作目录内的test文件夹内的a.txt文件

- 绝对路径，==以==`/`开头的称之为绝对路径

  绝对路径从`根`开始描述路径

#### 特殊路径符

- `.`，表示当前，比如./a.txt，表示当前文件夹内的`a.txt`文件
- `..`，表示上级目录，比如`../`表示上级目录，`../../`表示上级的上级目录
- `~`，表示用户的HOME目录，比如`cd ~`，即可切回用户HOME目录

### mkdir命令

功能：创建文件夹

语法：`mkdir [-p] 参数`

- 参数：被创建文件夹的路径
- 选项：-p，可选，表示创建前置路径

### touch命令

功能：创建文件

语法：`touch 参数`

- 参数：被创建的文件路径

### cat命令

功能：查看文件内容

语法：`cat 参数`

- 参数：被查看的文件路径

### more命令

功能：查看文件，可以支持翻页查看

语法：`more 参数`

- 参数：被查看的文件路径
- 在查看过程中：
  - `空格`键翻页
  - `q`退出查看

### cp命令

功能：复制文件、文件夹

语法：`cp [-r] 参数1 参数2`

- 参数1，被复制的
- 参数2，要复制去的地方
- 选项：-r，可选，复制文件夹使用

示例：

- cp a.txt b.txt，复制当前目录下a.txt为b.txt
- cp a.txt test/，复制当前目录a.txt到test文件夹内
- cp -r test test2，复制文件夹test到当前文件夹内为test2存在

### mv命令

功能：移动文件、文件夹

语法：`mv 参数1 参数2`

- 参数1：被移动的
- 参数2：要移动去的地方，参数2如果不存在，则会进行改名

### rm命令

功能：删除文件、文件夹

语法：`rm [-r -f] 参数...参数`

- 参数：支持多个，每一个表示被删除的，空格进行分隔
- 选项：-r，删除文件夹使用
- 选项：-f，强制删除，不会给出确认提示，一般root用户会用到



> rm命令很危险，一定要注意，特别是切换到root用户的时候。

### which命令

功能：查看命令的程序本体文件路径

语法：`which 参数`

- 参数：被查看的命令

### find命令

功能：搜索文件

语法1按文件名搜索：`find 路径 -name 参数`

- 路径，搜索的起始路径
- 参数，搜索的关键字，支持通配符*， 比如：`*`test表示搜索任意以test结尾的文件

### grep命令

功能：过滤关键字

语法：`grep [-n] 关键字 文件路径`

- 选项-n，可选，表示在结果中显示匹配的行的行号。
- 参数，关键字，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用””将关键字包围起来
- 参数，文件路径，必填，表示要过滤内容的文件路径，可作为内容输入端口



> 参数文件路径，可以作为管道符的输入

### wc命令

功能：统计

语法：`wc [-c -m -l -w] 文件路径`

- 选项，-c，统计bytes数量
- 选项，-m，统计字符数量
- 选项，-l，统计行数
- 选项，-w，统计单词数量
- 参数，文件路径，被统计的文件，可作为内容输入端口



> 参数文件路径，可作为管道符的输入

### 管道符|

写法：`|`

功能：将符号左边的结果，作为符号右边的输入

示例：

`cat a.txt | grep itheima`，将cat a.txt的结果，作为grep命令的输入，用来过滤`itheima`关键字



可以支持嵌套：

`cat a.txt | grep itheima | grep itcast`

### echo命令

功能：输出内容

语法：`echo 参数`

- 参数：被输出的内容

### `反引号

功能：被两个反引号包围的内容，会作为命令执行

示例：

- echo \`pwd\`，会输出当前工作目录

### tail命令

功能：查看文件尾部内容

语法：`tail [-f] 参数`

- 参数：被查看的文件
- 选项：-f，持续跟踪文件修改

### head命令

功能：查看文件头部内容

语法：`head [-n] 参数`

- 参数：被查看的文件
- 选项：-n，查看的行数

### 重定向符

功能：将符号左边的结果，输出到右边指定的文件中去

- `>`，表示覆盖输出
- `>>`，表示追加输出

### vi编辑器

#### 命令模式快捷键

![image-20221027215841573](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011279.png)

![image-20221027215846581](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011352.png)

![image-20221027215849668](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011315.png)

#### 底线命令快捷键

![image-20221027215858967](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011290.png)

### 命令的选项

我们学习的一系列Linux命令，它们所拥有的选项都是非常多的。

比如，简单的ls命令就有：-a -A -b -c -C -d -D -f -F -g -G -h -H -i -I -k -l -L -m -n -N -o -p -q -Q -r-R -s -S -t -T -u -U -v -w -x -X -1等选项，可以发现选项是极其多的。

课程中， 并不会将全部的选项都进行讲解，否则，一个ls命令就可能讲解2小时之久。

课程中，会对常见的选项进行讲解， 足够满足绝大多数的学习、工作场景。

### 查看命令的帮助

可以通过：`命令 --help`查看命令的帮助手册

![image-20221027220005610](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011594.png)

### 查看命令的详细手册

可以通过：`man 命令`查看某命令的详细手册

![image-20221027220009949](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011160.png)

## Linux常用操作

### 各类小技巧快捷键

```c
ctrl + c		// 强制停止
ctrl + d		// 退出账户的登录(不能用于退出vi/vim) 
history			// 查看历史输入过的命令
光标移动快捷键：
    ctrl + a			跳到命令开头
    ctrl + e			跳到命令结尾
    ctrl + 键盘左键		 向左跳一个单词
    ctrl + 键盘右键		 向右跳一个单词
ctrl + l		// 清空终端内容
clear			// 清空终端内容
```

### 软件安装

- CentOS系统使用：
  - yum [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索
    - -y，自动确认
- Ubuntu系统使用
  - apt [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索
    - -y，自动确认

> yum 和 apt 均需要root权限

### systemctl

功能：控制系统服务的启动关闭等

语法：`systemctl start | stop | restart | disable | enable | status 服务名`

- start，启动
- stop，停止
- status，查看状态
- disable，关闭开机自启
- enable，开启开机自启
- restart，重启

### 软链接

功能：创建文件、文件夹软链接（快捷方式）

语法：`ln -s 参数1 参数2`

- 参数1：被链接的
- 参数2：要链接去的地方（快捷方式的名称和存放位置）

### 日期

语法：`date [-d] [+格式化字符串]`

- -d 按照给定的字符串显示日期，一般用于日期计算

- 格式化字符串：通过特定的字符串标记，来控制显示的日期格式
  - %Y   年%y   年份后两位数字 (00..99)
  - %m   月份 (01..12)
  - %d   日 (01..31)
  - %H   小时 (00..23)
  - %M   分钟 (00..59)
  - %S   秒 (00..60)
  - %s   自 1970-01-01 00:00:00 UTC 到现在的秒数



示例：

- 按照2022-01-01的格式显示日期

  ![image-20221027220514640](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011959.png)

- 按照2022-01-01 10:00:00的格式显示日期

  ![image-20221027220525625](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011130.png)

- -d选项日期计算

  ![image-20221027220429831](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011897.png)

  - 支持的时间标记为：

    ![image-20221027220449312](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011015.png)

### 时区

修改时区为中国时区

![image-20221027220554654](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011179.png)

### ntp

功能：同步时间

安装：`yum install -y ntp`

启动管理：`systemctl start | stop | restart | status | disable | enable ntpd`



手动校准时间：`ntpdate -u ntp.aliyun.com`

### ip地址

格式：a.b.c.d

- abcd为0~255的数字



特殊IP：

- 127.0.0.1，表示本机
- 0.0.0.0
  - 可以表示本机
  - 也可以表示任意IP（看使用场景）



查看ip：`ifconfig`

### 主机名

功能：Linux系统的名称

查看：`hostname`

设置：`hostnamectl set-hostname 主机名`

### 配置VMware固定IP

1. 修改VMware网络，参阅PPT，图太多

2. 设置Linux内部固定IP

   修改文件：`/etc/sysconfig/network-scripts/ifcfg-ens33`

   示例文件内容：

   ```shell
   TYPE="Ethernet"
   PROXY_METHOD="none"
   BROWSER_ONLY="no"
   BOOTPROTO="static"			# 改为static，固定IP
   DEFROUTE="yes"
   IPV4_FAILURE_FATAL="no"
   IPV6INIT="yes"
   IPV6_AUTOCONF="yes"
   IPV6_DEFROUTE="yes"
   IPV6_FAILURE_FATAL="no"
   IPV6_ADDR_GEN_MODE="stable-privacy"
   NAME="ens33"
   UUID="1b0011cb-0d2e-4eaa-8a11-af7d50ebc876"
   DEVICE="ens33"
   ONBOOT="yes"
   IPADDR="192.168.88.131"		# IP地址，自己设置，要匹配网络范围
   NETMASK="255.255.255.0"		# 子网掩码，固定写法255.255.255.0
   GATEWAY="192.168.88.2"		# 网关，要和VMware中配置的一致
   DNS1="192.168.88.2"			# DNS1服务器，和网关一致即可
   ```

### ps命令

功能：查看进程信息

语法：`ps -ef`，查看全部进程信息，可以搭配grep做过滤：`ps -ef | grep xxx`

### kill命令

![image-20221027221303037](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011542.png)

### nmap命令

![image-20221027221241123](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011698.png)

### netstat命令

功能：查看端口占用

用法：`netstat -anp | grep xxx`

### ping命令

测试网络是否联通

语法：`ping [-c num] 参数`

![image-20221027221129782](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011748.png)

### wget命令

![image-20221027221148964](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011887.png)

### curl命令

![image-20221027221201079](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011812.png)

![image-20221027221210518](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011803.png)

### top命令

功能：查看主机运行状态

语法：`top`，查看基础信息



可用选项：

![image-20221027221340729](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011431.png)



交互式模式中，可用快捷键：

![image-20221027221354137](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011418.png)

### df命令

查看磁盘占用

![image-20221027221413787](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011509.png)

### iostat命令

查看CPU、磁盘的相关信息

![image-20221027221439990](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011604.png)

![image-20221027221514237](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011619.png)

### sar命令

查看网络统计

![image-20221027221545822](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011636.png)

### 环境变量

- 临时设置：export 变量名=变量值
- 永久设置：
  - 针对用户，设置用户HOME目录内：`.bashrc`文件
  - 针对全局，设置`/etc/profile`

### PATH变量

​	记录了执行程序的搜索路径

​	可以将自定义路径加入PATH内，实现自定义命令在任意地方均可执行的效果

​	如export PATH=$PATH:自定义路径

配置完成后，通过source命令立刻生效

### $符号

可以取出指定的环境变量的值

语法：`$变量名`

示例：

`echo $PATH`，输出PATH环境变量的值

`echo ${PATH}ABC`，输出PATH环境变量的值以及ABC

如果变量名和其它内容混淆在一起，可以使用${}

### 压缩解压

#### 压缩

`tar -zcvf 压缩包 被压缩1...被压缩2...被压缩N`

- -z表示使用gzip，可以不写，不使用-z就是普通的tarball格式
- -c，创建压缩文件，用于压缩模式
- -v，显示压缩、解压过程，用于查看进度
- -x，解压模式
- -f，要创建的文件，或要解压的文件，-f选项必须在所有选项中位置处于最后一个
- -C，选择解压的目的地，用于解压模式

```c
tar -cvf test.tar 1.txt 2.txt 3.txt			// 将1.txt 2.txt 3.txt压缩到test.tar文件内
tar -zcvf test.tar.gz 1.txt 2.txt 3.txt		// 将1.txt 2.txt 3.txt压缩到test.tar.gz文件内，使用gzip模式
    -z选项如果使用的话，一般位于选项位第一个
    -f选项必须在选项位最后一个
```



`zip [-r] 参数1 参数2 参数N`

![image-20221027221906247](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011041.png)

#### 解压

`tar -zxvf 被解压的文件 -C 要解压去的地方`

- -z表示使用gzip，可以省略
- -C，可以省略，指定要解压去的地方，不写解压到当前目录







`unzip [-d] 参数`

![image-20221027221939899](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011981.png)

### su命令

切换用户

语法：`su [-] [用户]`

![image-20221027222021619](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011022.png)

### sudo命令

![image-20221027222035337](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011345.png)



比如：

```shell
itheima ALL=(ALL)       NOPASSWD: ALL
```

在visudo内配置如上内容，可以让itheima用户，无需密码直接使用`sudo`

### chmod命令

修改文件、文件夹权限



语法：`chmod [-R] 权限 参数`

- 权限，要设置的权限，比如755，表示：`rwxr-xr-x`

  ![image-20221027222157276](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011305.png)

- 参数，被修改的文件、文件夹

- 选项-R，设置文件夹和其内部全部内容一样生效

### chown命令

修改文件、文件夹所属用户、组



语法：`chown [-R] [用户][:][用户组] 文件或文件夹`

![image-20221027222326192](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011618.png)

### 用户组管理

![image-20221027222354498](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011549.png)

### 用户管理

![image-20221027222407618](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011696.png)

### getenv命令

- `getenv group`，查看系统全部的用户组

  ![image-20221027222446514](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011754.png)

- `getenv passwd`，查看系统全部的用户

  ![image-20221027222512274](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011003.png)

### env命令

查看系统全部的环境变量

语法：`env`

## 设置静态IP

1、`route -n`：查看路由表(查看网关地址)

2、`vim /etc/network/interfaces`

```
# 文件中添加
auto ens33
iface ens33 inet static
address xxx.xxx.xxx.xxx
netmask 255.255.255.0
gateway xxx.xxx.xxx.xxx
```

3、刷新ip

```shell
sudo ip addr flush ens33
sudo systemctl restart networking.service
```

4、设置DNS `vim etc/systemd/resolved.conf`

```
# 文件中添加
[Resolve]
DNS=xxx.xxx.xxx xxx.xxx.xxx.xxx		# 可以是网关地址(223.5.5.5)
```

5、重启systemd-resolved服务

`sudo systemctl restart systemd-resolved.service`

## 每天一个Linux命令

### awk

![](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011690.png)

### grep

![image-20230816002027297](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011014.png)

### Linux常用快捷键

![image-20230816003821034](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308180011120.png)

### useradd

![](https://picgo46.oss-cn-shenzhen.aliyuncs.com/img/202308202257802.png)





















