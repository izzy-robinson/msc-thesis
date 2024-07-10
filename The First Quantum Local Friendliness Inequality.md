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

```{figure} QLFgraph.svg
:name: QLF-graph-figure
:width: 400px
:align: center
Caption
```

## Proving the Bound is Tight

```{figure} key.svg
:name: key-figure
:width: 200px
:align: center
Caption
```

### Order of Operators 1

```{figure} order-of-operators-1.svg
:name: order-of-operators-1-figure
:width: 900px
:align: center
Caption
```

### Order of Operators 2

```{figure} order-of-operators-2.svg
:name: order-of-operators-2-figure
:width: 900px
:align: center
Caption
```

text here

\begin{equation}
chol(Q) = \begin{pmatrix}
\frac{1}{\sqrt{2}} & 0 & 0 & 0 & \frac{1}{\sqrt{2}} & 0 & \frac{1}{\sqrt{2}} \\
\\
0 & \sqrt{\frac{1+\sqrt{2}}{2}} & 0 & \sqrt{\frac{\sqrt{2}-1}{2}} & -\sqrt{\frac{\sqrt{2}-1}{2}} & \sqrt{\frac{\sqrt{2}-1}{2}} & \sqrt{\frac{\sqrt{2}-1}{2}} \\
\\
0 & 0 & \frac{2^{3/4}}{2} & 0 & \frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} & 0 \\
\\
0 & 0 & 0 & \frac{1}{\sqrt{2+\sqrt{2}}} & \frac{\sqrt{2-\sqrt{2}}}{2} & -\frac{\sqrt{2-\sqrt{2}}}{2} & \frac{1}{\sqrt{2+\sqrt{2}}}
\end{pmatrix}
\end{equation}

text here


```{math}
:label: SOS-equation-1
&\begin{pmatrix}
A_1 & A_2 & A_3 & B_1 & B_2 & B_3 & \mathbf{1}
\end{pmatrix}
\cdot chol(Q)^T
\\
\\
&= \begin{pmatrix}\frac{1}{\sqrt{2}}A_1 + \frac{1}{\sqrt{2}}B_2 + \frac{1}{\sqrt{2}}\mathbf{1}\end{pmatrix}^2
\\
\\
&+ \begin{pmatrix}\sqrt{\frac{1+\sqrt{2}}{2}}A_2 + \sqrt{\frac{\sqrt{2}-1}{2}}B_1 -\sqrt{\frac{\sqrt{2}-1}{2}}B_2 + \sqrt{\frac{\sqrt{2}-1}{2}}B_3 + \sqrt{\frac{\sqrt{2}-1}{2}}\mathbf{1} \end{pmatrix}^2
\\
\\
&+ \begin{pmatrix} \frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3 \end{pmatrix}^2
\\
\\
&+ \begin{pmatrix} \frac{1}{\sqrt{2+\sqrt{2}}}B_1 + \frac{\sqrt{2-\sqrt{2}}}{2}B_2 - \frac{\sqrt{2-\sqrt{2}}}{2}B_3 + \frac{1}{\sqrt{2+\sqrt{2}}}\mathbf{1} \end{pmatrix}^2
```

Expanding the first termof [Equation 4.1](#SOS-equation-1) gives $\frac{3}{2}\mathbf{1}+A_1B_2+A_1+B_2$.

Expanding the second term of [Equation 4.1](#SOS-equation-1) gives $\frac{5\sqrt{2}-3}{2}\mathbf{1}+A_2+$

Expanding the third term of [Equation 4.1](#SOS-equation-1) gives

Expanding the fourth term of [Equation 4.1](#SOS-equation-1) gives

Finally, putting all terms together leaves us with

### Order of Operators 3

```{figure} order-of-operators-3.svg
:name: order-of-operators-3-figure
:width: 900px
:align: center
Caption
```


### Order of Operators 4

```{figure} order-of-operators-4.svg
:name: order-of-operators-4-figure
:width: 900px
:align: center
Caption
```

### Order of Operators 5

```{figure} order-of-operators-5.svg
:name: order-of-operators-5-figure
:width: 900px
:align: center
Caption
```