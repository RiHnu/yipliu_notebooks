# 超链接
> [overleaf博客](https://www.overleaf.com/learn/latex/Hyperlinks)
\usepackage{hyperref}
\hypersetup{
    colorlinks=true,                 ->  Links will be coloured 默认是红色
    linkcolor=blue,                  ->  文中的 cross-referenced elements 将以蓝色显示
    filecolor=magenta,               ->  对 local file 将是 magenta 颜色
    urlcolor=cyan,                   ->  对 web site   将是 cyan 颜色
    pdftitle={Overleaf Example},     ->  当 pdf 阅读器打开 该文件时 显示的文件名称
    pdfpagemode=FullScreen,          ->  当 Pdf 阅读器打开 该文件时，将以全屏显示
    }

\urlstyle{same}



# 公式、图标文中引用
>[overleaf博客](https://www.overleaf.com/learn/latex/Aligning_equations_with_amsmath)

\begin{equation} \label{eu_eqn}
e^{\pi i} + 1 = 0
\end{equation}

The beautiful equation \ref{eu_eqn} is known as the Euler equation.


在公式旁边 写上 \label{eu_eqn}

在需要引用的时候写上 \ref{eu_eqn}



# 表格
[overleaf](https://www.overleaf.com/learn/latex/Tables)
```latex
\documentclass{article}
\usepackage{array}
\begin{document}
\begin{center}
\begin{tabular}{ | m{5em} | m{1cm}| m{1cm} | } 
  \hline
  cell1 dummy text dummy text dummy text& cell2 & cell3 \\ 
  \hline
  cell1 dummy text dummy text dummy text & cell5 & cell6 \\ 
  \hline
  cell7 & cell8 & cell9 \\ 
  \hline
\end{tabular}
\end{center}
\end{document}
```
m{5em} 设置第一列的长度为 5em
m{1cm} 是第二列，第三列的长度

对齐参数是：
- m: middle
- p: top
- b: bottom


# 列表
[overleaf解释](https://www.overleaf.com/learn/latex/Lists)
## itemize
无序列表

## enumerate
有序列表

## description
描述性列表