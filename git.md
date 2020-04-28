---
title: git
description: Some usefull git's command
published: true
date: 2020-04-28T21:48:09.736Z
tags: 
---

# Git

## Usefull commans

* Delete a local branch without checking status (merged or not)

```shell
git branch -D branchname
```

* Save credential each time needed for one hour

```shell
git config --global credential.helper 'cache --timeout=3600'
```

* Delete a remote branch

```shell
git push remote_name --delete branch_name
```

* Git diff without minus

```shell
git diff --color-words
```

* Nice output of git log

```shell
git log --graph --oneline --decorate --all
```

### Patch

* Create a git pacth

```shell
git format-patch -1 sha-of-commit
```

* Apply a git patch

```shell
git am < file.patch
```

### Reflog

Git save an historic of each locals modification done on local. This can be usefull to restore some commit on your local who aren't on the remote. (e.g when rebase need to be revert after it has been pushed to remote)

```shell
git reflog
```
> Get the list of local change

After there is according to the list given by the git reflog command. You can set you current branch at some point.

```shell
git reset HEAD@{8}
```
