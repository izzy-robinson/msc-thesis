---
subject: Mathematical Preliminaries | Chapter 4
subtitle:
short_title: Geometric Concepts
numbering:
  enumerator: 4.%s
---

# Geometric Concepts

> $\mathbf{epi}\hspace{0.5mm}f = \set{(x,t)|x\in\mathbf{dom}\hspace{0.5mm}f,f(x)\leq{t}}$
> - Stephen Boyd & Lieven Vandenberghe


The following discussion closely follows chapter 2 of @Boyd2004. 

(affine-geometry)=
## Affine Geometry

:::{prf:definition} Affine Combinations
:label: affine-combinations-definition
An affine combination of multiple points $x_1,...,x_k$ is given by $\sum_{i=1}^{k} \mu_i x_i$, where $\smash{\sum_{i=1}^{k} \mu_i = 1}$. This can be interpreted as a weighted sum, with each coefficient $\mu_i$, revealing what contribution its corresponding point $x_i$ makes to the mixture. 
:::


```{figure} affine-combinations.png
:name: affine-combinations-figure
:width: 600px
:align: center
Affine combinations of two points, $x_i$ and $x_j$, as parameterised by $\mu$ in [Equation 4.1](#affine-sets-equation).
```

:::{prf:definition} Affine Sets
:label: affine-sets-definition
A set $S$ is affine if, for any two elements $x_i$ and $x_j$, every affine combination is also contained within $S$. This condition is satisfied by all points of the form 
```{math}
:label: affine-sets-equation
 \set{\mu x_i + (1 - \mu) x_j | x_i \neq x_j \in S, \mu \in \mathbb{R}},
```
which lie on the infinite line passing through both $x_i$ and $x_j$. 
:::


:::{prf:definition} Affine Hulls
:label: affine-hulls-definition
The affine hull of a set $S$, denoted $\mathbf{aff}(S)$, is the set of all affine combinations for every point in $S$. Mathematically, this can be expressed as 
```{math}
:label: affine-hulls-equation
\mathbf{aff}(S) = \set{\sum_{i=1}^{k} \mu_i x_i | x_i \in S, \mu_i \in \mathbb{R}, \sum_{i=1}^{k} \mu_i = 1},
``````
which describes the smallest possible affine set containing $S$ as a subset.
:::


```{figure} affine-hulls.png
:name: affine-hulls-figure
:align: center
Examples of affine hulls. *Left:* The affine hull of two points in $\mathbb{R}^n$ is the infinite line passing through them. *Middle:* The affine hull of three non-collinear points in $\mathbb{R}^2$ is the entire space $\mathbb{R}^2$. *Right:* The affine hull of three non-collinear points in $\mathbb{R}^3$ is the infinite two-dimensional plane passing through them.
```


:::{prf:definition} Hyperplanes
:label: hyperplanes-definition
A hyperplane in $\mathbb{R}^n$ is an affine set of the form[^1]  
```{math}
:label: hyperplanes-equation
\set{\mathbf{x} | \mathbf{a} \cdot \mathbf{x} = b, \hspace{1mm} \mathbf{a} \neq \mathbf{0}, \hspace{1mm} \mathbf{a} \in \mathbb{R}^n, \hspace{1mm} b \in \mathbb{R}}.
```    
The vector $\mathbf{a}$ is normal to the plane; as such it defines a direction.[^2] A hyperplane's dimension is always one less than that of the ambient space in which it lives (i.e. $n-1$).
[^1]: Other sources may use the transpose notation 
$\mathbf{a}^T \mathbf{x}$ as opposed to the dot product notation $\mathbf{a} \cdot \mathbf{x}$. Adhering to the common convention of regarding $\mathbf{a},\mathbf{x}\in\mathbb{R}^n$ as $n$-dimensional column vectors (i.e. $n \times 1$ matrices), the two equations are entirely equivalent. We will therefore use them interchangeably as best suits the context (e.g. dot product when it is helpful to preserve geometric meaning and transpose when writing computer code).
[^2]: This fact will be useful when we come to discuss linear programming in chapter 5.
:::


```{figure} hyperplanes.png
:name: hyperplanes-figure
:align: center
Three hyperplanes in $\mathbb{R}^2$, each with the same normal vector $\mathbf{a}$ but for different values of $b$. When $b = 0$, the hyperplane passes through the
origin. When $b < 0$, the hyperplane is offset a distance $b$ from the origin in the opposite direction to $\mathbb{a}$. When $b > 0$, the hyperplane is offset a distance $b$ from the origin in the same direction as $\mathbf{a}$.
```

(convex-geometry)=
## Convex Geometry


:::{prf:definition} Convex Combinations
:label: convex-combinations-definition
A convex combination of multiple points $x_1,...,x_k$ is given by $\sum_{i=1}^{k} \mu_i x_i$, where $\mu_i \in [0,1]$ and $\sum_{i=1}^{k} \mu_i = 1$. This can be thought of as a weighted average, with each coefficient $\mu_i$ revealing what fraction of its corresponding point $x_i$ is found in the mixture.
:::

```{figure} convex-combinations.png
:name: convex-combinations-figure
:width: 400px
:align: center
Convex combinations of two points, $x_i$ and $x_j$, as parameterised by $\mu$ in [Equation 4.4](#convex-sets-equation)
```


:::{prf:definition} Convex Sets
:label: convex-sets-definition
A set S is convex if, for any two elements $x_i$ and $x_j$, every convex combination is also contained within $S$. This condition is satisfied by all points of the form 
```{math}
:label: convex-sets-equation
\set{\mu x_i + (1 - \mu) x_j | x_i,x_j \in S, \mu \in [0,1]},
```
which lie on the finite line segment between $x_i$ and $x_j$.
:::



```{figure} convex-sets.png
:name: convex-sets-figure
:width: 600px
:align: center
Distinguishing between convex and non-convex sets in $\mathbb{R}^2.$ *Left:* This set is convex. *Right:* This set is not convex as the finite line segment between the two points shown as dots lies partially outside the set.
```


:::{prf:definition} Convex Hulls
:label: convex-hulls-definition
The convex hull of a set $S$, denoted $\mathbf{conv}(S)$, is the set of all convex combinations for every point in $S$. Mathematically, this can be expressed as 
```{math}
:label: convex-hulls-equation     
\mathbf{conv}(S) = \set{\sum_{i=1}^{k} \mu_i x_i | x_i \in S,\mu_i \in [0,1], \sum_{i=1}^{k} \mu_i = 1},
```
which describes the smallest possible convex set containing $S$ as a subset.
:::


```{figure} convex-hulls.png
:name: convex-hulls-figure
:align: center
Examples of convex hulls. *Left:* The convex hull of two points in $\mathbb{R}^n$ is the finite line segment between them. *Middle:* The convex hull of three non-collinear points in $\mathbb{R}^2$ is the triangle with each point as a vertex. *Right:* The convex hull of three non-collinear points in $\mathbb{R}^3$ is the two-dimensional triangular plane with each point as a vertex.
```

```{figure} convex-hull.png
:name: convex-hull-figure
:width: 300px
:align: center
The convex hull of a non-convex set from [](#convex-sets-figure) is the combined shaded region (both dark and pale).
```

:::{prf:definition} Halfspaces
:label: halfspaces-definition
A hyperplane in $\mathbb{R}^n$ splits its ambient space into two convex sets called halfspaces. The *'lower'* halfspace takes a form $\set{\mathbf{x} | \mathbf{a} \cdot \mathbf{x} \leq b, \hspace{1mm} \mathbf{a} \neq 0, \hspace{1mm} \mathbf{a} \in \mathbb{R}^n, \hspace{1mm} b \in \mathbb{R}}$ and sits on the opposite side to the direction in which $\mathbf{a}$ points; the *'upper'* halfspace takes a form $\set{\mathbf{x} | \mathbf{a} \cdot \mathbf{x} \geq b, \hspace{1mm} \mathbf{a} \neq 0, \hspace{1mm} \mathbf{a} \in \mathbb{R}^n, \hspace{1mm} b \in \mathbb{R}}$ and sits on the same side as the direction in which $\mathbf{a}$ points. If the inequality is strict, the halfspace is said to be *'open'* as it excludes the hyperplane which defines it; if the inequality is not strict, the halfspace is said to be *'closed'* as it includes the associated hyperplane.
:::

```{figure} halfspaces.png
:name: halfspaces-figure
:align: center
A hyperplane (depicted by the central line) divides $\mathbb{R}^2$ into a lower halfspace (dark) and an upper halfspace (pale).
```

(convex-polytopes)=
## Convex Polytopes

Our main motivation for understanding the geometric notions introduced in [](#affine-geometry) and [](#convex-geometry) stems from their relevance to the study of convex polytopes.[^3] 

[^3]: Only *convex* polytopes are important for this thesis so, going forwards, we may sometimes leave their convexity implicit and simply call them polytopes. 

Consider the following two ways in which a polytope might naturally be defined.

1. **Vertex-representation** (i.e. $\mathbf{\mathcal{V}}$-representation): A $\mathcal{V}$-polytope is the convex hull of a finite set of vertices.
2. **Halfspace-representation** (i.e. $\mathbf{\mathcal{H}}$-representation): An $\mathcal{H}$-polytope is the solution set to a finite system of linear inequalities (i.e. a bounded intersection of closed halfspaces).

According to Weyl-Minkowski's theorem [@Weyl1934; @Minkowski1897], these two descriptions are interchangeable and it is possible to convert between them.[^4] Transforming from the $\mathcal{H}$-representation to the $\mathcal{V}$-representation is known as **vertex enumeration**; conversely, transforming from the $\mathcal{V}$-representation to the $\mathcal{H}$-representation is known as **facet enumeration**. Both directions of this problem are fundamentally equivalent, so we are free to restrict our discussion to only one of the two; in this instance, we will focus on vertex enumeration. A particular point of interest is the computational complexity of this process. As a worst-case scenario, the number of vertices (and hence the time taken to enumerate them) scales exponentially according to $\mathcal{O}(m^n)$, where $m$ is the number of constraints and $n$ is number of variables (i.e. the dimension of the polytope) [@Klee1972].[^5] However, in practice, many relevant problems terminate in polynomial time using either the double description method [@Motzkin1953] (as implemented in the package `cdd`) or the reverse search algorithm [@Avis1992] (as implemented in the package `lrs`). 

[^4]: You may be wondering why translating between equivalent descriptions is even worthwhile; the reason is that each has its own strengths and weaknesses. With the $\mathcal{V}$-representation, it is straightforward to sample random points inside the polytope but challenging to decide whether a particular point lies within the polytope; with the $\mathcal{H}$-representation, it is easy to check whether a particular point lies within the polytope but difficult to sample random points inside the polytope.

[^5]: This bound reduces if any constraints are redundant or linearly dependant.



