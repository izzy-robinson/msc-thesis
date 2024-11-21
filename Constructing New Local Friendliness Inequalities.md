---
subject: Results and Discussion | Chapter 11
subtitle:
short_title: Constructing New Local Friendliness Inequalities
numbering: 
    enumerator: 11.%s
abbreviations:
    LF: Local Friendliness
    CHSH: Clauser, Horne, Shimony, Holt
    CGLMP: Collins, Gisin, Linden, Massar, Popescu
    NPA: Navascués, Pironio, Acin
---

# Constructing New Local Friendliness Inequalities

> Each truth discovered was a rule available in the discovery of subsequent ones.
> - René Descartes

# Introduction

We saw in chapter 9 that an LF inequality based on the simplest $3$ settings and $2$ outcomes scenario can be decomposed into a CHSH part and a novel part made up of $\delta$ and $\gamma$. The big question raised here is whether it is possible to find LF inequalities for larger more computationally intractable scenarios. If we want to go up to the next simplest scenario (i.e. the $3$ settings and $3$ outcomes scenario) we should therefore take the associated interesting Bell inequality (i.e. CGLMP) and see if we can construct an extension based on the structure identified in chapter 9.

We initially focus on the strategies which saturate CGLMP; there are a huge set of these. We then add in a reward term with $\delta$; this narrows down the search space somewhat. Finally we choose a $\gamma$ such that none of these optimal strategies are rewarded (i.e. they are either penalised or neutral); we start off with a symmetric $\gamma$ then edit it through trial and error. There is significant work left to do if we are to formalise this technique, however we are ultimately left with the following ingredients:

```{figure} CGLMP-LF.jpg
:name: CGLMP-LF-figure
:align: center
```

Now we have a set of ingredients, we want to turn these into a concrete proposal for a CGLMP-LF inequality. To achieve this we will produce a two dimensional plot taking CGLMP as one axis and $\delta + \gamma$ as the other axis. From this we should be able to read off the optimal coefficients for each part.

```{figure} graph.svg
:name: graph-figure
:align: center
```

\begin{equation}
\textrm{CGLMP} + 3(\delta+\gamma) \leq 5
\end{equation}

Having obtained a concrete proposal for a CGLMP-LF inequality, we need to carefully check all strategies to find the LF bound. We do so numerically using MATLAB code found in Appendix B.3. It is discovered that the LF bound on our new inequality is $3$. The next step is to see if quantum mechanics is able to violate this bound. Luckily it is - the quantum bound is $3.69393>3$. However, with a rank of only $19$, this inequality is not a facet of the LF polytope. Is there anything we can do to locate a related facet inequality (i.e. can we rotate our non-facet inequality and find the facet inequality it lies above)? This is possible if we return to the graphical approach advocated for in chapter 9.

One potential criticism of our work so far is that we have found the maximum quantum violation assuming the quantum set is equal to the second level of the NPA hierarchy [@Navascues2007]. This is not strictly true as the NPA hierarchy provides an outer bound for the quantum set - there could be a gap between the two. We are unlikely to run into problems as the second level of the NPA hierarchy is typically an extremely good approximation to the quantum set. However, to be absolutely certain, we will find an explicit quantum measurement scheme which achieves the bound using a see-saw technique. This is implemented by code in Appendix B.3. Ultimately it is found that we can achieve the quantum bound $3.69393$ (up to the fourth decimal place) with the state

\begin{equation}
    |\phi\rangle = \sqrt{0.1378} |0\rangle |0\rangle + \sqrt{0.3980} |1\rangle |1\rangle + \sqrt{0.4642} |2\rangle |2\rangle. 
\end{equation}

This is stable for all methods which achieve the bound. The fact that we are able to find a method which achieves the bound proves that our fears were unfounded and there is no significant gap between the quantum set and the second level of the NPA hierarchy.

