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

## Introduction

In their original paper [@bong2020], Bong et al. introduced the notion of local friendliness (LF), as explained in chapter 8. Their key result is that, in the simplest scenario with $3$ inputs per player and $2$ outputs per input, they were able to derive all facets of the LF polytope using standard computational techniques (i.e. facet enumeration software). They found that there were a number of different inequalities and were able to group these into equivalence classes by relabelling the parties and the outcomes. However the structure of each equivalence class is largely left uninvestigated. Furthermore, because of the computational way the results were generated, Bong et al. do not offer any underlying guiding principles as to what is really going on. If we are to succeed in generalising LF inequalities from this particular scenario to others (which quickly become computationally intractable) then we will require a more conceptual understanding of the physical properties of LF inequalities; finding that deeper understanding is the goal of this chapter.

A structural aspect we are able to notice immediately is that one LF inequality contains traces of the CHSH inequality. This presents the following question - are we able to decompose this LF inequality into a CHSH part and a novel part? If so, we inherit a space of two parameters as we are able to consider the trade-off between both parts. This proves to be the case, and from this perspective we see additional structure emerge. We are consequently able to identify the first quantum LF inequality (in chapter 10) and to generalise LF inequalities for a larger scenario (in chapter 11).

The LF inequality we have chosen to focus on, appearing 256 times among the 932 facets [@Bong2020], is given in correlator form by

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

where the lower bound of $-10$ was found by trialling all strategies. Here we have introduced some notation which will prove very useful moving forwards. Alice's values ($x$ and $a$) are read along the left hand side whereas Bob's values ($y$ and $b$) are read along the uppermost side. The agents' measurement choice sets the larger scale $x,y\in\set{1,2,3}$ whilst the agents' measurement outcome sets the smaller scale $a,b\in\set{+1,-1}.$ In order to return to the correlator form of the inequality you simply take the dot product of the grid in question with the probability matrix

```{figure} probability-matrix.jpg
:name: probability-matrix-figure
:width: 500px
:align: center
```

In the next section we will use this grid form to decompose the inequality in a useful way.[^1] 

[^1]: We could of course have done so directly from the correlator form of the inequality, however it is useful to have a visual aid.

## Decomposition of the LF Inequality

Notice that our new grid form of the LF inequality immedately admits the following decomposition

```{figure} decompositions-original.JPG
:name: decompositions-original-figure
:align: center
```

where we have pulled out the standard CHSH inequality for settings $1$ and $2$, and have further decomposed the remainder into two terms which we shall analyse below.

However we need not stop there; we can simplify and make the structure more obvious by taking advantage of freedom due to no-signalling (this is where the grid representation shows its true power). The idea is that two inequalities can be viewed as equivalent if taking the dot product of their respective grids with the probability matrix returns the same result.

Recall the no-signalling conditions given by [Equation 7.1](#NS-equation). In the $(3,3,2,2)$ scenario, these divide into $36$ individual equations. One such equation is the following, where for the sake of example we are arbitrarily considering no-signalling between Alices' settings $x=1$ and $x'=2$ with Bob inputting $y=1$ and outputting $b=1$,

\begin{equation}
P(+1,+1|1,1)+P(-1,+1|1,1) = P(+1,+1|2,1) + P(-1,+1|2,1).
\end{equation}

Moving all terms to the left hand side, we generate a sum which equals zero,

\begin{equation}
P(+1,+1|1,1)+P(-1,+1|1,1) - P(+1,+1|2,1) + P(-1,+1|2,1) = 0.
\end{equation}

This can be written in grid format as

```{figure} NS-example.JPG
:name: NS-example-figure
:width: 225px
:align: center
```

If $LF \leq 6$ and we add this zero sum grid onto LF we get an equivalent inequality with the same bound,

\begin{equation}
\underbrace{LF + P(+1,+1|1,1)+P(-1,+1|1,1) - P(+1,+1|2,1) + P(-1,+1|2,1)}_\text{LF'} \leq 6.
\end{equation}

As has just been seen, we could perform this manipulation without ever using the grid notation - however it would be very messy and difficult to see which steps to take. We will now proceed with simplifying the LF inequality using freedom due to no-signalling in the grid notation. For instance, in the first step we are using no-signalling between Alice's settings $x=2$ and $x'=3$ where Bob inputs $y=2$ and outputs $b=1$.

```{figure} decompositions-shifting.JPG
:name: decompositions-shifting-figure
:align: center
```

This new grid admits the following decomposition. 

```{figure} shifted-decompositions.JPG
:name: decompositions-shifted-figure
:align: center
```
Although it superficially looks completely different, this is fully analagous to the original decomposition. The bounds of each component are simply shifted according to the equations below.

- $ \textrm{CHSH} = 4 \textrm{CHSH'} + 2 $

- $ \delta = 4\delta\textrm{'} - 1 $

- $ \epsilon = 4\epsilon\textrm{'} - 2 $

- $ \gamma = 4\gamma\textrm{'} - 1 $

- $ \textrm{LF} = 4\textrm{LF'} - 6 $

Notice how $\delta'$ is easy to undestand as a 'reward' term and $\gamma'$ is now localised in the (3,3) setting. Another immediate benefit of decomposing our LF inequality as above is that we have identified a very natural two dimensional projection of the LF polytope in which we can investigate; plotting in this parameter space we get a graph of $\epsilon$' against CHSH'.[^2]

[^2]: Note that, rather than amalgamating $\delta'$ and $\gamma'$ into a single $\epsilon'$, we could have produced a three dimensional representation of CHSH' against $\delta'$ against $\gamma'$. However we prefer the two dimensional representation as it is sufficient for our needs and easier to interpret.

```{figure} LFgraph.JPG
:name: LF-graph-figure
:width: 400px
:align: center
**A projection of the LF polytope on axes of $\epsilon$' against CHSH'.** The line AE denotes the LF inequality. The orange line denotes the second level of the NPA hierarchy (i.e. an outer bound for the quantum set). The hollow pink point represents the maximal quantum violation of LF (as found in the supplemental material of @Bong2018). The filled pink point represents the maximal quantum violation of LF which is not simply a hidden violation of the CHSH inequality between settings $1$ and $2$ (i.e. its nonlocality stems from violating other symmetries of CHSH); we propose this as a new point of interest due to its neat closed form nature. Indeed, the entire opaque orange triangle is of note as this is the area which lies outside of the LF set but inside the quantum set without violating CHSH between settings $1$ and $2$.
```

For future reference, we document the vertices of the LF polytope along the LF inequality from [](#LF-graph-figure). The saturating local deterministic strategies, and their scores for each part of the decomposition, are shown in the table below.

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

## A New Point of Interest

As noted in @Bong2020, the maximal quantum violation of the LF inequality (denoted in [](#LF-graph-figure) by a hollow pink point) is given by the following P(a,b|x,y):

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

where $c=\frac{1}{2}\textrm{cos}^2(\frac{\pi}{8})$ and $s=\frac{1}{2}\textrm{sin}^2(\frac{\pi}{8})$. Having found our new box, we are able to compare it with the maximal quantum violation of LF in the table below, which links nonlocality with local friendliness. Because there are three measurement settings for Alice and three measurement settings for Bob, we could try to break it down into something simpler by isolating two out of the three settings for each and asking what properties those statistics have. There are nine two by two sub-experiments contained within the larger experiment. It is reasonable to expect locality in the settings where both parties use a $1$ as this corresponds to both parties opening the box and asking its occupant for their result. Hence we categorise the options according to the number of times setting $1$ is used.

```{figure} L_NL_LF_graph.JPG
:name: L_NL_LF_graph-figure
:width: 375px
:align: center
```

As an example, we will show how we reached our conclusion that the box is local in the [(1,2),(1,2)] setting. If we violate CHSH (or any of its symmetries) then we are nonlocal (NL), whereas if we don't then we are local (L). This amounts to taking the score of the correlators, adding them with either three plus signs and one minus sign or three minus signs and one plus sign, and checking if we exceed the upper bound of $2$.

```{figure} local-example.JPG
:name: local-example-figure
:width: 275px
:align: center
```

Here we have $\langle A_1B_1\rangle =\frac{1}{\sqrt2}$, $\langle A_1B_2\rangle = -1$, $\langle A_2B_1\rangle = -1$ and $\langle A_2B_2\rangle =\frac{1}{\sqrt2}$. The highest score we can achieve is by calculating $-1(\frac{1}{\sqrt2}) -1 (-1) -1 (-1) +1(\frac{1}{\sqrt2}) = 2$ which does not exceed the bound, making these statistics local.

It can be seen that, whereas our box is by construction local in the setting [(1,2),(1,2)] and coincidentally local in the setting [(1,3),(1,3)], their box is local in the settings [(1,3),(1,3)], [(1,2),(1,3)] and [(1,3),(1,2)]. This raises an interesting question as to how to compare. Whilst their box may be viewed as superior in the sense that its nonlocality is concentrated only in the [(1,2),(1,2)] setting as opposed to being split between the settings [(1,2),(1,3)] and [(1,3),(1,2)] as is the case for our box, ours is much 'cleaner' with each value taking a closed form as opposed to a decimal. This may render it worthy of further exploration. An interesting question would be whether it is possible to find a box which is local in all four setting combinations [(1,2),(1,2)],[(1,3),(1,3)],[(1,2),(1,3)] and [(1,3),(1,2)], as both identified boxes fail in this task. It is obviously an option to numerically check this, however it may also be the case that a careful examination of our box allows us to analytically prove whether or not this is achieveable. We leave this for later work.

## Summary

Several disparate ideas have been conveyed within this first results chapter; it is therefore worth offering a recap of the essential points moving forwards:

1.  We have decomposed an LF inequality from @Bong2020 into a simpler format.
2.  We have plotted a graph in our new parameter space generated by this decomposition.
3.  We have logged the vertices of the LF polytope along the LF inequality.
4.  We have identified a new point of potential interest.

Of these points, it is the first two which we shall return to and substantially build upon in the subsequent results chapters.