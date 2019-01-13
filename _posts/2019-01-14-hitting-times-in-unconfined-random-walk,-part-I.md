---
layout: post
title: "Hitting times in unconfined random walk, Part I"
date: 2019-01-14
---

Let us consider $\Pi(t, \mathbf{x_0}, \mathbf{x})$, the probability of hitting location $\mathbf{x}$ for the first time in a time $t$, starting from location $\mathbf{x_0}$, in a box of side $L$. For now, we are thinking about these quantities as describing a discrete lattice. I want to talk about two ways of solving first-passage time problems. We'll start with the classic idea of absorbing surfaces and work out in detail a pedagogical example.

Solving hitting times with absorbing barriers
---------------------------------------------

The main problem about using the usual diffusion equation

$$
\frac{\partial}{\partial t}P(\mathbf{x}, t)  = D \Delta_{\mathbf{x}}P(\mathbf{x}, t)
$$

in order to understand the first-passage time problem is that $P(\mathbf{x}, t)$ gives the probability of the particle being in position $\mathbf{x}$ at time $t$ without any constraint on what happened before, ie, the particle might have hit position $\mathbf{x}$ many times before $t$ as well. To get around this problem, the idea is to add specific boundary conditions to the diffusion equation:

$$
\frac{\partial}{\partial t}P(\mathbf{x}, t) & = D \Delta_{\mathbf{x}}P(\mathbf{x}, t) 
$$

$$
P(\mathbf{x}, t) & =  0 \quad \forall \mathbf{x} \in \partial \omega
$$

with $\partial \omega$ being the surface of a specified volume $\omega$. This surface is an absorbing barrier: in this problem, whenever the particle touches the surface, it gets absorbed out of space in which it is moving about. At any time $t$ the particle is either in a position $\mathbf{x}$ out of the absorbing volume or it has been absorbed by the barrier:

$$
\int_{V \setminus \omega} P_c(\mathbf{x}, t) d \mathbf{x} + P_{ABS}(t) = 1
$$

so $P_c(\mathbf{x}, t)$, the solution of the diffusion equation with the appropriate boundary conditions, is NOT normalized in this case. $P_{ABS}(t)$ is the probability of the particle having been already absorbed before $t$. On the other hand $1-P_{ABS}(t)$ is usually called the surviving probability. If you think about it for a second, the probability of having been absorbed before $t$ $P_{ABS}(t)$ is exactly the probability that the particle has hit the barrier before time $t$, ie, the cumulative distribution of the first-passage times. Then:

$$
\Pi(t, \omega) = - \frac{\partial}{\partial t} \int_{V \setminus \omega} P_c(\mathbf{x}, t) d \mathbf{x}
$$

This equation gives a recipe for finding the distribution of hitting times: first, solve the diffusion equation with the appropriate boundary conditions, then derive and integrate in the manner above. If you want the hitting time distribution for a particular location, choose $\omega$ as the a small volume around target $\mathbf{x}$ of linear size roughly the size of the particle.

Next, we are going to apply the recipe above to the classic one-dimensional absorbing barrier problem, perhaps the simplest calculation you can carry through exactly. This is already interesting because it shows some rather non-trivial properties of the distribution of hitting times, like heavy-tailedness.

In this problem the particle is confined to diffuse only on the positive $x$-axis and whenever it touches $x=0$ the particle is absorbed out of the picture. In mathematical terms, this is written as

$$
\cases{
\frac{\partial}{\partial t}P(x, t)  = D \frac{\partial^2}{\partial x^2}P(x, t) \\
P(0, t) = 0 \\
P(x, 0) = \delta(x-x_0)
}
$$

We encode the initial condition with the use of dirac deltas

$$
\cases{
\frac{\partial}{\partial t}P(x, t)  - D \frac{\partial^2}{\partial x^2}P(x, t) = \delta(t)\delta(x-x_0) \\
P(0, t) = 0 
}
$$

It might be not immediately obvious that adding dirac deltas this way in the diffusion equation fixes also the initial condition. You could convince yourself by working out the free diffusion problem first but in general, it's quite clear that dirac deltas in differential equation encode boundary conditions of various kinds, as such pseudo-functions are zero everywhere except on some fixed specific points so the equation and the dynamics remains the same everywhere except on those points. This example is slightly more contrived than usual I think, but here's a general proof with differential operator $\hat{\xi_x}$. Start with $\frac{\partial}{\partial t}P = \hat{\xi_x} P+ f_0(x)\delta(t)$,  then $P(x,t) = \int_0^t \hat{\xi_x}  P(x, t') dt' + \int_0^t f_0(x)\delta(t') dt'$ and $ P(x, t) = \int_0^t \hat{\xi_x}  P(x, t') dt' + f_0(x)$. Since the first term vanishes for $t \rightarrow 0$, we have proved that adding the term $f_0(x)\delta(t)$ forces the solution to have $f_x(0)$ as the initial condition. In our case $f_x(0) = \delta(x-x_0)$ which may add technical difficulties, but I think that the 'proof' is satisfying otherwise.

Why going through all this trouble with dirac deltas? It turns out they simplify finding the right solution rather often. It happens all the time that in solving a differential equation you find a very general solution expressed a linear combination of solutions and then you have to work out the coefficient of the combination that give you the appropriate initial or boundary conditions, but this job is automatically done by the dirac delta here.

Let's move to the $s$-domain with the Laplace transform. The equation becomes:

$$
sL(x, s)  - D \frac{\partial^2}{\partial x^2}L(x, s) = \delta(x-x_0) 
$$

We are going to solve this equation by joining together two solutions for $x > x_0$ and $x < x_0$. In order to do this, we need a prescription for joining the solutions together as well. Continuity is one natural prescription. Furthermore, by integrating the equation above around $x_0$, it is easy to find:

$$
L'(x_0^{+}, s)- L'(x_0^{-}, s) = \frac{1}{D}
$$

meaning the spatial derivative of the laplace transform must be discontinuous. Keeping in mind these prescriptions to join the solutions, we find them both by considering the equation above in the desired range. We obtain:

$$
\frac{\partial^2}{\partial x^2}L(x, s) = \frac{s}{D}L(x, s)
$$

Taking account normalization, the equation has the following general solution:

$$
L(x, s) = \cases{
A \exp \left[-\sqrt{\frac{s}{D}}x \right] & x > x_0 \\
B \exp \left[+\sqrt{\frac{s}{D}} x \right] + C\exp \left [-\sqrt{\frac{s}{D}} x \right] & x < x_0
}
$$

Next, insert the absorption condition $P(0, t) = 0 \iff L(0, s) = 0$ and therefore $B = -C$.

$$
L(x, s) = \cases{
A \exp \left[-\sqrt{\frac{s}{D}}x \right] & x > x_0 \\
B \sinh \left[\sqrt{\frac{s}{D}} x \right]  & x < x_0
}
$$

Finally $A$ and $B$ can be found imposing the joining conditions, ie, continuity of the function and discontinuity of the derivative equal to $\frac{1}{D}$. After quite some algebra, we obtain

$$
L(x, s) = \cases{
\frac{1}{2\sqrt{sD}} \left[ \exp \left(\sqrt{\frac{s}{D}} (x_0 - x) \right) - \exp \left(-\sqrt{\frac{s}{D}} (x_0 + x) \right) \right]   & x > x_0 \\
\frac{1}{2\sqrt{sD}} \left[ \exp \left(\sqrt{\frac{s}{D}} (x - x_0) \right) - \exp \left(-\sqrt{\frac{s}{D}} (x+x_0) \right) \right]  & x < x_0
}
$$

We could try to invert this, but since this expression is full of exponential and we are interested in the distribution of first passage times, it seems smarter to perform the integral in $x$ first. We obtain:

$$
\int_0^{\infty} L(x, s) dx = \frac{1}{s} - \frac{\exp \left(-\sqrt{\frac{s}{D}} x_0 \right)}{s}
$$

Inverting the second term is not exactly a piece of cake, but it's a fairly known Laplace transform, so at worst you can just look it up on some mathematical table. At any rate, we finally obtain the surviving probability:

$$
\int_0^{\infty} P(x, x_0, t) dx = \erf \left( \frac{x_0}{\sqrt{4Dt}} \right)
$$

with $\erf$ being the error function you find studying gaussian statistics. Finally we change sign and derive this expression to obtain the distribution of hitting times:

$$
\Pi(t, x_0) = \frac{x_0}{\sqrt{4 \pi Dt^3}} \exp \left( -\frac{x_0^2}{\sqrt{4Dt}} \right)
$$

For $t \rightarrow \infty$, $\Pi(t, x_0)$ falls off $t^{-\frac{3}{2}}$, indicating a fat tail and the absence of a well-defined mean hitting time. Fat tails are notoriously discussed in a number of contexts, as they fly off our tame gaussian understanding of the world. Among other things, some particles will hit the wall with a time several order of magnitude bigger than the time it takes for most of the particles to hit the wall, highlighting the presence of very strong fluctuations.