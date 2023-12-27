---
layout: post
title: Varieties and Their Coordinate Rings
tag: algebraic-geometry
tag: undergraduate
---

This post is written in preparation for the [Schemes Learning
Seminar]({{site.baseurl}}/seminars/schemes.html) I am organising, and is intended to provide a
refresher on algebraic varieties and their coordinate rings to generalise to schemes.

---

### What is a variety?

Our ambient space of choice in the study of varieties is the *\\(n\\)-dimensional affine space over
\\(k\\)*, where \\(k\\) is a field of arbitrary characteristic, which is simply \\(k^n\\) as a set.

Now we can begin to define algebraic varieties.

**Definition.** An *affine algebraic set* \\(X \subset \mathbb{A}^n\\) is the set
\\[
X = \left\\{P \in \mathbb{A}^n \middle| f_\alpha(P) = 0, \alpha \in A\right\\}
\\]
where \\(f_\alpha \in k[x_1, \dotsc, x_n]\\) are polynomials.

We can equip our algebraic sets with a topology.

**Definition.** The *Zariski topology of \\(\mathbb{A}^n\\)* is the topology whose closed sets are
the affine algebraic sets. We equip every affine algebraic set \\(X\\) in \\(\mathbb{A}^n\\) with
the induced topology, and call this the *Zariski topology* of \\(X\\).

Now experience has shown that one should also study maps between varieties that preserve the
structure. To get a meaningful and interesting notion, we will need the local functions (that is,
maps from our variety to \\(k\\)); and thus the formal definition of a variety includes what is
known as the 'sheaf of local functions', or the 'structure sheaf'. (The notion of a set of
functions forming a sheaf should be understood as requiring the defining property to be a 'local
property' - examples include continuous, differentiable, and analytic functions.)

**Definition.** For \\(U \subset \mathbb{A}^n\\) Zariski open, we define
\\(\mathcal{O}_{\mathbb{A}^n}(U)\\) to be the set of functions \\(f : U \to k\\) such that every
\\(x \in U\\) has an open neighbourhood \\(V(x)\\) on which \\(f = \frac{p}{q}\\) for polynomials
\\(p, q \in k[x_1, \dotsc, x_n]\\) where \\(q(y) \neq 0\\) for all \\(y \in V(x)\\).

This set of functions clearly forms a sheaf. It is also easy to see that for any subset (in
particular, affine algebraic sets) \\(X \subset \mathbb{A}^n\\), we can get an induced sheaf from
\\(\mathcal{O}_{\mathbb{A}^n}\\), in a similar manner to the subspace topology. Thus we finally
arrive at the following definition.

**Definition.** Suppose \\(X \subset \mathbb{A}^n\\) is an affine algebraic subset together with
the Zariski topology \\(\mathfrak{T}\\). We define \\(\mathcal{O}\_X\\) to be the restriction of
the sheaf \\(\mathcal{O}\_{\mathbb{A}^n}\\) to \\(X\\). Then the triple \\((X, \mathfrak{T},
\mathcal{O}_X)\\), and more generally any topological space with a sheaf of \\(k\\)-valued
functions that is isomorphic to this data, is called an *affine algebraic variety*. The functions
in \\(\mathcal{O}_X(U)\\) for any open subset \\(U\\) are called *regular functions*.

I remark here that one can similarly define projective algebraic sets and projective varieties in a
similar manner up to requiring the relevant polynomials to be homogeneous. For brevity, I will
assume sufficient comfort with these and freely refer to them later.

---

### Coordinate rings

We can use Hilbert's Nullstellensatz to describe rings of regular functions of affine varieties:

**Theorem.** If \\(X \in \mathbb{A}^n\\) is a closed subvariety, then
\\[
\mathcal{O}_X(X) \simeq k[x_1, \dotsc, x_n]/I(X).
\\]

**Definition.** One customarily calls \\(k[x_1, \dotsc, x_n]/I(X)\\) the *coordinate ring* of the
affine variety \\(X\\), .

The coordinate ring of an affine variety over an algebraically closed field \\(k\\) satisfies two
conditions:
1. it is a finitely generated \\(k\\)-algebra; and
2. it is an integral domain.

It turns out that a ring satisfying these two conditions is the coordinate ring of some variety
\\(X\\), and that there is a functor between affine varieties and the opposite of the category of
rings satisfying the above conditions, given by \\(X \mapsto k[x_1, \dotsc, x_n]/I(X)\\), which is
an equivalence of categories.

Hilbert's Nullstellensatz along with the existence of prime decompositions of radical ideals also
tells us that prime ideals of \\(k[x_1, \dotsc, x_n]/I(X)\\) are in bijection with irreducible
subvarieties of \\(X\\), and the points of \\(X\\) are in bijection with maximal ideals.

Taken together, the above results identify affine varietiex \\(X\\) with the affine schemes
corresponding to rings satisfying the above conditions. Generalising to any affine scheme
corresponds to dropping these conditions and only requiring our ring be commutative.