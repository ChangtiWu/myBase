# Latex使用笔记

使用字体颜色：

```
\usepackage{color}
\textcolor{color}{text}
```

使用删除线、波浪线等：

```
\usepackage{ulem}
\sout{}
```



```
\usepackage{booktabs}
\toprule
\midrule
\bottomrule
```



打勾叉：

```
\usepackage{bbding}
```



使用latex的subfigure并排放置多张图

```
\usepackage{graphicx}
\usepackage{subfigure}
```

插入eps图片：

```
\usepackage{graphicx}
\usepackage{epstopdf}
```



如果想让图表横跨双栏，在标签上加*：

```
\begin{table*}[htbp]
\end{table*}

\begin{figure*}[htbp]
\end{figure*}
```

