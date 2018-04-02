# Patching

## cherry-pick

cherry-pick 会重演指定的 commit，也就是把某个 commit 中的内容在当前分支上重新提交一遍。新 commit 与原 commit 拥有不同的 ID 号，也不会将原 commit 视作父节点——下图中 `f142b` 仅将 `ed489` 视作父节点，这点与 merge 有明显区别。如果提交过程中出现冲突，则需要手动修改。如果没有冲突，则会保留原 commit 中的说明信息。cherry-pick 可用于不同分支，也可用于同一分支。

```bash
# 衍合1或多个commit到前分支中
$ git cherry-pick [commit...]
```

![herry-pick_](C:\Users\iwhal\Documents\GitHub\git_notes\images\cherry-pick_1.png)

参考：
[git cherry-pick用法](https://www.jianshu.com/p/d577dcc36a08)
[git cherry-pick 小结](https://blog.csdn.net/wh_19910525/article/details/7554430)

## rebase

```bash
# 重定位当前分支的基底，将当前分支在目标分支上重演
$ git rebase [-i] <branch>

# 重定位当前分支的基底，将当前分支中<newbase>之后的commit在目标分支上重演
$ git rebase <branch> [-i] [--onto <newbase>]

# [-i]:交互模式
```

`rebase` 与 `merge` 的区别在于，`merge` 产生的历史记录是非线性的。`rebase` 会在目标分支上重演当前分支中的 commit，留下线性历史记录。
`rebase` 命令本质上可看一个自动化的 `cherry-pick` 命令。`rebase` 命令会自动获取一系列需要重演的 commit，然后在目标分支上逐个 `cherry-picks` 这些 commit。

下图中的命令，会获取所有存在于当前分支(topic)中的 commit，并在目标分支 master 中重演这些 commit。是将当前分支的 commit 在目标分支中逐个重演，而非从目标分支获取 commit 在当前分支重演，使用时一定要注意。注意，如果不存在对旧的 commit 的引用，那么它们将被垃圾回收。

![ebase_](C:\Users\iwhal\Documents\GitHub\git_notes\images\rebase_1.png)

使用 `--onto` 选项可限制重演的范围。下图中的命令会在 master 分支中重演当前分支中 169a6 之后的 commit。

![ebase_](C:\Users\iwhal\Documents\GitHub\git_notes\images\rebase_2.png)

注意：永远不要在公有分支上使用 `rebase` 命令。

参考：
[译：Git rebase VS. Git merge](https://www.jianshu.com/p/318b4f0f57ff)
[git rebase简介(基本篇)](https://www.jianshu.com/p/c92f552da60c)