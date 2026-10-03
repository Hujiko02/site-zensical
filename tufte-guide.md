# Tufte 风格网站使用说明

> 面向只会 HTML 的人。不用写一行 CSS，不用写一行 JavaScript。
> 所有代码块都可以直接复制到你的页面里用。

## 目录

- [0. 你现在有什么](#0-你现在有什么)
- [1. 五分钟跑起来](#1-五分钟跑起来)
- [2. 三条铁律](#2-三条铁律)
- [3. 最小页面（整份可复制）](#3-最小页面整份可复制)
- [4. 片段库（复制粘贴用）](#4-片段库复制粘贴用)
- [5. 出错自查表](#5-出错自查表)
- [6. 中文写文章要特别注意的几件事](#6-中文写文章要特别注意的几件事)
- [7. 「我想做 X」速查](#7-我想做-x速查)
- [8. 想改样式（不懂 CSS 也能改的地方）](#8-想改样式不懂-css-也能改的地方)
- [9. 这套东西「没有」的功能](#9-这套东西没有的功能)

---

## 0. 你现在有什么

| 文件 / 文件夹 | 作用 | 你要不要动 |
| --- | --- | --- |
| `tufte.html` | **你的文章。** 从这份开始改 | 只改中文文字 |
| `tufte-full.html` | 所有功能各演一遍，当字典查 | 不用动，只用来复制 |
| `tufte-guide.md` | 本教程 | — |
| `images/1.jpg` | 示例图片 | 换成你自己的图 |
| `assets/tufte/tufte.css` | 官方样式表（tufte-css 1.9.0） | **别动**，出问题不好查 |
| `assets/tufte/local.css` | 中文相关的小修改 | 只有想改字体/颜色才动 |
| `assets/tufte/et-book/` | 字体文件（20 个） | **别动，别删** |

一句话记住分工：

- `.html` 决定**写什么**
- `.css` 决定**长什么样**

新手阶段你只需要碰 `.html`。

---

## 1. 五分钟跑起来

### 推荐：用一个小工具把文件夹「当成网站」打开

在文件夹里打开命令行，输入（然后别关这个窗口）：

```bash
cd /home/wuji/Projects/html
python3 -m http.server 8000
```

浏览器访问：<http://localhost:8000/tufte.html>

关掉命令行窗口就等于关掉网站。

### 更省事：VS Code 的 Live Server 插件

装完插件，在 `tufte.html` 上右键 → `Open with Live Server`。改完文件保存，浏览器自动刷新。

### 直接双击 html 文件行不行？

- **Firefox**：可以，一切正常。
- **Chrome**：页面能看，但**字体会被拒绝加载**（浏览器安全规则：`file://` 打开的页面不许跨文件取字体）。你会看到 Palatino / Georgia 这类系统衬线字体，而不是 Tufte 原版 ET Book。

所以：双击能应急，正式当作要长期写的东西，请用上面两种方式之一。

---

## 2. 三条铁律

这三条不是建议，是这套样式正常工作的**前提**。违反了页面就会歪，但你不会看到任何报错。

### 铁律 1：整篇文章包在 `<article>` 里

```html
<body>
<article>
  ...你的全部内容...
</article>
</body>
```

**为什么**：样式表靠 `<article>` 划出「正文窄栏 + 右边空白栏」这个布局。没有它，边注会跑出屏幕外。

**违反后**：边注不出现，或出现在页面右边缘被切掉。

### 铁律 2：每段内容外面套一个 `<section>`

```html
<section>
  <p>这里是一段话。</p>
  <p>这里是另一段话。</p>
</section>

<section>
  <p>这是新的一块，比如要放图片了。</p>
</section>
```

**为什么**：正文宽度限制在 55% 的规则写在 `section > p` 上，也就是「`section` 里面的 `p`」。

**违反后**：文字横向拉满整个屏幕，读起来很累。

**常见误解**：`section` 不是「一层套一层」的意思，是「一块一块并排」。一篇长文就是十几个 `section` 排下来。

### 铁律 3：边注必须连成一串写

```html
<label for="sn-1" class="margin-toggle sidenote-number"></label><input type="checkbox" id="sn-1" class="margin-toggle"><span class="sidenote">边注内容。</span>
```

这三个标签之间**不要回车、不要敲空格**，就写成一整行。

**为什么**：样式表用「紧挨着开关的下一个元素」来定位边注内容。中间夹了空白就不算紧挨着。

**违反后**：电脑上看起来完全正常，但**手机上点编号展不开**。这个问题很难自己发现，务必照抄。

---

## 3. 最小页面（整份可复制）

把下面全部内容存成 `new.html`，放在 `tufte.html` 同一个文件夹，就是一个能用的空文章：

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>标签页上的标题</title>
  <link rel="stylesheet" href="assets/tufte/tufte.css">
  <link rel="stylesheet" href="assets/tufte/local.css">
</head>
<body>
<article>

  <h1>文章大标题</h1>
  <p class="subtitle">副标题，不要就删掉这行</p>

  <section>
    <p>第一段正文。</p>
    <p>第二段正文。</p>
  </section>

</article>
</body>
</html>
```

三处可以改：`<title>` 里的字（浏览器标签页）、`<h1>`（页面上最大的标题）、`<p>` 里的正文。

注意：`<p class="subtitle">` 里有个 `class`，`<h1>` 里没有。`class` 相当于给标签起的「外号」，样式表靠它认出这是副标题而不是普通段落。**照抄时别把 class 弄丢。**

---

## 4. 片段库（复制粘贴用）

下面每一段都可以直接粘进 `<article>` 里面。

### 4.1 大标题与副标题

```html
<h1>文章大标题</h1>
<p class="subtitle">副标题</p>
```

一篇只写一个 `<h1>`。

### 4.2 小标题（分节）

```html
<section>
  <h2>第一小节</h2>
  <p>小节内容。</p>
</section>
```

`<h2>` 是斜体小标题。还有 `<h3>`，更小一号，用在 `h2` 里面再分层。

> **中文注意**：样式表里还有个 `<span class="newthought">` 玩法（段首几个词排成小型大写），但汉字没有小型大写这个概念，中文用它**看不出任何变化**。中文文章一律用 `<h2>` 分节就好。

### 4.3 边注（带自动编号，最常用）

```html
<p>这句话需要一个出处<label for="sn-1" class="margin-toggle sidenote-number"></label><input type="checkbox" id="sn-1" class="margin-toggle"><span class="sidenote">这里写边注内容。</span>，然后再接着写正文。</p>
```

复制第二条时，**把两处 `sn-1` 改成 `sn-2`**（`for` 和 `id` 必须一模一样，且全文不能重复）。编号 1、2、3 会自动排，不用你写。

**检查方法**：全文搜索 `sn-`，看每个名字是不是都只出现两次（一次 `for=`，一次 `id=`）。

### 4.4 无编号旁注

```html
<p>这句话需要一条旁白<label for="mn-1" class="margin-toggle">⊕</label><input type="checkbox" id="mn-1" class="margin-toggle"><span class="marginnote">这里写旁注内容。宽屏上它排在右边；窄屏上正文里会出现一个 ⊕，点开才显示。</span>，接着说。</p>
```

和 4.3 的区别：把 `sidenote-number` 换掉、`sidenote` 换成 `marginnote`、`label` 里填 `⊕` 符号。旁注不带编号，适合「顺带一提」，不适合「出处引用」。

`⊕` 就是复制这个字符，不是图片。

### 4.5 把图放到页面右边（页边小图）

```html
<p>这句话旁边配了张小图<label for="mn-2" class="margin-toggle">⊕</label><input type="checkbox" id="mn-2" class="margin-toggle"><span class="marginnote"><img src="images/1.jpg" alt="图说明">图的说明文字也可以写在这里。</span>，让它贴着这句话。</p>
```

就是 4.4 的旁注里塞了个 `<img>`。

### 4.6 正文栏里的图（最常用的插图）

```html
<figure>
  <img src="images/1.jpg" alt="图片内容说明">
  <figcaption>图 1：说明文字，会自动排到右边。</figcaption>
</figure>
```

三个要点：

1. 图片描述写进 `alt="..."`，看不见图的人靠它理解。
2. 不想带说明文字，就把 `<figcaption>` 整行删掉。
3. `<figure>` **不要**塞进 `<p>` 里面，单独占一块。

### 4.7 满宽的图（铺满整页）

```html
<figure class="fullwidth">
  <img src="images/1.jpg" alt="满宽图说明">
  <figcaption>图 2：说明文字。</figcaption>
</figure>
```

和 4.6 只差 `class="fullwidth"`。适合地图、时间线、大图表这类缩小就看不清的图。

### 4.8 题词（章节开头引用一段话）

```html
<div class="epigraph">
  <blockquote>
    <p>引用的那句话。</p>
    <footer>作者名，<cite>书名</cite></footer>
  </blockquote>
</div>
```

正文里普通的引用（不放在开头），直接把 `<blockquote><p>...</p></blockquote>` 独立成块就行。

### 4.9 表格

```html
<div class="table-wrapper">
  <table>
    <caption>表格标题</caption>
    <thead>
      <tr><th>列名一</th><th>列名二</th></tr>
    </thead>
    <tbody>
      <tr><td>内容</td><td>内容</td></tr>
      <tr><td>内容</td><td>内容</td></tr>
    </tbody>
  </table>
</div>
```

记忆方式：

- `tr` = 一行（table row）
- `th` = 表头格子，会**自动加粗**吗？不会。这里的表头只是普通字重的字，区别只在于它上下各有一条横线
- `td` = 普通格子
- `thead` / `tbody` = 表头区 / 内容区

外面那层 `<div class="table-wrapper">` 是关键：窄屏幕上它让表格可以横向滑动，而不是把页面撑破。

> **重要事实**：官方 tufte-css 1.9.0 根本**没有写表格的边框样式**。你直接用 `<table>` 会看到一张没有线的白板。上面那些横线是 `assets/tufte/local.css` 里的第 4 节补的（Tufte 书里的 booktabs 风格：只有横线，没有竖线）。

### 4.10 代码

行内一小段：

```html
<p>用 <code>python3 -m http.server</code> 起一个本地网站。</p>
```

整段代码：

```html
<pre><code>第一行
第二行</code></pre>
```

代码块会自己限制宽度并出现横向滚动条。

> **坑**：代码内容里如果出现 `<` 或 `>`，必须写成 `&lt;` 和 `&gt;`，否则浏览器会把它当成标签解析，页面直接乱掉。这是 HTML 的通用规则，不是这套样式特有的。

### 4.11 列表

```html
<ul>
  <li>第一项</li>
  <li>第二项</li>
</ul>

<ol>
  <li>第一步</li>
  <li>第二步</li>
</ol>
```

`ul` 是圆点列表，`ol` 是数字列表。

### 4.12 链接

```html
<p>参考<a href="https://example.com">这个网站</a>。</p>
```

这套样式里链接**和正文同色、带下划线、鼠标移上去不变色**（作者刻意如此，他认为蓝字刺眼）。

### 4.13 分节横线

```html
<hr>
```

单独一行，宽度自动是正文的 55%。

### 4.14 嵌入视频

```html
<figure class="iframe-wrapper">
  <iframe src="视频地址" title="视频说明" allowfullscreen></iframe>
</figure>
```

外层那个 `figure` 自带 16:9 比例，所以视频不会变形。不要自己算高度。

---

## 5. 出错自查表

| 你看到的现象 | 原因 | 怎么改 |
| --- | --- | --- |
| 文字拉满整个屏幕，右边没留白 | 段落的 `<p>` 没套在 `<section>` 里 | 补上 `<section>` |
| 边注跑到屏幕外面，或被切掉 | 内容没包在 `<article>` 里 | 补上 `<article>` |
| 电脑上正常，手机上点编号没反应 | 边注三个标签之间断开了（回车或空格） | 删掉所有换行和空格，连成一串 |
| 编号重复、或编号不连续 | 两个边注用了同一个 `id` | 搜索 `sn-`，第 n 条改成 `sn-n` |
| 边注编号点了没用 | `for="..."` 和 `id="..."` 写的不一样 | 两边写成完全相同的字 |
| 页面样式完全没生效（白底黑字、无衬线） | 两个 `<link>` 路径写错，或文件挪了位置 | 确认 `assets/tufte/tufte.css` 这个相对路径对得上 |
| Chrome 里字体不是 Tufte 那个样子 | 直接双击 html 打开，`file://` 下字体被浏览器拦了 | 用 `python3 -m http.server` 或 Live Server |
| 图不显示 | `src="images/1.jpg"` 路径错，或文件不在了 | 用相对路径，确认图片真的在那个位置 |
| 表格完全没有线 | 这是官方样式的原生状态 | 别自己加样式，看我给你的 `local.css` 第 4 节 |
| 粘贴了中文全角引号/空格进标签里 | `class="…"` 里混入了全角的 `”` 或空格 | 标签内的符号一律用英文半角 |

---

## 6. 中文写文章要特别注意的几件事

1. **`newthought` 对中文无效。** 见 4.2。中文一律用 `<h2>` 分节。
2. **行高专门调宽了。** 这套样式原生行距（1.43 倍）是给拉丁字母设计的，汉字挤在一起不好读，已在 `local.css` 里放宽到约 1.57 倍。
3. **字体是「一半英文一半中文」的组合。** ET Book 只有拉丁字符，所以你看到的英文和数字是 Tufte 原版字体，中文会自动换成你电脑上的宋体类字体（顺序：思源宋体 → 苹方/宋体 → 系统默认）。想指定中文用某款字体，看第 8 节。
4. **标点挤压只在 Chrome 里生效。** 作用是避免行尾的「。」「，」把右边挤出一道锯齿。其他浏览器会忽略，不影响阅读。

---

## 7. 「我想做 X」速查

| 我想…… | 用这个 |
| --- | --- |
| 加一段话 | `<p>…</p>` |
| 加一个小标题 | `<h2>…</h2>` |
| 加一条引用出处，放到页面右边并自动编号 | 4.3 的边注 |
| 加一句旁白，不带编号 | 4.4 的旁注 |
| 插图 | 4.6 |
| 插一张要大展示的图 | 4.7 加 `class="fullwidth"` |
| 放表格 | 4.9 |
| 放代码 | 4.10 |
| 让数字显示成老式排版（3、4、7 会下沉） | 给数字包一层 `<span class="numeral">79</span>` |
| 让某几个字用小号大写（只对英文有效） | `<span class="newthought">Latin</span>` |
| 让一段文字左右都对齐 | 不建议，这套风格的右边缘就该是自然的锯齿 |
| 删掉副标题 | 删掉 `<p class="subtitle">` 那一整行 |
| 换成自己的图片 | 把 `images/1.jpg` 替换掉，文件名保持一致最省事 |

---

## 8. 想改样式（不懂 CSS 也能改的地方）

打开 `assets/tufte/local.css`，里面按编号分了 4 节，每节开头都有中文注释说明在干什么：

| 文件里的编号 | 管什么 | 例子 |
| --- | --- | --- |
| 1) | 字体 | 想换中文宋体的优先级，改 `body { font-family: ... }` 那一列的先后顺序 |
| 2) | 行高 | `line-height: 2.2rem` 就是行距。嫌挤改大，嫌松改小 |
| 3) | 中文标点挤压 | 一般不用动 |
| 4) | 表格横线 | 想让表格线变细，把 `2px` 改成 `1px` |

改颜色（页面底色、正文颜色）不在这里，在 `assets/tufte/tufte.css` 里的 `body` 那几行：

```css
background-color: #fffff8;   /* 页面底色，纸白 */
color: #111;                 /* 正文颜色，近黑 */
```

**改之前先复制一份备份**，或者在文件顶上写一行注释记下你改了什么。`tufte.css` 是官方原文件，改了以后升级版本会比较麻烦。

---

## 9. 这套东西「没有」的功能

避免你找半天。以下都是 tufte-css **故意不做**的（作者原话：不在项目范围内）：

- **没有 JavaScript**，所以：没有折叠目录、没有图片灯箱、没有搜索。边注在手机上的展开是靠隐藏的复选框实现的纯 CSS 技巧，不是脚本。
- **没有表格外观样式**（已经帮你补上了，见 4.9）。
- **没有打印样式**，打印出来是网页的样子。
- **没有暗色模式开关**，但会**跟随你系统**：系统是暗色，页面自动变暗（`prefers-color-scheme`）。
- **没有自动生成目录、页码、脚注编号复用**。边注编号是自动的，但你把边注从第 3 条移到第 5 条，编号会自己重排——这是好事，不要手工写数字。
- **不集成任何博客系统**。想接 Markdown、Hugo、Quarto 这些，得另找它们自己的 Tufte 主题。

---

## 附：改文章的标准流程

1. 复制一份 `tufte.html`，改个名字，比如 `my-post.html`。
2. 用编辑器打开，改 `<title>`、`<h1>`、`<p class="subtitle">`。
3. 一段一段替换 `<p>` 里的中文，需要分节就加 `<section>`。
4. 需要边注，就从 `tufte-guide.md` 第 4.3 节复制，**记得把 `sn-1` 改成没出现过的名字**。
5. 保存，刷新浏览器看效果。改窄窗口到手机宽度，检查边注能不能点开。
6. 全文搜索 `sn-` 和 `mn-`，确认没有重复的 `id`。
