---
subject: Conceptual Background | Chapter 6
subtitle:
short_title: Basic Wigner's Friend Scenarios
numbering: 
     enumerator: 6.%s
---

# Basic Wigner's Friend Scenarios

> There were three determinate states the cat could be in: these being Alive, Dead, and Bloody Furious.
> - Terry Pratchett

## The Measurement Problem

Perhaps the oldest and thorniest issue faced by the quantum foundations community is that of the measurement problem. At its crux is an apparent tension between the deterministic unitary evolution undergone by closed quantum systems and the probabilistic non-unitary state update observed upon measurement; in other words, how can an indefinite superposition yield a definite outcome? This dilemma is often illustrated via a whimsical thought experiment known as Schrödinger's cat (@Schrodinger1935).[^1]

Suppose a cat is placed inside a box along with a mechanism whereby the cat will be killed if a certain quantum event occurs (for instance, if a radioactive atom decays causing a vial of poison gas to shatter). Prior to the box being opened, the fate of this cat is unknown - assuming the atom has a 50% chance of decaying, it could be either alive or dead with equal probability; in other words, the cat is in a superposition of both states (as depicted in [](#schrodingers-cat-figure)). It is only upon opening the box that we find out whether the cat has survived its ordeal (i.e. no superposition is actually observed).

```{figure} schrodingers-cat-figure.PNG
:name: schrodingers-cat-figure
:align: center
**Schrodinger's cat pictorial equation.** The cat has equal probability of being found alive or dead.
```

## Wigner's Original Paradox

In 1961, Eugene Wigner conceived of a hypothetical scenario commonly referred to as Wigner's Friend paradox (@Wigner1961).[^2]  This thought experiment highlights the role of the observer in the measurement problem. The argument runs as follows. Wigner’s friend $(F)$ is located inside a sealed laboratory $(L)$ along with a quantum system $(S)$ prepared as an equally weighted, normalised superposition of the computational basis states $\ket{0}_S$ and $\ket{1}_S$. The composite system $L$ (which consists of $S$ and $F$ as subsystems) is therefore initialised as

\begin{equation}
\label{WF1-equation-1}
\ket{\Psi_\textrm{initial}}_L=\sqrt{\frac{1}{2}}\big(\ket{0}_S+\ket{1}_S\big)\otimes\ket{\cdot}_F,
\end{equation}

 where $\ket{\cdot}_F$ denotes that the friend's apparatus begins in an empty ready-to-measure state.[^3] [^4] Wigner's friend measures the original system in the computational basis $\{\ket{0}_S,\ket{1}_S\}$ and observes one of two possible binary outcomes by means of her apparatus assuming one of two macroscopically distinguishable configurations $\ket{0}_F$ or $\ket{1}_F$ ; this results in the laboratory adopting a post-measurement state $\ket{\Psi_\textrm{final}}_{L}=\ket{0}_S\ket{0}_F$ or $\ket{\Psi_\textrm{final}}_{L}=\ket{1}_S\ket{1}_F$ respectively. A trivial application of the quantum Born rule reveals that each possibility occurs with probability $\frac{1}{2}$. However Wigner himself $(W)$, located outside of the sealed laboratory, does not know what this measurement outcome is or even if his friend obtained a definite result at all. From his perspective then, assuming quantum theory is universal in the sense that the entire laboratory can be treated as a system in its own right, the laboratory's final state state is derived by applying unitary time evolution to the laboratory's initial state; Wigner therefore assigns to the situation a linear superposition of the original system being in state $\ket{0}_S$ whilst his friend's measuring device is in state $\ket{0}_F$ and the original system being in state $\ket{1}_S$ whilst his friend's measuring device is in state $\ket{1}_F$,

\begin{equation}
\label{WF1-equation-2}
\ket{\Psi_\textrm{final}}_L=\sqrt{\frac{1}{2}}\big(\ket{0}_S\ket{0}_F+\ket{1}_S\ket{1}_F\big).
\end{equation}

```{figure} WF1-compressed.png
:name: WF1-compressed-figure
:align: center
**Schematic of the original Wigner's friend thought experiment.** Wigner's friend (F) is located inside a sealed laboratory (L) containing a two level quantum system (S) and a measuring device equipped with a single fixed setting; she contemplates 'I observe a definite outcome'. Wigner himself (W) is located outside of this room; he considers 'I imagine a superposition state'.
```

As depicted in [](#WF1-compressed-figure), there is an obvious discrepancy between the view of events from Wigner's perspective (i.e. that the laboratory is in a superposition state) and the description of reality from his friend's perspective (i.e. that she observes a single measurement outcome). Although this seems unsettling, it is not inherently contradictory. Multiple mainstream interpretations of quantum theory posit that measurement outcomes do not simply reflect the state of the system being measured; they are inherently relative to something else (whether that 'something else' is the context in which the measurement takes place as in Copenhagen interpretations, the agent performing the measurement as in relational quantum mechanics, or the beliefs held by each observer as in QBism).\footnote{The resolutions provided by this particular group of interpretations have been highlighted as the concepts they introduce motivate subsequent developments. However other interpretations (such as the many-worlds hypothesis, Bohmian mechanics, collapse interpretations and the consistent histories framework) also offer satisfactory explanations.} It is therefore possible to simultaneously affirm both statements. Nevertheless, the disagreement prompts questions regarding when (if ever) the wave function is reduced. Does it happen the moment Wigner's friend completes her measurement? Is it only when Wigner himself is made aware of the outcome? Are both accounts accurate? Or is neither narrative appropriate?

[^1]: Note that Schrödinger intended his commentary to be taken as a reductio ad absurdum proof that orthodox quantum theory was flawed - the idea of cats that are both alive and dead simultaneously was never a serious suggestion, despite it being adopted as such by various popular science outlets.

[^2]: To avoid confusion generated by the eponymous nature of the apparent paradox, we will always use 'Eugene Wigner' when referring to the real life scientist and simply 'Wigner' when referring to the fictional agent who takes part in demonstrations.

[^3]: In practice, the friend's apparatus would be initialised to either $\ket{0}_F$ or $\ket{1}_F$ since we are considering qubits rather than qutrits. However the device's properties need not be specified further than confirming the capacity to record a measurement outcome; referring to an empty state (although technically imprecise) makes it clear that this measurement has not yet occurred.

[^4]: For ease of notation, this is taken to imply that the friend's brain also begins in an empty ready-to-measure state. In full, we could write $\ket{\cdot}_F=\ket{\cdot}_{F_{A}}\ket{\cdot}_{F_{B}}$ where the subscript $F_A$ stands for the friend's apparatus and the subscript $F_B$ labels the friend's brain; however this is unnecessarily clunky, as the state of the friend's apparatus is correlated with that of the friend's brain such that the outcome is automatically and identically copied over.

## Deutsch's Reformulation


In 1985, Deutsch proposed an extended version of Eugene Wigner's argument with the intention of converting the aforementioned questions into claims which may be empirically verified or falsified. This is achieved via a two pronged approach. Firstly, Wigner's friend is given a notebook in which she must record whether she observes a definite result. Secondly, Wigner is required to perform a corroborating measurement on the entire laboratory. The following examination demonstrates how these modifications address the unresolved issues from Eugene Wigner's earlier version of the thought experiment. 

```{figure} WF2-compressed.png
:name: WF2-compressed-figure
:align: center
**Schematic of Deutsch's modified Wigner's friend scenario.** A notebook (N) confirming that the friend observed a definite measurement outcome is passed through a secure communication channel in the wall of the laboratory to Wigner. Both F and W possess measuring devices equipped with a single fixed setting.
```

Wigner's friend ($F$) is located inside a sealed laboratory ($L$) along with a notebook ($N$) and a qubit prepared in the same equally weighted superposition as before. The initial state of $L$ (a composite system consisting of $S$, $F$ and $N$ as subsystems) is therefore given by

\begin{equation}
\label{WF2-equation-1}
\ket{\Psi_\textrm{initial}}_L=\sqrt{\frac{1}{2}}\big(\ket{0}_S+\ket{1}_S\big)\otimes\ket{\cdot}_F\otimes\ket{\cdot}_N,
\end{equation}

where $\ket{\cdot}_F$ is defined as previously and $\ket{\cdot}_N$ denotes that the friend's notebook begins in an empty ready-to-record state. Wigner's friend measures the original system in the computational basis $\{\ket{0}_S,\ket{1}_S\}$ and observes one of two possible binary outcomes by means of her apparatus assuming the form $\ket{0}_F$ or $\ket{1}_F$. In both instances, she writes in her notebook that she has obtained a definite outcome.[^5] Therefore the laboratory adopts a post-measurement state

\begin{equation}
\label{WF2-equation-2}
~~~~\ket{\Psi_\textrm{final}}_{L}&=\ket{0}_S\ket{0}_F\ket{\textrm{`I observed a definite result'}}_N  
\end{equation}

\begin{equation}
\label{WF2-equation-3}
\textrm{or }\ket{\Psi_\textrm{final}}_{L}&=\ket{1}_S\ket{1}_F\ket{\textrm{`I observed a definite result'}}_N. 
\end{equation}

Once again, each possibility occurs with probability $\frac{1}{2}$. However this time (as depicted in figure [](#WF2-compressed-figure)) the notebook is passed through a secure communication channel in the laboratory's wall.[^6] So, although Wigner is still unaware of which measurement outcome his friend observed, he does at least know that she observed a definite result. This unravels the mystery of whether Wigner's friend actually obtains an objective outcome, answering the question affirmatively. 

As before, the state of the laboratory evolves unitarily from Wigner's perspective, ultimately taking the form

\begin{equation}
\label{WF2-equation-4}
\ket{\Psi_\textrm{final}}_L=\sqrt{\frac{1}{2}}\big(\ket{0}_S\ket{0}_F+\ket{1}_S\ket{1}_F\big)\otimes\ket{\textrm{`I observed a definite result'}}_N.
\end{equation}

In order to check this state assignment, Wigner projects onto it the operator

\begin{equation}
\label{WF2-equation-5}
\hat{A}=\ket{0}_S
\ket{0}_F\bra{1}_S\bra{1}_F-\ket{1}_S
\ket{1}_F\bra{0}_S\bra{0}_F
\end{equation}

which corresponds to the observable $A$. If such a measurement always yields the same result (either $A=+1$ or $A=-1$) then this serves as evidence that the friend's laboratory has collapsed into one of the states [Equation 5.4](#WF2-equation-2) or [Equation 5.5](#WF2-equation-3) respectively. However if such a measurement randomly yields different results (sometimes $A=+1$ and sometimes $A=-1$) then this provides proof that the friend's laboratory remains in the superposition state [Equation 5.6](#WF2-equation-4). Therefore Wigner's measurement is able to solve the puzzle regarding what happens inside the laboratory. Assuming the latter case, Wigner is justified in believing both that his friend observed a definite measurement outcome (i.e. that the wave function has been reduced) and that the laboratory is in a superposition state wherein both measurement results remain possible (i.e. that the wave function has not been reduced). This appears to imply that both facts coexist, leaving us with a concrete query - can these seemingly incompatible accounts really be reconciled with one another?

## What do Different Interpretations Have to Say?

Wigner's own solution to this supposed paradox was based on the idea that conciousness is central to the measurement process.[^7] He argued that the wave function would collapse as soon as Wigner's friend interacted with it, so Wigner himself would necessarily see the same result. The fact that he doesn't know which result this would be is therefore not an ontic issue (intrinsic to nature) but an epistemic problem (due to ignorance). Few, if any, physicists still support the view that conciousness is relevant to the measurement process; mots endorse one of the following interpretations of quantum theory and would explain the apparent contradiction accordingly.

Proponents of Copenhagen interpretations[^8] posit a Heisenberg cut which distinguished between the quantum world of the observed system and the classical world of the observing agent. In the **conventional-Copenhagen interpretation**  (@Heisenberg1958, @Bohr1996), the location of the Heisenberg cut is objective; all agents must be on the classical side of the divide regardless of whether they are currently applying quantum theory or having quantum theory applied to them. Since the friend must be treated as a classical object, it is illegitimate for Wigner to consider her existing in a superposition state. Therefore the only sensible description of the Wigner's friend scenario is that the friend observes a definite outcome of either spin-down or spin-up, and Wigner observes the same definite outcome. In the **neo-Copenhagen interpretation** (@Muynck2004), the location of the Heisenberg cut is subjectibe; only the agent who is currently applying quantum theory must be on the classical side of the divide. Since Wigner may treat his friend as a quantum object, he can meaningfully consider her as existing in the superposition state [Equation 6.6](#WF2-equation-4). The fact that this description of events diverges from the friend's assertion that she detected a definite outcome is no cause for concern; it is simply indicative of the different perspectives being taken.

Those who subscribe to the **many-worlds hypothesis** (@Everett1957) argue for the existence of a universal wave function evolving unitarily according to the Schrödinger equation. Measurements result in the branching of this universal wave function such that each possible outcome occurs in one branch. Therefore Wigner's interpretation of the scenario is correct; the two terms in the superposition state [Equation 6.6](#WF2-equation-4) correspond to the two branches, one in which Wigner's friend obtained the outcome spin-down and one in which she obtained the outcome spin-up. Although the friend perceives herself as being in only one of these branches, having obtained only one of these outcomes, she is aware in principle that the other branch must exist so she ultimately agrees with Wigner's conclusion.

Supporters of **Bohmian mechanics** (@Bohm1952) postulate both a universal wave function (whose unitary evolution is governed by the Schrödinger equation) and a configuration space of physical particles (whose deterministic evolution obeys a guiding equation). As in the many-worlds case, the overall state generated by the Wigner's friend scenario is represented by the superposition [Equation 6.6](#WF2-equation-4). However, unlike in the many-worlds case, the outcomes that each constituent term correspond to are not considered equally real; only one result is physically realised, but knowledge of which outcome actually occurs is conditional on classical hidden variables.

Advocates for **QBism** (@Caves2002) maintain that, by definition, quantum states encode subjective views held by agents rather than objective elements of reality. Due to their different perspectives, Wigner and his friend possess different information,  so it makes complete sense that they assign different quantum states to the situation.

Those who adhere to **relational quantum mechanics** (@Rovelli1996) also reject the notion of observer-independent facts. In this interpretation, assertions about measurement outcomes do not simply reflect the state of the system being measured; they are necessarily relative to the agent doing the measuring. It is therefore possible to simultaneously affirm that from the friend's frame of reference a definite outcome was obtained, and from Wigner's frame of reference the situation is described by the superposition state [Equation 6.6](#WF2-equation-4). Both views may be true without entailing contradiction.

## Outlook

Whilst it seems that each of the aforementioned interpretations has successfully nullified the apparent paradox, Wigner's friend type thought experiments are far from being relegated to the sidelines of research into the foundations of quantum theory, as we shall see in chapter 8.

[^5]: Cases in which the friend has *not* obtained a definite outcome are deliberately ignored because they conflict with sensible definitions of what it means to conduct an experiment, such as Bohr's claim that 'by the word 'experiment' we refer to a situation where we can tell others what we have done and what we have learned'.

[^6]: By 'secure communication channel' it is meant that all degrees of freedom, other than the one which corresponds to the message recorded in the notebook, remain protected. It is essential that this is the case if [Equation 5.6](#WF2-equation-4) is to remain a separable state rather than becoming entangled.

[^7]: He later abandoned this opinion, instead becoming convinced that macroscopic systems cannot be described using quantum mechanics due to the effects of decoherence.

[^8]: There is no official definition of the Copenhagen interpretation; rather, the term refers to a collection of ideas developed by Niels Bohr, Werner Heisenberg, Max Born, and several others who pioneered quantum physics during the 1920's. Not only is this interpretation unclear on certain issues due to disagreements between group members, it is also silent on others as many questions which are central to modern research has not yet been asked at the time of its creation.