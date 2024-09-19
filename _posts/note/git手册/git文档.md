#### 设置默认的git默认编辑器
git config --global core.editor "'D:\tool\Notepad++\notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
#### 检查配置信息
如果想要检查你的配置，可以使用 git config --list 命令来列出所有 Git 当时能找到的配置
#### git help config
可以跳转到**配置命令**帮助网站

### 如何初始化一个git仓库
#### 在本地已存在的目录初始化一个git
1. cd 目的目录
2. 执行git init (仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪。)

#### 从服务器上clone一个git仓库

1. cd 目的目录
2. 执行git clone <url> (这个命令会在本地创建一个目录，目录名字就是仓库名字，然后把远程仓库的所有数据拉下来放到这个目录里。)

### 查看git仓库的状态
#### 几种状态
| 状态 | 说明 |
| :--- | :--- |
| Untracked | 未跟踪 |
| Unmodified | 未修改 |
| Modified | 已修改 |
| Staged | 已暂存 |
#### 查看当前仓库的状态
1. cd 目的目录
2. git status on branch <分支名>
3. git status -s (简化版)
#### 在仓库里面跟踪文件
git add <文件名>

### 忽略文件
https://github.com/github/gitignore

### 查看已暂存和未暂存的修改
#### git diff 比较的是工作目录中当前文件和暂存区域快照之间的差异
#### git diff --staged | --cached 比较的是已暂存的将要添加到下次提交里的内容

### 提交更新
#### git commit -m <message> 提交暂存区域的文件
#### git commit -a -m <message> 提交工作目录自上次commit之后的变化，直接跳过git add步骤
#### git rm <file> 暂存区域中删除文件
##### 例子：git rm log/\*.log
不小心把log目录下的所有.log文件都添加到暂存区域了，现在想要不提交，但是保存在本地目录，并且下次提交的时候不再跟踪这些文件。
### 将文件改名
git mv <oldfile> <newfile>
#### 三步操作
1. mv <oldfile> <newfile>
2. git rm <oldfile>
3. git add <newfile>
### 查看提交历史
#### git log
| 选项 | 说明 |
| :--- | :--- |
| -p | 按补丁格式显示每个更新之间的差异 |
| --stat | 显示每次更新的文件修改统计信息 |
| --shortstat | 只显示 --stat 中最后的行数修改添加移除统计 |
| --name-only | 仅在提交信息后显示已修改的文件清单 |
| --name-status | 显示新增、修改、删除的文件清单 |
| --abbrev-commit | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符 |
| --relative-date | 使用较短的相对时间显示（比如，“2 weeks ago”） |
| --graph | 显示 ASCII 图形表示的分支合并历史 |
| --pretty | 使用其他格式显示历史提交信息。可用的选项包括 oneline、short、full、fuller 和 format（后跟指定格式） |
| --oneline | --pretty=oneline --abbrev-commit 合并使用 |
| --no-merges | 不显示合并提交 |
| --decorate | 显示标签、HEAD 指针等引用的名称 |
| --color | 启用色彩显示 |
| --all | 显示所有分支（默认仅显示当前分支） |
| --author=<pattern> | 仅显示作者符合指定模式的提交 |
| --committer=<pattern> | 仅显示提交者符合指定模式的提交 |
| --grep=<pattern> | 仅显示提交说明符合指定模式的提交 |
| --since=<date> | 仅显示指定时间之后的提交。格式可以是“2008-01-15”、“2 years 1 day 3 minutes ago”等 |
| --until=<date> | 仅显示指定时间之前的提交 |

##### --pretty选项
| 选项 | 说明 |
| :--- | :--- |
| oneline | 每个提交放在一行显示 |
| short | 显示40个字符的SHA-1值和提交说明 |
| full | 显示所有提交信息 |
| fuller | 显示完整的提交信息 |
| format | 指定格式 |
##### format选项
| 选项 | 说明 |
| :--- | :--- |
| %H | 提交对象（commit）的完整哈希字串 |
| %h | 提交对象的简短哈希字串 |
| %T | 树对象（tree）的完整哈希字串 |
| %t | 树对象的简短哈希字串 |
| %P | 父对象（parent）的完整哈希字串 |
| %p | 父对象的简短哈希字串 |
| %an | 作者（author）的名字 |
| %ae | 作者的电子邮件地址 |
| %ad | 作者修订日期（可以用 --date=选项定制格式） |
| %ar | 作者修订日期，按多久以前的方式显示 |
| %cn | 提交者(committer)的名字 |
| %ce | 提交者的电子邮件地址 |
| %cd | 提交日期 |
| %cr | 提交日期，按多久以前的方式显示 |
| %s | 提交说明 |
#### 查看最近两次提交 git log -p -2

























