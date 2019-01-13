---
layout: post
title: "Confined random walk, Part II, Hitting Times"
date: 2019-01-14
---

We now proceed to study computationally the hitting time in a confined random walk. First of all, we ask the shape of the hitting times distribution. To this end, we consider a simple discrete $L \times L$ lattice, start from an initial position $\mathbf{x_0}$, run the program until the particle hits the target $\mathbf{x}$ and record the hitting time. The results in figure $1$ show an exponential distribution, a rather different result from unconfined random walk. Could we have expected this result somehow?

<figure>
<img src="{{ site.url }}/blog/img/hitting_times_all_data_fixed_distance.png" width="60%" alt="hitting_times">
<figcaption><b>Fig.1 Mean hitting time in $L \times L$ discrete lattices.</b> We have used an initial position $\mathbf{x_0} = (10,10)$ and target $\mathbf{x} = (5,5)$. The statistics is computed out of $10^3$ simulated hitting times for each $L$. The plot shows the quadratic scaling of the mean hitting time with the linear size $L$ of the lattice.</figcaption>
</figure>

From 

$$
\Pi(t, \mathbf{x_0}, \mathbf{x}) = \frac{\text{# of trajectories reaching x in t steps}}{\text{# of possible trajectories t-steps long}}
$$

we can try to think about the statistics of the trajectories. It is easy to understand that the number of possible trajectories $t$-steps long is $(2d)^t$. This is because at each step there are $2d$ possibilities and we simply consider all the possibilities each time. Technically, at the border we have fewer than $2d$ possibilities because one direction is blocked, but at any rate the number of trajectories grows exponentially with time. It seems fairly natural to think that the number of trajectories also grows somewhat exponentially, although there's really some hindsight here as this is not true for confined random walk for instance. Then:

$$
\Pi(t, \mathbf{x_0}, \mathbf{x}) \approx \left ( \frac{\alpha}{2d} \right)^{t} = \exp\left[ -\frac{t}{\frac{1}{\log \frac{\alpha}{2d}}}\right]
$$

After considering the shape of the distribution, it is interesting to investigate the dependence of the mean hitting time with the size of the lattice and the distance between the initial position and the target. We start with the first problem.

In figure $2$ we show the way $\tau$ scales with the linear size $L$ of the lattice. The scaling is quadratic and it's rationalized fairly easily if we accept that $L$ is the typical distance the particle has to travel before reaching the target. Then the typical scaling relating times and distances in brownian motion does the rest.

<figure>
<img src="{{ site.url }}/blog/img/tau_vs_L_fixed_distance.png" width="60%" alt="hitting_times">
<figcaption><b>Fig.1 Mean hitting time in $L \times L$ discrete lattices.</b> We have used an initial position $\mathbf{x_0} = (10,10)$ and target $\mathbf{x} = (5,5)$. The statistics is computed out of $10^3$ simulated hitting times for each $L$. The plot shows the quadratic scaling of the mean hitting time with the linear size $L$ of the lattice.</figcaption>
</figure>