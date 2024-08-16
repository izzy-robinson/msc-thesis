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

Section 8 is dedicated to a systematic examination of the most relevant Extended Wigner's Friend Scenario (EWFS) - namely, the formulation by Bong and Cavalcanti et al. [@Bong2020] - which involves a fusion of elements from both simple Wigner's Friend scenarios and Bell Test set ups. There do exist multiple other EWFS's - specifically those of Brukner [@Brukner2018], Frauchiger and Renner [@Frauchiger2018], Pusey and Masanes, Żukowski and Markiewicz [@Zukowski2021], and Guerin et al. [@Guerin2021] - however these are not directly relevant to our results and are therefore beyond the scope of this thesis.

## Bong and Cavalcanti et al.'s Argument

Recall Deutsch's query regarding whether Wigner and his friend's contradictory accounts of the same situation are reconcilable. Bong et al. [@Brukner2018] sought to explore a generalisation of this - specifically, whether it is possible to assign a joint probability distribution to statements made by different agents about their own independent measurement outcomes. 

## Local Friendliness Assumptions

To this end, Bong et al. listed the following four assumptions which one might reasonably expect a physical theory to obey.

1. **Absoluteness of Observed Events (AOE):** *Observed events are real (i.e. not relative to anything or anyone). Therefore one can jointly assign truth values to propositions regarding the measurement outcomes of different (super)observers.* 

In the context of this EWFS, the AOE assumption entails that there exists a theoretical joint probability distribution $P(a,b,c,d|x,y)$ from which the empirical probability $\mathcal{P}(a,b|x,y)$ can be obtained: 

\begin{equation}
\mathcal{P}(a,b|x,y)=\sum_{c,d}P(a,b,c,d|x,y).
\end{equation} 

Furthermore, AOE ensures consistency is maintained between observers and superobservers when $x,y=1 (i.e. when the superobserver simply opens the observer's laboratory, asks what their outcome was and then sets their own result to be equal) 

\begin{equation}
P(a|c,d,x=1,y)&=\delta_{a,c} \\
P(b|c,d,x,y=1)&=\delta_{b,d}.
\end{equation}

2. **No Conspiracy (NC):** *The choice of measurement settings is statistically independent from the preparation of the system being measured.* In the context of this EWFS, the NC assumption enforces that the observers' measurement outcomes be uncorrelated with the superobservers' measurement settings:

\begin{equation}
P(c,d|x,y)=P(cd).
\end{equation}

3. **No Action at a Distance (NAD):** *Provided the agents are sufficiently space-like separated,[^1] the measurement settings used by one (super)observer do not influence the measurement outcomes obtained by another (super)observer.* In the context of this EWFS, the NAD assumption dictates that the local settings $x$ and $y$ are uncorrelated with the distant outcomes $b$ and $a$ (respectively):

\begin{equation}
P(b|c,d,x,y)=P(b|c,d,y) \\
P(a|c,d,x,y)=P(a|c,d,x).
\end{equation}

4. **Universal Validity of Quantum Theory (UVQT):** *Quantum predictions hold true at any scale, regardless of the complexity of the system under consideration.[^2]*

Notice that the outcomes $c,d$ play the same role as the hidden variables $\lambda$ that go into the assumptions for Bell's theorem.

Bong et al. proceeded to analyse a scenario, adapted from that considered by Brukner [@Brukner2018] - which was in turn inspired by both the set-up of Deutsch's simple Wigner's Friend Scenario and the protocol of a standard Bell test - according to these assumptions. A contradiction arose, indicating that the conjunction of assumptions $1-4$ is untenable and prompting to proposal of a no-go theorem: at least one of assumptions $1-4$ must be rejected as false. This no-go theorem is technically neutral in the sense that it does not dictate which particular assumption should be denied. However assumptions $2-4$ are extremely well motivated. Rejecting the NC assumption would render most forms of scientific research impracticable; if one cannot examine a system without changing its preparation, one cannot hope to find information about its true state. To permit action at a distance is to deny a key premise of Einstein's theory of special relativity. And quantum theory's domain of validity is widely believed to be unlimited due to its extraordinary success in accurately predicting the results of experiments. In summary, dismissing any of assumptions $2-4$ entails straying from the well-worn path and risking far reaching unattractive consequences. Therefore, quite naturally, Bong, et al. took their theorem to disprove the existence of assumption $1$ i.e. AOE.

## The Specific EWFS

```{figure} bong-cavalcanti-figure.JPG
:name: bong-cavalcanti-figure
:align: center
**Schematic of Bong and Cavalcanti et al.'s EWFS.** Observers ($A_1$ and $B_1$) perform **fixed** measurements, the results of which remain inside their respective laboratories. Superobservers ($A_2$ and $B_2$) choose between **three** different measurement options and their results are knowable outside of the laboratories.
```

## Local Friendliness Inequalities

[^1]: A sufficient distance is defined as one which demands that a signal from one laboratory must travel faster than the speed of light in order to reach the other laboratory in time to affect any results.

[^2]: This is simply a statement that '[t]here is nothing in quantum theory making it applicable to three atoms and inapplicable to $10^{23}$'. It is recognised that '[w]hile quantum theory can in principle describe anything, a quantum description cannot include everything'. However it is emphasized that this is not a flaw specific to quantum theory but rather a logical necessity required of any physical theory (classical or quantum) which hopes to avoid problems related to self-reference.