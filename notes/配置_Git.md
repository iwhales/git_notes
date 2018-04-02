# 配置 Git

`git config` 用于获取和设置“配置变量”，以控制 Git 的外观和操作方式。

这些变量被存储在三个不同的位置：

1. `/etc/gitconfig` ：系统级配置文件，该配置对系统中的每个用户创建的仓库均有效。如果在 `git config` 中添加 `--system` ，便可读写该文件。此配置需要管理员或超级用户权限。
   Win 会在 Git 的安装目录中查找该文件，即 `Git\mingw64\etc\gitconfig` 。如果 Win 上的 Git 高于 2.x 版本，那么还存在另一个系统级配置文件：XP 中位于 `C:\Documents and Settings\All Users\Application Data\Git\config` ；Vista 之后的系统位于 `C:\ProgramData\Git\config` 。该文件需要以管理员身份执行 `git config -f <file>` 才能修改。
2. `~/.gitconfig` 或 `~/.config/git/config` ：用户级配置文件，通过 `--global` 可读写该文件。
   Win 会在 `$HOME`（即 `C:\Users\$USER`）中查找该文件。
3.  `.git/config`：项目级配置文件，仅针对当前仓库。

参数优先级：项目级>用户级>系统级，因此“项目级”中的值会覆盖“系统级”中的值。

## 配置用户信息

```bash
# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

## 配置文本编辑器 

当 Git 需要我们输入信息时，便会调用默认的文本编辑器。如果没有配置默认编辑器，Git 将使用系统默认的编辑器。

```bash
# 配置编辑器为emacs
$ git config --global core.editor emacs 
```

在 Windows 系统中配置此项时，必须填写编辑器可执行文件的完整路径。同时由于编辑器打包方式的差异，所以具体参数可能会有差异。示例如下：

```bash
# 在64(32)位系统中配置64(32)位Notepad++
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"
# 在64位系统中配置32位Notepad++
$ git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```

## 编辑和查看

```bash
# 在编辑器中编辑Git配置文件
$ git config -e [--global]

# 查看配置信息列表
# 部分key-value对可能多次出现，这是因为Git会冲不同的文件中读取相同的key，
# 比如会从/etc/gitconfig和~/.gitconfig中读取相同的key，
# 但是Git会使用每个key的最后一个值。
$ git config [--global] --list

# 查看某个key的配置信息
$ git config <key>
$ git config user.name
John Doe

# 查看某个key的所属文件和配置信息
$ git config --show-origin core.editor
file:.git/config        'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession
```

## 别名

当我们只输入部分命令时，Git 并不会自动推测我们需要命令。如果想简写某个命令，可通过 `git config alias` 为命令配置别名(alias)。
如果以原本已存在的 Git 命名名作为别名(如 `git config alias.add status`)，此时原命令不会被视作别名，依旧保持原有含义。
通过 `git config alias` 配置别名时，如果试图为两个不同的命令配置相同的别名，那么第一次的配置会被第二次的配置覆盖。

```bash
# 配置别名，也可通过配置文件手动配置
$ git config [--global] alias.co checkout
$ git config [--global] alias.br branch
$ git config [--global] alias.ci commit
$ git config [--global] alias.st status

$ git config --global alias.unstage 'reset HEAD --'
$ git config --global alias.unstage 'reset HEAD'

$ git config --global alias.last 'log -1 HEAD'
$ git config --global alias.last 'log -1'

$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# 配置外部命令的别名，需以!作为外部命令的前缀
# 外部命令不是Git的子命令
$ git config --global alias.visual '!gitk'

# 删除别名，也可通过配置文件手动删除
$ git config [--global] --unset alias.shortname
```

## 其它

```bash
# 设置显示颜色，让输出更醒目
$ git config --global color.ui true

# 显示中文文件名
# https://blog.csdn.net/hawkdowen/article/details/38585949
# https://blog.csdn.net/zhanlanmg/article/details/49862779
$ git config --global core.quotepath false  
$ git config core.quotepath false 
```

