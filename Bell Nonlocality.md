---
subject: Conceptual Background | Chapter 7
subtitle:
short_title: Bell Nonlocality
numbering: 
    enumerator: 7.%s
---

# Bell Nonlocality

> Bell's Second Theorem: Misunderstandings of Bell's Theorem happen so fast that they violate locality.
> - XKCD

## Bell Tests

Bell nonlocality (@Brunner2014, @Scarani2019) is the study of correlations which defy any classical (i.e. local) explanation; it enforces the radical statement that there is inherent indeterminacy in nature, making nonlocality a particularly fascinating prediction of quantum mechanics. For an accessible introduction from an expert in the topic see @Gisin2014. 

A Bell scenario consists of multiple players in space-like separation who share a common resource.[^1] It is defined by the number of players (named alphabetically as Alice, Bob etc.),[^2] the list of inputs per player, and the list of outputs per input; we therefore label each scenario with the tuple $(M_A,M_B,m_A,m_B)$ where $M_A,M_B$ denote the number of inputs per player and $m_A,m_B$ denote the number of outputs per input. The rules of play are known in advance and the players are allowed to prepare a common strategy prior to the test beginning.

[^1]: We will discuss the reasons for this space-like separation later on.
[^2]: Note that we will consider only two player, or bipartite, scenarios because generalisation to multipartite scenarios is both trivial and beyond the scope of this thesis.

### Laboratories and Games

Bell nonlocality can be explored in multiple ways; specifically, we can think of either the experimental setups found in physics laboratories (see [](#bell-test-figure)) or the cooperative games known by computer scientists as 'interactive proof systems' (see [](#bell-game-figure)). Whilst the convention of nonlocal games most clearly reveals the crucial nature of nonlocality, it is the inequality format which will help with the results section of this thesis; therefore we will, for the most part, stick to this notation. It is also within the laboratory framework that we can examine the experimental evidence which transforms nonlocality from a theoretical possibility to a proven fact.

```{figure} bell-test.PNG
:name: bell-test-figure
:align: center
:width: 400px
**Schematic of a laboratory based Bell test.** A shared quantum state $\rho_{AB}$ is prepared and a list of measurements ${M^x},{M^y}$ are chosen. Which of these measurements is performed in a given round depends on the settings $x,y$. The data for multiple rounds are sorted to establish correlations between the measurement settings $x,y$ and the measurement outcomes $a,b$.
```

```{figure} bell-game-figure.PNG
:name: bell-game-figure
:align: center
**Schematic of a Bell game.** A referee (Raya) distributes inputs to and collects outputs from the players (Alice and Bob). The data for multiple rounds are sorted to establish correlations between the inputs $x,y$ and the outputs $a,b$.
```

### Useful definitions

#### Processes and behaviours

Processes, denoted $\lambda$, describe the mechanism by which outputs are generated from inputs; this could be anything from tossing coins or casting dice to computing functions or measuring entangled particles - they are therefore treated as a 'black-boxes' from which an external party can only observe the behaviours, denoted $P(a,b|x,y)$, which describe coarse grained statistics regarding correlations between inputs and outputs.

#### Non-signalling correlations

The most interesting kind of resources are non-signalling ones; if players were able to communicate during the game they would easily win 100% of the time. Non-signalling constraints are formally expressed as

\begin{equation}
\sum_b P(a,b|x,y) = \sum_b P(a,b|xy') = \sum_b P(a,b|x) \hspace{5mm}\forall \hspace{2mm} a,x,y,y'\\
\sum_a P(a,b|x,y) = \sum_a P(a,b|x'y) = \sum_a P(a,b|y) \hspace{5mm} \forall \hspace{2mm} b,x,y,x'.
\end{equation}

These can be interpreted as saying that Alice's local marginals are independent of Bob's measurement setting hence Bob cannot signal to Alice by his choice of input; likewise, Bob's local marginals are independent of Alice's measurement setting hence Alice cannot signal to Bob by her choice of input.

#### Local correlations

A more restrictive condition is locality. Formally, the set of local behaviours is given by

\begin{equation}
P(a,b|x,y) = \int d\lambda Q(\lambda) P(a|x,\lambda) P(b|y,\lambda)
\end{equation}

where $Q(\lambda)$ is a probability distribution describing the strategy (i.e. how frequently a particular process $\lambda$ is used). If a behaviour cannot be written in this form it is referred to as nonlocal.

#### Quantum correlations

The set of behaviours achievable within the framework of quantum mechanics can be written in the form

\begin{equation}
P(a,b|x,y) = tr (\rho_{AB} M_{a|x} \otimes M_{b|y})
\end{equation}

where $\rho_{AB}$ denotes a quantum state in the joint Hilbert space $\mathcal{H_A}\otimes\mathcal{H_B}$, $M_{A|x}$ denotes the measurement operators on Alice's Hilbert space such that 

\begin{equation}
M_{a|x} \geq 0 \\
\sum_a M_a|x = \mathbf{1}
\end{equation}

and $M_{b|y}$ denotes the measurement operators on Bob's Hilbert space such that

\begin{equation}
M_{b|y} \geq 0 \\
\sum_b M_b|y = \mathbf{1}.
\end{equation}

Quantum correlations can be stronger than those allowed by local hidden variable (LHV) theories, leading to the violation of Bell inequalities. These violations are a key feature that distinguishes quantum mechanics from classical physics.

## Examples

At this point, with much of the formalism under our belt, it is best to jump straight into some example Bell scenarios.

### The $(2,2,2,2)$ Scenario: CHSH

In correlator form, the CHSH inequality is given by

\begin{equation}
| \langle A_1B_1 \rangle + \langle A_1B_2 \rangle + \langle A_2B_1 \rangle - \langle A_2B_2 \rangle| \leq 2.
\end{equation}

In probability form this becomes

\begin{equation}
 P(a=b|1,1) + P(a=b|1,2) + P(a=b|2,1) + P(a \neq b|2,2) \leq 3.
\end{equation}

#### LHV strategies

With a classical, or LHV, strategy the maximum probability of winning the game is $\frac{3}{4}$ 0r $75\%$. We will prove this by exhaustion. There are $4$ possible deterministic processes which might be followed by Alice, namely

1. The result is always $a=1$, regardless of the choice for $x$.
2. The result is always $a=2$, regardless of the choice for $x$.
3. The result is always identical to the choice for $x$ (i.e. $a=x$).
4. The result is always different from the choice for $x$ (i.e. $a \neq x$).

Likewise, there are $4$ deterministic processes which might be followed by Bob. This means a total of $4 \times 4 = 16$ combinations of processes for both Alice and Bob. All of these are listed in the table below, where it can be seen that none score more than $3$.

```{figure} chsh-scores.JPG
:name: chsh-scores-figure
:align: center
```

#### A quantum strategy

With a quantum strategy, the maximum probablility of winning the game is $\frac{2+\sqrt{2}}{4}$ or $85.4\%$. Violation of the CHSH inequality is achieved through a combination of a maximally entangled quantum state and carefully chosen measurement settings. A typical choice of measurement angles that leads to maximum violation of the CHSH inequality is


- $A_1 = 0^\circ = \hat{X}$ 
- $A_2 = 90^\circ = \hat{Z}$ 
- $B_1 = 45^\circ = \frac{\hat{X}+\hat{Z}}{\sqrt{2}}$ 
- $B_2 = -45^\circ = \frac{\hat{X}-\hat{Z}}{\sqrt{2}}$


```{figure} chsh-quantum-strategy.JPG
:name: chsh-quantum-strategy-figure
:width: 350 px
:align: center
The measurement directions used by Alice (x) and Bob (y) in a winning quantum strategy for Bell's game.
```

### The $(2,2,d,d)$ Scenario: CGLMP

In probability form, the CGLMP inequality is given by

\begin{equation}
    P(a-b-0|1,1) + P(a-b=0|1,2) + P(a-b=0|2,1) \\
    + P(a-b=1|2,2) - P(a-b=2|1,1) - P(a-b=1|1,2) \\
    - P(a-b=1|2,1) - P(a-b=0|2,2) \leq 2
\end{equation}

where all subtractions are modulo $3$.[^3]

[^3]: Here and hereafter we use the phrase 'modulo $3$' in the natural (rather than strictly mathematical) sense of circulating through the values $1,2,3$; $3$ modulo $3$ is taken to be $1$ rather than $0$.

#### LHV strategies

There are $9$ possible deterministic processes which might be followed by Alice, namely

1. The result is always $a=1$, regardless of the choice for $x$.
2. The result is always $a=2$, regardless of the choice for $x$.
3. The result is always $a=3$, regardless of the choice for $x$.
4. The result is always identical to the choice for $x$ (i.e. $a=x$).
5. The result is always different from the choice for $x$ such that $a=x+1$.
6. The result is always different from the choice for $x$ such that $a=x+2$.
7. The result is always different from the choice for $x$ such that $a=-x$.
8. The result is always given by $a=-(x+2)$.
9. The result is always given by $a=-(x+1)$.

Likewise, there are $9$ possible deterministic processes which might be followed by Bob. This means a total of $9 \times 9 = 81$ combinations of processes for both Alice and Bob. It would of course be possible to create a table of tables as we did in the CHSH case, however this would be a little unwieldy to actually produce given its $81$ elements; so we won't show it explicitlty.

#### A quantum strategy


## Experimental Considerations

### Methods

### Loopholes

Due to the revolutionary nature of their results, Bell tests have been subjected to intense scrutiny; this is only natural since 'extraordinary claims require extraordinary evidence'. Some of the weaknesses (commonly referred to as 'loopholes') in both the reasoning and the experimental implementation are conveyed in this section. However, so as not to confuse the reader, we note now that all known loopholes have been satisfactorily closed under reasonable assumptions (i.e. to the extent that rejecting these assumptions would constitute a more radical view than accepting the strangeness of Bell nonlocality itself).

- **The Detection Loophole**

In real life photonic experiments (as opposed to the theoretical games we discussed earlier) it is common for detectors to have poor efficiency; in other words, photons can go missing. If enough of these lost photons correspond to cases which pull the value of $S$ in the wrong direction then it is possible to fake a Bell inequality violation. 

```{figure} photon-missing-poster.PNG
:name: photon-missing-poster-figure
:width: 500px
:align: center
```

There are several ways to deal with this issue. The first is to simply ignore any rounds in which the photon is lost (i.e. postselect only on occasions in which a response is elicited); however this relies on a fair sampling assumption (i.e. the detected events must accurately represent the full set of statistics which would have been collected had the detectors been 100% efficient). This assumption is well motivated - after all, why should nature conspire against us to cheat on Bell tests? However it is still an assumption worth keeping in mind; to convincingly avoid falling foul of the detection loophole one must force the referee to provide an outcome in every single round of the experiment, even those in which no results are recieved from the players - in such cases the referree should simply make up an answer.

- **The Locality Loophole**

Bell inequality violations are only interesting if the players are unable to communicate with each other after the game begins (i.e. if the shared resource is nonlocal); if a local communication channel exists then the locality loophole would be open meaning the violation is trivial. Luckily, special relativity dictates that the speed at which information propagates is (along with everything else) upper bounded by the speed of light in a vacuum. Therefore, provided Alice and Bob are sufficiently space-like separated (i.e. information about Alice's input cannot reach Bob until after he has reported his output and vice versa) the locality loophole can be closed. Mathematically, this condition may be expressed as 

\begin{equation}
\label{locality-equation-1}
P(a|x,y,b,\lambda) = P(a|x,\lambda) \hspace{3mm} , \hspace{3mm} P(b|x,y,a,\lambda) = P(b|y,\lambda).
\end{equation}

```{figure} locality-loophole.PNG
:name: locality-loophole-figure
:align: center
Space-time diagram showing a regime in which the locality loophole (and the meaurement independence loophole) is closed.
```

```{figure} spaceships.jpg
:name: spaceships-figure
:align: center
An illustration showing two space-like separated parties in laymans terms.
```

There are, of course, technical difficulties associated with generating and maintaining entangled pairs across large distances. However, as theoreticians, we need not concern ourselves with such intricacies; suffice it to say that this is possible.

- **The Measurement Independence Loophole**

A feature of [](#locality-loophole-figure) that we have not yet paid attention to is the hidden variable $\lambda$. If the choice of measurement settings is correlated with any past common causal factor (denoted by this hidden variable) then the measurement independence loophole is said to be open. Closing the meaurement independence loophole requires the following mathematical statement to be satisfied:

\begin{equation}
\label{locality-equation-2}
q(\lambda|x,y) = q(\lambda).
\end{equation}

 Various methods of choosing suitable inputs have been trialled, from quantum random number generators and fluctuations in radiation emitted by distant stellar objects to letters from the Geneva phone book and timestamps from a TV sitcom. It is impossible to close this loophole completely since superdeterminists could always claim the behaviour of our system is correlated with these sources of information; however such a viewpoint is so conspiratorial as to be ignored. Furthermore, measurement independence is not just an issue for Bell nonlocality - rejecting measurement independence would render most forms of scientific research impracticable; once reasonable precautions have been made, it is typically assumed and rarely questioned (other than in cases of deliberate tampering).
 

### Loophole-free Bell Tests

- Three loophole-free Bell tests were performed in 2015 by the following groups:
    - TU Delft
    - IQOQI Vienna 
    - NIST Boulder 
- Further progress since has included the Big Bell Test at ICFO.