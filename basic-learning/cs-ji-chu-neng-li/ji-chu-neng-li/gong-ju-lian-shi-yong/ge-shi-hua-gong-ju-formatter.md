<!-- Copyright (c) 2023 谢骐 <https://github.com/shynur>

     Permission is hereby granted, free of charge, to any person obtaining a copy
     of this software and associated documentation files (the "Software"), to deal
     in the Software without restriction, including without limitation the rights
     to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
     copies of the Software, and to permit persons to whom the Software is
     furnished to do so, subject to the following conditions:

     The above copyright notice and this permission notice shall be included in all
     copies or substantial portions of the Software.

     THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
     IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
     FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
     AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
     LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
     OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
     SOFTWARE.
-->

---
description: shynur
---

# 格式化工具（Formatter）

笔者使用的工具是 `clang-format`, 是 LLVM 开源项目的组成部分, 该项目由 Apple Inc. 主持. 另外该项目的 clang 也是非常强大的 C/C++ 编译器 (Apple 是三大编译器厂商之一). 在写下这段话时, `clang-format` 是目前最流行的格式化工具. `clang-format` 的配置方案及使用方法可以去官网查看.

#### 例子

有些人可能没听说什么是格式化工具, 这里举个例子, 有如下代码:

```c
#include<stdio.h>
int  main  (
) { puts ( "Hello, world!")
; return
0;
}
```

格式化之后:

```c
#include <stdio.h>
int main() {
    puts("Hello, world!");
    return 0;
}
```

<figure><img src="../../../../.gitbook/assets/formatting-code.gif" alt=""><figcaption><p>代码格式化（编者按：为什么又崩坏三）</p></figcaption></figure>

这里使用的是**笔者自己编写的 Emacs Lisp 函数**, 创建一个外部子进程 `clang-format` (ELisp 还是一门面向对象的语言, 所以 process 实际上是内置类型), 将选中区域输入到 `clang-format` 这个进程, 替换为输出结果, 代码如下 (你应当略作修改就可以复用):

```lisp
(keymap-global-set "C-c f"
  (lambda ()
    "调用“clang-format --Werror --fallback-style=none --ferror-limit=0 --style=file:~/.emacs.d/clang-format.yaml”.
在C语系中直接美化代码(且光标的相对位置得到保留),否则美化选中区域"
    (interactive)
    (let ((clang-format "d:/Progs/LLVM/bin/clang-format.exe")
          (options `("--Werror"
                     "--fallback-style=none"
                     "--ferror-limit=0"
                     ,(format "--style=file:%s"
                              (file-truename "~/.emacs.d/clang-format.yaml"))))
          (programming-language (pcase major-mode
                                  ('c-mode    "c"   )
                                  ('c++-mode  "cpp" )
                                  ('java-mode "java")
                                  ('js-mode   "js"  )
                                  (_ (unless mark-active
                                       (user-error (shynur/message-format "无法使用“clang-format”处理当前语言")))))))
      (if (stringp programming-language)
          (without-restriction
            (apply #'call-process-region
                   1 (point-max) clang-format t t nil
                   (format "--assume-filename=a.%s" programming-language)
                   (format "--cursor=%d" (1- (point)))
                   options)
            (beginning-of-buffer)
            (goto-char (1+ (string-to-number (prog1 (let ((case-fold-search nil))
                                                      (save-match-data
                                                        (buffer-substring-no-properties
                                                         (re-search-forward "\\`[[:blank:]]*{[[:blank:]]*\"Cursor\":[[:blank:]]*")
                                                         (re-search-forward "[[:digit:]]+"))))
                                               (delete-line))))))
        (let ((formatted-code (let ((buffer-substring `(,(current-buffer) ,(region-beginning) ,(region-end))))
                                (with-temp-buffer
                                  (apply #'insert-buffer-substring-no-properties
                                         buffer-substring)
                                  (apply #'call-process-region
                                         1 (point-max) clang-format t t nil
                                         (format "--assume-filename=a.%s"
                                                 (completing-read #("assume language: "
                                                                    0 16 (face italic))
                                                                  '("c" "cpp" "java" "js" "json" "cs")))
                                         options)
                                  (buffer-substring-no-properties 1 (point-max)))))
              (point-at-region-end (prog1 (= (point) (region-end))
                                     (delete-active-region))))
          (if point-at-region-end
              (insert formatted-code)
            (save-excursion
              (insert formatted-code))))))))
```

<!-- Local Variables: -->
<!-- coding: utf-8-unix -->
<!-- End: -->
