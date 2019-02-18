---
layout: post
title: "Handling Langevin equations 101, Part II: Ito's lemma"
tags: simulation stochastic-equations
---

In the previous post, we have derived the following finite-difference equation to use in order to simulate stochastic trajectories with white noise (ie, noise adds independent contributions at each step):

$$
x(t+dt) = x(t) + f(x(t))dt + \eta \sqrt{Ddt}
$$

or

$$
dx(t) = f(x(t))dt + \eta \sqrt{Ddt}
$$

with $\eta$ extracted from a normal distribution $N(0, 1)$.

Now let us consider an observable $O(x(t))$

$$
O(x(t+dt)) - O(x(t)) = O'(x(t))dx(t) + \frac{O''(x(t))}{2}dx(t)^2 + o(dt)
$$

Because $dx(t)$ does not trivially scale linearly with $dt$, the term in $dx(t)^2$ cannot be ignored. By substituting the expression for $dx(t)$, it is immediate to prove that

$$
dO(x(t)) = O'(x(t))dx(t) + \frac{O''(x(t))}{2} \eta^2 D dt + o(dt)
$$

At this point, $\eta^2$ is typically substituted with $1$, ie, its average value. I believe there is a bit of confusion as to why and when this is true when people learn this. An easy way to shed some light on this is to actually simulate the trajectories.

Let's consider the simple scenario with $D=1$ and $dx(t) = \eta\sqrt{dt}$. This gives a prescription to simulate to generate $x(t)$. Then, let us take $O(x(t)) = \mathrm{sin}(x(t))$. We can generate $x(t)$, then insert it in $O(x(t))$ to have the $O$-trajectory. At the same time, we can generate the $O$-trajectory by making use of the prescription for $dO(x(t))$, at least provided $dt$ is small enough. We can maintain $\eta^2$ or replace with 1 and see what changes.

You can see in the figure below that the two prescription are not equivalent _for the chosen dt_. It is only in the limit of infinitesimal $dt$ that the two prescriptions will match up.

<figure>
<img src="{{ site.url }}/img/ito_bigdt.png" alt="ito_bigdt">
<figcaption><b>Fig. 1. Timestep dt = 0.1.</b> Replacing $\eta^2$ with $1$ does not give the same result. Keeping the $\eta^2$ term random instead of making it deterministic gives better matching to the exact result.</figcaption>
</figure>

Analytically this is seen by considering

$$
| dO_1(x(t)) - dO_{\eta}(x(t)) | = \frac{1}{2} |O''(x(t))| |  1 - \eta^2 | dt
$$

which does vanish as $dt$ approaches zero. This argument did bother me for some time when I first saw it. It seemed that the vanishing of the difference didn't matter really because of course the difference gets smaller as $dt$ get smaller, but the relative difference won't and that is what truly matters (otherwise it's all equivalent to a global time rescaling). Let us consider the relative difference then:

$$
\frac{ | dO_1(x(t)) - dO_{\eta}(x(t)) |}{dO_{\eta}(x(t))} = \frac{1}{2} \frac{ O''(x(t)) (1 -\eta^2 ) dt}{ O'(x(t))\eta\sqrt{dt} + \frac{1}{2}O''(x(t)) \eta^2 D dt}
$$

As $dt \rightarrow 0$ the numerator vanishes as $dt$, _while the denominator vanishes as_ $\sqrt{dt}$. The relative difference scales as $\sqrt{dt}$ and truly vanishes as $dt \rightarrow 0$.

<figure>
<img src="{{ site.url }}/img/ito_smalldt.png" alt="ito_smalldt">
<figcaption><b>Fig. 2. Timestep dt = 0.001. </b> Replacing $\eta^2$ with $1$ does give the same result when $dt$ is small enough. The black curve is perfectly superimposed by the other two curves. </figcaption>
</figure>

All of this tells you that can can indeed write:

$$
dO(x(t)) = O'(x(t))dx(t) + \frac{O''(x(t))}{2} D dt
$$

for $dt$ small enough. This is essentially the celebrated Ito's lemma, modifying the usual rules of calculus when dealing with random variables. In the next post, I am going to write down stochastic equations in the usual symbolic notation, make a few comments on why they are both useful and ambiguous and clarify the differences and connections between the Stratonovich and the Ito conventions.