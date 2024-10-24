---
subject: Results and Discussion | Chapter 10
subtitle:
short_title: The First Quantum Local Friendliness Inequality
numbering: 
    enumerator: 10.%s
abbreviations:
  SOS: Sums of Squares
  PSD: Positive Semidefinite
  LF: Local Friendliness
  CHSH: Clauser, Horne, Shimony, Holt
---

# The First Quantum Local Friendliness Inequality

> The purpose of visualisation is insight, not pictures.
> - Ben Shneiderman

In chapter 9, we took a fresh perspective on LF inequalities in which we identified a two dimensional projection of the LF polytope. This was originally demonstrated in [](#LF-graph-figure) but is reproduced below in [](#QLF-graph-figure). It can be noticed that, within the region identified as 'of interest', the quantum boundary contains a number of straight lines. The one parallel to the y-axis is nothing other than the CHSH bound, but interestingly there is another straight line which is parallel to neither axis. This is therefore a 'quantum LF inequality' (i.e. a linear inequality which is satisfied by quantum mechanics) which we will call QLF.[^1] The purpose of this chapter is to investigate QLF and prove it is genuine; in other words, we want to find a bound.

[^1]: Note how the point we identified in chapter 9 lies on this inequality so is extremal in this sense.

```{figure} QLFgraph.JPG
:name: QLF-graph-figure
:width: 400px
:align: center
**A reproduction of figure 9.5 with additional information.** In purple is the tangent to the quantum boundary within the region identified as 'of interest' (i.e. the first quantum LF inequality).
```

How can we find the bound on our new inequality? We can do so via a technique known as Sums of Squares (SOS). In chapter 5, on optimisation problems, we first encountered the concept of SOS. For this chapter it will be necessary to link SOS decompositions to quantum mechanics. We will do this via the example of the CHSH inequality, as it is the simplest interesting case.

:::{prf:example} Proving the CHSH bound

Suppose we want to prove that the upper bound on the CHSH inequality is $2\sqrt{2}$ for all quantum states and measurements. How might we achieve this? We will use the SOS technique. First, the Bell operator and the bound are sandwiched between two generic quantum states $| \psi \rangle$.

\begin{equation}
\langle \psi | A_1 \otimes B_1 + A_1 \otimes B_2 + A_2 \otimes B_1 - A_2 \otimes B_2 | \psi \rangle \leq  \langle \psi | 2\sqrt{2}\mathbf{1} | \psi \rangle
\end{equation}

From this, an operator equation is formed.

\begin{equation}
X = 2\sqrt{2}\mathbf{1} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \geq 0
\end{equation}

A sufficient condition for finding $X \geq 0$ is to find the $T_k$'s such that $X=\sum_k T_k^2$ (i.e. it is enough to find an SOS decompsition of $X$). Now consider some $Y$,

\begin{equation}
\label{Y-equation}
Y = \sum_{i,j} Q_{ij} S_i S_j
\end{equation}

where $S$ is given by the list

\begin{equation}
S = (\mathbf{1} \otimes \mathbf{1}, A_1 \otimes \mathbf{1}, A_2 \otimes \mathbf{1}, \mathbf{1} \otimes B_1, \mathbf{1} \otimes B_2).
\end{equation}

Imposing the following constraints sets $Y$ equal to $X$.

- Identity coefficients: $2\sqrt{2}$ = Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) 

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

The question now is can we find a $Q \geq 0$ which satisfies these constraints? The answer is yes!

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

See Appendix B for the MATLAB code which shows where this information comes from. An SOS decomposition can always be found provided there exists some PSD $Q$, so this already is sufficient to prove the bound; however it is interesting to go one step further and actually find the SOS decomposition. Since $Q$ is PSD, we can take its Cholesky decomposition,

\begin{equation}
\label{cholesky-equation}
Q= L^T L
\end{equation}

which is specifically solvable through MATLAB to be

\begin{equation}
L = chol(Q) = \begin{pmatrix}
0 & \sqrt{\frac{2}{2\sqrt{2}}} & 0 & -\frac{1}{\sqrt{2\sqrt{2}}} & -\frac{1}{\sqrt{2\sqrt{2}}} \\
\\
0 & 0 & \sqrt{\frac{2}{2\sqrt{2}}} & -\frac{1}{\sqrt{2\sqrt{2}}}  & \frac{1}{\sqrt{2\sqrt{2}}} \\
\end{pmatrix}.
\end{equation}

If you like, we can verify this by direct calculation. As $Q$ is of the form given by equation [Equation 10.6](#cholesky-equation), we now need the matrix elements of $Q$ (i.e. $Q_{ij}$) in terms of the matrix elements of $L$. These are

\begin{equation}
\label{matrix-elements-equation}
Q_{ij}= \sum_k L_{ki} L_{kj}.
\end{equation}

Substituting [Equation 10.8](#matrix-elements-equation) into [Equation 10.3](#Y-equation), we find

\begin{equation}
Y = X &= \sum_{i,j} Q_{ij} S_i S_j \\
&= \sum_{i,j,k} L_{ki} L_{kj} S_i S_j \\
&= \sum_k (\sum_i L_{ki} S_i) (\sum_j L_{kj} S_j) \\
&= \sum_k T_k^2 
\end{equation}

Therefore, finally, the SOS decomposition is 

\begin{equation}
\label{CHSH-SOS-equation}
2\sqrt{2}\mathbf{1} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \\
= \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_1 - \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \\
+ \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_2 - \frac{1}{\sqrt{2\sqrt{2}}}B_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \geq 0
\end{equation}

where the first line of the SOS is $T_1$ and the second line of the SOS is $T_2$. This is true under the assumption that the eigenvalues are $\pm{1}$ i.e. $A_i^2=B_j^2=\mathbf{1}^2=\mathbf{1}$. With [Equation 10.10](#CHSH-SOS-equation) we have provided an analytical proof that the upper bound on the CHSH inequality is $2\sqrt2$ for all quantum states and measurements.

:::

## Analytically Proving the Bound on QLF

We will carry out the sum of squares decomposition for QLF several times with different orders of operators, some natural and some randomised, to provide five different proofs of the bound. Any one of these on their own would constitute a full proof of the bound, however with each order of operators we generate a different SOS decomposition. We do not know if any SOS decomposition is more useful than another when it comes to self-testing @supic2020, so we preserve several for the record.

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
The list $S$ is given by the operators above and to the left of the grid. The necessarily zero terms (i.e. those which are not physically measurable so will never appear in the inequality) are left white. The potentially non-zero terms are colour coded for ease of equating coefficients.
```

The cholesky decomposition of the matrix Q is given by

\begin{equation}
L = chol(Q) = \begin{pmatrix}
1 & \frac{1}{2} & \frac{1}{2} & 0 & \frac{1}{2} & \frac{1}{2} & 0 \\
\\
0 & \frac{1}{2} & -\frac{1}{2} & 0 & -\frac{1}{2} & \frac{1}{2} & 0 \\
\\
0 & 0 & \frac{2^{3/4}}{2} & 0 & 0 & -\frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} \\
\\
0 & 0 & 0 & \frac{2^{3/4}}{2} & 0 & \frac{1}{2^{3/4}} & \frac{1}{2^{3/4}} \\
\end{pmatrix}
\end{equation}

See Appendix B for the MATLAB code which shows where this information comes from. We perform the sum of squares calculation as follows

\begin{equation}
&(\mathbf{1} + \frac{1}{2}A_1 + \frac{1}{2}A_2 + \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+ (\frac{1}{2}A_1 - \frac{1}{2}A_2 - \frac{1}{2}B_1 + \frac{1}{2}B_2)^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}

Expanding the brackets and combining all terms gives

\begin{equation}
\label{QLF-SOS-equation}
(3&+2\sqrt2)\mathbf{1} + A_1 + A_2 + B_1 + B_2 \\
&+ A_1B_2 + A_2B_1 - A_2B_2 + A_2B_3 + A_3B_2 + A_3B_3.
\end{equation}

With [Equation 10.13](#QLF-SOS-equation) we have provided an analytical proof that the upper bound on the QLF inequality is $3 + 2\sqrt2$ for all quantum states and measurements.

### Order of Operators 2

```{figure} order-of-operators-2.JPG
:name: order-of-operators-2-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix Q is given by

\begin{equation}
L = chol(Q) = \begin{pmatrix}
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
&(\frac{1}{\sqrt2}A_1 + \frac{1}{\sqrt2}B_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\sqrt{\frac{1+\sqrt2}{2}}A_2 + \sqrt{\frac{\sqrt2-1}{2}}B_1 - \sqrt{\frac{\sqrt2-1}{2}}B_2 + \sqrt{\frac{\sqrt2-1}{2}}B_3 + \sqrt{\frac{\sqrt2-1}{2}}\mathbf{1})^2 \\
&+ (\frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{\sqrt{2+\sqrt2}}B_1 + \frac{\sqrt{2-\sqrt2}}{2}B_2 - \frac{\sqrt{2-\sqrt2}}{2}B_3 + \frac{1}{\sqrt{2+\sqrt2}}\mathbf{1})^2 
\end{equation}

### Order of Operators 3

```{figure} order-of-operators-3.JPG
:name: order-of-operators-3-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix Q is given by

\begin{equation}
L = chol(Q) = \begin{pmatrix}
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
&(\mathbf{1} + \frac{1}{2}A_1 + \frac{1}{2}B_1 + \frac{1}{2}A_2 + \frac{1}{2}B_2)^2 \\
&+ (\frac{1}{2}A_1 - \frac{1}{2}B_1 - \frac{1}{2}A_2 + \frac{1}{2}B_2)^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{2^{3/4}}B_2 + \frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}


### Order of Operators 4

```{figure} order-of-operators-4.JPG
:name: order-of-operators-4-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix Q is given by

\begin{equation}
L = chol(Q) = \begin{pmatrix}
1 & \frac{1}{2} & \frac{1}{2} & \frac{1}{2} & \frac{1}{2} & 0 & 0 \\
\\
0 & \frac{1}{2} & -\frac{1}{2} & -\frac{1}{2} & \frac{1}{2} & 0 & 0 \\
\\
0 & 0 & 0 & \frac{2^{3/4}}{2} & -\frac{1}{2^{3/4}} & 0 & \frac{1}{2^{3/4}} \\
\\
0 & 0 & 0 & 0 & \frac{1}{2^{3/4}} & \frac{2^{3/4}}{2} & \frac{1}{2^{3/4}}
\end{pmatrix}
\end{equation}

We perform the sum of squares calculation as follows

\begin{equation}
&(\frac{1}{\sqrt2}A_1 + \frac{1}{\sqrt2}B_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{1}{\sqrt2}B_1 - \frac{1}{\sqrt2}A_2 - \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{2^{3/4}}{2}A_2 - \frac{1}{2^{3/4}}B_2 + \frac{1}{2^{3/4}}B_3)^2 \\
&+ (\frac{1}{2^{3/4}}B_2 + \frac{2^{3/4}}{2}A_3 + \frac{1}{2^{3/4}}B_3)^2
\end{equation}

### Order of Operators 5

```{figure} order-of-operators-5.JPG
:name: order-of-operators-5-figure
:width: 900px
:align: center
```

The cholesky decomposition of the matrix Q is given by

\begin{equation}
L = chol(Q) = \begin{pmatrix}
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
&(\frac{2^{3/4}}{2}B_3 + \frac{1}{2^{3/4}}A_2 + \frac{1}{2^{3/4}}A_3)^2 \\
&+ (\frac{1}{\sqrt2}B_1 + \frac{1}{\sqrt2}A_2 + \frac{1}{\sqrt2}\mathbf{1})^2 \\
&+ (\frac{1}{2^{3/4}}A_2 - \frac{2^{3/4}}{2}B_2 -  + \frac{1}{2^{3/4}}A_3)^2 \\
&+ (\frac{1}{\sqrt2}A_1 - \frac{1}{\sqrt2}\mathbf{1} - \frac{1}{\sqrt2}B_2 )^2
\end{equation}

In this chapter, we have provided five independent but related proofs that the upper bound on QLF is $3+2\sqrt{2}$ and hence that it is a genuine quantum LF inequality. Our proofs are based on different SOS decompositions of the inequality. Although we won't explore this within the thesis, each of these has the potential to be interesting in their own right. In the study of nonlocality, SOS decompositions have found application in the theory of self-testing; roughly speaking, this is questioning to what extent are the quantum state and measurements which maximally violate a Bell inequality unique. Our results raise the possibility that we could do some self testing based upon the theory of LF.