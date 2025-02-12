---
title: "Git 技巧"
description: "Git 技巧"
date: "2023-12-15"
tags:
  - git
---

## Git Rebase

提交代码时，我曾经使用随意消息，但发现这不是一个好习惯。所以我想删除该提交。我找到了以下命令。

首先，使用git日志查找要更改的提交的提交哈希，并运行以下命令：

```
git rebase -i <casual-message-commit-hash>~2
```

然后，git 将打开待办事项编辑器，你可以更改每个提交的操作。在那里，我们只需要找到要删除的提交的哈希，然后将其前面的动作从 `pick` 改为 `fixup`。

然后保存并退出。
此操作将使它与父提交合并，使用父提交的提交信息。最后，使用 `git push -f` 将代码推向远程。

或者，可以使用 `sqush` 或 `reword` 而不是 `fixup`

这是 `rebase` 中的所有命令：

```
Commands:
p, pick <commit> = use commit
r, reword <commit> = use commit, but edit the commit message
e, edit <commit> = use commit, but stop for amending
s, squash <commit> = use commit, but meld into previous commit
f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
                   commit's log message, unless -C is used, in which case
                   keep only this commit's message; -c is same as -C but
                   opens the editor
x, exec <command> = run command (the rest of the line) using shell
b, break = stop here (continue rebase later with 'git rebase --continue')
d, drop <commit> = remove commit
l, label <label> = label current HEAD with a name
t, reset <label> = reset HEAD to a label
m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
        create a merge commit using the original merge commit's
        message (or the oneline, if no original merge commit was
        specified); use -c <commit> to reword the commit message
u, update-ref <ref> = track a placeholder for the <ref> to be updated
                      to this position in the new commits. The <ref> is
                      updated at the end of the rebase

These lines can be re-ordered; they are executed from top to bottom.

If you remove a line here THAT COMMIT WILL BE LOST.

However, if you remove everything, the rebase will be aborted.

```
