---
subject: Results and Discussion | Chapter 10
subtitle:
short_title: The First Quantum Local Friendliness Inequality
numbering: 
    enumerator: 10.%s
---

# The First Quantum Local Friendliness Inequality

> The purpose of visualisation is insight, not pictures.
> - Ben Shneiderman

```{figure} QLFgraph.JPG
:name: QLF-graph-figure
:width: 400px
:align: center
Caption
```

## Proving the Bound is Tight

```{figure} key.JPG
:name: key-figure
:width: 200px
:align: center
Caption
```

### Order of Operators 1

```{figure} order-of-operators-1.JPG
:name: order-of-operators-1-figure
:width: 900px
:align: center
```


\begin{equation}
chol(Q) = \begin{pmatrix}
1 & \frac{1}{2} & \frac{1}{2} & 0 & \frac{1}{2} & \frac{1}{2} & 0 \\
\\
0 & \frac{1}{2} & -\frac{1}{2} & 0 & -\frac{1}{2} & \frac{1}{2} & 0 \\
\\
0 & 0 & \frac{2^{3/4}}{2} & 0 & 0 & -\frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} \\
\\
0 & 0 & 0 & \frac{2^{3/4}}{2} & 0 & \frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} \\
\end{pmatrix}
\end{equation}

\begin{equation}
&|| (\mathbf{1} \hspace{2mm} A_1 \hspace{2mm} A_2 \hspace{2mm} A_3 \hspace{2mm} B_1 \hspace{2mm} B_2 \hspace{2mm} B_3) \cdot chol(Q)^T ||^2 \\
&= (\mathbf{1} + \frac{1}{2}A_1 + \frac{1}{2}A_2 + \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+ (\frac{1}{2}A_1 - \frac{1}{2}A_2 - \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+
&+
\end{equation}

### Order of Operators 2

```{figure} order-of-operators-2.JPG
:name: order-of-operators-2-figure
:width: 900px
:align: center
```

\begin{equation}
chol(Q) = \begin{pmatrix}
\frac{1}{\sqrt2} & 0 & 0 & 0 & \frac{1}{\sqrt2} & 0 & \frac{1}{\sqrt2} \\
\\
0 & \sqrt{\frac{1+\sqrt2}{2}} & 0 & \sqrt{\frac{\sqrt{2}-1}{2}} & -\sqrt{\frac{\sqrt{2}-1}{2}} & \sqrt{\frac{\sqrt{2}-1}{2}} & \sqrt{\frac{\sqrt{2}-1}{2}} \\
\\
0 & 0 & \frac{2^{3/4}}{2} & 0 & \frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} & 0 \\
\\
0 & 0 & 0 & \frac{1}{\sqrt{2+\sqrt2}} & \frac{\sqrt{2-\sqrt2}}{2} & -\frac{\sqrt{2-\sqrt2}}{2} & \frac{1}{\sqrt{2+\sqrt2}}
\end{pmatrix}
\end{equation}

### Order of Operators 3

```{figure} order-of-operators-3.JPG
:name: order-of-operators-3-figure
:width: 900px
:align: center
```

\begin{equation}
chol(Q) = \begin{pmatrix}
\frac{1}{\sqrt2} & 0 & 0 & \frac{1}{\sqrt2} & 0 & 0 & \frac{1}{\sqrt2} \\
\\
0 & \frac{1}{\sqrt2} & \frac{1}{\sqrt2} & 0 & 0 & 0 & \frac{1}{\sqrt2} \\
\\
0 & 0 & \frac{2^{3/4}}{2} & -\frac{1}{2^{3/4}} & 0 & \frac{1}{2^{3/4}} & 0 \\
\\
0 & 0 & 0 & \frac{1}{2^{3/4}} & \frac{2^{3/4}}{2} & \frac{1}{2^{3/4}} & 0
\end{pmatrix}
\end{equation}

### Order of Operators 4

```{figure} order-of-operators-4.JPG
:name: order-of-operators-4-figure
:width: 900px
:align: center
```

\begin{equation}
chol(Q) = \begin{pmatrix}
1 & \frac{1}{2} & \frac{1}{2} & \frac{1}{2} & \frac{1}{2} & 0 & 0 \\
\\
0 & \frac{1}{2} & -\frac{1}{2} & -\frac{1}{2} & \frac{1}{2} & 0 & 0 \\
\\
0 & 0 & 0 & 0 & 0 & 0 & 0 \\
\\
0 & 0 & 0 & \frac{2^{3/4}}{2} & -\frac{1}{2^{3/4}} & 0 & \frac{1}{2^{3/4}} \\
\\
0 & 0 & 0 & 0 & \frac{1}{2^{3/4}} & \frac{2^{3/4}}{2} & \frac{1}{2^{3/4}}
\end{pmatrix}
\end{equation}

### Order of Operators 5

```{figure} order-of-operators-5.JPG
:name: order-of-operators-5-figure
:width: 900px
:align: center
```
\begin{equation}
chol(Q) = \begin{pmatrix}
\frac{2^{3/4}}{2} & 0 & \frac{1}{2^{3/4}} & 0 & 0 & 0 & \frac{1}{2^{3/4}} \\
\\
0 & \frac{1}{\sqrt2} & \frac{1}{\sqrt2} & 0 & \frac{1}{\sqrt2} & 0 & 0 \\
\\
0 & 0 & \frac{1}{2^{3/4}} & 0 & 0 & -\frac{2^{3/4}}{2} & -\frac{1}{2^{3/4}} \\
\\
0 & 0 & 0 & \frac{1}{\sqrt2} & \frac{1}{\sqrt2} & \frac{1}{\sqrt2} & 0
\end{pmatrix}
\end{equation}