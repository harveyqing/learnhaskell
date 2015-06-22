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

[Cabal](https://www.haskell.org/cabal/download.html)是一个集项目管理及依赖解析于一身的工具，通常你会用它将项目安装到专属沙箱中。

Cabal相当于Ruby Bundler、Python pip、Node NPM、Maven等包管理组件。GHC可以用来打包，Cabal则可以选择安装版本。