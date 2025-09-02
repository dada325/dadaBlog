---
title: "Higher Genus RiemannRoch and the Geometry of Curves"
date: 2023-04-19T07:20:51+08:00
# weight: 1
# aliases: ["/first"]
tags: ["Math","Algebraic Geometry","Moduli Spaces","Curves","Riemann-Roch"]
author: dada
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Higher genus riemann roch and the geometry of curves"
canonicalURL: "https://dada325.github.io/dadaBlog/Higher-Genus-RiemannRoch-and-the-Geometry-of-Curves"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
mathjax: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Higher Genus Riemann-Roch and the Geometry of Curves

Riemann-Roch theorem is elegant and its proof is a cornerstone of any first course in algebraic geometry or complex analysis (for Riemann surfaces), its implications, particularly for curves of genus $g \ge 2$, continue to drive research and provide essential tools for understanding their intricate geometry. This post aims to delve into the Riemann-Roch theorem beyond the familiar low-genus cases, exploring its quantitative power and its role in unlocking deeper properties of algebraic curves.

Let $C$ be a smooth, projective, irreducible algebraic curve of genus $g$ defined over an algebraically closed field $k$ (for simplicity, one can think of $k=\mathbb{C}$, in which case $C$ is a compact Riemann surface). The genus $g$, topologically the number of "handles" of the corresponding Riemann surface, is a fundamental invariant. Algebraic geometers often define it via sheaf cohomology as $g = h^1(C, \mathcal{O}_C)$, the dimension of the first cohomology group of the structure sheaf.

**The Statement of the Riemann-Roch Theorem**

At its heart, the Riemann-Roch theorem relates the dimension of the space of global sections of a line bundle (or, equivalently, the space of meromorphic functions associated with a divisor) to its degree and the genus of the curve.

Let $D$ be a divisor on $C$. Recall that a divisor is a formal finite sum of points $D = \sum n_P P$ with $n_P \in \mathbb{Z}$. The degree of $D$ is $\deg(D) = \sum n_P$. Associated to $D$ is the sheaf $\mathcal{O}_C(D)$, whose global sections $H^0(C, \mathcal{O}_C(D))$ can be identified with the vector space
$$ L(D) = \{ f \in k(C)^\* \mid \text{div}(f) + D \ge 0 \} \cup \{0\}, $$
where $k(C)$ is the function field of $C$, and $\text{div}(f)$ is the principal divisor associated to $f$. The condition $\text{div}(f) + D \ge 0$ means that the function $f$ has poles only at points $P$ where $n_P > 0$, with order at most $n_P$, and must have zeros at points $P$ where $n_P < 0$, with order at least $|n_P|$. We denote the dimension of this $k$-vector space by $h^0(C, \mathcal{O}_C(D))$ or $\ell(D)$.

The canonical divisor $K_C$ is the divisor associated with a non-zero rational differential form $\omega$ on $C$. While $K_C$ depends on the choice of $\omega$, its linear equivalence class, the _canonical class_, is well-defined. The sheaf $\mathcal{O}_C(K_C)$ is the canonical sheaf $\omega_C$.

The Riemann-Roch Theorem states:
$$ h^0(C, \mathcal{O}\_C(D)) - h^0(C, \mathcal{O}\_C(K_C - D)) = \deg(D) - g + 1 $$

Using sheaf cohomology and Serre Duality, this statement takes a more symmetric form. Recall that Serre Duality on a curve $C$ states that for any coherent sheaf $\mathcal{F}$ (in particular, line bundles $\mathcal{L} = \mathcal{O}_C(D)$), there is a natural isomorphism $H^1(C, \mathcal{L}) \cong H^0(C, \omega_C \otimes \mathcal{L}^{-1})^\vee$. Since $\omega_C = \mathcal{O}_C(K_C)$ and $\mathcal{L}^{-1} = \mathcal{O}_C(-D)$, we have $\omega_C \otimes \mathcal{L}^{-1} \cong \mathcal{O}_C(K_C - D)$. Thus, $h^1(C, \mathcal{L}) = h^0(C, \mathcal{O}_C(K_C - D))$. Denoting $h^i(C, \mathcal{L}) = \dim_k H^i(C, \mathcal{L})$, the Riemann-Roch theorem becomes:
$$ h^0(C, \mathcal{L}) - h^1(C, \mathcal{L}) = \deg(\mathcal{L}) - g + 1 $$
where $\mathcal{L} = \mathcal{O}_C(D)$ and $\deg(\mathcal{L}) = \deg(D)$.

**Interpreting the Terms in Higher Genus**

- **$h^0(C, \mathcal{O}_C(D))$**: This is the dimension of the space of functions whose poles are "controlled" by $D$. Geometrically, if $D$ is effective (i.e., $n_P \ge 0$ for all $P$), $h^0(C, \mathcal{O}_C(D))$ measures the size of the linear system $|D|$, the set of effective divisors linearly equivalent to $D$. If $|D|$ is base-point-free, it defines a morphism $\phi_D: C \to \mathbb{P}^N$ where $N = h^0(C, \mathcal{O}_C(D)) - 1$. Understanding $h^0$ is thus key to mapping curves into projective space.

- **$h^1(C, \mathcal{O}_C(D))$ (or $h^0(C, \mathcal{O}_C(K_C - D))$)**: This "correction term" is where much of the subtlety lies, especially in higher genus. It measures the dimension of the space of obstructions, or, via Serre Duality, the dimension of the space of global sections of the line bundle $\mathcal{O}_C(K_C - D)$. Geometrically, this corresponds to the space of holomorphic differentials $\omega$ such that $\text{div}(\omega) \ge D$. If $D$ is effective, these are the differentials vanishing at the points specified by $D$ (with appropriate multiplicities).

  - For $g=0$, $K_C$ has degree $-2$, so $h^0(K_C)=0$. If $\deg(D) \ge -1$, then $\deg(K_C - D) < 0$, implying $h^0(K_C - D) = 0$. RR becomes $h^0(D) = \deg(D) + 1$ for $\deg(D) \ge -1$.
  - For $g=1$, $K_C$ has degree $0$ and $h^0(K_C)=1$. $K_C \sim 0$ (linearly equivalent to the zero divisor). RR becomes $h^0(D) - h^0(-D) = \deg(D)$. If $\deg(D) > 0$, $h^0(-D)=0$, so $h^0(D) = \deg(D)$.
  - For $g \ge 2$, the term $h^1(D) = h^0(K_C - D)$ is frequently non-zero for divisors of moderate degree, making the direct calculation of $h^0(D)$ more challenging. This non-vanishing is characteristic of higher genus geometry.

**Immediate Consequences**

Let's apply Riemann-Roch to the canonical divisor itself:
Take $D = K_C$.
$$ h^0(K_C) - h^0(K_C - K_C) = \deg(K_C) - g + 1 $$
$$ h^0(K_C) - h^0(\mathcal{O}\_C) = \deg(K_C) - g + 1 $$
Since $C$ is projective and irreducible, the only global regular functions are constants, so $h^0(\mathcal{O}_C) = 1$. We also know $h^0(K_C) = h^0(\omega_C)$, which is the dimension of the space of holomorphic 1-forms. This is often taken as *another* definition of the genus, so $h^0(K_C) = g$. Plugging this in:
$$ g - 1 = \deg(K_C) - g + 1 $$
$$ \boxed{\deg(K_C) = 2g - 2} $$
This is a fundamental result. The degree of the canonical divisor is intrinsically tied to the genus.

Now consider a divisor $D$. If $\deg(D) > \deg(K_C) = 2g - 2$, then $\deg(K_C - D) = \deg(K_C) - \deg(D) < 0$. A divisor of negative degree cannot have any non-zero global sections (since $\text{div}(f)$ has degree 0, $\text{div}(f) + (K_C - D) \ge 0$ would imply $\deg(K_C - D) \ge 0$). Thus, $h^0(K_C - D) = 0$.
In this case, Riemann-Roch simplifies significantly:
$$ h^0(D) = \deg(D) - g + 1 \quad \text{if } \deg(D) > 2g - 2 $$
This formula is extremely useful. It tells us that for divisors of sufficiently high degree, the dimension of the associated linear system grows linearly with the degree and is independent of the specific choice of divisor (within that degree).

**Applications to the Geometry of Curves**

The power of Riemann-Roch truly shines when we use it to deduce geometric properties of curves, especially those of genus $g \ge 2$.

1.  **Existence of Non-Constant Maps:**
    For $g=0$, take any point $P$. $\deg(P)=1$. $h^0(P) = \deg(P) - g + 1 = 1 - 0 + 1 = 2$. This means there exists a non-constant function $f$ in $L(P)$. This function must have a simple pole at $P$ and no other poles. Such a function defines an isomorphism $f: C \to \mathbb{P}^1$. Thus, any curve of genus 0 is isomorphic to $\mathbb{P}^1$.

2.  **Hyperelliptic Curves:**
    A curve $C$ of genus $g \ge 2$ is called _hyperelliptic_ if it admits a degree 2 map to $\mathbb{P}^1$. This is equivalent to the existence of a linear system $|D|$ of dimension $r=1$ and degree $d=2$, denoted $g^1_2$. Let $D$ be such a divisor (e.g., $D=P+Q$ where $\phi(P)=\phi(Q)$ for the 2:1 map $\phi$). Then $h^0(D) \ge r+1 = 2$.
    Let's check this with Riemann-Roch for $g=2$. $\deg(K_C) = 2(2)-2 = 2$. Let $D$ be a divisor of degree 2.
    $h^0(D) - h^0(K_C - D) = \deg(D) - g + 1 = 2 - 2 + 1 = 1$.
    Since $\deg(K_C - D) = 2-2 = 0$, $h^0(K_C - D)$ can be 0 or 1.

    - If $h^0(K_C - D)=1$, then $K_C - D$ must be linearly equivalent to 0, so $K_C \sim D$. In this case, $h^0(D) = 1 + 1 = 2$. This is the _generic_ case for a divisor of degree 2 on a genus 2 curve. Any such $D$ gives $h^0(D)=2$, defining a $g^1_2$. Thus, _all_ curves of genus 2 are hyperelliptic. The canonical map associated to $|K_C|$ is precisely this $g^1_2$.
    - If $h^0(K_C - D)=0$, then $h^0(D)=1$. This means $D$ is not linearly equivalent to $K_C$. This case doesn't occur for $g=2$.

    For $g \ge 3$, a _general_ curve is _not_ hyperelliptic. The existence of a $g^1_2$ (i.e., $h^0(D)=2$ for some $D$ with $\deg(D)=2$) is a special property.

3.  **The Canonical Embedding:**
    A central tool for studying curves is the _canonical map_ $\phi_K: C \to \mathbb{P}^{g-1}$ defined by the canonical linear system $|K_C|$, provided $h^0(K_C) = g \ge 2$. This map is defined by choosing a basis $\{\omega_0, \dots, \omega_{g-1}\}$ for $H^0(C, \omega_C)$ and sending $P \in C$ to $[\omega_0(P) : \dots : \omega_{g-1}(P)]$ (local coordinates are needed for a rigorous definition).
    We need to know if $\phi_K$ is an embedding (a closed immersion). This requires $|K_C|$ to be _very ample_, which means:
    a) $|K_C|$ is base-point-free: For every $P \in C$, $h^0(K_C - P) = h^0(K_C) - 1 = g-1$.
    b) $\phi_K$ separates points: For every distinct $P, Q \in C$, $h^0(K_C - P - Q) = h^0(K_C) - 2 = g-2$.
    c) $\phi_K$ separates tangent vectors: For every $P \in C$, $h^0(K_C - 2P) = h^0(K_C) - 2 = g-2$.

    Let's use Riemann-Roch to analyze these conditions.
    Consider $h^0(K_C - P)$. By RR:
    $h^0(K_C - P) - h^0(K_C - (K_C - P)) = \deg(K_C - P) - g + 1$
    $h^0(K_C - P) - h^0(P) = (2g - 2 - 1) - g + 1 = g - 2$
    Since $P$ is a point, $h^0(P)=1$ (only constants live in $L(P)$) _unless_ $g=0$, which we exclude.
    So, $h^0(K_C - P) - 1 = g - 2 \implies h^0(K_C - P) = g - 1$. This holds for all $P$. Thus, $|K_C|$ is base-point-free for $g \ge 2$.

    Now consider $h^0(K_C - P - Q)$ for distinct $P, Q$. By RR:
    $h^0(K_C - P - Q) - h^0(P + Q) = \deg(K_C - P - Q) - g + 1$
    $h^0(K_C - P - Q) - h^0(P + Q) = (2g - 2 - 2) - g + 1 = g - 3$
    $h^0(K_C - P - Q) = g - 3 + h^0(P + Q)$.
    We want this to be $g-2$. This happens if and only if $h^0(P + Q) = 1$.
    If $h^0(P + Q) \ge 2$, it means there exists a non-constant function $f$ with at most simple poles at $P$ and $Q$. This function defines a map $f: C \to \mathbb{P}^1$ of degree at most 2. If $\deg(f)=1$, $C \cong \mathbb{P}^1$ ($g=0$). If $\deg(f)=2$, $C$ is hyperelliptic, and $P+Q$ is a divisor in the $g^1_2$.
    So, $\phi_K$ separates points if and only if $C$ is _not_ hyperelliptic (assuming $g \ge 3$, since $g=2$ curves are always hyperelliptic).

    A similar analysis for $h^0(K_C - 2P)$ shows it equals $g-2$ if and only if $h^0(2P)=1$. If $h^0(2P)=2$, this again implies $C$ is hyperelliptic (with $P$ being a ramification point of the hyperelliptic map).

    **Conclusion:** The canonical map $\phi_K: C \to \mathbb{P}^{g-1}$ is an embedding if and only if $C$ is not hyperelliptic and $g \ge 3$.

    - If $C$ is hyperelliptic and $g \ge 3$, $\phi_K$ is a 2-to-1 map onto a rational normal curve of degree $g-1$ in $\mathbb{P}^{g-1}$.
    - If $g=2$, $C$ is hyperelliptic, $\deg(K_C)=2$, $h^0(K_C)=2$. The canonical map is $\phi_K: C \to \mathbb{P}^1$, which is the degree 2 hyperelliptic map itself.

    The image of the canonical embedding is a curve of degree $\deg(K_C) = 2g - 2$ in $\mathbb{P}^{g-1}$. This provides a fundamental geometric realization of non-hyperelliptic curves.

4.  **Clifford's Theorem:**
    Riemann-Roch gives an exact value for $h^0(D) - h^1(D)$. However, it doesn't directly constrain $h^0(D)$ itself when $h^1(D) > 0$. A divisor $D$ is called _special_ if both $h^0(D) \ge 2$ (i.e., $|D|$ contains more than just $D$ itself, assuming $D$ effective) and $h^1(D) = h^0(K_C - D) \ge 1$ (by RR, this implies $h^0(D) > \deg(D) - g + 1$). Clifford's Theorem provides a fundamental upper bound on the dimension of a special linear system relative to its degree.

    **Clifford's Theorem:** Let $D$ be a special divisor on $C$. Then
    $$ h^0(C, \mathcal{O}\_C(D)) - 1 \le \frac{1}{2} \deg(D) $$
    Or equivalently, using $r = h^0(D)-1$ (the dimension of the linear system $|D|$):
    $$ r \le \frac{1}{2} \deg(D) $$
    Equality holds if and only if $D=0$, $D=K_C$, or $C$ is hyperelliptic and $D$ is linearly equivalent to $nP$ or $nP + Q$ where $P+Q$ is the hyperelliptic divisor $g^1_2$ (i.e., $D$ is composed from the $g^1_2$).

    Clifford's theorem is a powerful constraint. For example, if we find a $g^r_d$ (a linear system of dimension $r$ and degree $d$) on a non-hyperelliptic curve, we know $r \le d/2$, unless this system is the canonical system ($r=g-1, d=2g-2$) or the trivial system ($r=0, d=0$). This theorem is proven using techniques building upon Riemann-Roch, often involving induction or geometric arguments related to Castelnuovo's base point free pencil trick.

5.  **Brill-Noether Theory:**
    A central question in curve theory is: For a given genus $g$, what kinds of linear systems $g^r_d$ (dimension $r$, degree $d$) does a curve $C$ possess? Riemann-Roch provides a starting point. We are looking for divisors $D$ of degree $d$ such that $h^0(D) \ge r+1$.
    RR tells us $h^0(D) = d - g + 1 + h^1(D)$. So, the condition is $d - g + 1 + h^1(D) \ge r+1$, or $h^1(D) \ge g - d + r$.
    The _expected_ or _generic_ dimension of the space of such linear systems is given by the Brill-Noether number:
    $$ \rho(g, r, d) = g - (r+1)(g - d + r) $$
    This formula arises from considering the "expected" dimension of the variety $W^r_d(C) = \{ \mathcal{L} \in \text{Pic}^d(C) \mid h^0(C, \mathcal{L}) \ge r+1 \}$ inside the Picard variety $\text{Pic}^d(C)$, which has dimension $g$. The Brill-Noether Theorem (proven by Griffiths, Harris, Lazarsfeld, Gieseker, and others) states that for a _general_ curve $C$ of genus $g$:

    - If $\rho(g, r, d) \ge 0$, then $W^r_d(C)$ is non-empty and has dimension _at least_ $\rho(g, r, d)$. Furthermore, for a _general_ curve, the dimension is _exactly_ $\rho$.
    - If $\rho(g, r, d) < 0$, then $W^r_d(C)$ is empty.

    Riemann-Roch is the fundamental input here. It sets the relationship $h^0 - h^1 = d - g + 1$. Brill-Noether theory then investigates the geometry of the varieties $W^r_d(C)$ parametrizing linear systems with _at least_ the required dimension, whose structure is deeply tied to the subtle interplay between $h^0$ and $h^1$ dictated by RR. For specific curves (non-generic), the dimensions might be larger than $\rho$.

6.  **Embeddings in $\mathbb{P}^3$:**
    A classical question is whether a general curve $C$ of genus $g$ can be embedded in $\mathbb{P}^3$. For this, we need a very ample divisor $D$ such that $h^0(D) = 4$.
    Let's try a divisor $D$ of degree $d$. If $d > 2g-2$, then $h^0(D) = d - g + 1$. We want $d - g + 1 = 4$, so $d = g+3$.
    Is a general divisor $D$ of degree $d=g+3$ very ample? One needs to check the base-point-free and separation conditions. Using arguments related to Riemann-Roch and Clifford's Theorem, one can show that for a _general_ curve of genus $g \ge 4$, a general divisor $D$ of degree $d \ge g+3$ is very ample. In particular, taking $d=g+3$, we get an embedding into $\mathbb{P}^{h^0(D)-1} = \mathbb{P}^{g+3-g+1-1} = \mathbb{P}^3$.
    (Note: Special curves might not embed, e.g., hyperelliptic curves, trigonal curves, etc., require higher degree embeddings in $\mathbb{P}^3$).

**Beyond Curves: Grothendieck-Riemann-Roch and Index Theorems**

The Riemann-Roch theorem for curves is just the tip of the iceberg. Its generalizations are fundamental across algebraic geometry and related fields.

- The Hirzebruch-Riemann-Roch theorem generalizes RR to higher-dimensional smooth projective varieties $X$, relating the Euler characteristic $\chi(\mathcal{F}) = \sum (-1)^i h^i(X, \mathcal{F})$ of a vector bundle $\mathcal{F}$ to intersection products involving the Chern character of $\mathcal{F}$ and the Todd class of the tangent bundle of $X$.
  $$ \chi(X, \mathcal{F}) = \int_X \text{ch}(\mathcal{F}) \cdot \text{Td}(T_X) $$
- The Grothendieck-Riemann-Roch theorem (GRR) generalizes further to a statement about proper morphisms $f: X \to Y$ between smooth varieties (or more generally). It relates the Chern character of the pushforward complex $Rf_* \mathcal{F}$ to the pushforward of the Chern character of $\mathcal{F}$ twisted by the Todd class of the relative tangent bundle.
  $$ \text{ch}(Rf*\* \mathcal{F}) \cdot \text{Td}(T_Y) = f*\* (\text{ch}(\mathcal{F}) \cdot \text{Td}(T_X)) $$
    The classical RR for curves is the special case where $Y = \text{pt}$ (a point).

Analytically, over $\mathbb{C}$, Riemann-Roch can be viewed as a special case of the Atiyah-Singer Index Theorem applied to the $\bar{\partial}$-operator acting on sections of a line bundle $L \to C$. The index of this operator, $\text{Index}(\bar{\partial}_L) = \dim \ker(\bar{\partial}_L) - \dim \text{coker}(\bar{\partial}_L)$, corresponds precisely to $h^0(C, \mathcal{O}_C(L)) - h^1(C, \mathcal{O}_C(L))$, and the index theorem computes this as $\deg(L) - g + 1$.

**Conclusion**

Even centuries after its inception, the Riemann-Roch theorem remains a vital, quantitative tool in the study of algebraic curves. For genus $g \ge 2$, it moves beyond simple classification (like $g=0$) or group structure description (like $g=1$) to become the engine driving our understanding of embeddings, special divisors, and the existence of linear systems through Clifford's Theorem and Brill-Noether theory. It dictates the degree of the canonical embedding and explains why hyperelliptic curves are special. Here at IAS, whether discussing moduli spaces like $\mathcal{M}_g$, derived categories, or arithmetic properties of curves, the implications stemming from Riemann-Roch are often just below the surface, a testament to its enduring power and central position within algebraic geometry. It's a beautiful example of how a single, elegant equation can encode a wealth of geometric information.

---
