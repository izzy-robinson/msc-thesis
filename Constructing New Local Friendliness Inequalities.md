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
---

# Constructing New Local Friendliness Inequalities

> Each truth discovered was a rule available in the discovery of subsequent ones.
> - René Descartes

We saw in chapter 9 that an LF inequality based on the simplest $3$ settings and $2$ outcomes scenario can be decomposed into a CHSH part and a novel part made up of $\delta$ and $\gamma$. The big question raised here is whether it is possible to find LF inequalities for larger more computationally intractable scenarios. If we want to go up to the next simplest scenario (i.e. the $3$ settings and $3$ outcomes scenario) we should therefore take the associated interesting Bell inequality (i.e. CGLMP) and see if we can construct an extension based on the structure identified in chapter 9.

We initially focus on the strategies which saturate CGLMP; there are a huge set of these. We then add in a penalisation term with $\delta$; this narrows down the search space somewhat. Finally we choose a $\gamma$ such that none of these optimal strategies are rewarded (i.e. they are either penalised or neutral); we start off with a symmetric $\gamma$ then edit it through trial and error. We are ultimately left with the following proposal:

Now we have a concrete proposal for a CGLMP-LF inequality, we need to carefully check all strategies to find the LF bound. We do so numerically using MATLAB code found in Appendix B. It is discovered that the LF bound on our new inequality is $3$. The next step is to see if quantum mechanics is able to violate this bound. Luckily it is - the quantum bound is $3.69393>3$. 

Our new inequality is not a facet of the CGLMP-LF polytope.

assume either the maximally entangled state of two qutrits or the state which maximally violates cglmp - find measurements which get 3.69 - as small criticism is finding this is the score in Q2 and there could be a gap between Q2 and quantum mechanics. unlikely as Q2 is very good approximation to quantum mechanics. we can figure this out using see-saw approach.