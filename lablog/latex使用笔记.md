# Latex使用笔记

## 文字

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



## 图片

### 并置多张图

使用latex的subfigure并排放置多张图。

```
\usepackage{graphicx}
\usepackage[caption=false,font=normalsize,labelfont=sf,textfont=sf]{subfig}
```

用`\\`换行，用`\hspace{1pt}`控制行内间距。

```latex
\begin{figure}[htbp]
	\centering
	\subfloat[The model size is 200,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_200000.pdf}}\hspace{1pt}
	\subfloat[The model size is 400,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_400000.pdf}}\\
	\subfloat[The model size is 600,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_600000.pdf}}\hspace{1pt}
	\subfloat[The model size is 800,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_800000.pdf}}\\
	\subfloat[The model size is 1,000,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_1000000.pdf}}\hspace{1pt}
	\subfloat[The model size is 1,200,000.]{\includegraphics[width=0.49\columnwidth]{fig/comp_1200000.pdf}}\\
	\caption{Average computational cost of each IoT device in each training round}
	\label{comp_cost}
\end{figure}
```

### 设置子图标题字体

修改开头的控制命令（原始）：
```latex
\usepackage[caption=false,font=normalsize,labelfont=sf,textfont=sf]{subfig}
```

为

```latex
\usepackage[caption=false,font=footnotesize,labelfont=rm,textfont=rm]{subfig}
```

其中font=footnotesize，表示修改大小为很小，可供选择的有：\tiny, \scriptsize, \footnotesize, \small, \normalsize, \large, \Large, \LARGE, \huge, \Huge，依次从小到大
labelfont=rm,textfont=rm，表示修改字体为罗马字体。原本的sf为无衬线字体。还有tt为打印机字体

### 横跨双栏显示

如果想让图表横跨双栏，在标签上加*：

```
\begin{table*}[htbp]
\end{table*}

\begin{figure*}[htbp]
\end{figure*}
```





> 参考资料：
>
> 1. https://blog.csdn.net/qq_43153628/article/details/126050272
