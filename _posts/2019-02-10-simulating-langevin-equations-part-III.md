---
layout: post
title: "Handling Langevin equations 101, Part III: Integration Schemes"
date: 2019-02-10
tags: langevin-series stochastic-equations
---

Physicists like to summarize the process generating the stochastic trajectories with the following symbolic notation:

$$
\frac{dx}{dt} = A(x(t)) + B(x(t)) \xi(t)
$$

This is the real Langevin equation, with $\xi(t)$ being some random variable. Here I'm being vague on purpose, we'll clarify the nature of $\xi(t)$ soon. Why is this only a symbolic notation? Why is it still useful, though? For starters, if you go back and look at the equation we've derived and write the difference quotient:

$$
\frac{x(t+dt) - x(t)}{dt} = f(x(t)) + \sqrt{D(x(t))} \frac{\eta}{\sqrt{dt}}
$$

you'll see that $\xi(t) = \lim_{dt \to 0}\frac{\eta(t)}{\sqrt{dt}} = \infty$, therefore the equation is meaningless if taken literally. Remember $\eta$ is a random variable sampled from a normal distribution $N(0, 1)$.

On the other hand, you could simply take the equation to be a short-hand of the finite difference equation we've already described:

$$
x(t+dt) = x(t) + f(x(t))dt + \eta \sqrt{Ddt}
$$

It's not very clear why that would be particularly useful. Well, one of the cool things about writing down time evolution with derivatives instead of finite-differences is that all finite-difference schemes are perfectly identical for sufficiently small time-increments. Some of these schemes might be more computationally efficient, others give conceptual insight, at any rate we have different ways of looking at the same thing, which is always useful and the 'same thing' is represented by the equation with the derivatives.

Is this the case for stochastic evolution? Does $\frac{dx}{dt} = A(x) + B(x) \xi(t)$ or some version of it encode an identical limit of many finite-difference schemes? Note in particular that in particular the finite difference equation we have derived is only one of these schemes. In fact, let us consider the following class of finite-difference schemes:

$$
\frac{\Delta x}{\delta} = A(x+\alpha \Delta x)+B(x+\alpha \Delta x) \frac{\eta}{\sqrt{\delta}}
$$

with $\delta$ represing the finite time-increment. The parameter $\alpha$ determines the particular discretization-scheme. If $\alpha = 0$ we obtain the finite-difference equation we have used so far. Except for this specific choiche, we always have implicit equations for $\Delta x$. Are all of these schemes equivalent in the limit $dt \rightarrow 0$?

To answer this question, let us consider the mean increment:

$$
\langle \Delta x \rangle = \langle A(x+\alpha \Delta x) \rangle \delta + \langle B(x+\alpha \Delta x) \eta \rangle \sqrt{\delta}
$$

Derive and ignore higher-order terms like $\Delta x^2$. One obtains:

$$
\langle \Delta x \rangle = A(x) \delta + \alpha B'(x)\langle \Delta x \eta \rangle \sqrt{\delta}
$$

Now $\langle \Delta x \eta \rangle \sqrt{\delta}$ cannot be broken because of course the value of $\Delta x$ depends on the random value extracted with $\eta$. On the other hand if you re-insert in this 'correlation' the expression for $\Delta x$ given two equations ago and play around with the order of the terms, you will obtain $\langle \Delta x \eta \rangle \sqrt{\delta} = B(x) \delta + o(\delta)$. Therefore:

$$
\langle \Delta x \rangle = A(x) \delta + \alpha B'(x)B(x) \delta
$$

or 

$$
\frac{\langle \Delta x (x) \rangle}{dt} = A(x) + \alpha B'(x)B(x)
$$

$\Delta x (x) $ is the increment starting from $x$. This equation is highly dependent on $\alpha$, therefore the class of $\alpha$-discretization schemes _are not equivalent_. This result is kind of disappointing perhaps, as it shows that anytime you are shown an equation $\frac{dx}{dt} = A(x) + B(x) \xi(t)$, you need to specify the discretization scheme that you have in mind. The choice of a discretization scheme isn't just a computational tool with stochastic equations, it actually affects the physics of your system. This is particularly evident if instead of considering $\langle \Delta x \rangle$, you pick $\Delta x$ and prove that :

$$
\Delta x  = [A(x) +\alpha B'(x)B(x)] \delta + B(x) \eta \sqrt{\delta}
$$

which shows that changing the discretization scheme is equivalent to changing the interaction $A(x) \rightarrow A(x) + \alpha B'(x)B(x)$. You can use the usual Euler scheme with a modified interaction to generate the trajectories you'd obtain with the usual interaction but modified approximation scheme. Note that you can prove as an exercise that $\frac{ \langle (\Delta x)^2 \rangle }{dt} = B^2(x)$ for _any_ discretization scheme, so $B(x)$ is basically the diffusion coefficient.

Finally, let us reconsider the chain-rule for this class of discretization schemes:

$$
dO(x(t)) = O' \left(x(t)+\alpha dx(t)\right) dx(t) + \frac{O''\left(x(t) + \alpha dx(t)\right)}{2} dx(t)^2 + o(dt)
$$

By expanding it is easy to see that:

$$
dO(x(t)) = O'(x(t))dx(t) + \frac{O''(x(t))}{2} (1-2\alpha) dx(t)^2 + o(dt)
$$

which means that in the special case $\alpha = \frac{1}{2}$ we obtain the usual derivation rules

$$
dO(x(t)) = O'(x(t))dx(t) + o(dt)
$$

This special scheme in which we take the midpoint to integrate the expression is called the Stratonovich scheme and it's very commonly used precisely because it preserves the rules of ordinary calculus.
