---
subject: Outlook | Chapter 13
subtitle:
short_title: Outlook 
numbering: 
    enumerator: 13.%s
abbreviations:
    SOS: Sums of Squares
    LF: Local Friendliness
---

# Outlook 

Over the course of discovering the results conveyed within this thesis, several loose-ends were left untied. These prompt multiple open questions, of which a non-exhaustive list is now supplied.

- We only used one of the derived LF inequalities (Equation 8.9) as a basis for decomposition; if we use any of the other three, we may yet uncover further structure to explore.

- We have the maximal violation of LF from @Bong2020 which is simply a hidden violation of CHSH between settings $1$ and $2$, and we have our own violation of LF which doesn't violate CHSH between settings $1$ and $2$ or $1$ and $3$ but does violate other symmetries of CHSH. Is it possible to find the violation of LF which minimises all types of nonlocality, especially those relating to setting $1$? 



- We found the bound on our new quantum LF inequality. It would be good to find a quantum state and explicit measurement scheme which yields this maximum.

- We identified a simple algorithm for generating different SOS decompositions of QLF; to do this one must simply permute the order of operators in the string $S$. Each SOS decomposition independently leads to a set of self-testing equations. Could we use any of these to perform interesting self-testing based on the theory of LF?



- If we are to formalise the method for finding new LF inequalities based on different scenarios there is still work to be done, as the current approach relies non-trivially on trial and error. This may take the form of understanding what exactly is $\gamma$.

- It is unclear how we could move to larger more computationally intractable scenarios with our current toolkit as we still rely on being able to enumerate all vertices of the LF polytope. Finding a way to get around this would widen the range of scenarios our technique is applicable to.

- We have a full list of vertices of the CGLMP-LF polytope; we could feed that back into the software LRS and look for the corresponding hyperplane description.

- Our proposed CGLMP-LF inequality is not a facet. We ideally want a facet inequality as that is a more faithful representation of a polytope. But luckily there are two ways we might go about rotating our non-facet inequality to find the facet it lies above. Firstly, we might use linear programming and various forms of robustness. Secondly, we might try varying the relative weightings of $\delta$ and $\gamma$.

- It can be noticed that the quantum boundary on our graph of CGLMP against $\epsilon$ has several straight sections. Each of these constitutes a quantum CGLMP-LF inequality. Investigating these is a logical next step.

Given time, we hope to engage in these future directions.