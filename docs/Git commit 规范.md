# 为什么需要规范 commit 信息？

1. 为了逼格：规范的 commit 信息能够让你的开发显得更专业。
2. ~~为了避免强迫症患者暴起刀人：规范的 commit 信息能或许能够安抚它们的情绪。~~
3. 为了规避无效劳动：敲一段规范清晰的 commit 信息能够让你知道你在这一次提交中究竟干了什么，你总不想花了力气敲了几个火星文上去，回过头来却还是要对着这段外星文明留下的通讯“若有所思”地摩挲下巴吧？
4. 为了能够更敏捷地梳理项目结构并进行项目管理：规范清晰的 commit 新能够在绝大部分场合直截了当地告诉你“这里有什么”“什么事情曾在这里发生过”，而不需要你再去累死累活地大规模手动翻阅源码，理清思路——小小的也很可爱。
5. 为了甩锅：哪一天项目突然罢工了，就去翻一翻提交历史记录，你可以像霸总眉头一皱，道一句“自己出来”，然后就会 commit 们就会站出来指认它们之中最可疑的那些家伙。到这一步你只需要眨巴眨巴眼睛，大底上就该知道哪个倒霉蛋需要背上“干崩项目”这口又大又黑的锅了。
6. 为了便于回溯与定位及修复错误：参照上一条，不会真有人甩了锅就想删库跑路吧？早知如此当初何必还要往程序开发这大坑跳呢？
7. 为了便于自动化管理：没毛病，只要 commit 信息或者其“规范/约定”本身足够规范清晰，自然而然地就能够衍生出自动化工具来强迫你规范你的提交记录或轻松地对 commit 数据进行进一步的处理，如生成版本号、导出 CHANGELOG.md 等等。
8. 为了减少开发误操作，提高容错率与整体开发效率：看了前面几条这还需要说？

# 什么能算得上规范的 commit 信息

> 以下内容整合自互联网各个角角落落，并非 commit 标准，仅作为从实践经验中总结而来的习惯性的“建议”存在。

## commit 信息的一般格式

```text
<type>[(<scope>)][!]: <subject>

[<body>]

[<footer>]
```

- type: 本次 commit 信息的类型
- scope: 本次 commit 提交的影响范围（可选）
- subject: 本次 commit 的简要描述
- body: 本次 commit 的详细描述（可选）
- footer: 本次 commit 的脚注（可选）

## commit type 的常用类别

### 主要类别

#### feat

引入了新功能或新特性，通常需要提升项目的 minor 版本号。

`keywords: feature minor-version`

#### fix

修补了一个已知漏洞，通常需要提升项目的 patch 版本号。

`keywords: bug patch-version`

### 其它类别

#### to

对已知的漏洞进行了一定程度的修复，通常将漏洞修复过程产生的代码改动置入 to 提交，并最终合并为一个 fix 提交作为最终的漏洞修复提交。

`keywords: bug fix diff`

#### docs

对项目的文档进行了修正或更新。

`keywords: document`

#### perf

对代码进行了关于性能方面的改动。

这些改动不应该涉及代码特性的变更、漏洞的修复等等。

`keywords: performance-only`

#### refactor

对代码进行了重构性的改动，如代码接口调整、注释的增减等等。

这些改动不应该涉及代码特性的变更、漏洞的修复等等。

`keywords: refactor-only`

#### style

改变了现有内容的风格，如代码风格等。

这些改动不应该对代码的含义有任何影响。

`keywords: style-only`

#### test

添加测试单元或纠正了现有的测试内容。

`keywords: test`

#### chore

对项目构建及辅助工具相关的内容进行了更改，如构建系统的调整、外部依赖的调整等等。

`keywords: build-system external-dependency`

#### revert

进行了版本的回滚。

提交 revert commit 时，其格式如下：

```text
revert: <commit-header>

This reverts commit <commit-hash>
```

commit 示例：

```text
revert: fix: fix a bug in the import when size != 1

This reverts commit 227f6c7ab4bfe52d05287f6c78976933aa1560d4
```

事实上，关于 revert 的提交可能远比这要复杂（如多 commit 的回滚），所以宽松化 revert commit 信息是有必要的。据此，可以有另一种推荐的 revert 规范：

```text
revert: <subject>

Refs: <commit-hash> [, ...]
```

commit 示例：

```text
revert: never should we crash into the fxxking incident again

Refs: 72f18ca, eb92461, 2d28174
```

`keywords: revert`

#### merge

进行了分支的合并。

提交格式与 revert 类似。

`keywords: merge-branch`

#### ci

对自动化工作流的配置文件或脚本进行了改动。

`keywords: continuous-integration`

### 自定义类别

可以根据自己的项目的实际情况拟定，但一般不太推荐，若有必要也请务必做好规范化工作。

建议将所有的 commit 都归类到上述类型中。

## 关于 commit scope  的说明

scope 用于指明当前提交的影响范围，该项需要根据项目的具体类型决定。

可以根据 package 区分影响范围，也可以根据项目的架构层次来划分，较为灵活宽松。

不过至少，请保证你的 scope 是个名词。当然我想 global 之流也是可行的，但是像 global 这种真的还有必要写范围吗？

## commit subject 的一般规范

subject 包含了对本次 commit 的简洁描述，至少需要服从以下几点内容：

1. 使用祈使句
2. 首字母小写
3. 句末不追加点号

此外，为了保证“简洁”，通常 commit 首行的描述不超过 50 （宽）字符。

## commit body 的一般规范

body 作为可选内容，用于对 subject 进行补充。

body 的内容格式是自由的，但请尽可能使用祈使句与一般现在时。在 body 中，你可能需要包含本次提交的上下文/动机，并说明本次提交与之前的行为的差异。

## commit footer 的一般规范

footer 负责对 Breaking Changes 与相关联 issues 或其它的必要信息进行注解。

### 脚注重大变更 Breaking Changes

```text
<type>[(<scope>)]!: <subject>

[<body>]

BREAKING CHANGE: <content>

[<other-footers>]
```

当本次提交包含重大变更时，通常需要在 commit type 后加上感叹号 `!` 以示说明，并在脚注部分增加服从 `BREAKING CHANGE: <content>` 格式的重大变更的说明。

### 脚注关联 Issues

对于相关联 issues 的注解一般包含以下情况：

1. 相关联 issue 的编号
2. 审阅/处理人（可选）
3. 对于相关联 issue 的动作（关闭等）

footer 对于 issue 的注解（仅脚注部分）可参考如下：

```text
Reviewed-by: Mr. Z
Refs: #114514
```

```text
Closes: #114, #514, #666
```

## 特殊的 commit

### 仓库首次提交

```text
first commit
```

创建仓库后的第一个提交，通常包括了 .gitignore/.gitattributes/LICENCE/README.md 等前置性的基础项目文件。

# Reference

- [如何规范你的 Git commit？](https://zhuanlan.zhihu.com/p/182553920)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Commit Message Conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.fpepsvr2gqby)
