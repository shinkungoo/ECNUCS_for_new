---
description: shynur
---

# 编辑器（Editor）

笔者曾经使用的编辑器是 VS Code, 现在是 [Emacs](https://gnu.org/s/emacs). 两款都是十分优秀的编辑器, 笔者都有丰富的使用经验, 我先简单对比一下双方的优缺点, 再着重讲一下 Emacs 的相关内容.

## `VS Code` vs `Emacs`

VS Code 的优点是: 开箱即用. 具体来说, 指的是它的 UI 和 语言相关的插件 的默认方案都较为优秀, 比如 语法高亮, 自动补全 等. Emacs 虽然也有, 但远不如 VS Code 这么省心, Emacs 的宗旨是 把_定制_留给用户, 必须得承认, 默认 UI 丑的一批.

VS Code 的缺点也很明显, 它的配置比较麻烦. 这主要体现在两方面, 一是设置中的各个选项意义不明, 文档残缺; 二是很难自己编写插件. 我曾经想为 VS Code 写 C++ 装一个 LSP (非常棒的工具, 使 编辑器 具有 IDE 的语义分析能力), 搞了半天都没成功, 后来在 Emacs 上很轻松就完成了.

Emacs 的缺点是: 学习门槛很高。

<figure><img src="../../../../.gitbook/assets/editor-learning-curve.jpg" alt=""><figcaption><p>经典编辑器学习曲线</p></figcaption></figure>

这一点无解, 我只能给一些学习路线（见下文）

Emacs 的优点非常多, 包括但不限于:

* 高度可定制化. 真正贯彻的自由软件的思想, Emacs 完全信任用户, 你编写的 ELisp 代码是一等公民, 可以完全 hack 进 Emacs; 与之相反的是 VS Code 这种, 插件永远是二等公民。
* 文档详细. Emacs 中的大部分配置都是由 ELisp 变量完成的 (这么说不太准确, 其实是你用 Emacs 这个解释器运行别人编写的 ELisp 代码, 别人编写的代码根据相关的变量判断是否要执行某些操作), 每个变量都有相应的用途及注意事项。
* 函数式嵌入式语言: Emacs Lisp 笔者同时掌握着 Common Lisp 和 Emacs Lisp, 体感上 Emacs Lisp 更简单更适合入 Lisp 系语言的门。
* 背靠 FSF 和 GNU。作为对比，Notepad++，GitHub Atom 等编辑器的靠山不够强大,，就烂尾了。

## 学习使用 Emacs

### **文档**

#### **入门 Lisp**

**必须**首先阅读 [_An Introduction to Programming in Emacs Lisp_](https://gnu.org/s/emacs/manual/html\_node/eintr/index.html). 该文档内置在 Emacs 中, 执行 ELisp 表达式 `(info "(eintr)")` 即可到达该书的扉页, 或者使用快捷键 `Control+h i g (eintr) RET`.

这本书不仅是学习 ELisp 的绝佳入门书, 也是非常适合入门 Lisp. 笔者还读过有名的 Practical Common Lisp (三遍), 但没这么通俗易懂. 当然, 如果你已经有 Lisp 基础, 那么读 Intro to ELisp 这本书应该只需要半个月.

#### **论坛**

[Emacs China](https://emacs-china.org/), 国内活跃的 Emacs 社区, 大佬众多 (比如 Deepin 创始人 lazycat). 加入 Emacs China, 混个眼熟, 对你找工作有帮助.
