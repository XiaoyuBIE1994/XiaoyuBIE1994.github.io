---
layout: post
title: LaTex常用数学符号整理
category: 实用工具
tags: latex
---



在论文和博客的写作中，经常会用到Latex的语法来书写数学公式，一份详细的数学符号对照表必不可少，本文重写了部分[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)，用以熟悉相关的语法，也以免在这一网站宕机给公式的书写带来不便



## 1. 常用公式

|     描述     |                  写法                  |                效果展示                |
| :----------: | :------------------------------------: | :------------------------------------: |
|    上下标    |               a_1 / e_x                |             $a_1$ / $e_x$              |
|    平方根    |               \sqrt\{x\}               |               $\sqrt{x}$               |
| 上下方水平线 |  \overline\{m+n\} / \underline\{m+n\}  |  $\overline{m+n}$ / $\underline{m+n}$  |
| 上下方大括号 | \overbrace\{m+n\} / \underbrace\{m+n\} | $\overbrace{m+n}$ / $\underbrace{m+n}​$ |
|     向量     |                 \vec a                 |                $\vec a$                |
|     分数     |            \frac\{1\}\{2\}             |             $\frac{1}{2}$              |
|     求和     |             \sum_\{i=1\}^n             |         $\sum\limits_{i=1}^n$          |
| 积分 | \int_0^\{\pi/2\} | $\int_0^{\pi/2}​$  |
| 累乘 | \prod_\epsilon | $\prod\limits_\epsilon$ |
| 优化 | \mathop\{\arg\min\}_\{\theta\} | ​$\mathop{\arg\min}\limits_{\theta}$ |



#### 1.1 大尺度运算符

|   符号    |  写法   |    符号     |   写法    |    符号     |   写法    |     符号     |    写法    |
| :-------: | :-----: | :---------: | :-------: | :---------: | :-------: | :----------: | :--------: |
|  $\sum$   |  \sum   |  $\bigcup$  |  \bigcup  |  $\bigvee$  |  \bigvee  | $\bigoplus$  | \bigoplus  |
|  $\prod$  |  \prod  |  $\bigcap$  |  \bigcap  | $\bigwedge$ | \bigwedge | $\bigotimes$ | \bigotimes |
| $\coprod$ | \coprod | $\bigsqcup$ | \bigsqcup |             |           |  $\bigodot$  |  \bigodot  |
|  $\int$   |  \int   |   $\oint$   |   \oint   |             |           | $\biguplus$  | \biguplus  |



#### 1.2 矩阵

需要 `amsmath` 宏包：

```latex
\[ \begin{pmatrix} a&b\\\\c&d \end{pmatrix} \quad
\begin{bmatrix} a&b\\\\c&d \end{bmatrix} \quad
\begin{Bmatrix} a&b\\\\c&d \end{Bmatrix} \quad
\begin{vmatrix} a&b\\\\c&d \end{vmatrix} \quad
\begin{Vmatrix} a&b\\\\c&d \end{Vmatrix} \]
```


$$
\begin{pmatrix} a&b\\c&d \end{pmatrix} \quad
\begin{bmatrix} a&b\\c&d \end{bmatrix} \quad
\begin{Bmatrix} a&b\\c&d \end{Bmatrix} \quad
\begin{vmatrix} a&b\\c&d \end{vmatrix} \quad
\begin{Vmatrix} a&b\\c&d \end{Vmatrix}
$$



使用 `smallmatrix` 环境，可以生成行内公式的小矩阵：

```latex
Marry has a little matrix $ ( \begin{smallmatrix} a&b\\c&d \end{smallmatrix} ) $
```


$$
\text{Marry has a little matrix } ( \begin{smallmatrix} a&b\\c&d \end{smallmatrix} )
$$



#### 1.3 括号


| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $($ | ( | $)$ | ) | $\uparrow$ | \uparrow | $\Uparrow$ | \Uparrow |
| $\lbrack$ | \\[ or \lbrack | $\rbrack$ | \\] or \rbrack | $\downarrow$ | \downarrow | $\Downarrow$ | \Downarrow |
| $\lbrace$ | \\{ or \lbrace | $\rbrace$ | \\} or \rbrace | $\updownarrow$ | \updownarrow | $\Updownarrow$ | \Updownarrow |
| $\langle$ | \langle | $\rangle$ | \rangle | $\vert$ | \| or \vert | $\Vert$ | \parallel |
| $\lfloor$ | \lfloor | $\rfloor$ | \rfloor | $\lceil$ | \lceil | $\rceil$ | \rceil |
| $/$ | / | $\backslash$ | \backslash |  | |  |  |
| $\lgroup$ | \lgroup | $\rgroup$ | \rgroup | $\lmoustache$ | \lmoustache | $\rmoustache$ | \rmoustache |
| $\arrowvert$ | \arrowvert | $\Arrowvert$ | \Arrowvert | $\bracevert$ | \bracevert |  |  |



- 不同大小的括号 `\Bigg ( \bigg [ \Big \{\big \langle \left \vert \parallel \frac{a}{b}  \parallel \right \vert \big \rangle \Big \} \bigg ] \Bigg )`: 

$$
  \Bigg ( \bigg [ \Big \{\big \langle \left \vert \| \frac{a}{b} \| \right \vert \big \rangle \Big \} \bigg ] \Bigg )
$$

- 自适应大小的括号 `\left( \frac{a}{b} \right)`：

$$
\left( \frac{a}{b} \right)
$$

- 单边括号 `\left . \frac{a}{b} \right \rbrace` :  

$$
\left . \frac{a}{b} \right \}
$$



- 混合括号 `\left \langle \psi \right \vert` : 

$$
\left \langle \psi \right \vert
$$





#### 1.4 空格

LaTex 在数学公式中的字符间隔是默认自动调整的，直接输入空格会被忽略掉，当我们需要自定义字母间隔时，需要手动输入空格：

| 空格         | 写法       | 显示         | 备注           |
| ------------ | ---------- | ------------ | -------------- |
| 两个quad空格 | a \qquad b | $a \qquad b$ | 两个*m*的宽度  |
| quad空格     | a \quad b  | $a \quad b$  | 一个*m*的宽度  |
| 大空格       | a\ b       | $a\ b$       | 1/3*m*宽度     |
| 中等空格     | a\;b       | $a\;b$       | 2/7*m*宽度     |
| 小空格       | a\,b       | $a\,b$       | 1/6*m*宽度     |
| 没有空格     | ab         | $ab$         |                |
| 紧贴         | a\!b       | $a\!b$       | 缩进1/6*m*宽度 |



## 2. 重音符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\hat{a}$ | \hat\{a\} | $\check{a}$ | \check\{a\} | $\tilde{a}$ | \tilde\{a\} | $\acute{a}$ | \acute\{a\} |
| $\grave{a}$ | \grave\{a\} | $\dot{a}$ | \dot{a\} | $\ddot{a}$ | \ddot{a\} | $\breve{a}$ | \breve{a\} |
| $\bar{a}$ | \bar{a\} | $\vec{a}$ | \vec{a\} | $\widehat{A}$ | \widehat{A\} | $\widetilde{A}$ | \widetilde{A\} |



## 3. 希腊字母

#### 3.1 小写希腊字母

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\alpha$ | \alpha | $\theta$ | \theta | $o$ | o | $\upsilon$ | \upsilon |
| $\beta$ | \beta | $\vartheta$ | \vartheta | $\pi$ | \pi | $\phi$ | \phi |
| $\gamma$ | \gamma | $\iota$ | \iota | $\varpi$ | \varpi | $\varphi$ | \varphi |
| $\delta$ | \delta | $\kappa$ | \kappa | $\rho$ | \rho | $\chi$ | \chi |
| $\epsilon$ | \epsilon | $\lambda$ | \lambda | $\varrho$ | \varrho | $\psi$ | \psi |
| $\varepsilon$ | \varepsilon | $\mu$ | \mu | $\sigma$ | \sigma | $\omega$ | \omega |
| $\zeta$ | \zeta | $\nu$ | \nu | $\varsigma$ | \varsigma |  | |
| $\eta$ | \eta | $\xi$ | \xi | $\tau$ | \tau |  | |



#### 3.2 大写希腊字母

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\Gamma$ | \Gamma | $\Lambda$ | \Lambda | $\Sigma$ | \Sigma | $\Psi$ | \Psi |
| $\Delta$ | \Delta | $\Xi$ | \Xi | $\Upsilon$ | \Upsilon | $\Omega$ | \Omega |
| $\Theta$ | \Theta | $\Pi$ | \Pi | $\Phi$ | \Phi |  | |



## 4. 二元符号

#### 4.1 二元关系符

可以在下述的命令中加上 \not 来得到

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $<$ | < | $>$ | > | $=$ | = | $\leq$ | \leq or \le |
| $\geq$ | \geq or \ge | $\equiv$ | \equiv | $\ll$ | \ll | $ \gg$ | \gg |
| $\doteq$ | \doteq | $\prec$ | \prec | $\succ$ | \succ | $\sim$ | \sim |
| $\preceq$ | \preceq | $\succeq$ | \succeq | $\simeq$ | \simeq | $\approx$ | \approx |
| $\subset$ | \subset | $\supset$ | \supset | $\subseteq$ | \subseteq | $\supseteq$ | \supseteq |
| $\sqsubset$ | \sqsubset | $\sqsupset$ | \sqsupset | $\sqsubseteq$ | \sqsubseteq | $\sqsupseteq$ | \sqsupseteq |
| $\cong$ | \cong | $\Join$ | \Join | $\bowtie$ | \bowtie | $\propto$ | \propto |
| $\in$ | \in | $\ni$ | \ni or \owns | $\vdash$ | \vdash | $\dashv$ | \dashv |
| $\models$ | \models | $\mid$ | \mid | $\parallel$ | \parallel | $\perp$ | \perp |
| $\smile$ | \smile | $\frown$ | \frown | $\asymp$ | \asymp | $:$ | : |
| $\notin$ | \notin | $\neq$ | \neq or \ne |  | |  | |



#### 4.2 二元运算符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $+$ | + | $-$ | - | $\times$ | \times | $\div$ | \div |
| $\pm$ | \pm | $\mp$ | \mp | $\triangleleft$ | \triangleleft | $\triangleright$ | \triangleright |
| $\cdot$ | \cdot | $ \setminus$ | \setminus | $\star$ | \star | $\ast$ | \ast |
| $\cup$ | \cup | $\cap$ | \cap | $\sqcup$ | \sqcup | $\sqcap$ | \sqcap |
| $\vee$ | \vee or \lor | $\wedge$ | \wedge or \land | $\circ$ | \circ | $\bullet$ | \bullet |
| $\oplus$ | \oplus | $\ominus$ | \ominus | $\odot$ | \odot | $\oslash$ | \oslash |
| $\otimes$ | \otimes | $\bigcirc$ | \bigcirc | $\diamond$ | \diamond | $\uplus$ | \uplus |
| $\bigtriangleup$ | \bigtriangleup | $\bigtriangledown$ | \bigtriangledown | $\lhd$ | \lhd | $\rhd$ | \rhd |
| $\unlhd$ | \unlhd | $\unrhd$ | \unrhd | $\amalg$ | \amalg | $\wr$ | \wr |
| $\dagger$ | \dagger | $\ddagger$ | \ddagger | | | | |





## 5. 箭头

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\gets$ | \leftarrow or \gets | $\to$ | \rightarrow or \to | $\longleftarrow$ | \longleftarrow | $\longrightarrow$ | \longrightarrow |
| $\uparrow$ | \uparrow | $\downarrow$ | \downarrow | $\updownarrow$ | \updownarrow | $\leftrightarrow$ | \leftrightarrow |
| $\Uparrow$ | \Uparrow | $\Downarrow$ | \Downarrow | $\Updownarrow$ | \Updownarrow | $\longleftrightarrow$ | \longleftrightarrow |
| $\Leftarrow$ | \Leftarrow | $\Longleftarrow$ | \Longleftarrow | $\Rightarrow$ | \Rightarrow | $\Longrightarrow$ | \Longrightarrow |
| $\Leftrightarrow$ | \Leftrightarrow | $\Longleftrightarrow$ | \Longleftrightarrow | $\mapsto$ | \mapsto | $\longmapsto$ | \longmapsto |
| $\nearrow$ | \nearrow | $\searrow$ | \searrow | $\swarrow$ | \swarrow | $\nwarrow$ | \nwarrow |
| $\hookleftarrow$ | \hookleftarrow | $\hookrightarrow$ | \hookrightarrow | $\rightleftharpoons$ | \rightleftharpoons | $\iff$ | \iff |
| $\leftharpoonup$ | \leftharpoonup | $\rightharpoonup$ | \rightharpoonup | $\leftharpoondown$ | $\leftharpoondown | $\rightharpoondown$ | \rightharpoondown |
| $\leadsto$ | \leadsto | | | | | | |



## 6. 其他符号

|      符号      | 写法          | 符号         | 写法       | 符号        | 写法      | 符号         | 写法       |
| :------------: | ------------- | ------------ | ---------- | ----------- | --------- | ------------ | ---------- |
|    $\dots$     | \dots         | $\cdots$     | \cdots     | $\vdots$    | \vdots    | $\ddots$     | \ddots     |
|    $\hbar$     | \hbar         | $\imath$     | \imath     | $\jmath$    | \jmath    | $\ell$       | \ell       |
|     $\Re$      | \Re           | $\Im$        | \Im        | $\aleph$    | \aleph    | $\wp$        | \wp        |
|   $\forall$    | \forall       | $\exists$    | \exists    | $\mho$      | \mho      | $\partial$   | \partial   |
|      $'$       | '             | $\prime$     | \prime     | $\emptyset$ | \emptyset | $\infty$     | \infty     |
|    $\nabla$    | \nabla        | $\triangle$  | \triangle  | $\Box$      | \Box      | $\Diamond$   | \Diamond   |
|     $\bot$     | \bot          | $\top$       | \top       | $\angle$    | \angle    | $\surd$      | \surd      |
| $\diamondsuit$ | \diamondsuit  | $\heartsuit$ | \heartsuit | $\clubsuit$ | \clubsuit | $\spadesuit$ | \spadesuit |
|     $\neg$     | \neg or \lnot | $\flat$      | \flat      | $\natural$  | \natural  | $\sharp$     | \sharp     |



## 7. 其他

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: |
| $\S$ | \S | $\P$ | \P |  |  |



|     字体      |    写法     |
| :-----------: | :---------: |
| $\mathbb{R}$  | \mathbb{R}  |
| $\mathcal{L}$ | \mathcal{L} |



PS: 原文中还有其他符号（如AMS运算符，希伯来字母等），但MathJax中或是不支持，或是使用频率太低，故而在这里不再写入



## 参考

[1] [常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)

[2] [LaTeX Notes 雷太赫排版系统简介 v2.56 包太雷](https://github.com/huangxg/lnotes)



