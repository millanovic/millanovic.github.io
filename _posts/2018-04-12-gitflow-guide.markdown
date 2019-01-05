---
layout:     keynote
title:      "git-flow规范"
navcolor:   "invert"
date:       2018-4-12
author:     "Mill"
header-img: img/post-bg-stonehenge.jpg
tags:
    - 前端开发
    - JavaScript
    - git
---

# git-flow 规范

## 流程规范

### git-flow 流程

![git-flow流程图](/img/git-model.jpeg)
| 分支        | 功能描述    | 允许合入的分支    |
| --------   | --------  | --------  |
| master | 生产环境分支 |  release, hotfix  |
| develop | 基于master拉出的开发分支，保持最新的开发代码 |  feature, release, hotfix |
| release_xxx | 基于develop拉出的预发布分支，测试完成后合并入master和develop，打tag |  不允许任何分支合并  |
| feature_xxx | 基于develop拉出的功能分支，开发完成后合入develop |  |
| hotfix_xxx | 基于master拉出的hotfix分支，测试完成后合并入master和develop |  不允许任何分支合并  |

### 开发流程

- 从develop分支迁出一个feature分支
- 待feature开发完成，合并入develop分支，删除feature分支，做全面测试
- 测试完成后，从develop分支迁出release_xxx分支，做上线前准备及bug修复
- 待release完成后合并入master以及develop，打上tag，并删除release_xxx分支
- 基于master发布，或者基于tag发布

### HotFix流程

- 从master迁出一个hotfix_xxx分支
- 修复完成并通过测试后，合并入master以及develop分支，并删除hotfix_xxx分支

## 操作命令

### 若不使用git-flow工具需要注意所有的merge都使用

```bash
$ git merge --no-ff
```

![git-merge流程图](/img/git-flow-branch.png)
```git merge –no-ff``` 可以保存你之前的分支历史。能够更好的查看 merge历史，以及branch 状态。 
```git merge``` 则不会显示 feature，只保留单条分支记录。

### 使用git flow工具

#### 安装git-flow工具

```bash
$ brew install git-flow
```
git-flow 初始化，输入一些必要的信息，如命名约定
```bash
$ git flow init
Which branch should be used for bringing forth production releases?
   - master
Branch name for production releases: [master]
Branch name for "next release" development: [develop]
How to name your supporting branch prefixes?
Feature branches? [feature/] 
Release branches? [release/] 
Hotfix branches? [hotfix/] 
Support branches? [support/] 
Version tag prefix? []
```

#### 新增feature

该命令会从develop分支迁出feature分支，并切换到该feature分支
```bash
$ git flow feature start myfeature 
```

#### feature开发完毕

该命令会合并myfeature分支到develop，删除myfeature分支，并且切回develop分支

```bash
$ git flow feature finish myfeature
```

#### 新增release

该命令会从develop迁出release/0309

```bash
$ git flow release start 0309
```

#### 完成release

该命令会从合并release/0309到master以及develop分支，删除release/0309分支，最后用release分支名打上tag
```bash
$ git flow release finish 0309
```

#### 开启hotfix

该命令会从master迁出hotfix/xxx分支

```bash
$ git flow hotfix start xxx 
```

#### 完成hotfix

该命令会从合并hotfix代码到master和develop，并打上tag

```bash
$ git flow hotfix finish xxx 
```

### 使用SourceTree进行git-flow操作

可参考[git-flow-sourcetree](https://www.jianshu.com/p/8a3988057d0f)