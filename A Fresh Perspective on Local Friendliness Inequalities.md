---
subject: Results and Discussion | Chapter 9
subtitle:
short_title: A Fresh Perspective on Local Friendliness Inequalities
numbering: 
    enumerator: 9.%s
abbreviations:
  LF: Local Friendliness
  CHSH: Clauser, Horne, Shimony, Holt
---

# A Fresh Perspective on Local Friendliness Inequalities

> To arrive where we started and know the place for the first time.
> - T.S. Eliot

In their original paper [@Bong2018], Bong et al. derive all facets of the LF polytope using standard computational techniques (i.e. facet enumeration software). They are then able to group these into equivalence classes. However the structure of each equivalence class is largely left uninvestigated. If we are to succeed in generalising LF inequalities from this particular scenario, with $3$ inputs per player and $2$ outputs per input, to others (which may be computationally intractable) then we will require a more in depth understanding of the physical properties of LF inequalities.

A structural aspect we are able to notice immediately is that one LF inequality contains traces of the CHSH inequality. This presents the following question - are we able to decompose this LF inequality into a CHSH part and a novel part? If so, we inherit a space of two parameters as we are able to consider the trade-off between both parts. This proves to be the case, and from this perspective we see additional structure emerge. We are consequently able to identify the first quantum LF inequality (in chapter 10) and to generalise LF inequalities for a larger scenario (in chapter 11).

The LF inequality we have chosen to focus on, appearing 256 times among the 932 facets [@Bong2018], is given in correlator form by

\begin{equation}
\begin{aligned}
    &-\langle{A_1}\rangle-\langle{A_2}\rangle-\langle{B_1}\rangle-\langle{B_2}\rangle \\
    &-\langle{A_1B_1}\rangle-2\langle{A_1B_2}\rangle-2\langle{A_2B_1}\rangle\overset{\phantom{LF}}+2\langle{A_2B_2}\rangle \\
    &-\langle{A_2B_3}\rangle-\langle{A_3B_2}\rangle-\langle{A_3B_3}\rangle\overset{LF}{\leq}{6}.
\end{aligned}
\end{equation}

This can be translated into probability form using the standard relations

\begin{equation}
\begin{aligned}
    \langle{A_x}\rangle &= \sum_{a,\hspace{0.25mm}b}a{P(a,b{|}x,y)}\\
    \langle{B_y}\rangle &= \sum_{a,\hspace{0.25mm}b}b{P(a,b{|}x,y)}\\
    \langle{A_xB_y}\rangle &= \sum_{a,\hspace{0.25mm}b}a\hspace{0.5mm}b{P(a,b{|}x,y)}
\end{aligned}
\end{equation}

where $x,y\in\set{1,2,3}$ denote the measurement settings chosen by Alice and Bob, and $a,b\in\set{+1,-1}$ denote the measurement outcomes obtained by Alice and Bob (see Appendix A for details). The resulting grid is

```{figure} LF-grid-original.JPG
:name: original-decomposition-figure
:width: 275px
:align: center
```

Here we have introduced some notation which will prove very useful moving forwards. Alice's values ($x$ and $a$) are read along the left hand side whereas Bob's values ($y$ and $b$) are read along the uppermost side. The agents' measurement choice sets the larger scale $x,y\in\set{1,2,3}$ whilst the agents' measurement outcome sets the smaller scale $a,b\in\set{+1,-1}.$ In order to return to the correlator form of the inequality you simply take the dot product of the grid in question with the probability matrix

```{figure} probability-matrix.jpg
:name: probability-matrix-figure
:width: 500px
:align: center
```

## Decomposition of the LF Inequality

Notice that our new grid form of the LF inequality immedately admits the following decomposition.

```{figure} decompositions-original.JPG
:name: decompositions-original-figure
:align: center
```

However we need not stop there; we can simplify and make the pattern more obvious by taking advantage of freedom due to no-signalling. For instance, in the first step we are using no-signalling between Alice's settings $x=2$ and $x=3$ where Bob inputs $y=2$. The idea is that two inequalities can be viewed as equivalent if taking the dot product of their respective grids with the probability matrix returns the same result.

```{figure} decompositions-shifting.JPG
:name: decompositions-shifting-figure
:align: center
```

This new grid admits the following decomposition. 

```{figure} decompositions-shifted.JPG
:name: decompositions-shifted-figure
:align: center
```
Although it superficially looks completely different, this is fully analagous to the original decomposition. The bounds of each component are simply shifted according to the equations below.

- $ \textrm{CHSH} = 4 \textrm{CHSH'} + 2 $

- $ \delta = 4\delta\textrm{'} - 1 $

- $ \epsilon = 4\epsilon\textrm{'} - 2 $

- $ \gamma = 4\gamma\textrm{'} - 1 $

- $ \textrm{LF} = 4\textrm{LF'} - 6 $

One immediate benefit of decomposing our LF inequality as above is that we have identified a very natural two dimensional projection of the LF polytope in which we can investigate; plotting in this parameter space we get a graph of $\epsilon$' against CHSH'.

```{figure} LFgraph.JPG
:name: LF-graph-figure
:width: 400px
:align: center
**A projection of the LF polytope on axes of $\epsilon$' against $CHSH$'.** The line AE denotes the LF inequality. The orange line denotes the second level of the NPA hierarchy (i.e. an outer bound for the quantum set). The hollow pink point represents the maximal quantum violation of LF (as found in the supplemental material of @Bong2018). The filled pink point represents the maximal quantum violation of LF which is not simply a hidden violation of the CHSH inequality between settings $1$ and $2$ (i.e. its nonlocality stems from violating other symmetries of CHSH); we propose this as a new point of interest due to its neat closed form nature. Indeed, the entire opaque orange triangle is of note as this is the area which lies outside of the LF set but inside the quantum set without violating CHSH between settings $1$ and $2$.
```

For future reference, we preserve the vertices of the LF polytope along the LF inequality from [](#LF-graph-figure). The saturating local deterministic strategies, and their scores for each part of the decomposition, are shown in the table below.

```{figure} saturating-ld-strategies.JPG
:name: saturating-ld-strategies-figure
:align: center
```

The specific saturating local deterministic boxes referred to in the table above are numbered as follows. 

```{figure} saturating-ld-boxes.JPG
:name: saturating-ld-boxes-figure
:align: center
```

Each of these corresponds to a vertex of the LF polytope along the LF inequality in [](#LF-graph-figure) - specifically, they all map to point E. Likewise, the saturating PR strategies along with their scores for each part of the decomposition are shown in the following table. 

```{figure} saturating-pr-strategies.JPG
:name: saturating-pr-strategies-figure
:align: center
```

The specific saturating PR boxes referred to in the table above are numbered as follows.

```{figure} saturating-pr-boxes.JPG
:name: saturating-pr-boxes-figure
:align: center
```

As before, each of these corresponds to a vertex of the LF polytope along the LF inequality in [](#LF-graph-figure) - specifically, two map to point E and one maps to point A.

As noted in @Bong2018, the maximal quantum violation of the LF inequality (denoted in [](#LF-graph-figure) by a hollow pink point) is given by the following point:

```{figure} their_point.JPG
:name: their_point-figure
:width: 275px
:align: center
```

The point we identified as potentially of interest (denoted in [](#LF-graph-figure) by a filled pink point) is given by

```{figure} our_point.JPG
:name: our_point-figure
:width: 275px
:align: center
```

where $c=\frac{1}{2}cos^2(\frac{\pi}{8})$ and $s=\frac{1}{2}sin^2(\frac{\pi}{8})$. Having found our new point, we are able to compare it with the maximal quantum violation of LF in the table below, which links nonlocality with local friendliness. It is reasonable to expect locality in the settings where both parties use a $1$ as this corresponds to both parties opening the box and asking its occupant for their result. Hence we categorise the options according to the number of times setting $1$ is used.

```{figure} L_NL_LF_graph.JPG
:name: L_NL_LF_graph-figure
:width: 375px
:align: center
```

It can be seen that, whereas our point is by construction local in the setting [(1,2),(1,2)] and coincidentally local in the setting [(1,3),(1,3)], their point is local in the settings [(1,3),(1,3)], [(1,2),(1,3)] and [(1,3),(1,2)]. Whilst their point may be viewed as superior in the sense that its nonlocality is concentrated only in the [(1,2),(1,2)] setting as opposed to being split between the settings [(1,2),(1,3)] and [(1,3),(1,2)] as is the case for our point, ours is much cleaner with each value taking a closed form as opposed to a decimal. This may render it worthy of further exploration. An interesting question would be whether it is possible to find a point which is local in all four setting combinations [(1,2),(1,2)],[(1,3),(1,3)],[(1,2),(1,3)] and [(1,3),(1,2)], as both identified points fail in this task. It is obviously an option to numerically check this, however it may also be the case that a careful examination of our point allows us to analytically prove whether or not this is achieveable.

Several disparate ideas have been conveyed within this first results chapter; it is therefore worth offering a recap of the essential points moving forwards:

1.  We have decomposed an LF inequality from @Bong2018 into a simpler format.
2.  We have plotted a graph in our new parameter space generated by this decomposition.
3.  We have logged the vertices of the LF polytope along the LF inequality.
4.  We have identified a new point of potential interest.

Of these points, it is the first two which we shall return to in the subsequent results chapters.