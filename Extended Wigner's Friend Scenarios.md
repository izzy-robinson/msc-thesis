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

Section 8 is dedicated to a systematic examination of all relevant Extended Wigner's Friend Scenarios (EWFS) - namely, the formulations by Brukner, Bong and Cavalcanti et al., Frauchiger and Renner, Pusey and Masanes, and Żukowski and Markiewicz. Each of these involve a fusion of elements from both simple Wigner's Friend scenarios and Bell Test set ups.

## Brukner's Argument

Recall Deutsch's query regarding whether Wigner and his friend's contradictory accounts of the same situation are reconcilable. Brukner sought to explore a generalisation of this - specifically, whether it is possible to assign s joiny probability distribution to statements made by different agents about their own independent measurement outcomes. To that end, Brukner listed the following four assumptions which one might reasonably expect a physical theory to obey.

1. **Observer-Independent Facts (OIF):** *One can jointly assign truth values to propositions regarding the measurement outcomes of different (super)observers.*

2. **No Conspiracy (NC):** *The choice of measurement settings is statistically independent from the preparation of the system being measured.*

3. **No Action at a Distance (NAD):** *Provided the agents are sufficiently space-like separated,* [^1] *the measurement settings used by one (super)observer do not influence the measurement outcomes obtained by another (super)observer.*

4. **Universal Validity of Quantum Theory (UVQT):** *Quantum predictions hold true at any scale, regardless of the complexity of the system under consideration.*[^2]

Brukner proceeded to analyse a novel scenario, inspired by both the set-up of Deutsch's simple Wigner's Friend Scenario and the protocol of a standard Bell test, according to these assumptions.
A contradiction arose, indicating that the conjunction of assumptions $1-4$ is untenable and prompting to proposal of a no-go theorem: at least one of assumptions $1-4$ must be rejected as false. This no-go theorem is technically neutral in the sense that it does not dictate which particular assumption should be denied. However assumptions $2-4$ are extremely well motivated. Rejecting the NC assumption would render most forms of scientific research impracticable; if one cannot examine a system without changing its preparation, one cannot hope to find information about its true state. To permit action at a distance is to deny a key premise of Einstein's theory of special relativity. And quantum theory's domain of validity is widely believed to be unlimited due to its extraordinary success in accurately predicting the results of experiments. In summary, dismissing any of assumptions $2-4$ entails straying from the well-worn path and risking far reaching unattractive consequences. Therefore, quite naturally, Brukner took his theorem to disprove the existence of assumption $1$ i.e. OIF.

```{figure} brukner-figure.JPG
:name: brukner-figure
:align: center
**Schematic of Brukner's EWFS.** Observers ($A_1$ and $B_1$) perform **fixed** measurements, the results of which remain inside their respective laboratories. Superobservers ($A_2$ and $B_2$) choose between **binary** measurement options and their results are knowable outside of the laboratories.
```


## Bong and Cavalcanti et al.'s Argument

1. **Absoluteness of Observed Events (AOE):** *Observed events are real (i.e. not relative to anything or anyone).* 

In the context of this EWFS, the AOE assumption entails that there exists a theoretical joint probability distribution $P(a,b,c,d|x,y)$ from which the empirical probability $\mathcal{P}(a,b|x,y)$ can be obtained: 

\begin{equation}
\mathcal{P}(a,b|x,y)=\sum_{c,d}P(a,b,c,d|x,y).
\end{equation} 

Furthermore, AOE ensures consistency is maintained between observers and superobservers when $x,y=1$: 

\begin{align}
P(a|c,d,x=1,y)&=\delta_{a,c} \\
 P(b|c,d,x,y=1)&=\delta_{b,d}.
\end{align}

2. **No Conspiracy (NC):** *The choice of measurement settings is statistically independent from the preparation of the system being measured.* In the context of this EWFS, the NC assumption enforces that the observers' measurement outcomes be uncorrelated with the superobservers' measurement settings:

\begin{equation}
P(c,d|x,y)=P(cd).
\end{equation}

3. **No Action at a Distance (NAD):** *Provided the agents are sufficiently space-like separated, the measurement settings used by one (super)observer do not influence the measurement outcomes obtained by another (super)observer.* In the context of this EWFS, the NAD assumption dictates that the local settings $x$ and $y$ are uncorrelated with the distant outcomes $b$ and $a$ (respectively):

\begin{equation}
P(b|c,d,x,y)=P(b|c,d,y) \\
P(a|c,d,x,y)=P(a|c,d,x).
\end{equation}

4. **Universal Validity of Quantum Theory (UVQT):** *Quantum predictions hold true at any scale, regardless of the complexity of the system under consideration.*

Notice that the outcomes $c,d$ play the same role as the hidden variables $\lambda$ that go into the assumptions for Bell's theorem.

```{figure} bong-cavalcanti-figure.JPG
:name: bong-cavalcanti-figure
:align: center
**Schematic of Bong and Cavalcanti et al.'s EWFS.** Observers ($A_1$ and $B_1$) perform **fixed** measurements, the results of which remain inside their respective laboratories. Superobservers ($A_2$ and $B_2$) choose between **three** different measurement options and their results are knowable outside of the laboratories.
```

## Frauchiger and Renner's Argument

```{figure} pusey-masanes-frauchiger-renner-figure.JPG
:name: pusey-masanes-frauchiger-renner-figure
:align: center
**Schematic of Frauchiger and Renner's EWFS.** All observers ($A_1$ and $B_1$) and superobservers ($A_2$ and $B_2$) perform **fixed** measurements. Results found by observers remain inside their respective laboratories whereas results found by superobservers are knowable outside of the laboratories.
```

## Pusey and Masanes' Argument

```{figure} pusey-masanes-frauchiger-renner-figure.JPG
:name: pusey-masanes-frauchiger-renner-figure
:align: center
**Schematic of Pusey and Masanes' EWFS.** All observers ($A_1$ and $B_1$) and superobservers ($A_2$ and $B_2$) perform **fixed** measurements. Results found by observers remain inside their respective laboratories whereas results found by superobservers are knowable outside of the laboratories.
```

## Żukowski and Markiewicz' Argument

For completeness, it is worth mentioning that there exist extended Wigner's Friend arguments which do not rely on any Bell Test elements, for example @Guerin et al.; however such work is irrelevant to our results and therefore beyond the scope of this thesis.


[^1]: A sufficient distance is defined as one which demands that a signal from one laboratory must travel faster than the speed of light in order to reach the other laboratory in time to affect any results.

[^2]: This is simply a statement that '[t]here is nothing in quantum theory making it applicable to three atoms and inapplicable to $10^{23}$'. It is recognised that '[w]hile quantum theory can in principle describe anything, a quantum description cannot include everything'. However it is emphasized that this is not a flaw specific to quantum theory but rather a logical necessity required of any physical theory (classical or quantum) which hopes to avoid problems related to self-reference.