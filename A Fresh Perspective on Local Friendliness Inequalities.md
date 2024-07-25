---
subject: Results and Discussion | Chapter 9
subtitle:
short_title: A Fresh Perspective on Local Friendliness Inequalities
numbering: 
    enumerator: 9.%s
---

# A Fresh Perspective on Local Friendliness Inequalities

> To arrive where we started and know the place for the first time.
> - T.S. Eliot

One local friendliness inequality, appearing 256 times among the 932 facets [@Bong2020], is given in correlator form by

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
    \langle{B_y}\rangle &= \sum_{a,\hspace{0.25mm}b}\beta{P(a,b{|}x,y)}\\
    \langle{A_xB_y}\rangle &= \sum_{a,\hspace{0.25mm}b}a\hspace{0.5mm}b{P(a,b{|}x,y)}
\end{aligned}
\end{equation}

where $x,y\in\set{1,2,3}$ denote the measurement settings chosen by Alice and Bob, and $a,b\in\set{+1,-1}$ denote the measurement outcomes obtained by Alice and Bob (see Appendix A for details). The resulting grid is

```{figure} LF-grid-original.svg
:name: original-decomposition-figure
:width: 275px
:align: center
Caption
```

## Decomposition of the LF Inequality

Notice that this immedately admits a decomposition

```{figure} original-decomposition.svg
:name: original-decomposition-figure
:align: center
Caption
```

But we can simplify and make pattern more obvious by taking advantage freedom due to no-signalling.

```{figure} LF-inequality-transformation.svg
:name: QLF-graph-figure
:align: center
Caption
```

```{figure} decompositions-shifted.pdf
:name: decompositions-shifted-figure
:align: center
Caption
```


$ \textrm{CHSH} = 4 \textrm{CHSH'} + 2 $


$ \delta = 4\delta\textrm{'} - 1 $


$ \epsilon = 4\epsilon\textrm{'} - 2 $


$ \gamma = 4\gamma\textrm{'} - 1 $


$ \textrm{LF} = 4\textrm{LF'} - 6 $


Plotting in our new parameter space

```{figure} LFgraph.svg
:name: LF-graph-figure
:width: 400px
:align: center
Caption
```

```{figure} saturating-ld-strategies.svg
:name: saturating-ld-strategies-figure
:align: center
Caption
```

```{figure} saturating-pr-strategies.svg
:name: saturating-pr-strategies-figure
:align: center
Caption
```

```{figure} saturating-ld-boxes.svg
:name: saturating-ld-boxes-figure
:align: center
Caption
```

```{figure} saturating-pr-boxes.svg
:name: saturating-pr-boxes-figure
:align: center
Caption
```