---
subject: Results and Discussion | Chapter 10
subtitle:
short_title: The First Quantum Local Friendliness Inequality
numbering: 
    enumerator: 10.%s
abbreviations:
  SOS: Sums of Squares
---

# The First Quantum Local Friendliness Inequality

> The purpose of visualisation is insight, not pictures.
> - Ben Shneiderman

In chapter 5, on optimisation problems, we first encountered the concept of sums of squares (SOS). For this chapter it will be necessary to link SOS decompositions to quantum mechanics. We will do this via the example of the CHSH inequality, as it is the simplest interesting case.

:::{prf:example} Proving the CHSH bound

Suppose we want to prove that the upper bound on the CHSH inequality is $2\sqrt{2}$ for all quantum states and measurements. How might we achieve this? We will use the SOS tecnique. First, the Bell operator and the bound are sandwiched between two generic quantum states $| \psi \rangle$.

\begin{equation}
\langle \psi | A_1 \otimes B_1 + A_1 \otimes B_2 + A_2 \otimes B_1 - A_2 \otimes B_2 | \psi \rangle \leq  \langle \psi | 2\sqrt{2}\mathbf{1} | \psi \rangle
\end{equation}

Then, an operator equation is formed.

\begin{equation}
X = 2\sqrt{2}\mathbf{1} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \geq 0
\end{equation}

A sufficient condition for finding $X \geq 0$ is to find the $T_k$'s such that $X=\sum_k T_k^2$ (i.e. it is enough to find an SOS decompsition of $X$).

\begin{equation}
Y = \sum_{i,j} Q_{ij} S_i S_j
\end{equation}

\begin{equation}
S = (\mathbf{1} \otimes \mathbf{1}, A_0 \otimes \mathbf{1}, A_1 \otimes \mathbf{1}, \mathbf{1} \otimes B_0, \mathbf{1} \otimes B_1)
\end{equation}

Imposing the following constraints sets $Y$ equal to $X$.

- identity coefficients: $2\sqrt{2}$ = Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) 

- A1 coefficients: 0 = Q(1,2) + Q(2,1)
- A2 coefficients: 0 = Q(1,3) + Q(3,1) 

- B1 coefficients: 0 = Q(1,4) + Q(4,1) 
- B2 coefficients: 0 = Q(1,5) + Q(5,1) 

- A1A2 coefficients: 0 = Q(2,3) 
- A2A1 coefficients: 0 = Q(3,2)

- B1B2 coefficients: 0 = Q(4,5)
- B2B1 coefficients: 0 = Q(5,4)

- A1B1 coefficients: -1 = Q(2,4) + Q(4,2)
- A1B2 coefficients: -1 = Q(2,5) + Q(5,2)
- A2B1 coefficients: -1 = Q(3,4) + Q(4,3) 
- A2B2 coefficients: 1 = Q(3,5) + Q(5,3)

Can we find a $Q \geq 0$ which satisfies these constraints?

An SOS decomposition can be found provided there exists some PSD Q 

\begin{equation}
Q = \begin{pmatrix}
0 & 0 & 0 & 0 & 0 \\
\\
0 & \frac{1}{\sqrt{2}} & 0 & -\frac{1}{2} & -\frac{1}{2} \\
\\
0 & 0 & \frac{1}{\sqrt{2}} & -\frac{1}{2} & \frac{1}{2} \\
\\
0 & -\frac{1}{2} & -\frac{1}{2} & \frac{1}{\sqrt{2}} & 0 \\
\\
0 & -\frac{1}{2} & \frac{1}{2} & 0 & \frac{1}{\sqrt{2}} \\
\end{pmatrix}
\end{equation}

\begin{equation}
Q= L^T L
\end{equation}

\begin{equation}
L = chol(Q) = \begin{pmatrix}
0 & \sqrt{\frac{2}{2\sqrt{2}}} & 0 & -\frac{1}{\sqrt{2\sqrt{2}}} & -\frac{1}{\sqrt{2\sqrt{2}}} \\
\\
0 & 0 & \sqrt{\frac{2}{2\sqrt{2}}} & -\frac{1}{\sqrt{2\sqrt{2}}}  & \frac{1}{\sqrt{2\sqrt{2}}} \\
\end{pmatrix}
\end{equation}

\begin{equation}
X &= \sum_{i,j} Q_{ij} S_i S_j \\
&= \sum_{i,j,k} L_{ki} L_{kj} S_i S_j \\
&= \sum_k (\sum_i L_{ki} S_i) (\sum_j R_{kj} S_j) \\
&= \sum_k T_k^2 
\end{equation}

\begin{equation}
\label{CHSH-SOS-equation}
2\sqrt{2} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \\
= \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_1 - \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \\
+ \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_2 - \frac{1}{\sqrt{2\sqrt{2}}}B_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \geq 0
\end{equation}

With equation [Equation 10.2](#CHSH-SOS-equation) we have provided an analytical proof that the upper bound on the CHSH inequality is $2\sqrt2$ for all quantum states and measurements.

:::

It can be noticed from figure 9.5 that, within the region identified as 'of interest', the quantum boundary falls along a straight line. This is therefore a quantum LF inequality.

```{figure} QLFgraph.JPG
:name: QLF-graph-figure
:width: 400px
:align: center
**A reproduction of figure 9.5 with additional information.** In purple is the tangent to the quantum boundary within the region identified as 'of interest' (i.e. the first quantum LF inequality).
```

## Analytically Proving the Bound 

We will carry out the sum of squares decomposition several times with different orders of operators, some natural and some randomised, to provide five different proofs of the bound. We do not know if any SOS decomposition is more useful than another when it comes to self-testing, so we preserve several for the record.

```{figure} key.JPG
:name: key-figure
:width: 200px
:align: center
A colour coordination key.
```

### Order of Operators 1

```{figure} order-of-operators-1.JPG
:name: order-of-operators-1-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix is given by

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

We perform the sum of squares calculation as follows

\begin{equation}
&|| (\mathbf{1} \hspace{2mm} A_1 \hspace{2mm} A_2 \hspace{2mm} A_3 \hspace{2mm} B_1 \hspace{2mm} B_2 \hspace{2mm} B_3) \cdot chol(Q)^T ||^2 \\
&= (\mathbf{1} + \frac{1}{2}A_1 + \frac{1}{2}A_2 + \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+ (\frac{1}{2}A_1 - \frac{1}{2}A_2 - \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3.
\end{equation}

### Order of Operators 2

```{figure} order-of-operators-2.JPG
:name: order-of-operators-2-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix is given by

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

We perform the sum of squares calculation as follows

\begin{equation}
&|| (A_1 \hspace{2mm} A_2 \hspace{2mm} A_3 \hspace{2mm} B_1 \hspace{2mm} B_2 \hspace{2mm} B_3 \hspace{2mm} \mathbf{1}) \cdot chol(Q)^T ||^2 \\
&= (\frac{1}{\sqrt2}A_1 + \frac{1}{\sqrt2}B_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\sqrt{\frac{1+\sqrt2}{2}}A_2 + \sqrt{\frac{\sqrt2-1}{2}}B_1 - \sqrt{\frac{\sqrt2-1}{2}}B_2 + \sqrt{\frac{\sqrt2-1}{2}}B_3 + \sqrt{\frac{\sqrt2-1}{2}}\mathbf{1})^2 \\
&+ (\frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{\sqrt{2+\sqrt2}}B_1 + \frac{\sqrt{2-\sqrt2}}{2}B_2 - \frac{\sqrt{2-\sqrt2}}{2}B_3 + \frac{1}{\sqrt{2+\sqrt2}}\mathbf{1})^2 
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3
\end{equation}

as before.

### Order of Operators 3

```{figure} order-of-operators-3.JPG
:name: order-of-operators-3-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix is given by

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

We perform the sum of squares calculation as follows

\begin{equation}
&|| (\mathbf{1} \hspace{2mm} A_1 \hspace{2mm} B_1 \hspace{2mm} A_2 \hspace{2mm} B_2 \hspace{2mm} A_3 \hspace{2mm} B_3) \cdot chol(Q)^T ||^2 \\
&= (\mathbf{1} + \frac{1}{2}A_1 + \frac{1}{2}B_1 + \frac{1}{2}A_2 + \frac{1}{2}B_2)^2 \\
&+ (\frac{1}{2}A_1 - \frac{1}{2}B_1 - \frac{1}{2}A_2 + \frac{1}{2}B_2)^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{2^{3/4}}B_2 + \frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3
\end{equation}

as before.

### Order of Operators 4

```{figure} order-of-operators-4.JPG
:name: order-of-operators-4-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix is given by

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

We perform the sum of squares calculation as follows

\begin{equation}
&|| (A_1 \hspace{2mm} B_1 \hspace{2mm} A_2 \hspace{2mm} B_2 \hspace{2mm} A_3 \hspace{2mm} B_3 \hspace{2mm} \mathbf{1}) \cdot chol(Q)^T ||^2 \\
&= (\frac{1}{\sqrt2}A_1 + \frac{1}{\sqrt2}B_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{1}{\sqrt2}B_1 - \frac{1}{\sqrt2}A_2 - \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{2^{3/4}}B_2 + \frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3
\end{equation}

as before.

### Order of Operators 5

```{figure} order-of-operators-5.JPG
:name: order-of-operators-5-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix is given by

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

We perform the sum of squares calculation as follows

\begin{equation}
&|| (B_3 \hspace{2mm} B_1 \hspace{2mm} A_2 \hspace{2mm} A_1 \hspace{2mm} \mathbf{1} \hspace{2mm} B_2 \hspace{2mm} A_3) \cdot chol(Q)^T ||^2 \\
&= (\frac{2^{3/4}}{2}B_3 + \frac{1}{2^{3/4}}A_2 + \frac{1}{2^{3/4}}A_3)^2 \\
&+ (\frac{1}{\sqrt2}B_1 + \frac{1}{\sqrt2}A_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{1}{2^{3/4}}A_2 - \frac{2^{3/4}}{2}B_2 -  + \frac{1}{2^{3/4}}A_3)^2 \\
&+ (\frac{1}{\sqrt2}A_1 - \frac{1}{\sqrt2}\mathbf{1} - \frac{1}{\sqrt2}B_2 )^2
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3
\end{equation}

as before.