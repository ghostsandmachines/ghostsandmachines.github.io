---
layout: post
title: "Hitting times in unconfined random walk, Part II"
date: 2019-01-14
---

The purpose of this post is to derive a differential equation directly for the hitting times distribution, skipping the steps devoted to solving the diffusion equation with various absorbing conditions. Along the way, we derive an expression for the probability of a particle hitting any specified target in the limit $t \rightarrow \infty$. It turns out the behavior of this probability is highly dependent on the dimensionality of the space.

A differential equation for the distribution of hitting times
-------------------------------------------------------------

Let us start from the following trick:

$$
\Pi(t, \mathbf{x_0}, \mathbf{x})  = \sum_{\mathbf{x'} \in B(\mathbf{x_0})} \frac{1}{2d} \cdot \Pi(t-1, \mathbf{x'}, \mathbf{x})
$$

What we've done here is we've written the hitting time probability as the probability of making the first step in a specific neighbour of $\mathbf{x_0}$ times the probability of hitting $\mathbf{x}$ in $t-1$ steps after that. Spatial homogeneity and isotropy make for a particularly easy equation in this case, but the concept in general. In order to find out information about the form of hitting times distribution or absorbing states probabilities, think about the way these probabilities change when the initial condition changes and you will find precise constraint on your probability function by considering recurrence relations.

Consider first the case $t \rightarrow \infty$ as it's one of the main differences with the confined random walk and it's also easier to solve, as there isn't any time difference anymore in the two sides of the equation. What does it mean to hit our location at infinity? It means NOT hitting the location, we are going to compute the probability of never hitting $\mathbf{x}$. Obviously this is possible only if the particle can diffuse to infinity, which is not true for finite boxes. We are going to re-write the equation in the following way:

$$
\Pi_{\infty}(\mathbf{x_0}, \mathbf{x})  = \sum_d^D \frac{1}{2d} \cdot \left [ \Pi_{\infty}(\mathbf{x_0}+a \mathbf{e_d}, \mathbf{x}) + \Pi_{\infty}(\mathbf{x_0} - a \mathbf{e_d}, \mathbf{x}) \right] 
$$

The next step is to take the continuous limit $a \rightarrow 0$. Mathematically, this is allowed if $\Pi_{\infty}$ changes little over linear sizes $a$. What is physically the natural scale over which this probability (and others) essentially does not change? It's roughly the size of the particle. It's obvious that the very concept of position of a particle makes sense only with respect of the space it occupies. For instance, if a spherical particle has a $1\mu m$ radius, the probability of the particle occupying position  $(1 \mu m, 1\mu m)$ and $(1.001\mu m, 1.001\mu m)$ is essentially the same because if a portion of the particle occupies the first position, it's almost certain that the rest of the particle will somehow occupy the second position.

With this in mind, we obtain immediately the following equation by expanding in $a$ and keeping only the first term different from zero:

$$
\Delta_{\mathbf{x_0}} \Pi_{\infty}(\mathbf{x_0}, \mathbf{x})  = 0
$$

<p>the operator $\Delta$ being the Laplacian. Now, as we are studying a simple random walk,  $\Pi_{\infty}(\mathbf{x_0}, \mathbf{x})$ must depend only on $| \mathbf{x_0} - \mathbf{x} |$ by homogeneity and isotropy. This should be pretty obvious physically, just imagine translating or rotating the whole system and ask yourself if anything changes. Once again, the presence of a wall ($L \neq \infty$) breaks such symmetries, although well-deep within the wall they will hold approximately. At any rate, we can write:</p>

$$
\Delta_{\mathbf{r}} \Pi_{\infty}(r)  = 0
$$

with $\mathbf{r}$ being the distance vector between the desired initial and final location. The equation is easily solvable in any dimension by considering the Laplacian in spherical coordinates.

$$
\frac{1}{r^{D-1}} \frac{\partial}{\partial r} \left [ r^{D-1} \frac{\partial}{\partial r} \Pi_{\infty}(r) \right] = 0
$$

If $D > 2 $ one obtains

$$
\Pi_{\infty}(r) = \frac{A}{r^{D-2}} + B
$$

With $A$ and $B$ constants to be determined. If initially the two locations were at infinity from each other, the particle can't ever reach its destination, no matter how much we wait, implying $B = 0$. Furthermore, $A^D$ must be a length in order to have a dimensionless probability. The only length in the problem is $a$, roughly the linear size of the particle and therefore:

$$
\Pi_{\infty}(r) =\left ( \frac{a}{r} \right)^{D-2} 
$$

with $r > a$ implicitly. If $D \leq 2 $ one obtains easily that $\Pi_{\infty}(r)$ can only be a constant and therefore the behavior at $r \rightarrow \infty$ determines everything else, ie, $\Pi_{\infty}(r) = 0$. Then, if  $D \leq 2 $ the particle eventually hits the desired location for any final initial distance. All in all:

$$
\Pi_{\infty}(r) = \cases{
0 & D\ge 2 \cr
\left ( \frac{a}{r} \right)^{D-2} & D > 2 \cr
}
$$

The case $D \leq 2$ deserves some further discussion. In 1-d this is a well-known result, in fact, as the problem is formally equivalent to the gambler's ruin problem with a fair coin. Imagine the position on the $x$-axis represent your current wealth. Start from an arbitrary position, ie, some arbitrary wealth. At each toss, you can gain a dollar or lose a dollar with a probability $\frac{1}{2}$. What is the probability of eventually reaching $0$, ie, the probability of eventually going broke? This is $1$, no matter your initial wealth and we proved this result above, albeit a bit more tortuously than normal. In 2-d, I admit that I don't have a good intuition for this result. I can start muttering about topology and say that apparently the space of possible trajectories doesn't grow fast enough with time to compensate for how fast the particle explores the lattice, but the results still feels counterintuitive to me. If you have a convincing easy explanation, please let me know.

Let us now consider the problem with time. Actually, we can repeat the same steps following the starting recurrence relation, making time continuous as well and obtain:

$$
\frac{\partial}{\partial t}\Pi(t, r)  = \frac{a^2}{\tau} \Delta_{\mathbf{r}}\Pi(t, r) = D \Delta_{\mathbf{r}}\Pi(t, r)
$$

$\tau$ plays a similar role to $a$ for time, indicating the timescale over which $\Pi(t, \mathbf{r})$ is constant. $D$ is the diffusion constant, *not* the dimension obviously. In this equation $\Pi(t, r)$ is a probability density, not a probability. The normalization and boundary conditions are:

$$
\eqalignno{
\Pi_{\infty}(r) & + \int_0^{\infty} \Pi(t, r) dt = 1 \cr
\Pi(t, 0) &  = \delta(t)
}
$$

as if the particle is already in the desired location, we are done.

How would one go about solving this equation?  It looks very similar to Schrodinger's equation in free space, so it's tempting to think about in terms of a spectrum problem. If

$$
 \Delta_{\mathbf{r}}\Pi_k(r) = -\lambda_k \Pi_k(r)
$$

then in general

$$
\Pi(t, r) = \sum_k \alpha_k \exp (-t D \lambda_k) \Pi_k(r)
$$


and therefore we have to solve the spectrum of the Laplace operator in the case of spherical symmetry. Note that we look for negative eigenvalues only in order to avoid blow-ups in time which are forbidden by normalization. We know from the previous section, though, that heavy-tails are to be expected in the hitting times distribution and it is not quite clear how they would come about from a superposition of exponentials. I plan on clearing up some of this confusion, but now I want to move on to random walk in confined spaces.