# 文档规范（v1.0）

日期：2018.06.05  
作者：V3r@M!p

更新日期：  
作者：  
更新内容：  

-----

## 目录
1. [文件格式](#file-format)
2. [书写、命名规范](#naming-conventions)
3. [commit](#commit-contents)
4. [本文档更新规范](#update-current-doc)

-----

<span id="file-format"></span>
## 1. 文件格式

- 文档采用[Markdown语法](https://www.markdownguide.org/getting-started)编写，文件大小比word文档小，还便于文档排版、文档间跳转与控制变更
- 基本语法：[Basic Syntax](https://www.markdownguide.org/basic-syntax)
- 扩展语法：
    - [Extended Syntax](https://www.markdownguide.org/extended-syntax)
    - Markdown支持HTML语法，可以在文件中使用，如本文档用到的页内跳转、[2018.06.02-项目计划.md](planning/project/2018.06.02-项目计划.md)中的表格等

-----

<span id="naming-conventions"></span>
## 2. 书写、命名规范

- 日期使用 `yyyy.mm.dd` 格式命名
- 项目管理相关文件名使用 `日期-文件内容.md`格式命名，便于文件系统按日期排序
- 文件内容格式可参考已有的文件
- ...

-----

<span id="commit-contents"></span>
## 3. commit

- 更新文档时，commit需要详细说明更新地方，不可用“一次更新”，“修改了xx文档”等简单说明
- 添加新文档时，需要更新对应文件夹下的 `README.MD` 目录文件
- 需要使用图片时，在images文件夹内创建对应的文件夹管理，如tutorial
- commit可以直接提交到master分支，文档不做分支管理
- ...

-----

<span id="update-current-doc"></span>
## 4. 本文档更新规范

- 在文件开头简要叙述更新信息