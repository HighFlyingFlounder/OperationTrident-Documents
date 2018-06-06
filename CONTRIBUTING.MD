# 文档规范

<table>
    <tr>
        <th>更新日期</th>
        <th>作者</th>
        <th>更新内容</th>
        <th>版本</th>
    </tr>
    <tr>
        <td align="center">2018.06.05</td>
        <td align="center">V3r@M!p</td>
        <td>建立文档规范初版</td>
        <td align="center">v1.0</td>
    </tr>
    <tr>
        <td align="center">2018.06.06</td>
        <td align="center">V3r@M!p</td>
        <td>
            1. 修改<b>书写、命名规范</b>中文件名称的格式
            <br/>
            2. 修改更新时需要的记录（使用表格），并制定相应的书写格式
            <br/>
            3. 增加Q&A记录规范
            <br/>
            4. 增加表格书写规范
        </td>
        <td align="center">v1.1</td>
    </tr>
    <tr>
        <td align="center">2018.06.07</td>
        <td align="center">V3r@M!p</td>
        <td>
            1. 修改表格书写规范，修改GitHub不支持的语法
        </td>
        <td align="center">v1.2</td>
    </tr>
</table>

## 目录
1. [文件格式](#1-文件格式)
2. [书写、命名规范](#2-书写、命名规范)
3. [commit](#3-commit)
4. [本文档更新规范](#4-本文档更新规范)

## 1. 文件格式

- 文档采用[Markdown语法](https://www.markdownguide.org/getting-started)编写，文件大小比word文档小，还便于文档排版、文档间跳转与控制变更
- 基本语法：[Basic Syntax](https://www.markdownguide.org/basic-syntax)
- 扩展语法：
    - [Extended Syntax](https://www.markdownguide.org/extended-syntax)
    - Markdown支持HTML语法，可以在文件中使用，如本文档用到的页内跳转、[项目计划.md](planning/project/项目计划.md)中的表格等

## 2. 书写、命名规范

- 日期使用 `yyyy.mm.dd` 格式命名
- 需要保留多个版本的文件名使用 `日期-文件内容.md` 格式命名，便于文件系统按日期排序，如会议记录等
- 只需要保留一份最新文档的直接使用 `文件内容.md` 格式命名，如项目计划等
- 只保留最新的文档需要记录更新信息，简要模板为：
    ```html
        <table>
            <tr>
                <th>更新日期</th>
                <th>作者</th>
            </tr>
            <tr>
                <!-- 实际日期 -->
                <td align="center">yyyy.mm.dd</td>
                <!-- 修改人名称 -->
                <td align="center">name</td>
            </tr>
        </table>
    ```
    更新时只需要修改 `yyyy.mm.dd` 和 `name` 即可
- 文件内容格式可参考已有的文件
- `Q&A` 写在主页的[README.MD](./README.MD)中，日期用 `### 三级标题` ，在相同日期内的 `Q&A` 用 `> 块` 分开，问题使用 `**Q: xxxx**` 加粗
- 需要使用表格时，使用
    ```html
        <table>
            <tr>
                <th>title 1</th>
                <th>title 2</th>
                <th>title 3</th>
                <!-- <th>title x</th> -->
            </tr>
            <tr>
                <td>content 1-1</td>
                <td>content 1-2</td>
                <td>content 1-3</td>
                <!-- <td>content 1-x</td> -->
            </tr>
            <tr>
                <td>content 2-1</td>
                <td>content 2-2</td>
                <td>content 2-3</td>
                <!-- <td>content 2-x</td> -->
            </tr>
            <!-- <tr>...</tr> -->
        </table>
    ```
    如需使用跨多行或多列的表格，在 `<td></td>` 标签上添加
    ```html
        <!-- 跨x行 -->
        <td rowspan="x"><td>
        <!-- 跨x列 -->
        <td colspan="x"><td>
    ```
    `<td></td>` 中需要换行时，添加 `<br/>` 标签  
    `<td></td>` 中需要加粗内容时，使用 `<b>内容</b>`  
    表格太宽时，可以像[2018.06.05-剧情策划.md](planning/game/2018.06.05-剧情策划.md)一样，分为两个表格  
    当表格某一列需要占固定大小的宽度时，将该列title `<th></th>` 改为 `<th width="百分比"></th>` 
- 文中引用其他地方的文档时，需要加上链接，方便跳转
- ...

## 3. commit

- 更新文档时，commit需要详细说明更新地方，不可用“一次更新”，“修改了xx文档”等简单说明
- 添加新文档时，需要更新对应文件夹下的 `README.MD` 目录文件
- 需要使用图片时，在images文件夹内创建对应的文件夹管理，如tutorial
- commit可以直接提交到master分支，文档不做分支管理
- ...

## 4. 本文档更新规范

- 更新时，在本文档开头的更新信息记录内增添一栏
    ```html
        <tr>
            <!-- 实际日期 -->
            <td align="center">yyyy.mm.dd</td>
            <!-- 修改人名称 -->
            <td align="center">name</td>
            <!-- 更新内容简略说明 -->
            <td>contents</td>
            <!-- 更新后的版本号，更新一些细节加Y，整个文档重构加X -->
            <td align="center">vX.Y</td>
        </tr>
    ```