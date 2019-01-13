---
layout: post
title: "Confined random walk, Part I, Diffusion Equation"
date: 2019-01-15
---

We are going to obtain the probability distribution for the position of a particle subject to brownian motion in a confined box. Let us consider the diffusion equation

$$
\frac{\partial}{\partial t}P(x, t)  = D \frac{\partial^2}{\partial x^2}P(x, t)
$$

The appropriate boundary conditions for reflective barriers is

$$
\frac{\partial}{\partial x}P(0, t)  = \frac{\partial}{\partial x}P(L, t) = 0
$$

This should be understood considering that if the particle hits the wall, it will be right next to it immediately after and therefore locally the probabilities near the wall should be identical, ie, constant.

We look for factorized solution $T(t)X(x)$ first the boundary conditions. It's easy to prove that ignoring possible constant factors

$$
T_n(t) = \exp \left[-D\left(\frac{n\pi}{L}\right)^2 t \right]
$$

$$
X_n(x) = \cos \left(\frac{n \pi x}{L}\right)
$$

We write down the most general full solution with the appropriate normalization

$$
P(x, t) = \frac{1}{L} + \sum_{n=1} \alpha_n \exp \left[-D\left(\frac{n\pi}{L}\right)^2 t \right] \cos\left(\frac{n \pi x}{L}\right)
$$

from which we can also find the equilibration timescale $\tau_1 = \frac{L^2}{D \pi}$ roughly speaking the time it takes for a particle to move a distance $L$. The coefficient $\alpha_n$ are fixed by the initial conditions. One expects a similar solutions in higher dimensions as we look for factorized solutions in the other dimensions as well with identical boundary conditions. In $3$-$d$ for instance


$$
P(\mathbf{x}, t) = \frac{1}{L^3} + \sum_{n, m, l =1} \alpha_{nml} \exp \left[-(n^2+m^2+l^2) \frac{D \pi^2 t}{L^2} \right] X_{nml}(\mathbf{x})
$$

with

$$
X_{nml}(\mathbf{x}) = \cos\left(\frac{n \pi x}{L}\right) \cos\left(\frac{m \pi y}{L}\right) \cos\left(\frac{l \pi z}{L}\right)
$$


In particular the equilibration timescale is $\tau_1 = \frac{dL^2}{D \pi}$ in $d$-dimensions and it scales as $L^2$ in any dimension. The confined diffusion equation is therefore fully solved for simple diffusion.

In the next paragraph, I'll take a look the same problem in the discrete setting because I am interested in the technical problem of relating discrete and continuous models. Below, you'll see an example of effects arising purely because of discretization issues.

The discrete counterpart
-------------------------

Consider now the same problem in a discrete setting. Let us denote the discrete position with $n \in \{0, 1, .., L\}$. Then:

$$
P(n, t+1) = \sum_{n'} P(n|n') P(n', t) = P(n|n-1) P(n-1, t) + P(n|n+1) P(n+1, t)
$$

as the particle can only do a single jump at each step. Then, considering there's no preferred direction in the jumps, we find

$$
P(n, t+1) = \frac{P(n-1, t) + P(n+1, t)}{2}
$$

At the borders this is slightly different because one direction is not available, so

$$
P(n, t+1) = \cases{
\frac{P(n-1, t) + P(n+1, t)}{2} &  0 < n < L \\
\frac{P(1, t)}{2} &  n = 0 \\
\frac{P(L-1, t)}{2} &  n = L
}
$$

We look for an equilibrium solution, implicitly given by

$$
P_n = \cases{
\frac{P_{n-1} + P_{n+1}}{2} &  0 < n < L \\
\frac{P_1}{2} &  n = 0 \\
\frac{P_{L-1}}{2} &  n = L
}
$$

It turns out that there is no solution to this, meaning even with confinement there is no real equilibrium. You can check this yourself by trying to construct a solution from $P_{n+1} = 2 P_n - P_{n-1}$ satisfying all boundary conditions. Note especially that a uniform solution is not possible because once the particle hits the wall, it can only go back, so $P_1$ and $P_{L-1}$ are automatically more likely than the points at the wall. Note how this effect disappear in the continuum approximation, essentially because, I believe, the strip near the border where the probability spikes gets progressively thinner and thinner.