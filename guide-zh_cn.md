# 前言

这是我推荐的Haskell学习路线。

#### 请切记：*不要在暂时看不懂的地方停留，先继续读下去！*

## 社区

IRC频道是Freenode上的`#haskell-beginners`。

IRC web版客户端可[在这里获得](http://webchat.freenode.net/)。

Haskell[邮件列表](https://wiki.haskell.org/Mailing_lists)。

### 社区参与原则

[Chris Done的指导示例](http://chrisdone.com/posts/teaching)。

请友善待人。尖酸刻薄的言语会把人吓跑，使其不愿继续参与。

低劣的批评只会让你自己痛快，对听者却毫无益处。

不要总是用『这很简单』、『这没什么』来评价他人的提问或成果，这会让人觉得付出那么多努力才获得一点进步是因为自己不如别人。学得慢的人通常也是学得最全面的人，这值得赞赏！

当别人承认他不知道的时候，请不要故作惊讶。这会让他沮丧，而你除了自我感觉良好以外，什么也没得到。

不要说『其实...是这样的...』(well, actually...)。通常，当别人说的并不完全正确时，你会补充说『其实...是这样的』来做些细枝末节的纠正。这很恼人，尤其是当你的纠正与正在讨论的话题没有关系的时候。这并不是说我们不应该追求真理和精确，只是这样的补充通常作秀成分居多，对事实并无帮助。

---

上述部分内容来自[the Recurse Center手册](https://www.recurse.com/manual)。感谢他们的分享！

# 什么是Haskell、GHC和Cabal

Haskell是一门编程语言，有关它的信息请参阅下面这篇报告，此报告最新版为2010版：
[onlinereport](http://www.haskell.org/onlinereport/haskell2010/)

## GHC

[GHC](http://www.haskell.org/ghc/)是Haskell最主流的开发工具，它包含一个编译器、REPL（解释器）、包管理及其它工具。

## Cabal

[Cabal](https://www.haskell.org/cabal/download.html)是一个集项目管理及依赖解析于一身的工具，通常你会用它将项目安装到专属沙盒中。

Cabal相当于Ruby Bundler、Python pip、Node NPM、Maven等包管理组件。GHC可以用来打包，Cabal则可以选择安装版本。

# 安装Haskell和Cabal

## Ubuntu

[这个PPA](http://launchpad.net/~hvr/+archive/ghc)很棒！我在我所有的Linux开发及构建机器上都使用它。

具体步骤如下：

```bash
$ sudo apt-get update
$ sudo apt-get install python-software-properties # Ubuntu 12.04及以下版本
$ sudo apt-get install software-properties-common # Ubuntu 12.04及以上版本
$ sudo add-apt-repository -y ppa:hvr/ghc
$ sudo apt-get update
$ sudo apt-get install cabal-install-1.20 ghc-7.8.4 happy-1.19.4 alex-3.1.3
```

接着，把以下路径加入你的`$PATH`环境变量(bash\_profile, zshrc, bashrc等)中：

```
~/.cabal/bin:/opt/cabal/1.20/bin:/opt/ghc/7.8.4/bin:/opt/happy/1.19.4/bin:/opt/alex/3.1.3/bin
```

*注：* 你也可以将`.cabal-sandbox/bin`添加到路径中，这样当你的当前工作目录为cabal沙盒时，你可以从命令行获取到正在开发的代码。

## Debian

### 使用Ubuntu PPA

如果你使用的是非稳定版，你可以用和Ubuntu一样的流程，只是需要在命令`sudo add-apt-repository -y ppa:hvr/ghc`后加上：

```bash
$ sudo sed -i s/jessie/trusty/g /etc/apt/sources.list.d/hvr-ghc-jessie.list
```

对于其它的Debian版本，你只需要将上面这条命令中所有的`jessie`替换为你的版本名即可。

如果因为某些原因致使文件`/etc/apt/sources.list.d/hvr-ghc-jessie.list`不存在，此时`/etc/apt/sources.list`文件里应该会包含这样的一行：

    deb http://ppa.launchpad.net/hvr/ghc/ubuntu jessie main

将此行中的`jessie`用`trusty`替换即可。

### 手动编译

[这](http://www.davesquared.net/2014/05/platformless-haskell.html)是一篇Mac OS X上的安装指南。

注意：

- 编译前根据自己的需要来设定ghc的目录前缀(prefix)。
- 不要直接下载`cabal-install`二进制程序，请下载源码并运行`bootstrap.sh`脚本。

## Fedora 21

从非官方仓库安装Haskell 7.8.4（Fedora 22以上已经有官方版本）：

```bash
$ sudo yum-config-manager --add-repo \
> https://copr.fedoraproject.org/coprs/petersen/ghc-7.8.4/repo/fedora-21/petersen-ghc-7.8.4-fedora-21.repo 
$ sudo yum install ghc cabal-install
```

根据[petersen/ghc-7.8.4 copr page](https://copr.fedoraproject.org/coprs/petersen/ghc-7.8.4/)所述，此版本的ghc无法与Fedora/EPEL ghc并存。

## Arch Linux

从Arch Linux官方仓库安装Haskell：

```bash
$ sudo pacman -S cabal-install ghc happy alex haddock
```

## Gentoo

在Gentoo上，你可以通过Portage分别安装Haskell平台的各个组件。如果你设定了`ACCEPT_KEYWORDS=arch`（而不是`ACCEPT_KEYWORDS=~arch`），Portage将安装老版本的Haskell。因此，一旦你使用了`ACCEPT_KEYWORDS=arch`，请将下面的命令添加到`/etc/portage/package.keywords`中：

    dev-haskell/cabal-install
    dev-lang/ghc

然后执行：

```bash
$ emerge -jav dev-lang/ghc dev-haskell/cabal-install
```

Gentoo会保留一个“稳定”（老的）版本的`cabal-install`在Portage树中(Portage tree)，
如果你想通过`cabal-install`安装新版本，请执行以下操作（注意反斜杠是必须的）：

```bash
$ \cabal update                # 反斜杠
$ \cabal install cabal-install # 必须
```

现在你已经用portage在系统级安装了cabal，也通过`cabal-install`在home目录下安装了局部cabal，下一步是要确保每次你在终端中运行的`cacal`都是home目录下最新的局部cabal。你不妨将下面设置添加到shell配置文件中：

```bash
PATH=$PATH:$HOME/.cabal/bin
alias cabal="$HOME/.cabal/bin/cabal"
```

如果你不确定你使用的是哪个shell，那么多半是Bash。如果你用的是Bash，那么修改的配置文件是`~/.bashrc`；如果你用的是Z-shell，则需修改`~/.zshrc`。你可以通过下述命令找出shell版本：

```bash
echo $SHELL | xargs basename
```

我使用的是zsh，因此执行上述命令会输出`zsh`。

完成上述各项安装任务后，你可以接着安装`alex`和`happy`这两个工具：

```bash
$ cabal install alex happy
```

恭喜！你已经有了一个可以工作的Haskell环境了。

## Mac OS X

### 10.9

安装[GHC for Mac OS X](http://ghcformacosx.github.io/)，它包含了GHC和Cabal。安装完成后，它会提示你如何将GHC和Cabal添加到系统路径中。

### 10.6-10.8

用[这个tarball](https://www.haskell.org/platform/download/2014.2.0.0/ghc-7.8.3-x86_64-apple-darwin-r3.tar.bz2)来完成安装。