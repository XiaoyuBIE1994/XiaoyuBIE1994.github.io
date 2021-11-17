---
layout: post
title: LaTex 语法总结
category: 实用工具
tags: latex

---


<style>
img{
    width: 60%;
    padding-left: 20%;
}
</style>



第一次接触 LaTex 是刚来法国的时候，那时候有很多的TP实验要做，而法国实验小伙伴都是用 LaTex 来写报告。刚从国内过来的我对此却一窍不通，抱着不能打酱油的心态，开始了 LaTex 的学习路程，中间陆陆续续看过了许多的入门指南和技巧总结。

总体而言，LaTex 的入门非常简单，只需要一个下午的时间就可以进行基本的写作，但实际的使用中还是会碰到各式各样的问题，网上很容易找到答案，但时间过久了后还是容易忘记，所以决定在这里对所学习的 LaTex 知识进行整理，记录下基本使用方法和各类技巧，以备查询。

> 因为暂时没有中文的写作需求，这里暂时不整理中文和中英文混排的相关内容
>
> 详细的文档可以参考刘海洋老师的《LaTex入门》一书，本文只整理了自己常遇到的困难



## 1.  LaTex 介绍

#### 1.1 编辑器

LaTeX 是基于 TeX 的排版系统，利用 Tex 的控制命令，定义了许多新的控制命令并封装成一个可执行的文件，这个可执行文件会解释 LaTex 新定义的命令成为 Tex 的控制命令，并最后交由引擎进行排版。Tex 的源代码是后缀为 `.tex` 的纯文本文件，使用任意的纯文本编辑器都可以对 `.tex` 文件进行编辑，但实际在写 LaTex 时主要使用以下三种方法：

- online编辑方式，推荐使用 [overleaf](https://www.overleaf.com/) ，优点是不用自己配置环境，可以多人同步协作，缺点是需要有网络连接，且刷新较慢
- 通用文本编辑器+latex插件，例如 [MacOS下基于 VS Code 的 LaTex 配置](http://www.biexiaoyu1994.com/%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/2019/08/11/Mac_Latex/) ，缺点是配置麻烦
- 用于 Tex 的编辑+编译集成软件，如 [Texworks](http://www.tug.org/texworks/)，缺点是太丑，功能单一



#### 1.2 排版工具

Tex 可以有不同的排版工具，例如 pdfTeX, pdfLaTeX, XeTeX, XeLaTeX 等，其中大致的区别如下：

- pdfTeX-pdfLaTeX：pdfTeX可以直接输出 pdf 文件，而不是 Tex 引擎输出的 .dvi 文件，而 pdfLaTeX 添加了对 LaTex 语法的解释

-  XeTeX - XeLaTeX：添加了对 Unicode 字符的支持，也就是可以处理中日韩字符



## 2 LaTex 入门

#### 2.1 基础架构

LaTex 的初衷是让人集中精力于内容的创作，所以基本的语法并不复杂，如下：

```latex
\documentclass{article}
% 这里是导言区
\begin{document}
Hello, world!
\end{document}
```

其中有几点需要注意：

- LaTex 中以反斜杠 `\` 开头的叫做 `控制序列`，是以第一个 **空格或者非字母** 的字符结束的一串文字，控制序列不会被输出，但会影响输出文档的结果，控制序列对于字母的大小写是敏感的

- 控制序列后接上的大括号 `{}`表示必要参数，部分控制序列后会接上一组方括号 `[]`，里面是可选参数

- 控制序列中 `begin` 和 `end`总是成对出现，这两个控制序列以及中间的内容称为 **环境**，他们之后的第一个必要参数总是一致的，被称为 **环境名**

- 从 `\documentclass{article}` 开始到 `\begin{document}` 之前的部分被称为导言区，用于对正篇文档进行设置

- 只有在 `document` 环境中的内容，才会被正常输出到文档中去或是作为控制序列对文档产生影响，`\end{document}` 之后插入任何内容都是无效的

- LaTex 中以 `%` 开头的是注释内容，如果需要输入百分号，需要在符号前插入反斜杠 `\%`

- 如果需要插入中文，第一句改为 `\documentclass[UTF8]{ctexart}`或者插入宏包 ：

  ```latex
  \documentclass{article}
  \usepackage{xeCJK} %调用 xeCJK 宏包
  \setCJKmainfont{SimSun} %设置 CJK 主字体为 SimSun （宋体）
  \begin{document}
  你好，world!
  \end{document}
  ```

  

#### 2.2 作者，标题和时间

LaTex 针对文章的基本信息编辑在 `document` 环境之前，可以设定作者，标题和时间，在 `document` 环境中使用 `\maketitle`来显示相关信息，如下：

```latex
\documentclass{rticle}
\title{Hello, world!}
\author{Lee}
\date{\today}
\begin{document}
\maketitle
hello,word!
\end{document}
```



#### 2.3 段落

在文档类 `article`/`ctexart` 中，定义了五个控制序列来调整行文组织结构：

- `\section{·}`
- `\subsection{·}`
- `\subsubsection{·}`
- `\paragraph{·}`
- `\subparagraph{·}`

> 在`report`/`ctexrep`中，还有`\chapter{·}`；在文档类`book`/`ctexbook`中，还定义了`\part{·}`。

>  `\tableofcontents`会插入目录



#### 2.4 文字排版

**字体大小：**

| 符号 | 长度 | 符号 | 长度               | 符号 | 长度                    |
| ---- | ---- | ---- | ------------------ | ---- | ----------------------- |
| in   | 英寸 | pt   | point, 1/72.27 in  | em   | 当前字体中字母 M 的宽度 |
| cm   | 厘米 | bp   | big point, 1/72 in | ex   | 当前字体中字母 x 的高度 |
| mm   | 毫米 | pc   | pica, 12 pt        | mu   | math unit,1/18 em       |

> point 是个传统印刷业采用的单位,而 big point 是 Adobe 推出 PostScript 时定义的新单位。em 是个相对单位,比如当前字体是 11pt 时,1em 就是 11pt;ex 和 mu 也是相对单位



**换行：**

Latex里面有多种换行方式，区别如下：

- 两个反斜杠 `\` ，换行后下一段首行顶头，不缩进
- 使用命令 `\newline` ，效果同上
- 两段之间空一行，换行后首行缩进



**首行缩进：**

一般Latex会自动首行缩进，如果不想缩进，可在段落前加上 `\noindent`



## 粗体和斜体

- `\textbf{}` 粗体
- `\textif{}` 斜体



**脚注：**

```latex
正文\footnote{脚注}
```



**注释：**

可以用百分号来标明注释，但大段文字的注释会比较麻烦，这里可以使用`verbatim` 宏包的 `comment` 环境：

```latex
\begin{comment}
...
\end{comment}
```



**列表：**

- 无序列表

```latex
\begin{itemize}
  \item C++
  \item Java
  \item HTML
\end{itemize}
```



- 有序列表

```latex
\begin{enumerate}
  \item C++
  \item Java
  \item HTML
\end{enumerate}
```



- 描述列表

```latex
\begin{description}
  \item[C++] 编 程 语 言
  \item[Java] 编 程 语 言
  \item[HTML] 标 记 语 言
\end{description}
```



**盒子：**

LaTex在排版时把每个对象 (小到一个字母,大到一个段落) 都视为一个矩形盒子 (box)，较为常见的是`\mbox`和 `\fbox`，前者把一组对象组合起来,后者在此基础上加了个边框





## 3. 数学公式

#### 3.1 基本语法

LaTex可以很方便的输入数学公式：

- 行内公式： `$ ... $` （ `\(...\)` 或 `\begin{math} ... \end{math}` 也可，但比较麻烦）
- 带编号的行间公式：  `\begin{equation} ... \end{equation}` 
- 不带编号的行间公式： `\[ ... \]` （`\begin{displaymath} ... \end{displaymath}` 或`\begin{equation*} ... \end{equation*}` 也可以，但麻烦）
-  plainTeX 风格的 `$$ ... $$` 可以用来插入不编号的行间公式。但是在 LaTeX 中这样做会改变行文的默认行间距，不推荐
- 具体公式，请参考 [LaTex常用数学符号整理](http://www.biexiaoyu1994.com/%E5%AE%9E%E7%94%A8%E5%B7%A5%E5%85%B7/2019/01/28/latex-math/)







## 4. 图片和表格

#### 4.1 插入图片

 `graphicx` 宏包提供的 `\includegraphics` 命令可以插入多种图片

```latex
\includegraphics[width = .8\textwidth]{a.jpg}
```

这里是插入 0.8 页面宽度的 a.jpg



#### 4.2 插入表格

`tabular` 环境提供了最简单的表格功能。它用 `\hline` 命令表示横线，在列格式中用 `|` 表示竖线；用 `&` 来分列，用 `\\` 来换行；每列可以采用居左、居中、居右等横向对齐方式，分别用 `l`、`c`、`r` 来表示

```latex
\begin{tabular}{|l|c|r|}
 \hline
操作系统& 发行版& 编辑器\\\\
 \hline
Windows & MikTeX & TexMakerX \\\\
 \hline
Unix/Linux & teTeX & Kile \\\\
 \hline
Mac OS & MacTeX & TeXShop \\\\
 \hline
通用 & TeX Live & TeXworks \\\\
 \hline
\end{tabular}
```



| 操作系统   | 发行版   | 编辑器    |
| ---------- | -------- | --------- |
| Windows    | MikTeX   | TexMakerX |
| Unix/Linux | teTeX    | Kile      |
| Mac OS     | MacTeX   | TeXShop   |
| 通用       | TeX Live | TeXworks  |



- tabular 里的参数中，`l c r`分别代表左对齐，居中和右对齐， `|` 代表显示纵向的网格线
- `\hline` 代表画出相应的水平网格线


#### 4.3 浮动体

插图和表格通常需要占据大块空间，所以在文字处理软件中我们经常需要调整他们的位置。`figure` 和 `table` 环境可以自动完成这样的任务；这种自动调整位置的环境称作浮动体(float)。以 `figure` 为例：



```latex
\begin{figure}[htbp]
\centering
\includegraphics{a.jpg}
\caption{Picture a}
\label{fig:a}
\end{figure}
```

- 这里 `htbp` 分别代表 here, top, bottom, float page，可以自动根据情况来决定图片的位置，如果需要强制放置图片在当前位置，可以使用 `\usepackage{float}` 宏包，然后将可选参数改为 `[H]`
- `\caption{...}` 代表图片的名字，会出现在图片的下方
- `\label{...}` 代表图片的标签，不会出现在图片中，但在其他地方可以用 ` \ref{}`来对图片进行引用，在生成的 pdf 中可以通过点击来快速跳转到相应的图片位置，而且` \ref{}`会自动生成对应图片的编号，这样在对文章进行更改后不必再重新改变文字中的编号



#### 4.4 多张子图

LaTex 可以使用一个 `figure` 来同时插入多张子图，如下：

```latex
\begin{figure} [h]
\begin{tabular}{c}
\includegraphics[width = 0.9\textwidth]{data_association.png} \\\\
\bf{(a)} \\\\
\includegraphics[width = 0.9\textwidth]{signal_level.png} \\\\
\bf{(b)} \\\\
\includegraphics[width = 0.9\textwidth]{feature_level.png} \\\\
\bf{(c)}
\end{tabular}
\caption{The three groups for map-perception-aided localization. (a) Data association based localization system. (b) Signal-level filter based localization. (c) Feature-level filter based localization. }
\label{local_system}
\end{figure}
```

效果如下：

![][1]



#### 4.5 minipage

LaTex 也可以通过插入 minipage 来实现同行插入多张子图，或者一半插入图片，另一半插入文字，如下：

```latex
\begin{figure}[h]
\begin{minipage}[c]{0.39\linewidth}
\includegraphics[width=\textwidth]{NLm}
\caption{Research window in non-local means denoising\cite{Goudail:01}}
\end{minipage}
\hfill
\begin{minipage}[c]{0.59\linewidth}
As shown in the left figure, the big window is the research window centered at x which is the pixel we want to denoise. In the research window, we build two patch windows with the same size. which are marked with gray in the figure. One is also centered at x  while the other is centered at y, a certain pixel moving in the research window.\\
We build the research window to define the range of all the pixels nearby which participate in the calculation and the patch window is used to calculate the similarity.
\vspace{2cm}
\end{minipage}
\end{figure}
```

效果如下：

![][2]


- `\linewidt`代表页面宽度
- `\hfill` 是个弹性填充命令，它会把两边的内容“推”得尽可能远
- `\vspace{2cm}` 代表插入 2cm 的垂直间距，水平方向可使用 ``\hspace{2cm}``


## 5. 代码块

Latex可以插入代码块，并进行背景的编辑：

- 加入宏包 `\usepackage{listings}`
- 代码段：

```latex
\begin{lstlisting}
% 代码段
\end{lstlisting}
```



- 代码块的基本设置：

  ```latex
  \lstset{
   columns=fixed,       
   numbers=left,                                        % 在左侧显示行号
   numberstyle=\tiny\color{gray},                       % 设定行号格式
   frame=none,                                          % 不显示背景边框
   backgroundcolor=\color[RGB]{245,245,244},            % 设定背景颜色
   keywordstyle=\color[RGB]{40,40,255},                 % 设定关键字颜色
   numberstyle=\footnotesize\color{darkgray},           
   commentstyle=\it\color[RGB]{0,96,96},                % 设置代码注释的格式
   stringstyle=\rmfamily\slshape\color[RGB]{128,0,0},   % 设置字符串格式
   showstringspaces=false,                              % 不显示字符串中的空格
   language=c++,                                        % 设置语言
  }
  ```

- 另一个格式：

```latex
  \lstset{ %
    language=Octave,                % the language of the code
    basicstyle=\footnotesize,           % the size of the fonts that are used for the code
    numbers=left,                   % where to put the line-numbers
    numberstyle=\tiny\color{gray},  % the style that is used for the line-numbers
    stepnumber=2,                   % the step between two line-numbers. If it's 1, each line 
                                    % will be numbered
    numbersep=5pt,                  % how far the line-numbers are from the code
    backgroundcolor=\color{white},      % choose the background color. You must add \usepackage{color}
    showspaces=false,               % show spaces adding particular underscores
    showstringspaces=false,         % underline spaces within strings
    showtabs=false,                 % show tabs within strings adding particular underscores
    frame=single,                   % adds a frame around the code
    rulecolor=\color{black},        % if not set, the frame-color may be changed on line-breaks within not-black text (e.g. commens (green here))
    tabsize=2,                      % sets default tabsize to 2 spaces
    captionpos=b,                   % sets the caption-position to bottom
    breaklines=true,                % sets automatic line breaking
    breakatwhitespace=false,        % sets if automatic breaks should only happen at whitespace
    title=\lstname,                 % show the filename of files included with \lstinputlisting;
                                    % also try caption instead of title
    keywordstyle=\color{blue},          % keyword style
    commentstyle=\color{dkgreen},       % comment style
    stringstyle=\color{mauve},         % string literal style
    escapeinside={\%*}{*)},            % if you want to add LaTeX within your code
    morekeywords={*,...}               % if you want to add more keywords to the set
    }
```



## 6. 参考文献

BibTex 使用数据库的方式管理参考文献，BibTex 文件为后缀为 `.bib`，文件格式如下：

```latex
@article{name1,
author = {作者, 多个作者用 and 连接},
title = {标题},
journal = {期刊名},
volume = {卷20},
number = {页码},
year = {年份},
abstract = {摘要, 这个主要是引用的时候自己参考的, 这一行不是必须的}
}

@book{name2,
author ="作者",
year="年份2008",
title="书名",
publisher ="出版社名称"
}
```

**在 LaTex 中使用 BibTex：**

- 在 `.tex` 正文中，引用的格式为 `\cite{...}`
- 设置参考文献的类型 ， `\bibliographystyle{...}`，可选参数有：
  - plain，标准类型，参考文献按作者的字母排序
  - unsrt，基本和 plain 一致，参考文献按引用顺序排序
  - alpha， 基本和 plain 一致，参考文献按作者名字和出版年份排序
  - abbrv ， 缩写格式
-  告诉LaTeX生成参考文献列表，在 LaTeX 的结束前输入 `\bibliography{bibfile}`



## 7. 版面设置

#### 7.1 页边距

 推荐使用 `greometry` 宏包：

```latex
\usepackage{geometry}
\geometry{papersize={20cm,15cm}}
\geometry{left=1cm,right=2cm,top=3cm,bottom=4cm}
```

这里表示纸张的长度设置为 20cm、宽度设置为 15cm、左边距 1cm、右边距 2cm、上边距 3cm、下边距 4cm

或者如下设置：

```latex
\usepackage[a4paper,top=3cm,bottom=2cm,left=3cm,right=3cm,marginparwidth=1.75cm]{geometry}
```

具体参考 [CTEX - 在线文档 - TeX/LaTeX 常用宏包 geometry](http://www.ctex.org/documents/packages/layout/geometry.htm)



#### 7.2 页眉/页脚

推荐使用  `fancyhdr` 宏包

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}
\chead{\date}
\rhead{152xxxxxxxx}
\lfoot{}
\cfoot{\thepage}
\rfoot{}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\headwidth}{\textwidth}
\renewcommand{\footrulewidth}{0pt}
```

具体参考 [CTEX - 在线文档 - TeX/LaTeX 常用宏包 fanchdr](http://www.ctex.org/documents/packages/layout/fancyhdr.htm)



#### 7.3 行间距

通过 `setspace` 宏包提供的命令来调整行间距，如下行距设置为字号的 1.5 倍：

```latex
\usepackage{setspace}
\onehalfspacing
```

> 字号的 1.5 倍并不等于1.5 倍行距



#### 7.4 段间距

可以通过修改长度 `\parskip` 的值来调整段间距，如下在原有的基础上，增加段间距 0.4em

```latex
\addtolength{\parskip}{.4em}
```



## 8. Latex样本实例

#### 8.1 Overleaf example

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{...}
\author{... }
\date{October 2019}

\usepackage{natbib}
\usepackage{graphicx}

\begin{document}

\maketitle

\section{Introduction}

\begin{figure}[h!]
\centering
\includegraphics[scale=1.7]{universe}
\caption{The Universe}
\label{fig:universe}
\end{figure}

\section{Conclusion}
``I always thought something was fundamentally wrong with the universe'' \citep{adams1995hitchhiker}

\bibliographystyle{plain}
\bibliography{references}
\end{document}	
```



#### 8.2 个性化报告模板

这一模板会在封面插入个性化设置的报告首页

```latex
\documentclass[a4paper]{article}

%% Language and font encodings
\usepackage[english]{babel} % 确保解释器为英文
\usepackage[utf8x]{inputenc} % 确认为UTF8x
\usepackage[T1]{fontenc} % 如果需要添加音标时使用这个包

%% Sets page size and margins
\usepackage[a4paper,top=3cm,bottom=2cm,left=3cm,right=3cm,marginparwidth=1.75cm]{geometry}

%% Useful packages
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage[colorinlistoftodos]{todonotes}
\usepackage[colorlinks=true, allcolors=blue]{hyperref}
\usepackage{url} % bibliography of website
\usepackage{booktabs} % complex table
\usepackage{float} % picture
\usepackage{cite}
\usepackage{subfigure} % enable to draw sub figures

\title{...}
\author{...}
\date{\vspace{-5ex}}

\begin{document}

\begin{titlepage}
	\centering
	\vspace{2cm}
    \includegraphics[width=16cm]{logo.png} % 添加logo
	\vfill
  
	\begin{huge} % 输入标题
		....
    \vspace{5cm}
	\end{huge}
    \vfill    
	
	\begin{Large} % 作者，或者其他信息，可重复添加
		Name \\
    \vspace{1cm}
	\end{Large}
	\\[0\baselineskip]
	\vfill
\end{titlepage}     
\newpage

\tableofcontents
\newpage

\begin{abstract}
...
\end{abstract}

\section{...}

\bibliographystyle{unsrt}
\bibliography{sample}
\end{document}
```







## 参考

[1] [一份其实很短的 LaTeX 入门文档](https://www.kancloud.cn/thinkphp/latex/41811)

[2] [CTEX - 在线文档 - TeX/LaTeX 常用宏包](http://www.ctex.org/documents/packages/layout/)

[3] [LaTeX Notes 雷太赫排版系统简介 v2.56 包太雷](https://github.com/huangxg/lnotes)

[4] [LaTeX入门-刘海洋](https://leegoogol.com/documents/LaTeX%E5%85%A5%E9%97%A8-%E5%88%98%E6%B5%B7%E6%B4%8B_.pdf)

[5] [LaTeX技巧23:BIBTeX制作参考文献](http://blog.sina.com.cn/s/blog_5e16f1770100fw68.html)

[6] [Latex插入代码块](https://www.jianshu.com/p/fb1c1c6f2d02)





[1]: https://res.cloudinary.com/bxy1994/image/upload/v1571751300/LaTex/latex_subgraphics.png
[2]:https://res.cloudinary.com/bxy1994/image/upload/v1571751501/LaTex/latex_minipage.png
