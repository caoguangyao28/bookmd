![原理图](https://gitee.com/caoguangyao/upic/raw/master/uPic/1621577980882.jpg)

工作原理 / 流程：

1. GIT基础
## 1.1 高频命令

* git init
>将当前目录变成git仓库，且会在根目录下生成.git目录。如果.git目录删除，此目录即恢复为正常目录。
* git add
>将制定文件添加到版本库中，可以使用「git add .」批量添加当前目录和子目录所有修改的文件。或使用「git add path」指定某个路径的文件添加到【**暂存区】**  里。
* git commit
>将暂存区的文件提交到本地仓库，需要带“-m”参数添加提交注释说明。如「git commit -m "初始化代码"」
* git status
>查看当前仓库的状态，如有文件修改但是没添加到暂存区的，如暂存区代码提交到本地仓库但没提交到远程仓库，还有当前分支名称等。
* git push/pull
>将本地最新的代码推送远程仓库，或者将远程仓库最新的代码pull到本地仓库，如有冲突，命令会终止，需要额外处理冲突。
* git checkout
>检出所需要的分支，比如当前在master分支，使用「git checkout develop」可以检出develop分支代码。另「git chekout -b branchname」使用此命令可以基于当前分支拉出一个新分支，新分支名称为branchname
* git branch
>查看所有分支列表和当前代码所处的分支名称

**建议使用工具处理的常用命令：**

* git diff ：查看不同版本文件差异
* git reset ：回滚代码，重置仓库版本
* git merge ： 合并代码，解决代码冲突
* git log：查看历史版本信息
## 1.2 推荐工具

* **SourceTree**[https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/?fileGuid=NOAdP6yyJZtzFyAP)
* **SublimeMerge**[ https://www.sublimemerge.com/](https://www.sublimemerge.com/?fileGuid=NOAdP6yyJZtzFyAP)
* **fork**[https://git-fork.com/](https://git-fork.com/?fileGuid=NOAdP6yyJZtzFyAP)

**扩展阅读:**

1. 更详细的常用命令[http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html?fileGuid=NOAdP6yyJZtzFyAP)
2. 彻底搞懂git-rebase[http://jartto.wang/2018/12/11/git-rebase/](http://jartto.wang/2018/12/11/git-rebase/?fileGuid=NOAdP6yyJZtzFyAP)
# 2.GIT工作流程

![](https://gitee.com/caoguangyao/upic/raw/master/uPic/1621578109475.jpg)

* 2.1 主要分支 (The main branches)
>上图中绿色和橙色部分的即为主要分支，绿色为master，橙色为develop分支。主要分支的代码不经常变更，主要是从其他辅助分支里面合并过来的。原则上禁止任何开发人员在主要分支上进行代码的修改和开发。
* 2.2 辅助分支 (Supporting branches)
>如前面描述的，主要分支不直接用来修改代码，我们就需要平行于主要分支的辅助分支来配合进行代码更新。如图中的灰色、蓝色和黄色部分
>我们所用到这些的不同类型的辅助分支包括：
>①.Feature branches (功能分支)
>②.Release branches (预发布分支)
>③.Hotfix branches (热修复分支)
### 2.2.1 辅助分支详解

**功能分支(Feature branches)**

功能分支是用来给一个可预见的未来即将要发布的版本开发新功能的。功能分支通常只存在于开发者的本地仓库中，并不包含在远程库origin中。

分支创建自：develop；必须合并回：develop；

分支命名约定：除master, develop, release-*, 或hotfix-*以外的任何名字。建议 feature-*

**预发布分支 (Release branches)**

分支创建自：develop；必须合并回：develop和master；分支命名约定：release-*。

预发布分支主要用来协助一个新版本发布的准备工作。它允许对预发布版本做最后的打点。此外，它也允许做一些较小的bug修复并且准备一些发版的元数据(版本号和编译数据等)。在预发布分支做上述这些工作的同时，develop分支已经可以开始放心得为下一次发版进行新功能的开发了。

当预发布版本完成后，必须给针对master分支的该commit打一个标签(tag)。

**热修复分支 (Hotfix branches)**

分支创建自：master；必须合并回：develop和master；分支命名约定：hotfix-*。

热修复分支也是用来协助新版本发布的，在这点上和预发布分支相似，但该分支不是必须存在的。该分支的创建主要是用来及时应对线上版本所出现的意外情况。当线上版本出现一个需要立刻修复的严重bug时，我们可以从master分支上标记为当前线上版本号的tag处切出一个热修复分支。

这样做的好处是，在抽出一两个人来应对线上版本紧急bug修复的同时，团队其他成员依然可以继续在develop分支上进行日常开发工作。

当完成了紧急bug的修复时，要将该热修复分支合并回master分支，并且同时也要将其合并回develop分支，以确保对该bug的修复也同时包含在下一次发版中。这里的操作和结束预发布分支完全类似。

**扩展阅读：**

1. 一个完美的 Git 分支管理模型[http://matrixzk.github.io/blog/20141104/git-flow-model/](http://matrixzk.github.io/blog/20141104/git-flow-model/?fileGuid=NOAdP6yyJZtzFyAP)
2. GitFlow工作流程[https://www.cnblogs.com/jeffery-zou/p/10280167.html](https://www.cnblogs.com/jeffery-zou/p/10280167.html?fileGuid=NOAdP6yyJZtzFyAP)
# 3.Commit规范

在团队协作中我们经常碰到的问题是每个人都有自己的开发习惯，这个习惯包含但不限于编码风格，工具使用等，所以往往协作中就会出现各种各样的问题。这篇文章将会从很小的切入点开始讲，即如标题所诉 Git Commit Message。

### 3.1 为什么要规范 Git Commit Message

在项目开发开发中或许我们能经常看到

* 说不出所以然的一连串的 commit 提交日志
* commit 信息写的很简单，根本没有办法从 commit 信息中获知该 commit 用意的
* commit 信息写的很随意，commit 信息和变更代码之间不能建立联系的
* commit 信息写的过于冗余的

相信或多或少大家都曾碰到过。一旦涉及代码回滚，issue 回溯，changelog，语义化版本发布等操作时，作为 PM 肯定一脸懵逼 即使 PM 参与了全程的 CR 环节。

那理想中的 Git Commit Message 应该是要能较好的解决如上问题

* 发生问题时快速让 PM 识别问题代码并回滚
* commit 和 代码之间能建立起联系，并和相关的 issue 予以关联，做到任何代码都能区域性的解决问题（当然这也需要好的分支模型来支撑）

而 changelog，语义化版本发布这更像是合理化 commit 后水到渠成之事。

### 3.2 如何算比较好的 Git Commit Message

以个人来看，好的 commit 需要有以下特征

* 有节制性的
* 简明扼要的
* 和代码，issue 强关联，利于 CR 的
### 3.3 如何写出规范化的 Git Commit Message

当前业界应用的比较广泛的是[Angular Git Commit Guidelines](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines?fileGuid=NOAdP6yyJZtzFyAP)

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

``` bash
<type>(<scope>): <subject>
> // 空一行
> <body>
>// 空一行
>
><footer>
```



其中，Header 是必需的，Body 和 Footer 可以省略。

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

**3.3.1.1 Header**

Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。

**(1)  type**

type用于说明 commit 的类别，只允许使用下面7个标识。

>feat：新功能（feature）
>fix：修补bug
>docs：文档（documentation）
>style： 格式（不影响代码运行的变动）
>refactor：重构（即不是新增功能，也不是修改bug的代码变动）
>test：增加测试
>chore：构建过程或辅助工具的变动

如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

**(2) scope**

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

**（3）subject**

subject是 commit 目的的简短描述，不超过50个字符。

>以动词开头，使用第一人称现在时，比如change，而不是changed或changes
>第一个字母小写
>结尾不加句号（.）

**3.3.1.2 Body**

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

More detailed explanatory text, if necessary.  Wrap it to

about 72 characters or so.

>Further paragraphs come after blank lines.
>>- Bullet points are okay, too
>- Use a hanging indent

有两个注意点。

（1）使用第一人称现在时，比如使用change而不是changed或changes。

（2）应该说明代码变动的动机，以及与以前行为的对比。

**3.3.1.3 Footer**

Footer 部分只用于两种情况。

**（1）不兼容变动**

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

BREAKING CHANGE: isolate scope bindings definition has changed.

To migrate the code follow the example below:

Before:

scope: {

myAttr: 'attribute',

}

After:

scope: {

myAttr: '@',

}

>The removed `inject` wasn't generaly useful for directives so there should be no code using it.

**（2）关闭 Issue**

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

>Closes #234

也可以一次关闭多个 issue 。

>Closes #123, #245, #992

**3.3.1.4 Revert**

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

revert: feat(pencil): add 'graphiteWidth' option

>This reverts commit 667ecc1654a317a13331b17617d973392f415f02.

Body部分的格式是固定的，必须写成This reverts commit &lt;hash>.，其中的hash是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。

### 3.4 Commitizen

[Commitizen](https://github.com/commitizen/cz-cli?fileGuid=NOAdP6yyJZtzFyAP)是一个撰写合格 Commit message 的工具。

安装命令如下。

``` bash
$ npm install -g commitizen
```
然后，在项目目录里，运行下面的命令，使其支持 Angular 的 Commit message 格式。
``` zsh
$ commitizen init cz-conventional-changelog --save --save-exact
```
以后，凡是用到git commit命令，一律改为使用git cz。这时，就会出现选项，用来生成符合格式的 Commit message。
![图片](data:image/png;base64,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)


### 3.5 commitlint

### 由于validate-commit-msg 这个库⽂件，作者已经不再维护，推荐更换为 commitlint，固新项⽬中⼤多采⽤Commitizen 结合commitlint（⽤于⾃动验证） 使⽤。

commitlint⼀样⽤于检查 commit message 是否符合规范，安装⽅式正常的npm 安装

```
npm install --save-dev @commitlint/{cli,config-conventional} 
```
同时安装了 配置⽂件模块（有⼀定的默认规则配置，默认规则 与 commitizen 基本⼀致） 项⽬根⽬录新建⽂件commitlint.confifig.js
```
// commitlint.config.js
2 module.exports = { extends: ['@commitlint/config-conventional'] }
```
可以直接在 commitlint.confifig.js ⽂件中添加配置信息，也可以 新建其它配置⽂件配置修改规则例如：.commintlintrc.js , .commintlintrc.json 或者 在package.json 添commitlint 字段配置 ⼀般情况下⽆需进⾏额外配置 ，默认的规则基本以满⾜需求。
注意⾃动验证同样借助于git hooks这⾥借助使⽤较多的 husky （使⽤ husky 对node版本有要求 > = v10）

```

npm install --save-dev husky
// package.json 文件 添加 husky
{
"husky": {
 "hooks": {
   "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
   }
 }
} 
```
**使⽤验证（cmd 中 or shell）：**
```

git commit -m "foo: this will fail"
 husky > commit-msg (node v10.1.0)
 No staged files match any of provided globs.
 input: foo: this will fail
✖ type must be one of [build, chore, ci, docs, feat, fix, perf,
refactor, revert, style, test] [type-enum] 
```
### 3.6 生成 Change log

如果你的所有 Commit 都符合 Angular 格式，那么发布新版本时， Change log 就可以用脚本自动生成（[例1](https://github.com/ajoslin/conventional-changelog/blob/master/CHANGELOG.md?fileGuid=NOAdP6yyJZtzFyAP)，[例2](https://github.com/karma-runner/karma/blob/master/CHANGELOG.md?fileGuid=NOAdP6yyJZtzFyAP)，[例3](https://github.com/btford/grunt-conventional-changelog/blob/master/CHANGELOG.md?fileGuid=NOAdP6yyJZtzFyAP)）。

生成的文档包括以下三个部分。

>New features
>Bug fixes
>Breaking changes.

每个部分都会罗列相关的 commit ，并且有指向这些 commit 的链接。当然，生成的文档允许手动修改，所以发布前，你还可以添加其他内容。

[conventional-changelog](https://github.com/ajoslin/conventional-changelog?fileGuid=NOAdP6yyJZtzFyAP)就是生成 Change log 的工具，运行下面的命令即可。

```
$ npm install -g conventional-changelog
$ cd my-project
$ conventional-changelog -p angular -i CHANGELOG.md -w
```
上面命令不会覆盖以前的 Change log，只会在CHANGELOG.md的头部加上自从上次发布以来的变动。
如果你想生成所有发布的 Change log，要改为运行下面的命令。

```
$ conventional-changelog -p angular -i CHANGELOG.md -w -r 0
```
为了方便使用，可以将其写入package.json的scripts字段。
``` javascript
{
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -w -r 0"
  }
}
```
以后，直接运行下面的命令即可。
``` bash
$ npm run changelog
```
