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

We saw in chapter 9 that an LF inequality based on the simplest $3$ settings and $2$ outcomes scenario can be decomposed into a CHSH part and a novel part made up of $\delta$ and $\gamma$. The big question raised here is whether it is possible to find LF inequalities for larger more computationally intractable scenarios. If we want to go up to the next simplest scenario (i.e. the $3$ settings and $3$ outcomes scenario) we should therefore take the associated interesting Bell inequality (i.e. CGLMP[^1]) and see if we can construct an extension based on the structure identified in chapter 9.

[^1]: See chapter $7$ for a description of the CGLMP inequality. Note that, using the grid notation, [Equation 7.8](#cglmp-equation) is analagous to CGLMP in the format used within this chapter.

# Searching for a CGLMP-LF Inequality

We initially focus on the strategies which saturate CGLMP; there are a huge set of these. We then add in a reward term with $\delta$; this narrows down the search space somewhat. Finally we choose a $\gamma$ such that none of these optimal strategies are rewarded (i.e. they are either penalised or neutral); we start off with a symmetric $\gamma$ then edit it through trial and error. There is significant work left to do if we are to formalise this technique, however we are ultimately left with the following ingredients:

```{figure} cglmp-proposal.JPG
:name: cglmp-proposal-figure
:align: center
```

Now we have a set of ingredients, we want to turn these into a concrete proposal for a CGLMP-LF inequality. To achieve this we will produce a two dimensional plot taking CGLMP as one axis and $\epsilon = \delta + \gamma$ as the other axis. From this we should be able to read off the optimal coefficients for each part. Such an approach is analagous to how we discovered the quantum LF inequality in chapter 10. 

```{figure} cglmp-graph.JPG
:name: cglmp-graph-figure
:align: center
The dashed turqoise line represents the new CGLMP-LF inequality. The orange line denotes the second level of the NPA hierarchy (i.e. an outer bound for the quantum set).
```

From [](#cglmp-graph-figure), we are able to read off the precise CGLMP-LF inequality. It is given by

\begin{equation}
\textrm{CGLMP} + 3(\delta+\gamma) \leq 5.
\end{equation}

Having obtained a concrete proposal for a CGLMP-LF inequality, we need to carefully check all strategies to verify the LF bound. We do so numerically using MATLAB code found in Appendix B.3. It is discovered that the LF bound on our new inequality is $5$, as expected. The next step is to see if quantum mechanics is able to violate this bound. Luckily it is - the quantum bound is $5.8971>5$. 

Using the rank method, we see the dimension of the face of our polytope is only $37$ (not $47$); therefore this inequality is not a facet of the LF polytope. Is there anything we can do to locate a related facet inequality? We have a point outside the CGLMP-LF polytope (i.e. the quantum violation of our new inequality). This brings up the possibility of using linear programming and various forms of robustness to rotate our non-facet inequality and find the facet inequality it lies above. 

One potential criticism of our work so far is that we have found the maximum quantum violation assuming the quantum set is equal to the second level of the NPA hierarchy [@Navascues2008]. This is not strictly true as the NPA hierarchy provides an outer bound for the quantum set - there could be a gap between the two. We are unlikely to run into problems as the second level of the NPA hierarchy is typically an extremely good approximation to the quantum set. However, to be absolutely certain, we will find an explicit quantum measurement scheme which achieves the bound using a see-saw technique. This is implemented by code in Appendix B.3. Ultimately it is found that we can achieve the quantum bound $5.8971$ with a state that is locally unitarily equivalent to the maximally entangled state in qubit basis,

\begin{equation}
\frac{1}{\sqrt{2}}(|1\rangle |1\rangle + | 2 \rangle | 2 \rangle). 
\end{equation}

This is stable for all methods which achieve the bound. The fact that we are able to find a method which achieves the bound proves that our fears were unfounded and there is no significant gap between the quantum set and the second level of the NPA hierarchy. It is interesting that this state is neither in the qubit basis nor is it the same as the state which maximally violates the CGLMP inequality.

Note also that, in [](#cglmp-graph-figure), the quantum boundary contains several straight sections. Although we will not explore this within the thesis, each of these presents a quantum CGLMP-LF inequality which could be characterised. It is interesting that there appears to be so much simplicity contained within the quantum set for LF when the geometry of quantum sets for nonlocality are frequently very complex [@Goh2018].

# Summary

What have we achieved within this chapter? We have used our intuition, built through the previous two chapters, to construct by hand an entirely new LF inequality based on CGLMP rather than CHSH. We have discovered that this is not a facet inequality but have proposed a method whereby a related facet inequality may yet be uncovered. We have further found an explicit measurement scheme which achieves the maximum quantum violation, proving that our new inequality is genuinely violable by quantum mechanics and it is not simply a computational artefact. Finally, we have noticed the existence of several quantum CGLMP-LF inequalities; characterising these may be a direction for future work.

