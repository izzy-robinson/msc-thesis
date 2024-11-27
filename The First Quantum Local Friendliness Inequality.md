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
  SDP: Semidefinite Program
  NPA: Navascués, Pironio, Acin
---

# The First Quantum Local Friendliness Inequality

> The purpose of visualisation is insight, not pictures.
> - Ben Shneiderman

## Introduction

In chapter 9, we took a fresh perspective on LF inequalities in which we identified an interesting two dimensional projection of the LF polytope. This was originally demonstrated in [](#LF-graph-figure) but is reproduced below in [](#QLF-graph-figure). It can be noticed that, within the region identified as 'of interest', the quantum boundary contains a number of straight sections. The one parallel to the y-axis is nothing other than the CHSH bound, but interestingly there is another straight section of the boundary which is parallel to neither axis. This is therefore a 'quantum LF inequality' (i.e. an inequality which is satisfied by quantum mechanics) which we will call QLF.[^1] [^2] The purpose of this chapter is to investigate QLF and prove it is genuine; in other words, we want to find a bound.

[^1]: It is of course possible to have quantum LF inequalities for regions which are curved - this linear one is simply a natural one to try and characterise.
[^2]: Note how the point we identified in chapter 9 lies on this inequality so is extremal in this sense.

```{figure} QLFgraph.JPG
:name: QLF-graph-figure
:width: 400px
:align: center
**A reproduction of figure 9.5 with additional information.** In purple is the tangent to the quantum boundary within the region identified as 'of interest' (i.e. the first quantum LF inequality).
```

The first step towards finding a bound is to define what precisely is the inequality QLF. It is given by

\begin{equation}
\epsilon' - \textrm{CHSH}' \leq \frac{3}{2}+\frac{1}{\sqrt2}
\end{equation}

or, in correlator form,

\begin{equation}
- A_1 - A_2 - B_1 - B_2 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \\
- A_2 \otimes B_3 - A_3 \otimes B_2 - A_3 \otimes B_3 \leq 2 + \sqrt2.
\end{equation}

See below for the transformation between decomposition form and correlator form.

```{figure} QLF.JPG
:name: QLF-figure
:align: center
```

To see how we translated between correlator form and grid form in the first line, see Appendix A. 

## SOS Bounds

How can we find the bound on our new inequality? We can do so via a technique known as Sums of Squares (SOS). In chapter 5, on optimisation problems, we first encountered the concept of SOS. For this chapter it will be necessary to link SOS decompositions to quantum mechanics. We will do this via the example of the CHSH inequality, as it is the simplest interesting case.

:::{prf:example} Proving the CHSH bound

Suppose we want to prove that the upper bound on the CHSH inequality is $2\sqrt{2}$ for all quantum states and measurements. How might we achieve this? We will use the SOS technique. First, the Bell operator and the bound are sandwiched between two generic quantum states $| \psi \rangle$,

\begin{equation}
\langle \psi | A_1 \otimes B_1 + A_1 \otimes B_2 + A_2 \otimes B_1 - A_2 \otimes B_2 | \psi \rangle \leq  \langle \psi | 2\sqrt{2}\mathbf{1} | \psi \rangle.
\end{equation}

Since this must hold for all $| \psi \rangle $, it means the operator must be positive semidefinite (PSD). This is already one step forwards.

\begin{equation}
X = 2\sqrt{2}\mathbf{1} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \geq 0
\end{equation}

A sufficient condition for finding $X \geq 0$ is to find some operators $T_k$ such that $X=\sum_k T_k^2$ (i.e. it is enough to find an SOS decompsition of $X$). To see how we can find such a set of operators $T_k$, consider an operator $Y$

\begin{equation}
\label{Y-equation}
Y = \sum_{i,j} Q_{ij} S_i S_j
\end{equation}

where $S$ is given by the list

\begin{equation}
S = (\mathbf{1} \otimes \mathbf{1}, A_1 \otimes \mathbf{1}, A_2 \otimes \mathbf{1}, \mathbf{1} \otimes B_1, \mathbf{1} \otimes B_2).
\end{equation}

Setting $A_i^2=B_j^2=\mathbf{1}^2=\mathbf{1}$ and imposing the following constraints, we are able to ensure that $Y$ equals $X$.

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

The question now is can we find a $Q \geq 0$ which satisfies these constraints? The answer is yes! This problem is simply an SDP due to its linear constraints.

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

See Appendix B.2 for the MATLAB code which shows where this information comes from. An SOS decomposition can always be found provided there exists some PSD $Q$, so this already is sufficient to prove the bound; however it is interesting to go one step further and actually find the SOS decomposition. Since $Q$ is PSD, we can take its Cholesky decomposition,

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

If you like, we can verify this by direct calculation. As $Q$ is of the form given by [Equation 10.8](#cholesky-equation), we now need the matrix elements of $Q$ (i.e. $Q_{ij}$) in terms of the matrix elements of $L$. These are

\begin{equation}
\label{matrix-elements-equation}
Q_{ij}= \sum_k L_{ki} L_{kj}.
\end{equation}

Substituting [Equation 10.10](#matrix-elements-equation) into [Equation 10.5](#Y-equation), we find

\begin{equation}
Y = X &= \sum_{i,j} Q_{ij} S_i S_j \\
&= \sum_{i,j,k} L_{ki} L_{kj} S_i S_j \\
&= \sum_k (\sum_i L_{ki} S_i) (\sum_j L_{kj} S_j) \\
&= \sum_k T_k^2 
\end{equation}

where $T_k = \sum_i L_{ki} S_i$ is what we were looking for. Therefore, finally, the SOS decomposition is 

\begin{equation}
\label{CHSH-SOS-equation}
2\sqrt{2}\mathbf{1} - A_1 \otimes B_1 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \\
= \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_1 - \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \\
+ \Big(\sqrt{\frac{2}{2\sqrt{2}}}A_2 - \frac{1}{\sqrt{2\sqrt{2}}}B_1 + \frac{1}{\sqrt{2\sqrt{2}}}B_2\Big)^2 \geq 0
\end{equation}

where the first line of the SOS is $T_1$ and the second line of the SOS is $T_2$. This is true under the assumption that the eigenvalues are $\pm{1}$ i.e. $A_i^2=B_j^2=\mathbf{1}^2=\mathbf{1}.$ With [Equation 10.12](#CHSH-SOS-equation) we have provided an analytical proof that the upper bound on the CHSH inequality is $2\sqrt2$ for all quantum states and measurements.

:::

## Analytically Proving the Bound on QLF

We will now apply the SOS technique to QLF in order to show that it is a genuine quantum LF inequality. We will initially use the first level of the NPA hierarchy [@Navascues2008]  (as we did in the CHSH example) since this is the simplest. We will then go on to use a higher level of the NPA hierarchy when our initial attempt fails to yield the tight bound we are looking for.

### NPA Hierarchy Level 1

We proceed analagously to the CHSH case. First the Bell operator and the bound are sandwhiched between two generic quantum states $|\psi\rangle$,

\begin{equation}
\langle \psi | - A_1 - A_2 - B_1 - B_2 - A_1 \otimes B_2 - A_2 \otimes B_1 + A_2 \otimes B_2 \\
- A_2 \otimes B_3 - A_3 \otimes B_2 - A_3 \otimes B_3 | \psi \rangle \leq  \langle \psi | \nu \mathbf{1} | \psi \rangle.
\end{equation}

Since this must hold for all $|\psi\rangle$, it means the operator must be PSD

\begin{equation}
X = \nu \mathbf{1} + A_1 + A_2 + B_1 + B_2 + A_1 \otimes B_2 + A_2 \otimes B_1 - A_2 \otimes B_2 \\
+ A_2 \otimes B_3 + A_3 \otimes B_2 + A_3 \otimes B_3 \geq 0.
\end{equation}

A sufficient condition for finding $X \geq 0$ is to find some operators $T_k$ such that $X=\sum_k T_k^2$ (i.e. it is enough to find an SOS decompsition of $X$). To see how we can find such a set of operators $T_k$, consider an operator $Y$ of the form of [Equation 10.5](#Y-equation) where $S$ is given by the list of operators 


\begin{equation}
S = (\mathbf{1} \otimes \mathbf{1}, A_1 \otimes \mathbf{1}, A_2 \otimes \mathbf{1}, \mathbf{1} \otimes B_1, \mathbf{1} \otimes B_2).
\end{equation}


Setting $A_i^2=B_j^2=\mathbf{1}^2=\mathbf{1}$ and imposing the following constraints, we are able to ensure that $Y$ equals $X$.

- Identity coefficients: $\nu$ = Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7)

- A1 coefficients: 1 = Q(1,2) + Q(2,1)  
- A2 coefficients: 1 = Q(1,3) + Q(3,1)  
- A3 coefficients: 0 = Q(1,4) + Q(4,1)  

- B1 coefficients: 1 = Q(1,5) + Q(5,1)  
- B2 coefficients: 1 = Q(1,6) + Q(6,1)  
- B3 coefficients: 0 = Q(1,7) + Q(7,1) 

- A1B1 coefficients: 0 = Q(2,5) + Q(5,2)  
- A1B2 coefficients: 1 = Q(2,6) + Q(6,2)  
- A1B3 coefficients: 0 = Q(2,7) + Q(7,2)  
- A2B1 coefficients: 1 = Q(3,5) + Q(5,3)  
- A2B2 coefficients: -1 = Q(3,6) + Q(6,3)  
- A2B3 coefficients: 1 = Q(3,7) + Q(7,3)  
- A3B1 coefficients: 0 = Q(4,5) + Q(5,4)  
- A3B2 coefficients: 1 = Q(4,6) + Q(6,4)  
- A3B3 coefficients: 1 = Q(4,7) + Q(7,4)  

- A1A2 coefficients: 0 = Q(2,3)  
- A2A1 coefficients: 0 = Q(3,2)  
- A1A3 coefficients: 0 = Q(2,4)  
- A3A1 coefficients: 0 = Q(4,2)  
- A2A3 coefficients: 0 = Q(3,4)  
- A3A2 coefficients: 0 = Q(4,3)  

- B1B2 coefficients: 0 = Q(5,6)  
- B2B1 coefficients: 0 = Q(6,5)  
- B1B3 coefficients: 0 = Q(5,7)  
- B3B1 coefficients: 0 = Q(7,5)  
- B2B3 coefficients: 0 = Q(6,7)  
- B3B2 coefficients: 0 = Q(7,6) 

The question now is can we find a $Q \geq 0$ which satisfies these constraints? The answer is yes! This problem is simply an SDP due to its linear constraints.

\begin{equation}
Q=\begin{pmatrix}
1 & \frac{1}{2} & \frac{1}{2} & 0 & \frac{1}{2} & \frac{1}{2} & 0 \\
\\
\frac{1}{2} & \frac{1}{2} & 0 & 0 & 0 & \frac{1}{2} & 0 \\
\\
\frac{1}{2} & 0 & \frac{1+\sqrt2}{2} & 0 & \frac{1}{2} & -\frac{1}{2} & \frac{1}{2} \\
\\
0 & 0 & 0 & \frac{1}{\sqrt2} & 0 & \frac{1}{2} & \frac{1}{2}\\
\\
\frac{1}{2} & 0 & \frac{1}{2} & 0 & \frac{1}{2} & 0 & 0 \\
\\
\frac{1}{2} & \frac{1}{2} & -\frac{1}{2} & \frac{1}{2} & 0 & \frac{1+\sqrt2}{2} & 0 \\
\\
0 & 0 & \frac{1}{2} & \frac{1}{2} & 0 & 0 & \frac{1}{\sqrt2}
\end{pmatrix}
\end{equation}

See Appendix B.2 for the MATLAB code which shows where this information comes from. An SOS decomposition can always be found provided there exists some PSD $Q$, so this already is sufficient to prove the bound; however it is interesting to go one step further and actually find the SOS decomposition. Since $Q$ is PSD, we can take its Cholesky decomposition given by [Equation 10.8](#cholesky-equation), which is solvable using MATLAB to be

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

We perform the sum of squares calculation as follows

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

With [Equation 10.19](#QLF-SOS-equation) we have provided an analytical proof that the upper bound on the QLF inequality is $3 + 2\sqrt2$ for all quantum states and measurements. However, whilst accurate, we know that this is not a tight bound. If we are to prove a tight bound we must go to a higher level of the NPA hierarchy.

### NPA Hierarchy Level 1+AB

We proceed analagously to the case of NPA hierarchy level 1. The main difference is that, instead of a $7$ by $7$ $Q$ matrix with

\begin{equation}
S = (\mathbf{1} \otimes \mathbf{1}, A_1 \otimes \mathbf{1}, A_2 \otimes \mathbf{1}, \mathbf{1} \otimes B_1, \mathbf{1} \otimes B_2),
\end{equation}

we have a $16$ by $16$ $Q$ matrix with

\begin{equation}
S = (A_1 \otimes \mathbf{1}, A_2 \otimes \mathbf{1}, \mathbf{1} \otimes B_1, \mathbf{1} \otimes B_2, A_1 \otimes B_1, A_1 \otimes B_2, A_1 \otimes B_3, \\
A_2 \otimes B_1, A_2 \otimes B_2, A_2 \otimes B_3, A_3 \otimes B_1, A_3 \otimes B_2, A_3 \otimes B_3, \mathbf{1} \otimes \mathbf{1}).
\end{equation}

We now also require a larger number of constraints to set $Y$ equal to $X$; these constraints are explicitly listed in the MATLAB code contained within Appendix B.2. What is important is that, at this level of the NPA hierarchy, the code outputs a tight bound of $2+2\sqrt{2}$ proving that QLF is a genuine quantum LF inequality. We could easily generate the cholesky of $Q$ and expand this out into a full SOS decomposition for QLF. However, upon initial inspection, the cholesky's coefficients do not adopt closed forms. Neither do they do so upon permutation of the order of operators in the string $S$. Therefore there is nothing to be gained from including this numeric decomposition.

## Summary

In this chapter, we have found the first ever quantum LF inequality. We initially tried using the first level of the NPA hierarchy to find an upper bound on QLF, but the bound it provided was not tight. We then moved onto the 1+AB level of the NPA hierarchy which did result in a tight upper bound of $2+2\sqrt{2}$ for QLF. Our proof is based on SOS decompositions of the inequality. Although we won't explore this within the thesis, these SOS decompositions have the potential to be interesting in their own right. In the study of nonlocality, SOS decompositions have found application in the theory of self-testing; roughly speaking, this is questioning to what extent are the quantum state and measurements which maximally violate a Bell inequality unique. Our results raise the possibility that we could do some self testing based upon the theory of LF.