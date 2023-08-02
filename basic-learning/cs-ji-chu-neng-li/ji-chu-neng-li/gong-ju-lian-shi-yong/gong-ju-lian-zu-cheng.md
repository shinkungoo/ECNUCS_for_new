<!-- MIT License

     Copyright (c) 2023 谢骐 <https://github.com/shynur>

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

# 工具链组成

一套典型的 C 程序开发流程应当有以下组成部分:

1. 编辑器：用于编写代码。虽然 IDE 也有类似的功能, 但是它屏蔽了太多的（我们有义务知道的）细节, 本文着重讲原理，知道原理以后再使用 IDE，就会有种一切尽在掌控之中的感觉。
2. 版本管理系统：用于记录项目的每一次迭代。专业的软件工程师不会应聘任何一家不使用“版本管理系统”的公司。
3. 格式化工具：美化你写的人神共愤的代码。
4. 编译器：用于将你写的源码处理成二进制文件。本文所说的编译器指的是 `gcc` 这种集_编译，链接_等功能于一体的缝合怪。
5. 构建系统.：你会对你的项目文件进行各种操作 (例如, 编译), 构建系统将这一流程自动化。
6. 平台：可以理解为操作系统, 因为 MS-Windows 系和 UNIX 系上的工具集差别挺大的。

<!-- Local Variables: -->
<!-- coding: utf-8-unix -->
<!-- End: -->
