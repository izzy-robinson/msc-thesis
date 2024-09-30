---
subject: Conceptual Background | Chapter 8
subtitle:
short_title: Extended Wigner's Friend Scenarios
numbering: 
     enumerator: 8.%s
abbreviations:
  EWFS: Extended Wigner's Friend Scenario
  AOE: Absoluteness of Observed Events
  NC: No Conspiracy
  NAD: No Action at a Distance 
  OIF: Observer-Independent Facts
  UVQT: Universal Validity of Quantum Theory
---

# Extended Wigner's Friend Scenarios

> What you see and what you hear depends a great deal on where you are standing.
> - C.S. Lewis

Section 8 is dedicated to a systematic examination of the most relevant Extended Wigner's Friend Scenario (EWFS) - namely, the formulation by Bong et al. [@Bong2020] - which involves a fusion of elements from both simple Wigner's Friend scenarios and Bell Test set ups. There do exist multiple other EWFS's - specifically those of Brukner [@Brukner2018], Frauchiger and Renner [@Frauchiger2018], Pusey and Masanes, Żukowski and Markiewicz [@Zukowski2021], and Guerin et al. [@Guerin2021] - however these are not directly relevant to our results and are therefore beyond the scope of this thesis.

## Bong et al.'s Argument

Recall Deutsch's query regarding whether Wigner and his friend's contradictory accounts of the same situation are reconcilable. Bong et al. [@Bong2020] sought to explore a generalisation of this - specifically, whether it is possible to assign a joint probability distribution to statements made by different agents about their own independent measurement outcomes. To this end, Bong et al. proceeded to analyse an EWFS, adapted from that considered by Brukner [@Brukner2018], which was in turn inspired by both the set-up of Deutsch's simple Wigner's Friend Scenario and the protocol of a standard Bell test.[^1]

### The set-up

Consider a bipartite Wigner's friend scenario involving two superobservers (Alice and Bob) alongside their respective observers (Charlie and Dani).  The observer's are located inside sealed laboratories, each of which contains one particle from an entangled pair. The superobservers are located outside of these laboratories.

```{figure} bong-cavalcanti-figure.JPG
:name: bong-cavalcanti-figure
:align: center
**Schematic of Bong and Cavalcanti et al.'s EWFS.** Observers (Charlie and Dani) perform **fixed** measurements, the results of which remain inside their respective laboratories. Superobservers (Alice and Bob) choose between **three** different measurement options and their results are knowable outside of the laboratories.
```

The observers both measure their half of the entangled pair along a single direction (i.e. there is no choice of measurement settings). Then the superobservers come into play. They each choose between three different measurement settings. If $x=1$ ($y=1$), Alice (Bob) simply opens Charlie's (Dani's) laboratory and directly asks them for their outcome $c$ ($d$), assigning its value to their own outcome $a=c$ ($b=d$). If $x\in\set{2,3}$ ($y\in\set{2,3}$) the superobservers restore their respective observers' laboratories to their previous state and proceed to measure the particle directly along an arbitrary direction. 

What statistics are empircally accessible at the end of this process? Unless $x=1$ ($y=1$), the value for $c$ ($d$) is erased when Alice (Bob) performs their measurement, so in general this information is not available. Ultimately, the available values are $a$, $b$, $x$ and $y$; we can therefore measure (as frequencies) the empirical probabilities $\mathcal{P}(a,b|x,y)$.

### Local Friendliness Assumptions

Bong et al. listed the following four assumptions which one might reasonably expect a physical theory to obey.

1. **Absoluteness of Observed Events (AOE):** *Observed events are real (i.e. not relative to anything or anyone). Therefore one can jointly assign truth values to propositions regarding the measurement outcomes of different (super)observers.* 

In the context of this EWFS, the AOE assumption entails that there exists a theoretical joint probability distribution $P(a,b,c,d|x,y)$ from which the empirical probability $\mathcal{P}(a,b|x,y)$ can be obtained: 

\begin{equation}
\mathcal{P}(a,b|x,y)=\sum_{c,d}P(a,b,c,d|x,y).
\end{equation} 

Furthermore, AOE ensures consistency is maintained between observers and superobservers when $x,y=1$ (i.e. when the superobserver simply opens the observer's laboratory, asks what their outcome was and sets their own result to be equal): 

\begin{equation}
P(a|c,d,x=1,y)&=\delta_{a,c} \\
P(b|c,d,x,y=1)&=\delta_{b,d}.
\end{equation}

2. **No Conspiracy (NC):** *The choice of measurement settings is statistically independent from the preparation of the system being measured.* In the context of this EWFS, the NC assumption enforces that the observers' measurement outcomes be uncorrelated with the superobservers' measurement settings:

\begin{equation}
P(c,d|x,y)=P(cd).
\end{equation}

3. **No Action at a Distance (NAD):** *Provided the agents are sufficiently space-like separated,[^2] the measurement settings used by one (super)observer do not influence the measurement outcomes obtained by another (super)observer.* In the context of this EWFS, the NAD assumption dictates that the local settings $x$ and $y$ are uncorrelated with the distant outcomes $b$ and $a$ (respectively):

\begin{equation}
P(b|c,d,x,y)=P(b|c,d,y) \\
P(a|c,d,x,y)=P(a|c,d,x).
\end{equation}

4. **Universal Validity of Quantum Theory (UVQT):** *Quantum predictions hold true at any scale, regardless of the complexity of the system under consideration (i.e. quantum theory applies to observers).[^3]*

Notice that the outcomes $c,d$ play the same role as the hidden variables $\lambda$ that go into the assumptions for Bell's theorem.

Bong et al. then analysed the EWFS according to these assumptions. Subsequent generation of local friendliness inequalities violable by quantum theory indicates that the conjunction of assumptions $1-4$ is untenable and prompts the proposal of a no-go theorem: at least one of assumptions $1-4$ must be rejected as false. This no-go theorem is technically neutral in the sense that it does not dictate which particular assumption should be denied. However assumptions $2-4$ are extremely well motivated. Rejecting the NC assumption would render most forms of scientific research impracticable; if one cannot examine a system without changing its preparation, one cannot hope to find information about its true state. To permit action at a distance is to deny a key premise of Einstein's theory of special relativity. And quantum theory's domain of validity is widely believed to be unlimited due to its extraordinary success in accurately predicting the results of experiments. In summary, dismissing any of assumptions $2-4$ entails straying from the well-worn path and risking far reaching unattractive consequences. Therefore, quite naturally, Bong, et al. took their theorem to disprove the existence of assumption $1$ i.e. AOE.

### Describing Correlations

We now derive the general form for an LF probability distribution.

\begin{equation}
\mathcal{P}(a,b|x,y) \overset{AOE}=& \sum_{c,d} P(a,b|c,d,x,y) \\

 \overset{Bayes'}=& \sum_{c,d} P(a,b|c,d,x,y) P(c,d|x,y) \\

 \overset{NC} =& \sum_{c,d} P(a,b|c,d,x,y) P(c,d)
\end{equation}

Using Bayes' rule again, we can decompose $P(a,b|c,d,x,y)$ in two different ways. Adopting one decomposition approach for the final line of Equation $8.5$, we find the following:

\begin{equation}
\mathcal{P}(a,b|x,y) \overset{Bayes'} =& \sum_{c,d} P(a|b,c,d,x,y) P(b|c,d,x,y) P(c,d) \\
\overset{NS}=& \sum_{c,d} P(a|b,c,d,x,y) P(b|c,d,x,y) P(c,d) \\
=& \sum_{c,d} \delta_{a,c} P(B|c,d,y) P(c,d) \textrm{ if x=1.}
\end{equation}

Adopting the other decomposition approach for the final line of Equation $8.5$, we find the following:

\begin{equation}
\mathcal{P}(a,b|x,y)\overset{Bayes'} =&\sum_{c,d} P(b|a,c,d,x,y) P(a|c,d,x,y) P(c,d) \\
\overset{NS}=& \sum_{c,d}P(b|a,c,d,y)P(a|c,d,x) P(c,d) \\
=& \sum_{c,d} \delta_{b,d} P(a|c,d,x) P(c,d) \textrm{ if y=1.}
\end{equation}

Combining all we have learnt, we obtain the following:

\begin{equation}
\mathcal{P}(a,b|x,y) = 
\begin{cases}
   \sum_{c,d} P(a,b|c,d,x,y) P(c,d)\textrm{ if x,y} \neq \textrm{1.} \\
   \sum_{c,d} \delta_{a,c} P(B|c,d,y) P(c,d) \textrm{ if x=1.} \\
   \sum_{c,d} \delta_{b,d} P(a|c,d,x) P(c,d) \textrm{ if y=1.}
\end{cases}
\end{equation}

```{figure} LF-polytope.png
:name: LF-polytope-figure
:align: center
**Reproduced from [@Bong2020].** Two-dimensional slice of the space of correlations. The solid areas represent different polytopes of correlations. The local deterministic set (green) is a subset of the extended Wigner's friend scenario polytope (orange) which in turn is a subset of the no signalling polytope (purple). The red line represents the boundary of the quantum set which contains the local deterministic polytope and is contained within the no signalling polytope but neither contains nor is contained by the extended Wigner's friend scenario polytope.
```

### Local Friendliness Inequalities

Using the $96$ extreme points of the LF polytope and the software PANDA, which specialises in characterizing a convex polytope in terms
of either its extreme points or its facets, it is possible to obtain the inequalities defining the $932$ facets of the LF polytope. These $932$ inequalities can be categorized into equivalence classes based on any combination of the below relabellings:

- Parties Alice and Bob
- Alice's inputs $2$ and $3$
- Bob's inputs $2$ and $3$
- Alice's outputs for a particular $x$
- Bob's outputs for a particular $y$

The resultant $9$ equivalence classes of inequalities can be described as follows.

Genuine LF facet $1$ (appearing $256$ times amongst the $932$ facets):

\begin{equation}
\begin{aligned}
    &-\langle{A_1}\rangle-\langle{A_2}\rangle-\langle{B_1}\rangle-\langle{B_2}\rangle \\
    &-\langle{A_1B_1}\rangle-2\langle{A_1B_2}\rangle-2\langle{A_2B_1}\rangle\overset{\phantom{LF}}+2\langle{A_2B_2}\rangle \\
    &-\langle{A_2B_3}\rangle-\langle{A_3B_2}\rangle-\langle{A_3B_3}\rangle\overset{LF}{\leq}{6}.
\end{aligned}
\end{equation}

Genuine LF facet $2$ (appearing $256$ times amongst the $932$ facets):

\begin{equation}
\begin{aligned}
    &-\langle{A_1}\rangle-\langle{A_2}\rangle-\langle{A_3}\rangle-\langle{B_1}\rangle \\
    &-\langle{A_1B_1}\rangle-\langle{A_2B_1}\rangle-\langle{A_3B_1}\rangle\overset{\phantom{LF}}-2\langle{A_1B_2}\rangle \\
    &+\langle{A_2B_2}\rangle+\langle{A_3B_2}\rangle-\langle{A_2B_3}\rangle+\langle{A_3B_3}\rangle\overset{LF}{\leq}{5}.
\end{aligned}
\end{equation}

Bell-$I_{3322}$ with marginals over inputs $1$ and $2$ (appearing $256$ times amongst the $932$ facets):

\begin{equation}
\begin{aligned}
    &-\langle{A_1}\rangle-\langle{A_2}\rangle+\langle{B_1}\rangle-\langle{B_2}\rangle \\
    &+\langle{A_1B_1}\rangle-\langle{A_1B_2}\rangle-\langle{A_1B_3}\rangle\overset{\phantom{LF}}-\langle{A_2B_1}\rangle \\
    &+\langle{A_2B_2}\rangle-\langle{A_2B_3}\rangle-\langle{A_3B_1}\rangle-\langle{A_3B_2}\rangle\overset{LF}{\leq}{4}.
\end{aligned}
\end{equation}

Bell-$I_{3322}$ with marginals over inputs $2$ and $3$ (appearing $64$ times amongst the $932$ facets):

\begin{equation}
\begin{aligned}
    &-\langle{A_2}\rangle-\langle{A_3}\rangle+\langle{B_2}\rangle-\langle{B_3}\rangle \\
    &-\langle{A_1B_2}\rangle-\langle{A_1B_3}\rangle-\langle{A_2B_1}\rangle\overset{\phantom{LF}}-\langle{A_2B_2}\rangle \\
    &-\langle{A_2B_3}\rangle+\langle{A_3B_1}\rangle-\langle{A_3B_2}\rangle-\langle{A_3B_3}\rangle\overset{LF}{\leq}{4}.
\end{aligned}
\end{equation}
 
Bell-CHSH for inputs $1,2$ of Alice and $1,3$ of Bob (appearing $32$ times amongst the $932$ facets):

\begin{equation}
\langle{A_1B_1}\rangle - \langle{A_1B_3}\rangle - \langle{A_2B_1}\rangle - \langle{A_2B_3}\rangle \overset{LF}{\leq}{2}.
\end{equation}

Bell-CHSH for inputs $1,3$ of Alice and $2,3$ of Bob (appearing $32$ times amongst the $932$ facets):

\begin{equation}
-\langle{A_1B_2}\rangle - \langle{A_1B_3}\rangle - \langle{A_3B_2}\rangle - \langle{A_3B_3}\rangle \overset{LF}{\leq}{2}.
\end{equation}

Positivity for inputs $1$ of Alice and $1$ of Bob (appearing $4$ times amongst the $932$ facets):

\begin{equation}
1 + \langle{A_1}\rangle+ \langle{B_1}\rangle+ \langle{A_1B_1}\rangle \geq 0.
\end{equation}

Positivity for inputs $1$ of Alice and $2$ of Bob (appearing $16$ times amongst the $932$ facets):

\begin{equation}
1 + \langle{A_1}\rangle+ \langle{B_2}\rangle+ \langle{A_1B_2}\rangle \geq 0.
\end{equation}

Positivity for inputs $2$ of Alice and $2$ of Bob (appearing $16$ times amongst the $932$ facets):

\begin{equation}
1 + \langle{A_2}\rangle+ \langle{B_2}\rangle+ \langle{A_2B_2}\rangle \geq 0.
\end{equation}

The positivity facets simply reflect that all probability values must be between 0 and 1 and are thus trivial.


[^1]: The main difference between the set-ups of Brukner and Bong et al. is that Brukner allows the superobservers a choice between only two measurements, whereas Bong et al. allow the superobservers a choice between three measurements. This slight generalisation allows for the generation of new inequalities whereas Brukner, despite considering a novel scenario, simply recovered the CHSH inequality.

[^2]: A sufficient distance is defined as one which demands that a signal from one laboratory must travel faster than the speed of light in order to reach the other laboratory in time to affect any results.

[^3]: This is simply a statement that '[t]here is nothing in quantum theory making it applicable to three atoms and inapplicable to $10^{23}$'. It is recognised that '[w]hile quantum theory can in principle describe anything, a quantum description cannot include everything'. However it is emphasized that this is not a flaw specific to quantum theory but rather a logical necessity required of any physical theory (classical or quantum) which hopes to avoid problems related to self-reference.