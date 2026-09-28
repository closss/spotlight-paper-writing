# LaTeX 表格高亮模板

## 导言区

```latex
\usepackage{booktabs}
\usepackage[table]{xcolor}   % 提供 \cellcolor；若已加载 xcolor，改为 \PassOptionsToPackage{table}{xcolor} 放在 \documentclass 之前
\usepackage{multirow}

% 高亮色：三选一，全文只用一种。避免绿色系。
\definecolor{bestcell}{HTML}{DCE9F5}    % 浅蓝（默认推荐）
% \definecolor{bestcell}{HTML}{FBE5D6}  % 浅橙
% \definecolor{bestcell}{HTML}{ECECEC}  % 浅灰

\newcommand{\best}[1]{\cellcolor{bestcell}\textbf{#1}}   % 最优：色块 + 加粗
\newcommand{\second}[1]{\underline{#1}}                   % 次优：下划线
```

注意：`\cellcolor` 需要出现在单元格开头，`\best{}` 直接作为单元格内容使用即可。有些会议模板已经加载了 xcolor，重复加载带不同选项会报错，此时用 `\PassOptionsToPackage`。

## 示例表格

```latex
\begin{table}[t]
\centering
\caption{Main results on X and Y. Best results are \colorbox{bestcell}{\textbf{highlighted}}, second best \underline{underlined}.}
\label{tab:main}
\begin{tabular}{lccc}
\toprule
Method & Acc. (\%) $\uparrow$ & Mem. (GB) $\downarrow$ & Latency (ms) $\downarrow$ \\
\midrule
Baseline A & 71.2 & 24.1 & 118 \\
Baseline B & \second{73.5} & \second{18.6} & \second{97} \\
Baseline C & 72.8 & 21.0 & 105 \\
\midrule
\textbf{Ours} & \best{75.9} & \best{12.3} & \best{64} \\
\bottomrule
\end{tabular}
\end{table}
```

## 规则回顾

- 只在第一张表的 caption 说明一次高亮规则，后面的表可以写 "Same notation as Table 1"。
- 不加竖线，只用 `\toprule` / `\midrule` / `\bottomrule`。
- 同一列小数位统一；表头标注单位和 ↑/↓。
- 如果只想用加粗不想用色块，把 `\best` 改成 `\textbf{#1}` 即可，全文保持一致。
- 画图时使用与 `bestcell` 同色系的深色版本作为"我们的方法"的颜色（例如浅蓝色块对应 `#2F6DB5` 一类的蓝色线条/柱子），让图表视觉统一。
