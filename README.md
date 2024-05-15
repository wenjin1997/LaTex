# LaTeX学习笔记
### 书籍信息
书名：《LaTeX2e完全学习手册》

作者：胡伟 

出版社：清华大学出版社, 2011.1
### 笔记
* 在编译源文件时，LaTeX将忽略命令之后的所有空格，如果希望在命令后保留一个空格，
可在命令后紧跟一对空花括号{}和一个空格，或在命令后紧跟一个反斜杠\和一个空格。
### 摘要与关键词
```
\begin{abstract}
	\noindent %摘要无缩进
	{\bf 摘{} 要：}
	{\small 摘要内容}
	\newline %另起一行
	\textbf{关键词：}第一个关键词、第二个关键词、第三个关键词
\end{abstract}
```
### 展示方程组
如果要展示方程组，则可以放在case中，如下所示。同时一定要调用宏包amsmath。
```
\begin{equation} \label{eq_arry}%要调用宏包amsmath
	\begin{cases}
		{f}_1({x}_1,{x}_2,\cdots,{x}_n)=0\\
		{f}_2({x}_1,{x}_2,\cdots,{x}_n)=0\\
		\qquad \qquad \vdots\\
		{f}_n({x}_1,{x}_2,\cdots,{x}_n)=0
	\end{cases}	
\end{equation}
```
### 长表格
* 如果要展示的表格比较长，或者表格可能呈现在两页，就用longtable。 
* 使用longtable时需要引用的包为`\usepackage{booktabs,multirow,longtable}`。  
* `{ccccc}`表示表格的列数，这里是5列。 
* 表格标题：`\caption[]{表格标题}`，如`\caption[]{初值为$x_1=2,x_2=3$迭代结果表(续表)}`。
* `\multicolumn{4}{r}{\footnotesize 接上页}`这里的4是和表格的列数有关的，如果是n列，就设置为n-1。 
* 总结需要修改的地方有`\begin{longtable}{ccccc}`、`\caption[]{初值为$x_1=2,x_2=3$迭代结果表(续表)}\\`、`\multicolumn{4}{r}{\footnotesize 接上页}\\\hline`、
`\hline\multicolumn{4}{r}{\footnotesize 接下页}\\`，当然还有就是表格的内容。

```
\begin{longtable}{ccccc}
    \caption{初值为$x_1=2,x_2=3$迭代结果表}\\\hline
    $k$ & $x_1$ & $x_2$ & 
    \multicolumn{1}{c}{$\varepsilon$} \\\hline
    \endfirsthead
    \caption[]{初值为$x_1=2,x_2=3$迭代结果表(续表)}\\
    \multicolumn{4}{r}{\footnotesize 接上页}\\\hline
    $k$ & $x_1$ & $x_2$ & \multicolumn{1}{c}{$\varepsilon$}\\
    \hline\endhead
    \hline\multicolumn{4}{r}{\footnotesize 接下页}\\
    \endfoot\hline\hline\endlastfoot
    0 & 2 & 3  &   \\
    1 & 2.3577595003166416 & 2.0729245184716087 & 0.9937106261472258  \\
    2 & 2.6453725887186104 & 1.6564033096056225 & 0.5061730989052077  \\
    3 & 2.682536572837465  & 1.569304046831083  & 0.09469658542658627  \\
    4 & 2.687055240456386  & 1.5652630719960805 & 0.006061999230238282  \\
    5 & 2.687059785035585  & 1.5652561930950146 & 8.244542435561323e-06  \\
    6 & 2.6870597850598585 & 1.5652561930721185 & 3.336816135191078e-11  \\
\end{longtable}
```
### 配置展示python代码
展示python代码用`lstlisting`，配置代码如下：
```
\documentclass{article}
\usepackage{ctex}

\usepackage{listings}
\usepackage{color}

\definecolor{dkgreen}{rgb}{0,0.6,0}
\definecolor{gray}{rgb}{0.5,0.5,0.5}
\definecolor{mauve}{rgb}{0.58,0,0.82}

\lstset{frame=tb,
  language=Python,
  aboveskip=3mm,
  belowskip=3mm,
  showstringspaces=false,
  columns=flexible,
  basicstyle={\small\ttfamily},
  numbers=left, % 设置为none则不显示行号
  numberstyle=\tiny\color{gray},
  keywordstyle=\color{blue},
  commentstyle=\color{dkgreen},
  stringstyle=\color{mauve},
  breaklines=true,
  breakatwhitespace=true,
  tabsize=3
}


\begin{document}

下面是python代码。
\begin{lstlisting}
    print("Hello World!)
\end{lstlisting}


\end{document}
```
### 参考文献
* 新建bib文件夹，在bib文件夹下新建sample.bib文档，文档内容如下。主要是自己要引用的参考文献内容。
```
%# -*- coding: utf-8-unix -*-

@Book{numerical_1,
  Title                    = {现代数值计算方法},
  Address                  = {北京},
  Author                   = {马昌凤 and 林伟川},
  Publisher                = {科学出版社},
  Year                     = {2008},
  Month                    = {6}
}

@Book{numerical_2,
  Title                    = {数值分析},
  Address                  = {北京},
  Author                   = {钟尔杰 and 黄廷祝},
  Publisher                = {高等教育出版社},
  Year                     = {2004},
  Month                    = {7}
}
```
* 在文中需要引用参考文献的地方`\cite{}`
* 在主目录下要包括四个文件
* 为正常生成参考文献，一定要用biber命令运行，需要在编译文档的主目录下包含这四个文件gb7714-2015.bbx, gb7714-2015ay.bbx, gb7714-2015.cbx, gb7714-2015ay.cbx。  
运行代码顺序必须为
```
xelatex document.tex
biber document
xelatex document.tex
xelatex document.tex
```
* 关于参考文献问题，可查看[这里](https://github.com/hushidong/biblatex-gb7714-2015#jumptotutorial)。
