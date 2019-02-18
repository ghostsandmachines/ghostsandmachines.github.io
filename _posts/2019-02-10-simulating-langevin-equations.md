---
layout: post
title: "Handling Langevin equations 101, Part I: Simulating Trajectories"
date: 2019-02-09
tags: simulation langevin-series discrete-continuous-map stochastic-equations
---

Continuous limits are cool because many discrete processes have the same continuous limit and therefore you don't have to bother with keeping track of all the differences in the models you consider. In fact more generally, it's the presence of some quantities going to infinity that washes over the many different details of different models. A similar logic underlies the discovery of universality, a staple of modern statistical physics, and in that case it's the correlation length that diverges and make several models exhibit identical behavior near criticality. We marvel at such phenomena, but in fact ultimately they aren't much different conceptually from your 2<sub>nd</sub> year exercises on sequences of functions: as $n \rightarrow \infty$, $f_n(x, p)$ with parameter $p$ will usually converge to few functions depending on the range of $p$ and importantly many parameters will have the same limit form $f(x)$ for all $p$ in a set $\Delta$, so that the function sequence will have few limit forms corresponding to few parameter regions. 

A simple but important effect of the continuous limit shows up in the basic theory of stochastic processes. Consider the following simple random dynamical systems:

$$
x_{n+1} = x_n + \Delta x_n
$$

with $\Delta x_n$ extracted randomly from a distribution $P(\Delta x)$ identical for all $n$. This is a simple process with independent increment. It's clear that one can choose any distribution whatsoever for $\Delta x$, but this is not true in the continuous case. If you want independent increments, such increments must be sampled from a precise distribution. Why?

Consider the discrete setting still and

$$
x_{n} - x_0 =  \sum_{k=0}^{n_1} \Delta x_k
$$

For $n$ sufficiently big, $x_{n} - x_0$ must be distributed according to a gaussian distribution because of the central limit theorem as the increments $\Delta x_k$ are all independent. But in the continuous case, any increment can always be seen as the sum of infinite independent increments and therefore it must be distributed according to a gaussian.

$$
x(t+\Delta t) - x(t) =  \sum_{k=0}^{n_1} [x(t+k \cdot dt + dt) - x(t+k \cdot dt)]
$$

with $\Delta t = n \cdot dt$ with $n$ big (or small) as we please and $dt$ changing keeping $\Delta t$ fixed.

Any gaussian distribution is fixed by two parameters only, the mean $\mu$ and the variance $\sigma^2$. Let us focus on $\sigma^2$, which in fact is $\sigma^2(t)$. From the previous equation

$$
\mathrm{Var}[x(t+\Delta t) - x(t)] =  n \mathrm{Var}[x(t+dt) - x(t)] = \Delta t \frac{\mathrm{Var}[x(t+dt) - x(t)]}{dt}
$$

In order to obtain finite variance, we must have:

$$
\lim_{dt \to 0} \frac{\mathrm{Var}[x(t+dt) - x(t)]}{dt} = D
$$

This limit is well-known, but still highly non-trivial conceptually as it implies non-differentiability of the trajectory. Note that it's effectively a consequence of assuming the same dynamics at any scale $dt$.

Now imagine simulating such stochastic process. Of course any simulation is necessarily discrete. Pick a timestep $dt$ and generate the trajectory with the usual difference equation

$$
x_{n+1} = x_n + \Delta x_n
$$

$\Delta x_n$ is extracted from a gaussian distribution with variance $dtD$. It's easy to exploit the fact $N(\mu, \sigma^2) \approx \mu + \sigma N(0, 1)$ to rewrite the equation as

$$
x_{n+1} = x_n + \sqrt{dtD}\eta
$$

with $\eta$ extracted from a normal distribution $N(0, 1)$. It's clear that in this case $\langle x(t) \rangle$ is always equal to the initial position. To add a generic dynamic in the mean, also called the deterministic dynamics, simply consider:

$$
x_{n+1} = x_n + dt f(x_n) + \sqrt{dtD}\eta
$$

This is the basic equation to have in mind before embarking on more complicated scenarios and it's the one you use when you want to simulate stochastic trajectories.