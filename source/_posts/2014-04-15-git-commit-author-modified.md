title: (转)修正 Git 提交信息

date: 2014-04-15 08:54:47

tags: [Github, 效率]

categories: 
- Git


---
转自
>http://geeplanet.com/articles/git-commit-author-modified/

使用 Git 偶尔会由于更改自己的 ssh key 而忘记重新配置 user.name 和 user.email，所以会导致 Github 上面无法将这些 commit 识别为正确的 Github 用户。因此在查看 Graph 页面时，会发现自己的 contribute to master 为0！是不是心很痛，写了半天发现自己木有任何贡献。

据查到的资料显示，`git filter-branch`这个命令就可以很好地处理这个问题，在给出解决办法前，先确认一下问题的根本来源。可以使用`git rev-list`这个命令来查看详细的提交信息。

<!-- more -->

查看详细提交信息
-------
```bash
git rev-list --all --pretty=full
```
说明：
- `--all`是指全部commit
- `pretty=full` 是指输出格式，为全部内容 (full)


结果：（只截取了一条 commit log）

```bash
commit a198aaf5cf1ea73cf727efd35d5b92c43c4303bf
Author: Gnnng <gnnnnng@gmail.com>
Commit: Gnnng <gnnnnng@gmail.com>

init the repo

```

更改提交信息
------

如果上述的 author 或者 commit 后面的信息不正确的话，我们可以通过 `git filter-branch` 来解决（只需要保证 email 字段正确即可被 Github 识别）。


```bash
git filter-branch --env-filter '
  if test "$GIT_AUTHOR_EMAIL" = "Old-email"
then
  GIT_AUTHOR_EMAIL=New-email
  export GIT_AUTHOR_EMAIL
fi
if test "$GIT_COMMITTER_EMAIL" = "Old-email"
then
  GIT_COMMITTER_EMAIL=New-email
  export GIT_COMMITTER_EMAIL
fi
' -- --all

```
以上命令同时修改了 author 和 committer 两个信息（虽然目前还不知道这两个“角色”分别代表了什么）

最后
------
只需要强力 push 一下就好了，当然如果不放心的话可以先 push 一个分支，检查之后再 push 到 master 上。

```bash
# 直接强行 Push
git push -f

# 先 push 一个分支
git push origin master:change

# 没问题之后，可以删除掉远程分支
git push origin :change

```
