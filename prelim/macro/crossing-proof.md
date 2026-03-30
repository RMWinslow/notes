---
title: Crossing Proof
parent: Macro Prelim
grand_parent: UMN Prelims
math: mathjax
nav_order: 4
redirect_from:
  - /notes/econ/macroprelim/Kehoe/crossingProof.html
---

# Crossing Proof

*Used as a supporting lemma for the mean-preserving-spread comparative static
in the [McCall search problem](search.html).*

<div class="definition">
<b>Theorem</b><br>
Let \(f_1(x)\), \(f_2(x)\), and \(g(x)\) be functions of \(x\) over the real interval \(X\equiv[A,B]\). Also let \(x_1,x_2\in[A,B]\).
If:
<ul style="margin-top: 0em">
    <li>
        For all \(x\in[0,B]\), \(f_2(x) \geq f_1(x)\),
    </li>
    <li>
        \(f_1(x)\) is  increasing, \(g(x)\) is continuous,
    </li>
    <li>
        \(f_2(A) \geq f_1(A) > g(A)\),
    </li>
    <li>
        For each \(i\),  and \(\forall x \in X, f_i(x)=g(x)\Leftrightarrow x=x_i\),
    </li>
</ul>
Then \(x_2\geq x_1\)
</div>

## Proof

If $x < x_1$,
then $f_1(x)>g(x)$.

&emsp;Let $\dot{x} \equiv  \inf \left\\{     x\in X \mid f_1(x) \leq g(x) \right\\}$.

&emsp;If $x < \dot{x}$,
then $f_1(x)>g(x)$.

&emsp;It must be that $\dot{x}=x_1$.

&emsp;&emsp;Note that $\dot{x} > A$

&emsp;&emsp;&emsp; By the continuity of  $g(x)$,
there is an $\varepsilon > 0$
such that $g(x)< f_1(A)$
for all $x \leq A+\varepsilon$.

&emsp;&emsp;&emsp; But $f_1$ is increasing,
so for all $x\leq A+\varepsilon$,
$f_1(x)\geq
f_1(A)$.

&emsp;&emsp;&emsp; Thus for all $x\leq A+\varepsilon$,
$f_1(x) > g(x)$.
So $\dot{x} \geq A+\varepsilon$.

&emsp;&emsp;Note that if $x < \dot{x}$,
then $f_1(\dot{x})\geq
f_1(x) > g(x)$.

&emsp;&emsp;The set of $x<\dot{x}$ is nonempty,
so by the continuity of $g(x)$,
$f_1(\dot{x})\geq g(\dot{x})$.

&emsp;&emsp;If $f_1(\dot{x})> g(\dot{x})$,
then a contradiction arises:

&emsp;&emsp;&emsp; By the continuity of  $g(x)$,
there is an $\varepsilon > 0$
such that $ f_1(\dot{x}) > g(x)$
for all $x\in B_\varepsilon [\dot{x}]$.

&emsp;&emsp;&emsp; But $f_1$ is increasing,
so for all $x\geq\dot{x}$,
$f_1(x)\geq
f_1(\dot{x})$.

&emsp;&emsp;&emsp; Thus for all $x\leq \dot{x}+\varepsilon$,
$f_1(x)\geq
f_1(\dot{x}) > g(x)$.

&emsp;&emsp;&emsp; And so $\dot{x}$
is not the infimum of $\left\\{     x\in X \mid f_1(x) \leq g(x) \right\\}$. ↯.

&emsp;&emsp;Therefore $f_1(\dot{x})=g(\dot{x})$,
which implies that $\dot{x}=x_1$.

So if $x < x_1$
then $f_2(x)\geq
f_1(x) > g(x)$.

And $f_2(x_2)=
g(x_2)$,
so by contrapositive,
$x_2 \geq x_1$.


## But also, I mean, just look at it.

<table>
    <col><col width="169px">
    <tr> <td> If you shine a beam (\(g\)) up at two continuous barriers, and one barrier (\(f_1\)) is always on top of the other (\(f_2\)), then the beam will strike the barrier on the bottom first.</td><td>  <img src="img/laser1.png" width="169px"></td></tr>
    <tr><td>To strike the top barrier first, the beam has to make it through a gap in the bottom barrier without striking it. This kind of gap doesn't work because \(f_1\) is increasing. </td><td><img src="img/laser2.png"></td></tr>
    <tr><td>And this kind of gap doesn't work because to fly through it, the beam would have to travel to the left, which it can't do because it's a continuous function of \(x\). Even if we wiggle the beam a bit, it can't go left. So even if we allow for discontinuities, the beam can't get through. </td><td><img src="img/laser3.png"></td></tr>
</table>
