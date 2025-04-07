---
subject: Mathematical Preliminaries | Chapter 5
subtitle:
short_title: Optimisation Problems
numbering:
  enumerator: 5.%s
abbreviations:
  SOS: Sums of Squares
  PSD: Positive Semidefinite
---

# Optimisation Problems

> Premature optimisation is the root of all evil.
> - Donald Knuth, [@Hyde2009]

Optimisation problems arise in a wide variety of disciplines, from advertising and economics to healthcare and education. Regardless of the context, however, they always consist of the same four primary ingredients.

1. **Objective function:** The quantity we aim to optimise (i.e. maximise or minimise). Its arguments are given by *'decision variables'*.    
2. **Decision variables:** The quantities we have control over. These may be discrete or continuous, and further restrictions are placed on their allowed values by *'constraints'*.
3. **Constraints:** Restrictions that must be adhered to by the decision variables. These might appear as equalities (i.e. hyperplanes) or inequalities (i.e. halfspaces), whose intersection defines the *'feasible set'*.
4. **Feasible set:** The region in which all constraints are satisfied (i.e. the set of possible values from which the decision variables can be chosen).

Certain properties of these ingredients will determine which optimisation technique is most appropriate; we must therefore define a few more characteristics before going into detail about specific optimisation tools. Where not otherwise referenced, the information is gathered from chapter 3 of @Boyd2004.

:::{prf:definition} Linear Functions
:label: linear-functions-definition
A function $f:\mathbb{R}^n\rightarrow\mathbb{R}^m$ is linear if
```{math}
:label: linear-functions-equation  
f(\mu \mathbf{x_i} + \nu \mathbf{x_j}) = \mu f(\mathbf{x_i}) + \nu f(\mathbf{x_j})
```
$\forall \hspace{0.5mm} \mu,\nu \in \mathbb{R}, \hspace{1mm} \forall \hspace{0.5mm} \mathbf{x_i} , \mathbf{x_j} \in \mathbb{R}^n$. 
:::


:::{prf:lemma}Linear Functions
This is the case if and only if there exists a matrix $M\in\mathbb{R}^{m \times n}$ such that $f(\mathbf{x})=M\mathbf{x}, \hspace{1mm}\forall\hspace{0.5mm}\mathbf{x}\in\mathbb{R}^n$.
:::

:::{prf:definition} Affine Functions
:label: affine-functions-definition
A function $f:\mathbb{R}^n\rightarrow\mathbb{R}^m$ is affine if 
```{math}
:label: linear-functions-equation 
f(\mu \mathbf{x_i} + (1-\mu) \mathbf{x_j}) = \mu f(\mathbf{x_i}) + (1-\mu) f(\mathbf{x_j})
```
$\forall \hspace{0.5mm} \mu \in [0,1], \hspace{1mm} \forall \hspace{0.5mm} \mathbf{x_i} , \mathbf{x_j} \in \mathbb{R}^n$. 
:::

:::{prf:lemma} Affine Functions
This is the case if and only if there exists a matrix $M\in\mathbb{R}^{m \times n}$ and a vector $\mathbf{b}\in\mathbb{R}^m$ such that $f(\mathbf{x})=M\mathbf{x}+\mathbf{b}, \hspace{1mm}\forall\hspace{0.5mm}\mathbf{x}\in\mathbb{R}^n$.
:::

```{figure} linear-affine-functions.png
:name: linear-affine-functions-figure
:width: 350px
:align: center
Two-dimensional depiction of a linear function (dark purple) and an affine function (pale purple) with the same gradient. Notice that the linear function passes through the origin whilst the affine function is offset.
```


:::{prf:definition} Convex Functions
:label: convex-functions-definition
A function $f:\mathbb{R}^n\rightarrow\mathbb{R}^m$ is convex if
```{math}
:label: convex-functions-equation 
f(\mu \mathbf{x_i} + (1-\mu)\mathbf{x_j}) \leq \mu f(\mathbf{x_i}) + (1-\mu) f(\mathbf{x_j})
```
$\forall \hspace{0.5mm} \mu \in [0,1], \hspace{1mm} \forall \hspace{0.5mm} \mathbf{x_i} , \mathbf{x_j} \in \mathbb{R}^n$.
:::

:::{prf:lemma} Convex Functions
This is the case if and only if there exists an $\mathbf{a} \in \mathbb{R}^{m \times n}$ and a ${\mathbf{b}} \in \mathbb{R}^m$ such that $f({\mathbf{x}}) \leq \mathbf{a}{\mathbf{x}}+{\mathbf{b}}$.[^1]
[^1]: Convex sets and convex functions are related via the epigraph (mathematical) which is defined in the epigraph (literary) at the start of chapter 4; a function is convex if and only if its epigraph is a convex set.
:::

```{figure} convex-functions.png
:name: convex-functions-figure
:align: center
Two-dimensional depiction of a convex function (dark purple) and the chord between two points on it (pale purple). A chord (from the Latin chorda, meaning "bowstring") of a circle is a straight line segment whose endpoints both lie on a circular arc.  Axis values are labelled to motivate [Equation 5.3](#convex-functions-equation).
```

## Linear Programming

A linear program (LP) is an optimisation problem involving a *linear* objective function whose *real* valued arguments must obey *affine* constraints.[^2] LPs can be expressed in standard form as

[^2]: Linear programming is also applicable to scenarios involving *affine* objective functions, however we can treat these as if they were linear since constant terms do not affect the feasible set or optimal solution. 

\begin{equation}
\label{linear-program-equation-1}
\begin{aligned}
    \text{maximise} \hspace{3mm} &f(x_1,...,x_k)\\
    \text{subject to} \hspace{3mm} &g_i(x_1,...,x_k) = b_i, \hspace{3mm}  \forall \hspace{1mm} i = 1,...,m\\
    \text{and} \hspace{3mm} &h_j(x_1,...,x_k) \leq c_j, \hspace{3mm}  \forall \hspace{1mm} j = 1,...,n\\
\end{aligned}
\end{equation}

where $f(x_1,...,x_k)$ is the objective function, $g_i(x_1,...,x_k)$ denotes a system of $m$ equality constraints with associated values $b_i$, and $h_j(x_1,...,x_k)$ represents a set of $n$ inequality constraints each bounded by $c_j$. Each of $f$, $g$ and $h$ are themselves linear functions. Note that maximising a function $f$ is equivalent to minimising its negation $-f$, so we are free to consider only maximisation problems without loss of generality (WLOG). Note also that we need not always *optimise* the objective function at all; sometimes it is sufficient to simply determine whether there exists a solution that simultaneously satisfies every constraint (i.e. to check if the feasible set is empty) - this is called a 'feasibility LP'.[^3]

[^3]: See @Skrzypczyk2023 for a discussion on recasting feasibility LPs as standard LPs.

It is often less cumbersome to adopt a vectorial notation whereby we combine the decision variables into a single vector $\mathbf{x}=(x_1 \hspace{3mm} ... \hspace{3mm} x_k)^T$. This allows us to encode information as follows.

- The objective function $f$ can be specified by a vector $\mathbf{a}\in\mathbb{R}^k$ such that $f(x_1,...,x_k)=\mathbf{a}\cdot\mathbf{x}$.
- Equality constraints $g_i$ can be specified by a vector $\mathbf{r}_i\in\mathbb{R}^k$ such that $g_i(x_1,...,x_k)= \mathbf{r_i}\cdot \mathbf{x}$.
- Inequality constraints $h_i$ can be specified by a vector $\mathbf{s}_j\in\mathbb{R}^k$ such that $h_j(x_1,...,x_k) = \mathbf{s_j}\cdot\mathbf{x}$.

Consequently, we are able to rewrite LPs more compactly as

\begin{equation}
\label{linear-program-equation-2}
\begin{aligned}
    \text{maximise} \hspace{3mm} &\mathbf{a} \cdot \mathbf{x}\\
    \text{subject to} \hspace{3mm} &\mathbf{r}_i \cdot \mathbf{x} = b_i, \hspace{3mm}  \forall \hspace{1mm} i = 1,...,m\label{5.5b}\\
    \text{and} \hspace{3mm} &\mathbf{s}_j \cdot \mathbf{x} \leq c_j, \hspace{3mm}  \forall \hspace{1mm} j = 1,...,n.\label{5.5c}
\end{aligned}
\end{equation}

A further simplification is possible using matrix notation; consolidating all vectors $r_i$ into an $m \times k$ matrix $B=(r_1^T \hspace{3mm} ... \hspace{3mm} r_m^T)^T$, and grouping all vectors $s_j$ into an $n \times k$ matrix $C=(s_1^T \hspace{3mm} ... \hspace{3mm} s_n^T)^T$, transforms an LP into its most succinct form,

\begin{equation} 
\label{linear-program-equation-3}
\begin{aligned}
    \text{maximise} \hspace{3mm} &\mathbf{a} \cdot \mathbf{x} \label{Eq:5.6a} \\
    \text{subject to} \hspace{3mm} &B  \mathbf{x} = \mathbf{b} \label{Eq:5.6b} \\
    \text{and} \hspace{3mm} &C  \mathbf{x} \leq \mathbf{c}. \label{Eq:5.6c}
\end{aligned}
\end{equation}

Having arrived at a concise formulation of linear programming, we are ready to consider techniques for tackling problems of this type. Before we do so, however, it is a good idea to introduce some notation for the solutions we will obtain; let $\alpha$ represent the optimal value of the objective function, and denote by $\mathbf{x^*}$ the choice of decision variable which achieves this bound.[^4]

[^4]: Note that $\mathbf{x^*}$ is generally not a unique point; there could exist infinitely many coordinates which simultaneously saturate the objective.

### Solution Methods

The most popular methods for solving LPs (and therefore the ones we will touch upon in this section) are *graphical approaches*, *simplex algorithms* and *interior point techniques*.

#### A Graphical Approach

Simple linear programming scenarios can be solved graphically using the following steps.

- **Step 1:** Plot the hyperplanes (halfspaces) associated with each (in)equality constraint.
- **Step 2:** Find the feasible region (i.e. the intersection of all hyperplanes and halfspaces).
- **Step 3:** Identify the most extreme point at which the objective function touches the feasible region, and read off the corresponding choice for each decision variable.
- **Step 4:** Substitute these coordinates into the objective function to calculate its optimal value.

Upon performing this procedure, one of four things will happen: a unique optimal solution will be found, multiple optimal solutions will be discovered, the LP will be declared unbounded, or the LP will be pronounced infeasible. Each of the aforementioned cases is most clearly communicated via a two-dimensional example.

:::{prf:example} An LP with a unique optimal solution
:label: LP-unique-example

Suppose we want to *maximise* the objective function 

\begin{equation*}
f(x_1,x_2) = x_1 + x_2
\end{equation*}

subject to the inequality constraints

\begin{equation*} 
\begin{split}
    x_1 + 2x_2 &\leq 2\\
    2x_1 + x_2 &\leq 2\\
    x_1,x_2 &\geq 0.
\end{split}
\end{equation*}
We can portray this LP graphically in the following way.

```{figure} unique-example.png
:name: unique-example-figure
:width: 450px
:align: center
```

Within the feasible set (opaque purple region) the objective function (dashed black line) has its highest value at the vertex marked with a dot (i.e. for the optimal choice of decision variables $\mathbf{x^*}=(x_1^*,x_2^*)=(\frac{2}{3},\frac{2}{3})$). Here, the value for the objective function is $\alpha = f(x_1^*,x_2^*) = 1(\frac{2}{3})+1(\frac{2}{3}) = \frac{4}{3}$.

:::

:::{prf:example} An LP with multiple optimal solutions
:label: LP-multiple-example

Suppose we want to *maximise* the objective function 

\begin{equation*}
f(x_1,x_2) = 8x_1 + 4x_2
\end{equation*}

 subject to the inequality constraints 

\begin{equation*} 
\begin{split}
    2x_1 + x_2 &\leq 10\\
    3x_1 + 4x_2 &\leq 24\\
    x_1 - x_2 &\leq 3\\
    x_1,x_2 &\geq 0.
\end{split}
\end{equation*}
We can represent this LP graphically as below.

```{figure} multiple-example.png
:name: multiple-example-figure
:width: 450px
:align: center
```

The feasible set (opaque purple region) has a face which is parallel to the objective function (dashed black line), so both vertices marked with dots (and any point along the face connecting them) constitute valid optimal solutions. One such optimal choice of decision variables is $\mathbf{x^*} = (x_1^*,x_2^*) = (4,2)$; the corresponding value for the objective function is $\alpha = f(x_1^*,x_2^*) = 8(4)+4(2) = 40$.

:::

:::{prf:example} An unbounded LP with no optimal solution
:label: unbounded-LP-example

Suppose we want to *maximise* the objective function 

\begin{equation*}
f(x_1,x_2) = x_1 + x_2
\end{equation*}

subject to the inequality constraints

\begin{equation*} 
\begin{split}
    x_1 + 2x_2 &\geq 8\\
    2x_1 + x_2 &\geq 6.
\end{split}
\end{equation*}

We can depict this LP graphically in the following way.

```{figure} unbounded-example.png
:name: unbounded-example-figure
:width:450px
:align: center
```

Notice that within the feasible set (opaque purple region) the value of the objective function (dashed black line) can continue increasing to infinity without ever hitting a constraint (solid purple line). This means the LP is *unbounded* so no optimal solution can be found.[^5]

[^5]: Had our task been to *minimise* the objective function, we would have succeeded.


:::

:::{prf:example} An infeasible LP with no solution at all
:label: infeasible-LP-example

Suppose we want to optimise *any* objective function $f(x_1,x_2)$ subject to the set of inequality constraints

\begin{equation*} 
\begin{split}
   2 x_1 + 3x_2 &\leq 12\\
    x_1 &\geq 5\\
    x_2 &\geq 3.
\end{split}
\end{equation*}

We can view this LP graphically as follows.

```{figure} infeasible-example.png
:name: infeasible-example-figure
:width: 450px
:align: center
```

Observe that the halfspaces (translucent purple regions) defined by each inequality (solid purple lines) do not intersect to generate a feasible region. Therefore, regardless of the objective function chosen, no solution can simultaneously obey all necessary constraints (i.e. the LP is *infeasible*).

:::


Our (admittedly limited) selection of examples reveals an emerging pattern; for each solvable LP, at least one optimal solution is found at a vertex of its feasible region. This feature is not unique to the specific problems we have chosen to present - rather, it is true in general. Let us state this important result as a theorem whose proof we omit. See @Gass2003 for details.

:::{prf:theorem} Vertex solutions of LPs.
:label: vertex-solutions-theorem

If an LP is solvable, at least one optimal solution must be located at a vertex of its feasible region.

:::

As a corollary, we have now stumbled across a brute force algorithm for solving generic LPs; it suffices to find all vertices and then substitute the coordinates of each into the objective function - the highest (lowest) result is the optimal solution for a maximisation (minimisation) problem. However, as discussed in section [](#convex-polytopes), this method is not particularly efficient due to the number of vertices which must be considered; a different technique will be required for more complicated LPs involving higher dimensions or additional constraints. One potentially viable procedure is Dantzig's simplex algorithm [@Dantzig1963].


#### The Simplex Algorithm

Dantzig's simplex algorithm [@Dantzig1963] is an iterative process which involves moving between adjacent vertices, each with improving values for the objective function, until an optimal solution is reached. If a vertex is not optimal, there exists an edge containing it such that the value of the objective function is strictly increasing as you move away. Assuming the edge is finite, this edge connects to another vertex where the objective function has a greater value. The simplex algorithm walks along the edges of a polytope to vertices with greater and greater objective values. This continues until the maximum value is reached or an unbounded edge is visited (meaning the problem has no solution). Since this strategy evaluates vertices in an intelligent order rather than checking them randomly, it will (on average) be more efficient than the previous brute-force suggestion.[^6] The quickest way to gain intuition about the simplex method is through an example; to this end, please forgive a short diversion.[^7]

[^6]: Although the worst case run-time (associated with the *exceedingly* unlikely event in which our intelligent ordering is entirely unhelpful and we end up evaluating every vertex anyway) remains exponential.
[^7]: For simplicity, we guarantee termination of the simplex algorithm by applying it to a non-degenerate LP; in the case of degenerate LPs, where more than two constraint bounds pass through the same feasible vertex, precautions must be taken against cycling [@Bland1977].

:::{prf:example} Implementing Dantzig's pivot algorithm
:label: pivot-algorithm-example


Suppose we want to *maximise* the objective function 

\begin{equation*}
f(x_1,x_2) = 3x_1 + 5x_2
\end{equation*}

subject to the inequality constraints

\begin{equation*} 
\begin{split}
    x_1 + x_2 &\leq 4\\
    x_1 + 3x_2 &\leq 6\\
    x_1,x_2 &\geq 0.
\end{split} 
\end{equation*}

How might we achieve this via Dantzig's simplex method?

**Step 1: Transform the objective function and inequality constraints into a system of equations by introducing an *artificial
 variable* $\mathbf{Z}$ (which represents the value of the objective function) and *slack variables* $\mathbf{s}$ (which represent the difference between the LHS and RHS of each inequality).** 

\begin{equation*}
    \begin{split}
        - 3x_1 - 5x_2 + Z &= 0 \\
        x_1 + x_2 + s_1 &= 4 \\
         x_1 + 3x_2 + s_2 &= 6    
     \end{split}
\end{equation*}

**Step 2: Write this system of equations in augmented matrix (or `simplex tableau') form, where each column is labelled according to the variable it contains coefficients for and each row is labelled by the basic variable it is initially associated with.**

Note that each row corresponds to one of the equations, and we put the one for the objective function at the bottom by convention.

```{figure} tableau-grid-1.png
:name: tableau-grid-1-figure
:width: 350px
:align: center
```

**Step 3: Check the basic feasible solution corresponding to this tableau by setting the non-basic variables (whose columns contain more than one non-zero entry) to zero and solving for the basic variables (whose columns contain only one non-zero component). If the result is optimal, the process terminates; if the value of the objective function could still be improved, continue to step 4.**

Setting both non-basic variables ($x_1$ and $x_2$) to zero, we can read off the following values for our basic variables: $s_1=4$, $s_2=6$, $Z=0$. This solution is not optimal, as indicated by the presence of negative values in the objective row which could generate a higher $Z$ if increased. (If a value is less than zero, it means that the variable has not reached its optimal value.)


**Step 4: Exchange a basic variable with a non-basic variable (i.e. perform a *'pivot'*) using the following protocol.**
- **First, choose a *'pivot column'* (ideally whichever column has the most negative number in the objective row); this determines the \textit{`entering variable'} that is going to become non-basic.**
- **Then, choose a *'pivot row'* (ideally whichever row has the smallest non-negative ratio between its RHS and pivot column coefficient); this decides the *'departing variable'* that is going to become basic.**
- **Finally, apply matrix row operations to make the *'pivot element'* (which sits at the intersection of the pivot column and pivot row) one and all other coefficients in the pivot column zero.**

Performing the pivot procedure on the initial tableau (i.e. with $x_2$ as an entering variable and $s_2$ as a departing variable) generates a second tableau as below.

```{figure} tableau-grid-2.png
:name: tableau-grid-2-figure
:width: 350px
:align: center
```

**Step 5: Repeat steps $\mathbf{3}$ and  $\mathbf{4}$ until the optimal solution is reached.**

Setting both non-basic variables ($x_1$ and $s_2$) to zero, we can read off the following values for each basic variable: $s_1=2$, $x_2=2$, $Z=10$. This solution is not optimal, as indicated by the presence of a negative value in the objective row which could generate a higher $Z$ if increased.

Performing the pivot procedure on the second tableau (i.e. with $x_1$ as an entering variable and $s_1$ as a departing variable) generates a third tableau as below.

```{figure} tableau-grid-3.png
:name: tableau-grid-3-figure
:width: 350px
:align: center
```

Setting both non-basic variables ($s_1$ and $s_2$) to zero, we can read off the following values for each basic variable: $x_1=3$, $x_2=1$, $Z=14$. This solution is optimal, as indicated by the absence of any negative values in the objective row.


:::


For most practical purposes, the methods we have covered so far are more than sufficient. However one other class of algorithms, known as interior point techniques, is commonly applied to linear programming problems. We will consider these briefly, as they generalise well to the case of semidefinite programming (as discussed in section [](#semidefinite-programming)).

#### Interior Point Techniques

Interior point techniques involve traversing a path through the feasible region until an optimal vertex is converged upon. The speed of convergence (along with the exact route taken) depends upon which method is used: for example, Khachiyan's ellipsoid algorithm [@Khachiyan1980] theoretically scales in polynomial time $\mathcal{O}(mn^6)$ but functionally suffers from significant performance issues, Karmarkar's projective algorithm [@Karmarkar1984] successfully terminates in polynomial time $\mathcal{O}(mn^{3.5})$, and more recent proposals [@Vaidya1989; @Vaidya1990; @Lee2015; @Cohen2019] offer further improvements.[^8]

[^8]: As in section [](#convex-polytopes), $m$ refers to the number of constraints and $n$ denotes the number of variables. An in-depth discussion of these algorithms is unnecessary as, in practice, we will use a modelling system `cvx` implemented in MATLAB which enables us to easily test the performance of all available open source solvers, namely: SeDuMi, SDPT3,
Gurobi and MOSEK.

### Duality

Now that we understand how to approach solving LPs, it is time to introduce an essential concept known as *duality*.[^9] Every LP configured according to 
[Equation 4.5](#linear-program-equation-2), henceforth referred to as a *primal* problem, has an alternative formulation known as its *dual*. The standard structure of a dual LP is

[^9]: Our explanation of duality closely follows section $1.3$ of @Skrzypczyk2023.

\begin{equation}
\label{dual-linear-program-equation-1}
\begin{aligned}
    \text{minimise} \hspace{3mm} &\mathbf{b} \cdot \mathbf{y} + \mathbf{c} \cdot \mathbf{z} \label{Eq:4.7a} \\
    \text{subject to} \hspace{3mm} &B^T \mathbf{y} + C^T \mathbf{z} = \mathbf{a} \label{Eq:4.7b} \\
    \text{and} \hspace{3mm} &C  \mathbf{z} \geq \mathbf{0} \label{Eq:4.7c}
\end{aligned}
\end{equation}
where the vectors $(\mathbf{y},\mathbf{z})$ are dual variables and the matrices $(B,C)$ are defined as before. Analogously to the primal case, we introduce the following notation: let $\beta$ represent the optimal value of the objective function, and denote by $(\mathbf{y^*},\mathbf{z^*})$ the decision variables which achieve this bound.

#### Properties of Dual LPs

Duality is an extremely useful tool for linear programming because of the following properties.


:::{prf:theorem} Weak Duality of LPs.
:label: weak-duality-theorem

The optimal value of a dual LP provides an upper bound for the optimal value of its associated primal, and the optimal value of a primal LP provides a lower bound for the optimal value of its associated dual (i.e. $\alpha \leq \beta$) [@Skrzypczyk2023].

:::


```{figure} weak-duality.png
:name: weak-duality-figure
:width:500
:align: center
Conceptual representation of weak duality.

```


:::{prf:proof}
:label: full-proof

\begin{equation*}
\begin{aligned}
\alpha &= \mathbf{a} \cdot \mathbf{x^*}  \\
    &= (B^T \mathbf{y^*} + C^T \mathbf{z^*}) \cdot \mathbf{x^*} \\
    &= B^T \mathbf{y^*} \cdot \mathbf{x^*} + C^T \mathbf{z^*} \cdot \mathbf{x^*} ~~~~~ \text{linearity of the dot product} \\
    &= \mathbf{y^*} \cdot B \mathbf{x^*} + \mathbf{z^*} \cdot C \mathbf{x^*} ~~~~~~~~~ \text{definition of the transpose} \\
    &\leq \mathbf{y^*} \cdot \mathbf{b} + \mathbf{z^*} \cdot \mathbf{c}   \\
    &= \mathbf{b} \cdot \mathbf{y^*} + \mathbf{c} \cdot \mathbf{z^*} ~~~~~~~~~~~~~~~~~~~ \text{commutativity of the dot product} \\
    &= \beta 
\end{aligned}
\end{equation*}

The first line follows from [Equation 5.6](#linear-program-equation-2); the second, fifth and final lines follow from [Equation 5.7](#dual-linear-program-equation-1).

:::



An immediate corollary is that an unbounded dual LP (i.e. one with $\beta = - \infty$) must be associated with an infeasible primal; similarly, if a primal LP is unbounded (i.e. $\alpha = + \infty$) then its dual is necessarily infeasible.\footnote{The converse implications do not hold; it is possible to construct primal-dual pairs which are both infeasible.} It is also evident that, by construction, any feasible primal variable $\mathbf{x}$ provides a lower bound on the optimal value $\alpha$ (i.e. $\mathbf{a} \cdot \mathbf{x} \leq \alpha$) and any feasible pair of dual variables $(\mathbf{y},\mathbf{z})$ provide an upper bound on the optimal value $\beta$ (i.e. $\mathbf{b}\cdot\mathbf{y} + \mathbf{c}\cdot\mathbf{z} \geq \beta$). Putting this information together with the weak duality theorem allows us to write

\begin{equation}
 \mathbf{a} \cdot \mathbf{x} \leq \alpha \leq \beta \leq \mathbf{b}\cdot\mathbf{y} + \mathbf{c}\cdot\mathbf{z}.   
\end{equation}

Observe that, whenever the primal and dual variables satisfy $\mathbf{a}\cdot\mathbf{x} = \mathbf{b}\cdot\mathbf{y}+\mathbf{c}\cdot\mathbf{z}$, the optimal values for both problems are guaranteed to coincide (i.e. $\alpha=\beta$). In such cases, dual LPs offer an alternative route for arriving at the optimal solution of their associated primals. Perhaps unexpectedly, this behaviour is not rare; it is generic to all LPs which satisfy basic feasibility and boundedness conditions.

:::{prf:theorem} Strong Duality of LPs.
:label: strong-duality-theorem

Assuming a primal LP is both feasible and bounded (i.e. if there exists a finite optimal solution $\alpha$), its associated dual LP has a matching optimal value $\beta$; likewise, assuming a dual LP is both feasible and bounded (i.e. if there exists a finite optimal solution $\beta$), its associated primal LP has a matching optimal solution $\alpha$.[^10]

[^10]: See @Gass2003 for a formal proof of strong duality.

:::


```{figure} strong-duality.png
:name: strong-duality-figure
:width: 500px
:align: center
Conceptual representation of strong duality.
```


Strong duality is harnessed effectively by most computational solvers, which repeatedly alternate between the primal and dual versions of a problem until their respective objective values converge to an acceptable numerical precision; these solvers declare a solution as optimal if the duality gap, the primal infeasibilities, and the dual infeasibilities are smaller than a given tolerance.

#### Construction of Dual LPs

Having convinced ourselves that duality is a helpful notion, we are (hopefully) motivated to learn how the dual associated with a given primal might be derived.[^11] It is assumed WLOG that we begin with an LP in the standard form given by [Equation 5.5](#linear-program-equation-2).

[^11]: Note that the method discussed here is only effective for linear problems (such as those we will encounter in Part 4). For non-linear problems, a more complicated protocol is necessary; see chapter 5 of [@Boyd2004] for details. 

As a first step, we assign to each primal constraint a corresponding Lagrange multiplier or 'dual variable'; in this instance, let $y_i$ be the dual variable linked to the second line of [Equation 5.5](#linear-program-equation-2) and let $z_j$ be the dual variable linked to the third line of [Equation 5.5](#linear-program-equation-2). It is then possible to define the following Lagrangian, 

\begin{equation}
\label{linear-program-lagrangian-equation}
    \mathcal{L} = \mathbf{a} \cdot \mathbf{x} + \sum\limits_{i=1}^{m}y_i(b_i - \mathbf{r}_i\cdot\mathbf{x}) + \sum\limits_{j=1}^{n}z_j(c_j - \mathbf{s}_j \cdot \mathbf{x}).
\end{equation}

Notice that the second line of [Equation 5.5](#linear-program-equation-2) fixes the second term of [Equation 5.9](#linear-program-lagrangian-equation) equal to zero. Observe also that, upon imposing an additional restriction $z_j \geq 0$, the third line of [Equation 5.5](#linear-program-equation-2) forces the third term of [Equation 5.9](#linear-program-lagrangian-equation) to be non-negative. From these simplifications alone, we have already generated the inequality $\mathcal{L}\geq \mathbf{a} \cdot \mathbf{x}$; a tight upper bound on the objective value can therefore be obtained by simply minimising this Lagrangian. One final step is required — we want our Lagrangian to be dependent on only one set of variables (i.e. primal or dual but not both). This can be achieved by factorising out the primal vector 
\begin{equation}
    \mathcal{L} = \Big(\mathbf{a} - \sum\limits_{i=1}^{m}y_i\mathbf{r}_i - \sum\limits_{j=1}^{n}z_j\mathbf{s}_j \Big) \cdot \mathbf{x} + \sum\limits_{i=1}^{m}y_ib_i  + \sum\limits_{j=1}^{n}z_jc_j,
\end{equation}
and setting its new coefficient to zero,
\begin{equation}
    \mathbf{a} - \sum\limits_{i=1}^{m}y_i\mathbf{r}_i - \sum\limits_{j=1}^{n}z_j\mathbf{s}_j = 0.
\end{equation}

Putting everything together, we arrive at the dual LP

\begin{equation} 
\label{dual-linear-program-equation-2}
\begin{aligned}
    \text{minimise} \hspace{3mm} &\sum\limits_{i=1}^{m}y_ib_i  + \sum\limits_{j=1}^{n}z_jc_j\\
    \text{subject to} \hspace{3mm} &\mathbf{a} - \sum\limits_{i=1}^{m}y_i\mathbf{r}_i - \sum\limits_{j=1}^{n}z_j\mathbf{s}_j = 0\\   
    \text{and} \hspace{3mm} &z_j \geq 0.
\end{aligned}
\end{equation}

Recalling how we previously defined the matrices $B=(r_1^T \hspace{3mm} ... \hspace{3mm} r_m^T)^T$ and $C=(s_1^T \hspace{3mm} ... \hspace{3mm} s_n^T)^T$, this is immediately recognisable as equivalent to [Equation 5.7](#dual-linear-program-equation-1). It should be obvious from this simple algorithm that the dual is itself an LP; indeed, the dual of a dual is the original primal.

(semidefinite-programming)=
## Semidefinite Programming

Semidefinite programming is a natural generalisation of linear programming; as such, many ideas from section [](#linear-programming) transfer in a trivial way.[^12] For example, both techniques entail optimising a *linear* objective function in accordance with *affine* constraints. One major difference is that semidefinite programs (SDPs) involve matrix equations which accept as arguments *Hermitian operators*: $X=X^\dagger$. Given that only real elements are permitted, these can be equivalently represented by *symmetric matrices*. Consequently, SDPs exhibit a standard form

 [^12]: We expect the reader to be familiar with content from section [](#linear-programming) so, to avoid unnecessary repetition, [](#semidefinite-programming) will move at a faster pace.

\begin{equation} 
\label{semidefinite-program-equation-1}
\begin{aligned}
    \text{maximise} \hspace{3mm} &F(X) \label{SDP1a}\\
    \text{subject to} \hspace{3mm} &G_i(X) = B_i, \hspace{3mm}  \forall \hspace{1mm} i = 1,...,m\label{SDP1b}\\
    \text{and} \hspace{3mm} &H_j(X) \preceq C_j, \hspace{3mm}  \forall \hspace{1mm} j = 1,...,n\label{SDP1c}
\end{aligned}
\end{equation}

where $F(X)$ is the objective function, $G_i(X)$ denotes a hermiticity-preserving map to a system of $m$ equality constraints with associated values $B_i$, and $H_j(X)$ represents a hermiticity-preserving map to a set of $n$ inequality constraints each bounded by $C_j$; this should be viewed as analogous to [Equation 4.4](#linear-program-equation-1). Note the deliberate change of font from $\leq$ (which bounds vector components) to $\preceq$ (which bounds matrix eigenvalues); for clarity, we interpret line $3$ of [Equation 4.13](#semidefinite-program-equation-1) as stating that the matrix $\{H_j(X)-C_j\}$ is positive semidefinite.

:::{prf:definition} Positive Semidefinite
:label: positive-semidefinite-definition

An symmetric matrix $M$ is positive semidefinite (PSD) if and only if it satisfies any of the following equivalent conditions.
- All eigenvalues are non-negative.
- All principle minors are non-negative.
- There exists a Cholesky decomposition [@Benoit1924] of the form $M=L^TL$, where $L$ is a lower triangular matrix with real non-negative diagonal elements.

:::

As with LPs, it is sometimes convenient to adopt alternative notation. One simple improvement is to encode the objective function $F(X)$ in a matrix $A$ such that $F(X) = A \cdot X= \textrm{tr}(A^{T}X)$. Since X is necessarily symmetric, we can assume WLOG that the matrix A is also symmetric; consequently, the transpose has no impact and $F(X)$ reduces to $\textrm{tr}(AX)$. Rewriting [Equation 5.13](#semidefinite-program-equation-1) in this way, we can express SDPs as

\begin{equation} 
\label{semidefinite-program-equation-2}
\begin{aligned}
    \text{maximise} \hspace{3mm} &\textrm{tr}(AX) \label{SDP2a}\\
    \text{subject to} \hspace{3mm} &G_i(X) = B_i, \hspace{3mm}  \forall \hspace{1mm} i = 1,...,m\label{SDP2b}\\
    \text{and} \hspace{3mm} &H_j(X) \preceq C_j, \hspace{3mm}  \forall \hspace{1mm} j = 1,...,n.\label{SDP2c}
\end{aligned}
\end{equation}

Further specification is obviously possible, however the abstract form of [Equation 5.14](#semidefinite-program-equation-2) is most illuminating for present purposes. Before continuing, let us reiterate some terminology introduced in section [](#linear-programming): $\alpha$ represents the optimal value of the objective function and ${X^*}$ denotes the choice of decision variable which achieves this bound.\footnote{As in the case of LPs, ${X^*}$ is generally non-unique; there could exist infinitely many variables which simultaneously saturate the objective.}


### Solution Methods

Geometric and simplex-type solution methods are difficult to extend from the linear programming case to the semidefinite programming case. The reason behind this obstruction relates to [](#vertex-solutions-theorem) which, once translated to match the terminology of general convex optimisation problems, reads: If a convex optimisation problem is solvable, at least one optimal solution must be located at an extreme point of its feasible region. Unfortunately, whilst the feasible region for an LP is bounded by a set of (straight) hyperplanes which define a finite number of vertices, the feasible region for an SDP typically has a curved boundary which admits an infinite number of extreme points. As a result, exhaustive searches that involve systematically testing each extreme point until an ideal candidate is found are destined to fail when applied to SDPs. Luckily, interior point algorithms *have* been successfully generalised for solving SDPs; it is these approaches we will make use of in part 4.

### Duality

Notions of duality carry across fairly naturally from linear programming to semidefinite programming. There is, however, one key difference to be aware of: although weak duality is still guaranteed, feasibility and boundedness are no longer sufficient conditions for strong duality to hold (i.e. even properly constructed SDPs may have primal and dual solutions which do not coincide). Fortunately, in order to salvage strong duality, we need only strengthen our requirement slightly from feasibility (which implies a non-empty feasible region) to *strict* feasibility (which implies a feasible region with a non-empty *interior*) [@Slater1959]; informally, this means a feasible solution should still exist even if we replace all non-strict inequalities with strict inequalities.

#### Construction of Dual SDPs

The process of constructing dual SDPs is essentially identical to the linear programming case. Nevertheless, for the sake of completeness, we will reproduce the necessary steps within our current context.[^13]

[^13]: Our derivation closely follows section $2.2$ of @Skrzypczyk2023.

We first assign to each primal constraint a corresponding Lagrange multiplier or 'dual variable'; in this instance, let a Hermitian operator $Y_i$ be the dual variable linked to the second line of [Equation 5.14](#semidefinite-program-equation-2) and let a Hermitian operator $Z_j$ be the dual variable linked to the third line of [Equation 4.14](#semidefinite-program-equation-2). It is then possible to define the following Lagrangian, 

\begin{equation}
\label{semidefinite-program-lagrangian-equation-1}
    \mathcal{L} = \textrm{tr}(AX) + \sum\limits_{i=1}^{m}Y_i[B_i - G_i(X)] + \sum\limits_{j=1}^{n}Z_j[C_j - H_j(X)].
\end{equation}

Notice that the second line of [Equation 5.14](#semidefinite-program-equation-2) fixes the second term of [Equation 5.15](#semidefinite-program-lagrangian-equation-1) equal to zero. Observe also that, upon imposing an additional restriction $Z_j \succeq 0$, the third line of [Equation 5.14](#semidefinite-program-equation-2) forces the third term of [Equation 5.15](#semidefinite-program-lagrangian-equation-1) to be non-negative. We have now generated the inequality $\mathcal{L}\geq \textrm{tr}(AX)$; a tight upper bound on the objective value can therefore be obtained by simply minimising this Lagrangian. Before performing this optimisation, however, we must render our Lagrangian independent of the original primal variable; this can be achieved by using the definition of an adjoint map [^14] to rewrite [Equation 5.15](#semidefinite-program-lagrangian-equation-1) as

[^14]: If $\Gamma^\dagger(\cdot)$ is the adjoint of a map $\Gamma(\cdot)$ then $\textrm{tr}[\Gamma(A)B]=\textrm{tr}[A\Gamma(B)] \hspace{2mm} \forall \hspace{1mm} A,B$.

\begin{equation}
\label{semidefinite-program-lagrangian-equation-2}
    \mathcal{L} = \textrm{tr}\big([A-\sum\limits_{i=1}^{m}G_i^\dagger(Y_i)-\sum\limits_{j=1}^{n}H_j^\dagger(Z_j)]X\big) + \sum\limits_{i=1}^{m} \textrm{tr}(Y_iB_i) + \sum\limits_{j=1}^{n} \textrm{tr}(Z_jC_j)
\end{equation}

and setting all $X$ coefficients equal to zero,

\begin{equation}
    A-\sum\limits_{i=1}^{m}G_i^\dagger(Y_i)-\sum\limits_{j=1}^{n}H_j^\dagger(Z_j) = 0.
\end{equation}

Combining the above information allows us to write dual SDPs as

\begin{equation} 
\label{semidefinite-program-equation-3}
\begin{aligned}
    \text{maximise} \hspace{3mm} &\sum\limits_{i=1}^{m} \textrm{tr}(Y_iB_i) + \sum\limits_{j=1}^{n} \textrm{tr}(Z_jC_j)\label{SDPduala}\\
    \text{subject to} \hspace{3mm} &A-\sum\limits_{i=1}^{m}G_i^\dagger(Y_i)-\sum\limits_{j=1}^{n}H_j^\dagger(Z_j) = 0 \label{SDPdualb}\\
    \text{and} \hspace{3mm} &Z_j \succeq 0.\label{SDPdualc}
\end{aligned}
\end{equation}

As previously, it should be clear that the dual is itself an SDP and that taking the dual of a dual recovers the original primal.

### Application to SOS

The techniques covered thus far in section [](#semidefinite-programming) have spawned numerous applications. One in particular will be essential to our work in Part 4 — namely, sums of squares (SOS). 

A polynomial admits an SOS decomposition if it can be written as an SOS of other polynomials. Because each squared term is necessarily non-negative, the existence of an SOS decomposition constitutes a certificate of non-negativity for the original polynomial. However the converse implication holds only for univariate polynomials, quadratic polynomials and bivariate quartics [@Hilbert1888]; in general, it is possible to find non-negative polynomials which cannot be expressed as an SOS. One well-known example is Motzkin's bivariate sextic [@Motzkin1967],

\begin{equation}
    M(x,y) = x_1^4x_2^2 + x_1^2x_2^4 -3x_1^2x_1^2+1.
\end{equation}

Fortunately, despite being stricter, the conditions for an SOS decomposition are significantly more computationally tractable than the criterion for non-negativity; in fact, the former correspond exactly to an SDP [@Parrilo2000]. We will see this first in the notationally simple case of univariate polynomials, before generalising to the more cumbersome case of multivariate polynomials.[^15]

[^15]: The following exposition is inspired by [@Parrilo2012], to which the interested reader is referred for further details.

#### Univariate Polynomials

Consider a univariate polynomial of degree $2d$,

\begin{equation}
\label{univariate-polynomial-equation}
    p(x) = p_{2d}x^{2d} + p_{2d-1}x^{2d-1} + ... + p_1x + p_0.
\end{equation}

Assuming [Equation 5.20](#univariate-polynomial-equation) admits an SOS decomposition, there must exist other univariate polynomials $q_1(x),...,q_m(x)$ of highest degree $d$ such that

\begin{equation}
\label{univariate-squares-equation}
    p(x)=\sum_{k=1}^{m}q_k^2(x).
\end{equation}

We can combine these into a matrix of the form

\begin{equation}
    \mathbf{q}
=\begin{pmatrix}
q_1(x)\\
q_2(x)\\
.\\
.\\
.\\
q_m(x)
\end{pmatrix}
=
V
\begin{pmatrix}
1\\
x\\
.\\
.\\
.\\
x^d
\end{pmatrix}
=
V
\mathbf{x}
\end{equation}

and thereby reformulate [Equation 5.21](#univariate-squares-equation) as

\begin{equation}
    p(x) = \sum_{k=1}^{m}q_k^2(x) = \mathbf{q}\cdot\mathbf{q} = \Vert{V\mathbf{x}}\Vert^2 = (V\mathbf{x})^{T}V\mathbf{x} = \mathbf{x}^{T}V^{T}V\mathbf{x} = \mathbf{x}^{T}Q\mathbf{x}
\end{equation}

where $Q = V^{T}V$. Recalling the third bullet point of [](#positive-semidefinite-definition), it follows that $p(x)$ admits an SOS decomposition if and only if there exists a PSD matrix $Q$ satisfying [Equation 5.18](#semidefinite-program-equation-3). Determining whether such a matrix exists is an instance of a *feasibility* problem in semidefinite programming; actually finding such a matrix amounts to an *optimisation* problem in semidefinite programming. The aforementioned technique is most clearly communicated by way of example.


:::{prf:example} SOS for a univariate polynomial
:label: univariate-SOS-example

Suppose we want to find a sum of squares for the univariate polynomial $p(x)=x^4+4x^3+6x^2+4x+5$. It is of degree $2d=4$ (i.e. $d=2$), so the vector $\mathbf{x}$ contains all monomials of degree less than or equal to $2$: $\mathbf{x}=(1,x,x^2)^T$. An SOS decomposition can be found provided there exists some $Q\geq0$ such that

\begin{equation*}
\begin{split}
 p(x)&=\mathbf{x}^TQ\mathbf{x}\\
 ~~~ \\
&=
\begin{pmatrix}
1\\
x\\
x^2\\
\end{pmatrix}^T
\begin{pmatrix}
 Q(1,1) \hspace{3mm} Q(1,2) \hspace{3mm} Q(1,3)\\
 Q(1,2) \hspace{3mm} Q(2,2) \hspace{3mm} Q(2,3)\\
 Q(1,3) \hspace{3mm} Q(2,3) \hspace{3mm} Q(3,3)
 \end{pmatrix}
 \begin{pmatrix}1\\x\\x^2\end{pmatrix}\\
 ~~~ \\
 &= Q(3,3)x^4 + 2Q(2,3)x^3 + \big(2Q(1,3)+Q(2,2)\big)x^2 \\
 &~~~~~+ 2Q(1,2)x + Q(1,1).
\end{split}
\end{equation*}

Comparing coefficients, we obtain the following set of linear equalities:

\begin{equation*}
\begin{aligned}
 x^4 &: Q(3,3) = 1\\
 x^3 &: 2Q(2,3) = 4\\
 x^2 &: 2Q(1,3) + Q(2,2) = 6\\ x &: 2Q(1,2) = 4\\
 1 &: Q(1,1) = 5
\end{aligned}
\end{equation*}

Our first goal is to find a PSD $Q$ which satisfies these constraints (i.e. solve an SDP).  In this case, multiple non-unique solutions can be generated; an obvious choice is to take

\begin{equation*}
Q = \begin{pmatrix}
 5 \hspace{3mm} 2 \hspace{3mm} 0 \\
 2 \hspace{3mm} 6 \hspace{3mm} 2 \\
 0 \hspace{3mm} 2 \hspace{3mm} 1
 \end{pmatrix}
 \end{equation*}

  this contains the fewest non-zero entries. Our second task is to factorise the above Gram-matrix  in the form $Q = V^{T}V$. Performing a close inspection reveals

\begin{equation*}
V = \begin{pmatrix}
 0 \hspace{3mm} 2 \hspace{3mm} 1 \\
 \sqrt2 \hspace{3mm} \sqrt2 \hspace{3mm} 0 \\
 \sqrt3 \hspace{3mm} 0 \hspace{3mm} 0
 \end{pmatrix}
 \end{equation*}

 which yields an SOS decomposition

\begin{equation*}
    p(x) = \Vert{V\mathbf{x}}\Vert^2 = (2x + x^2)^2 + (\sqrt2 + \sqrt2{x})^2 + 3.
\end{equation*} 

 One can easily verify this holds by expanding the right hand side.

:::

#### Multivariate Polynomials

We are now in a position to apply our knowledge of the univariate case to the more general multivariate case. Consider a polynomial of degree $2d$ in $n$ variables,

\begin{equation}
p(x_1,...,x_n) = \sum_{\substack{\alpha_1,...,\alpha_n\\\alpha_1+...+\alpha_n\leq2d}} p_{\alpha_1,...,\alpha_n}(x_1^{\alpha_1},...,x_n^{\alpha_n}).
\end{equation}

Defining $\mathbf{x} = (1,x_1, ..., x_n, x_1^2,x_1x_2 ..., x_n^d)^T$ as the $\begin{pmatrix}{n+d}\\{d} \end{pmatrix}$ dimensional vector of monomials with highest degree $d$, and proceeding analogously to the univariate case, one can obtain a system of $\begin{pmatrix}{n+2d}\\2d\end{pmatrix}$ linear equations which must be satisfiable by some PSD matrix in order for the polynomial to admit an SOS decomposition. Specifically,

\begin{equation}
    p_\alpha = \sum_{\beta + \gamma = \alpha} Q_{\beta\gamma} \hspace{2mm},\hspace{2mm} Q\geq0
\end{equation}

where $\alpha\in\set{(\alpha_1,...,\alpha_n) : (\alpha_1+...+\alpha_n\leq2d) : (\alpha_i\geq{0}\hspace{2mm}\forall i\in\set{1,...,n}}$, and $\beta,\gamma$ are similarly defined tuples. As before, deciding membership of the set of SOS polynomials constitutes an SDP. We now provide an explicit example to help clarify what this fairly dense notation means.

:::{prf:example} SOS for a multivariate polynomial
:label: multivariate-SOS-example

Suppose we want to find a sum of squares for the bivariate polynomial $p(x_1,x_2)=2x_1^4+5x_2^4-x_1^2x_2^2+2x_1^3x_2+2x_1+2$. It is of degree $2d=4$ (i.e. $d=2$), so the vector $\mathbf{x}$ contains all monomials of degree less than or equal to $2$: $\mathbf{x}=(1,x_1,x_2,x_1^2,x_2^2)^T$. An SOS decomposition can be found provided there exists some $Q\geq0$ such that

\begin{equation*}
\begin{split}
&p(x)=\mathbf{x}^TQ\mathbf{x}\\
~~~ \\
&=
\begin{pmatrix}
1\\
x_1\\
x_2\\
x_1^2\\
x_1x_2\\
x_2^2
\end{pmatrix}^T
\begin{pmatrix}
 Q(1,1) \hspace{1.5mm} Q(1,2) \hspace{1.5mm} Q(1,3) \hspace{1.5mm} Q(1,4) \hspace{1.5mm} Q(1,5) \hspace{1.5mm} Q(1,6)\\
 Q(1,2) \hspace{1.5mm} Q(2,2) \hspace{1.5mm} Q(2,3) \hspace{1.5mm} Q(2,4) \hspace{1.5mm} Q(2,5) \hspace{1.5mm} Q(2,6)\\
 Q(1,3) \hspace{1.5mm} Q(2,3) \hspace{1.5mm} Q(3,3) \hspace{1.5mm} Q(3,4) \hspace{1.5mm} Q(3,5) \hspace{1.5mm} Q(3,6)\\
 Q(1,4) \hspace{1.5mm} Q(2,4) \hspace{1.5mm} Q(3,4) \hspace{1.5mm} Q(4,4) \hspace{1.5mm} Q(4,5) \hspace{1.5mm} Q(4,6)\\
 Q(1,5) \hspace{1.5mm} Q(2,5) \hspace{1.5mm} Q(3,5) \hspace{1.5mm} Q(4,5) \hspace{1.5mm} Q(5,5) \hspace{1.5mm} Q(5,6)\\
 Q(1,6) \hspace{1.5mm} Q(2,6) \hspace{1.5mm} Q(3,6) \hspace{1.5mm} Q(4,6) \hspace{1.5mm} Q(5,6) \hspace{1.5mm} Q(6,6)
 \end{pmatrix} \hspace{-0.5mm}
 \begin{pmatrix}1\\x_1\\x_2\\x_1^2\\x_1x_2\\x_2^2\end{pmatrix}\\
~~~ \\
 &= Q(4,4)x_1^4 + Q(6,6)x_2^4+ \big( 2Q(4,6) +Q(5,5) \big) x_1^2x_2^2 + 2Q(4,5)x_1^3x_2  \\
 &+ 2Q(5,6)x_1x_2^3 +2Q(2,4)x_1^3+2Q(3,6)x_2^3+ \big( 2Q(2,5)+2Q(3,4) \big)x_1^2x_2 \\
 &+ \big( 2Q(2,6)+2Q(3,5) \big)x_1x_2^2 +\big( 2Q(1,4) + Q(2,2) \big) x_1^2 \\
 &+ \big(2Q(1,5) + 2Q(2,3 \big) x_1x_2 +\big( 2Q(1,6) + Q(3,3) \big)x_2^2   \\
&+ 2Q(1,3)x_2 + 2Q(1,2) + Q(1,1).

\end{split}
\end{equation*}


Comparing coefficients, we obtain the following set of linear equalities:
 $$\begin{align*}
  x_1^4 &: Q(4,4) = 2\\
 x_2^4 &: Q(6,6) = 5\\
    x_1^2x_2^2 &: 2Q(4,6) + Q(5,5) = -1
     \end{align*}$$

$$ \begin{align*}
  x_1^3x_2 &: 2Q(4,5) = 2\\
 x_1 &: 2Q(1,2) = 2\\
 1 &: Q(1,1) = 2.
 \end{align*}$$
The remaining terms of the expansion are not present in our polynomial at all, so we set their coefficients to zero. Our first goal is to find a PSD $Q$ which satisfies these constraints (i.e. solve an SDP).  One such solution is given by

  $$Q = \begin{pmatrix}
 6 & 3 & 0 & -2 & 0 & -2 \\
 3 & 4 & 0 & 0 & 0 & 0 \\
 0 & 0 & 4 & 0 & 0 & 0 \\
 -2 & 0 & 0 & 6 & 3 & -4 \\
 0 & 0 & 0 & 3 & 5 & 0 \\
 -2 & 0 & 0 & -4 & 0 & 15 \\
 \end{pmatrix}.$$
Our second task is to factorise the above Gram-matrix  in the form $Q = V^{T}V$. Calculating the Cholesky reveals
 $$V = \begin{pmatrix}
 \sqrt{6} \hspace{3mm}& \sqrt{\frac{3}{2}} \hspace{3mm} & 0 & -\sqrt{\frac{2}{3}} & 0 & -\sqrt{\frac{2}{3}}\\
 0 & \sqrt{\frac{5}{2}} & 0 & 0 & 0 & \sqrt{\frac{2}{5}} \\
 0 & 0 & 2 & 0 & 0 & 0 \\
 0 & 0 & 0 & 2.2211 & 1.3507 & 2.2811 \\
 0 & 0 & 0 & 0 & 1.7820 & 1.7290 \\
 0 & 0 & 0 & 0 & 0 & 2.3959 
 \end{pmatrix}$$

 which yields an SOS decomposition

 \begin{equation*}
\begin{split}
p(x_1,x_2) &= \Vert{V\mathbf{x}}\Vert^2 \\
&=\Big(\sqrt{6} + \sqrt{\frac{3}{2}}x_1  -\sqrt{\frac{2}{3}}x_1^2 -\sqrt{\frac{2}{3}} x_2^2\Big)^2+\Big(\sqrt{\frac{5}{2}}x_1+\sqrt{\frac{2}{5}}x_2^2\Big)^2 \\
&+4x_2^2+\big(2.2211x_1^2 + 1.3507x_1x_2 + 2.2811x_2^2\big)^2 \\
&+\big(1.7820x_1x_2 + 1.7920x_2^2\big)^2+ 5.7403. 
\end{split}
\end{equation*}

As indicated by the presence of multiple decimal coefficients, finding closed form solutions is a non-trivial exercise.

:::


In Part 3, it will become clear how applying semidefinite programming to sums of squares relates to our study of Bell-type inequalities.