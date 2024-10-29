---
title: Abstract Algebra 1
tags:
  - School
---

# Math 103A

Sadly this markdown version does not render perfectly and it would take way too much work to port it over from the original notion source. Please refer to: the [Notion version of this text](https://www.notion.so/domogami/Math-103B-9b206bad0f60490e9dfaaa1b14842365?pvs=4)

### Monoid

A monoid has two properties,
$$3x^2$$

* ${\bf{Associative}}: x\cdot (y\cdot z) = (x\cdot y)\cdot z$
* ${\bf{Identity / Neutral\ Element}}: \exists\ e \in G: x\cdot e\ = e\cdot x \ =\ x$

Adding a third property

* ${\bf{Inverse}}: \forall\ x \in G\ \exists \ y \in G:\ x\cdot y = y\cdot x =\ e$
  * ($y = x^{-1}$)

### Groups

A Group is a Monoid with Inverses

### Abelian Group

A group with Communativity is an Abelian Group

* ${\bf{Commutativity}}: \forall x,y\in G: x\cdot y = y\cdot x$

**Examples:**

* $(\mathbb{Z}, +)$ - **Abelian Group**
* $(\mathbb{Z}, \cdot)$ - **Monoid** (Abelian Monoid because $n\cdot m = m \cdot n$)
  * 0 is not invertible
* $(\mathbb{Z}*n, +*{mod(n)})$ = {0, 1, ..., n - 1} - **Abelian Group**
* $(\mathbb{Z}*n, \cdot*{mod(n)})$ - **Monoid**
* $(\mathbb{Z}, +)$ - **Abelian Group**
* $(\mathbb{R}, \cdot)$ - **Monoid**
* $(M_n(\mathbb{R}), + )$ - **Abelian Group**
  * $$\begin{pmatrix}
    2 & 0\\
    1 & -1
    \\end{pmatrix} +
    \\begin{pmatrix}
    3 & 1\\
    0 & 1
    \\end{pmatrix} =
    \\begin{pmatrix}
    5 & 1\\
    1 & 0
    \\end{pmatrix}$$
  * Identity Element is the 0 matrix
  * Inverse - make each element in matrix negative
* $(M_n(\mathbb{R}), \cdot )$ - **Monoid**
  * $$\begin{pmatrix}
    2 & 0\\
    1 & -1
    \\end{pmatrix} \cdot
    \\begin{pmatrix}
    3 & 1\\
    0 & 1
    \\end{pmatrix} =
    \\begin{pmatrix}
    6 & 2\\
    3 & 0
    \\end{pmatrix}$$
  * Identity Element is the identity matrix
* $(f:\mathbb{R} \implies \mathbb{R}, +)$ - **Abelian Group**
  * $(f+g)(x) = f(x) + g(x)$
* $(f:\mathbb{R} \implies \mathbb{R}, \cdot)$ - **Monoid**
  * $(f\cdot g)(x) = f(x)g(x)$
  * Identity Element: $f(x)=1$
  * $f(x)=0$ is not invertible
  * Invertible elements have no roots (do not intersect x axis)
* $(f:\mathbb{Z} \implies \mathbb{R}, \circ)$ - Monoid
  * Not invertible, $f(x) = x^2$ is not invertible (Must be bijective)

# Rings

A **ring** is a set $(R, +, \cdot)$  with operations +, ⋅ such that

1. $(R, +)$ Abelian Group
1. $(R, \cdot)$ Monoid
1. ${\bf{Distributivity}}:\ \forall x,y,z\in R: x\cdot(y+z) = x\cdot y+x\cdot z \\ (x+y)\cdot z = x\cdot z + y\cdot z$

A ring is called **commutative** if $\forall x,y\in R: x\cdot y = y \cdot x$, $(R,\cdot)$ is a commutative monoid

* Matrix Multiplication / Addition is a non Communative Ring
* Continuous Functions form a communative ring
* Function Composition is not a ring

### SubRing Test

A subset $S \subseteq R$ is a subring if it is closed under $+,\cdot$ and

* $(S, +)$ is a subgroup of $(R,+)$
  * S is closed under subtraction $(x,y\in S \implies x-y\in S)$
* $(S, \cdot)$ is a submonoid of $(R,\cdot)$
  * S is closed under multiplication $(x,y\in S \implies x\cdot y \in S)$
* $1 \in S$

**Remark:** We also know $0 \in S$. Since $1 \in S$, so $-1 \in S$ 

**Example:**

1. $\mathbb{Z} \subset \mathbb{Q} \subset \mathbb{R} \subset \mathbb{C}$ are subrings!

1. $Z_n = {0,1,\cdots, n-1} \subset \mathbb{Z}={\cdots,\ -1,\ 0,\ 1, \cdots }$
   
   $0-1 = -1 \notin \mathbb{Z}\_n$ not a subring

1. $\mathbb{Z}\[\\sqrt{2}\] = {a+b\sqrt{2}\ |\ a, b \in \mathbb{Z} } \subset \mathbb{R}$
   
   Subring test: $1=1+0\sqrt2 \in \mathbb{Z}\[\\sqrt2\]$
   
   Multiplication: $(a+b\sqrt2)(c+d\sqrt2) = ac+ad\sqrt2+b\sqrt2c+ b\sqrt2\cdot d\sqrt2 = (ac+2bd)+(ad+bc)\sqrt2 \in \mathbb{Z}\[\\sqrt2\]$
   
   Subtraction: $(a+b\sqrt2)-(c+d\sqrt2)=(a-c)+(b-d)\sqrt2 \in Z\[\\sqrt2\]$
   
   $\therefore \mathbb{Z}\[\\sqrt2\] \subset \mathbb{R}$ it is a subring!

1. $\mathbb{Z}\[i\] = {\ a+bi\ |\ a,b\in\mathbb{Z}} \subset \mathbb{C}$ - Gaussian Integers (subring)

Remark: “lines are transitive” in this diagram, namely, if $S\subseteq R$ is a subring and $T\subseteq S$ is a subring, then $T \subseteq R$ is a subring

1. $$UT_n(\mathbb{R}) = \begin{pmatrix}

* & \cdots & \cdots & * \\ 
  0 & \ddots & \ddots & \vdots\\
  \\vdots & \ddots & \ddots & \vdots\\
  0 & \cdots & 0 & *
  \\end{pmatrix} \subset M_n(\mathbb{R})$$ is a subring

2. $B(\mathbb{R}) {f: \mathbb{R} \mathbb{R}ightarrow \mathbb{R}$ bounded continuous functions$}= {}\subset C(\mathbb{R}) = {f: \mathbb{R} \mathbb{R}ightarrow \mathbb{R}$ continous functions$}$

### Polynomial Rings

“Polynomial Ring over R” $\Longleftrightarrow \ R\[x\]$

$R\[x\] = {r_0+r_1x+r_2x^2+\cdots+r_nx^n\ |\ r_0,\cdots,r_n\in \mathbb{R}}$

**Polynomial Addition Formula**

$$
r_0+r_1x+\cdots+r_nx^n \\
s_0+s_1x+\cdots+s_mx^m \\
\\implies (r_0+r_1x+\cdots+r_nx^n )+(s_0+s_1x+\cdots+s_mx^m) \\
= (r_0+s_0)+(r_1+s_1)x+\cdots+(r_n+s_n)x^n+s\_{n+1}x^{n+1}+\cdots+s_mx^m
$$

**Polynomial Multiplication Formula**

$$
p(x)=\sum\_{i=0}^n r_ix^i=r_0+r_1x+\cdots+r_nx^n \\
q(x)=\sum\_{j=0}^m s_jx^j=rs_0+s_1x+\cdots+s_mx^m \\
p(x)\cdot q(x)=(r_0+r_1x+\cdots+r_nx^n )\cdot(s_0+s_1x+\cdots+s_mx^m) \\
= r_0+s_0+(r_1s_0+r_0s_1)x+(r_0s_2+r_1s_1+r_2s_0)x^2+\cdots \\
= (\sum\_{i=0}^n r_ix^i)(\sum\_{j=0}^m s_jx^j)\\
= \sum\_{d=0}^{n+m}(\sum\_{i+j=d}r_is_j)x^d)
$$

**Remark:** $(R\[x\], +, \cdot)$ is a ring (assuming R is an arbitary ring)

**Remark:** A ring is communitive if $x\cdot y = y \cdot x \ \forall \ x,y$

* $\mathbb{Z},\ \mathbb{Q},\ \mathbb{R},\ \mathbb{C}$ - Commutative Rings
* $M_2(\mathbb{R})$ - Non Commutative

When is $R\[x\]$ commutative? ⇒ if $R\[x\]$ is commutative then R is, conversely, if R is communative then $R\[x\]$ is commutative

Using the formula for polynomial multiplication, we find that

$$
p(x)\cdot q(x) = q(x)\cdot p(x) \\
\\sum\_{d=0}^{n+m}(\sum\_{i+j=d}r_is_j)x^d) = \sum\_{d=0}^{n+m}(\sum\_{j+i=d}s_jr_i)x^d)
$$

Therefore, $R\ is \ Commutative\ \Longleftrightarrow\ R\[x\]\\ is\ Commutative$

**Remark:** Is $\mathbb{R}\[x\] \subset C(\mathbb{R})$ a subring? ⇒ No, $e^x, sin(x), \cdots \in C(\mathbb{R})$ but $\notin \mathbb{R}\[x\]$

**Remark:** $R\[x\]$ is defined for an arbitary ring R. We can have a ring, $\mathbb{Z} \mathbb{R}ightarrow \mathbb{Z}\[x\] \mathbb{R}ightarrow (\mathbb{Z}\[x\])\[y\] = \mathbb{Z}\[x,y\]$ . Which gives us a polynomial of y with coefficents from x or vice versa.

### Direct Sums

Suppose that $R,S$ are rings. Define the direct sum $R \oplus S:$

$$
R \oplus S = {(r,s)\ |\ r\in R, s\in S}
$$

**Addition:**

$$
(r_1,\ s_1)+(r_2,\ s_2) = (r_1+\_Rr_2,\ s_1+\_Ss_2)
$$

**Multiplication:**

$$
(r_1,\ s_1)\cdot(r_2,\ s_2) = (r_1\cdot_Rr_2,\ s_1\cdot_Ss_2)
$$

$0\_{R\oplus S}=(0_R,\ 0_S),\ 1\_{R\oplus S}=(1_R,\ 1_S)$

Examples:

1. $M_2(\mathbb{R}) \oplus \mathbb{Z}\[x\]$
1. $\mathbb{Z}\_2 \oplus \mathbb{Z}\_3$
1. $\mathbb{Z} \oplus \mathbb{Z}$
1. $R_1 \oplus R_2 \oplus \cdots \oplus R_n$ ← Iterative direct sum

**Remarks on Direct Sums:**

1. If $R_1 \subseteq S_1, R_2 \subseteq S_2$ are subrings, then $R_1 \oplus R_2 \subseteq S_1 \oplus S_2$ is a subring
1. $R \oplus S \ is \ commutative \Longleftrightarrow\ R,\ S\ are\ commutative$
1. ${\ (r,r)\ |\ r\in R\ }\subset R\oplus R$ is a subring

**Ring Proofs**

$r\cdot 0=r\cdot(0+0)=r\cdot0+r\cdot 0 \implies 0=r\cdot 0$

### Commutativity

**Recall:** R is commutative if $\forall\ r,s \in R,\ r\cdot s = s\cdot r$

**Remark:** If R is commutative and $S \subseteq R$ is a subring, then S is also cummutative. In particular, $\mathbb{C}, \mathbb{R}, \mathbb{Q}, \mathbb{Z}, \mathbb{Z}\[\\sqrt2\], \mathbb{Q}\[i\]$ are all commutative

**Example:** $\mathbb{R} \oplus \mathbb{Z}\_7$ is commutative whereas $\mathbb{Q} \oplus M_2(\mathbb{C})$ is not

**Definition:** Let R be a ring. The center of R is:

$$
Z(R) ={\ r\in R\ |\ \forall x \in R, r\cdot x=x\cdot r\ }
$$

In other words, Z(R) is the set of elements in R which commute with any other element of R.

Remark: 

1. We always have $0,1 \in Z(R)$ this is because $1\cdot r = r \cdot 1 = r\\ 0\cdot r = r \cdot 0 = 0$
1. If $r,s\in Z(R)$ then $r-s\in Z(R)$
   Pf. Let $x\in R$ be arbitary, we need to show that $(r-s)\cdot x = x \cdot (r-s)$
   But, $(r-s)\cdot r = r \cdot x - s \cdot x = x \cdot r - x \cdot S = x \cdot (r-s)$ so, $r-s\in Z(R)$
1. If $r,s \in Z(R)$ then $r\cdot s \in Z(R)$
   Pf. Let $x\in R$ be arbitary, we need to show that $(r \cdot s)\cdot r = x \cdot (r\cdot s)$
   Indeed,
   $(r\cdot s) \cdot x$ 
   $=r\cdot (s\cdot x)$ ← Associativity of $\cdot$
   $= r \cdot (x\cdot s)$ ← $s \in Z(R),\ s\cdot x=x\cdot s$
   $= (r \cdot x) \cdot s$ ← Associativity of $\cdot$
   $= (x\cdot r) \cdot s$ ← $r \in Z(R),\ r\cdot x=x\cdot r$
   $=x\cdot(r\cdot s)$← Associativity of $\cdot$

**Corollary:** $Z(R)\subseteq R$ (the center) is a subring 

**Examples:** 

1. If R is commutative then $Z(R) = R$
1. $R=M_n(\mathbb{C})$, 
   then $$Z(R) = {\begin{pmatrix} 
   \\alpha & \cdots & 0 \\
   \\vdots & \ddots & \vdots \\
   0& \cdots & \alpha \\
   \\end{pmatrix}|\ \alpha \in \mathbb{C}}$$
1. If $R= M_n(S),$ (where S is another ring), then
   $$Z(R)={\begin{pmatrix} 
   \\alpha & \cdots & 0 \\
   \\vdots & \ddots & \vdots \\
   0& \cdots & \alpha \\
   \\end{pmatrix}|\ \alpha \in Z(S)}$$
1. $Z(R\[x\])=(Z(R))\[x\]$ ← The center of a polynomial ring is a polynomial ring over the center of R
1. $Z(R\oplus S)=Z(R)\oplus Z(S)$ ← The center of the direct sum of two wrings is the direct sum of the centers

## Units

Let R be a ring. The set of units in R is:

$$
U(R)=R^x={a\in R\ |\ \exists\ b \in R:\ ab=ba=1}
$$

Where $a$ and $b$ are units or invertible elements. We denote $b=a^{-1}$ or $b$ is the inverse of $a$

**Remark:** 

1. $U(R) \subseteq R$
1. $1\in U(R)$ since $1\cdot 1 = 1\cdot 1 = 1$
1. $0\notin U(R)$ since $0 \cdot b = b\cdot 0 = 0 \neq 1$
1. If $a\in U(R)$ then $a^{-1}$ is unique:
   if $ab_1=b_1a=1$ and $ab_2=b_2a=1$ then:
   $b_1=b_1(ab_2)=b_2ab_2=(b_1a)b_2=b_2$
1. One must be careful, it is possible that $ab=1$ but $a$ is not a unit

**Proposition:** $(U(R),\cdot)$ is a group

**Proof:** First, let us show that $U(R)$ is closed under ⋅ 
If $a_1,a_2 \in U(R)$ 
Then: 
$(a_1a_2)(a_2^{-1}a_1^{-1})=a_1(a_2a_2^{-1})a_1^{-1}=a_1a_1^{-1}=1$

$(a_2^{-1}a_1^{-1})(a_1a_2)=a_2^{-1}(a_1^{-1}a_1)a_2=a_2^{-1}a_2=1$

$\implies a_1a_2$ is a unit $((a_1a_2)^{-1}=a_2^{-1}a_1^{-1})$

Neutral Element ( Identity element ) is $1 \in U(R)$ by the above remark

If $a\in U(R)$ then, by the definition of a unit, there exits an $a^{-1}\in R$ such that $aa^{-1}=a^{-1}a=1$ but it follows that $a^{-1}\in U(R)\ \  ((a^{-1})^{-1})=a)$

Therefore $(U(R),\ \cdot)$ is a group. (Associativity of ⋅is ensured by the fact that R is a ring, hence $(R,\cdot)$ is associative.

**Examples:**

1. $R=\mathbb{R}, \mathbb{C}, \mathbb{Q}$ 
   $R^x=R\backslash {0}$
   $$ \mathbb{R}^x=\mathbb{R}\backslash{0} \\
   \\mathbb{C}^x=\mathbb{C}\backslash{0} \\
   \\mathbb{Q}^x=\mathbb{Q}\backslash{0} \\ $$
1. $R= \mathbb{Z}$ (What are the units in the ring of integers)
   $R^x= {±1}$ 
   $\mathbb{Z} \subset \mathbb{Q}$ ← (Every nonzero element of $\mathbb{Z}$ is invertible in $\mathbb{Q}$)

(For example, $2\in\mathbb{Z}$, not invertible within $\mathbb{Z}$ because $\frac{1}{2} \notin \mathbb{Z}$. However, if we think of $2\in \mathbb{Q}$, it is invertible within $\mathbb{Q}$ because $\frac{1}{2} \in \mathbb{Q}$)

1. $R = \mathbb{Z}\_n = {0,1,\cdots, n-1}$ ← What are the units of the integers mod n
   $R^x ={x\in \mathbb{Z}*n |\ \exists\ xy=1*{mod\ n}}$
   Exactly the coprime to n residues:
   $R^x=\mathbb{Z}\_n^x={\ 1\leq a \leq n-1\ |\ gcd(a,n)= 1\ }$
   The cardinality of $\mathbb{Z}\_n^x$ is $\phi(n)$ ← Eulers totient function

$n=6$
$\mathbb{Z}\_6= {\ 0, 1 ,2 ,3, 4,5\ } \implies \mathbb{Z}\_6^x={\ 1,\ 5 }$

$n=7$
$\mathbb{Z}\_7= {\ 0, 1 ,2 ,3, 4,5,6\ } \implies \mathbb{Z}\_7^x={\ 1,2,3,4,5,6 }$

**Remark:** (From 103A): 
$\mathbb{Z}\_n^x=\mathbb{Z}\_n\backslash {0} \Longleftrightarrow$  $n$ is prime
The units of the Integers mod n is equal to the integers up to n excluding zero if n is a prime number

**Question:** How to invert mod n?
$$17^{-1}(mod\ 48)=\ ? $$
$17,\ 48$ are coprime 
$$ (48,17) = (17, \mathbf{14} ) = (14, 3)=(3,2)=(2,1) $$
$48=2\cdot 17 +14$ ← $\mathbf{14}$ is the “Residue”
$17=1\cdot 14 +\mathbf{3}$
$14=4\cdot 3 + \mathbf{2}$
$3=1\cdot 2 + \mathbf{1}$ ← Once we have 1, we now invert
$1=3-2= 3-(14-4\cdot3)=-14+5\cdot 3=-14+5(17-14)=-6\cdot14+5\cdot 17=-6\cdot (48-2\cdot 17)+5\cdot 17=-6\cdot 48+17\cdot 17$

So, $17 \cdot 17 = 1(mod\ 48)$ so, $17^{-1}=17$ in $\mathbb{Z}\_{48}$

2. $R=M_n(\mathbb{R})$
   $R^x={A\in M_n(\mathbb{R})\ |\ \exists\ B \in M_n(\mathbb{R}):\ AB=BA=I_n\ }$ ← invertible matrices
   $={\ A\in M_n(\mathbb{R})\ |\ det(A) \neq 0\ } =\ GL_n(\mathbb{R})$
2. $R=\mathbb{Z}\[i\]={\ a+bi\ |\ a,b\in Z\ }$
   $\mathbb{Z}\[i\]^x=\ ?$

$={a+bi\ |\ \exists\ c,d \in \mathbb{Z}:\ (a+bi)(c+di)=1 \Leftrightarrow (a-bi)(c-di)=1}$
Using: $a+bi \mathbb{R}ightarrow\ a-bi$ or, $\bar{z}\bar{w} =\bar{z}\cdot \bar{w}$
$(a+bi)(a-bi)(c+di)(c-di)=1\cdot 1 =1$
$= (a^2+b^2)\cdot (c^2+d^2)= 1$ ← $(a^2+b^2)\in \mathbb{Z}$, $(c^2+d^2)\in \mathbb{Z}$
So, 
$a^2+b^2=1 \Longleftrightarrow a=0,\ b=\pm 1$ or $a=\pm1,\ b=0$
$c^2+d^2=1 \Longleftrightarrow c=0,\ d=\pm 1$ or $c=\pm1,\ d=0$
For conclusion, $\mathbb{Z}\[i\]^x={\pm1, \pm i}$

**Definition:** A ring is called a division ring if $R^x=R\backslash {0}$

**Definition:** A commutative division ring is called a field 

In other words, a field is a system $(R,0,1,\pm,\cdot, \div)$ with “all reasonable axioms” where we can divide except for $x\div 0$

**Examples:** 

$\mathbb{Q}, \mathbb{R}, \mathbb{C}\ -$ Fields

$\mathbb{Z}\_p -$ Field (p prime)

$\mathbb{Z},\ \mathbb{Z}\[i\], \mathbb{Z}\_6, \cdots$ not fields

$\mathbb{H}-$  division ring that is not a field 

**Remark:** 
$U(R\oplus S) = U(R) \times U(S)$

In other words, $(r,s)\in R\oplus S$ is a unit (in $R\oplus S$) iff $r\in U(R)$ and $s\in U(S)$

**Proof:**

**Example:** How many units are there in $\mathbb{Z}\_7 \oplus \mathbb{Z}\_8$ ?

$U(\mathbb{Z}\_7 \oplus Z_8) = U(\mathbb{Z}\_7)\times U(\mathbb{Z}\_8) = 6\times 4 = 24$ units

**Definition:** An element $a\in R$ is a zero-divisor if there exists $b\in R$ such that $ab=0$ or $ba= 0$

**Examples:** 

1. In $\mathbb{Z}\_6,$ 
   $2\cdot 3=0,\\ 4\cdot 3 = 0$
   2, 3, 4 are zero divisors and 1, 5 are units
1. In $M_2(\mathbb{R}),$

**Proposition:** If $a\in U(R),$ then $a$ is not a zero divisor

Units are never zero divisors

**Remark:** In general, there might be elements which are neither units nor zero divisors

**Note:** Units are generators in $\mathbb{Z}\_n$

## Domains

**Definition:** A ring R is a domain if it has no zero divisors. R is an integral domain if it is a communative domain

**Examples:**

1. $\mathbb{Z}$ is an integral domain
1. If R is a division ring then it is a domain

(Because in a division ring, non-zero elements are units, but we saw that units cannot be zero-divisors!)

1. If R is a field then it is an integral domain

### Properties of Domains

1. Domains are “canellative”
   If $ab=ac,\ a\neq0  \implies b=c$

Proof

**Remark:** If your ring is not a domain, do not expect it to be cancellative

In $\mathbb{Z}\_6$, $3\cdot 2 =3 \cdot 4$ but $3\neq 4$

**Proof:** Suppose R is a domain $S \subseteq R$  subring

Let $a,b \in S$ be non-zero, let us prove that $ab\neq 0$. But $a,b\in R$ are non-zero, and R is a domain, so $ab \neq 0$

If in addition R is commutative, then so is S

**Remark:** A subring of a field need not be a field
Ex. Not a field → $\mathbb{Z} \subset R$ ← Field

**Corollary:** $\mathbb{Z}, \mathbb{Z}\[{\sqrt2}\], \mathbb{Z}\[{i}\], \cdots \subset \mathbb{C}$ therefore they are integral domains

**Proposition:** If R is a domain then $R\[x\]$ is also a domain 

(And if R is an integral domain then so is $R\[x\]$

**Corollary:** If F is a field then $F\[x\]$ is an integral  domain. 

Moreover, $F\[x,y\],\ F\[x,y,z\],\cdots$  are integral domains

**Remark:** Any subring of a field is an integral domain and conversely, if R is an integral domain then it is a subring of a field

Ex. $\mathbb{Z} \subset \mathbb{Q},\ \mathbb{Z}\[i\] \subset \mathbb{Q}\[i\], \cdots$

**Remark:** Any subring of a division ring is a domain. It is tempting to conjugate that any domain is a subring of a division ring. But that’s not true!
