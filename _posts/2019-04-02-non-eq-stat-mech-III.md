---
layout: post
title: "A primer on non-equilibrium statistical physics Part III, Derivation of The Fluctuation-Dissipation Theorem"
date: 2019-04-02
tags: statistical-mechanics non-equilibrium-series fluctuation-dissipation-theorem
--- 

In the following, I am going to give a derivation of the fluctuation-dissipation theorem discussed in the previous post and you can find the exact statement of the theorem over there. The main point of this post is to go through what it takes technically to derive this and similar results.

We are going to start from the master equation of the perturbed system ($h \neq 0$) in matrix form:

$$
\frac{\partial}{\partial t} G^h(t, t_0) = W^h(t) G^h(t, t_0)
$$

$$
W^h_{kn} = w^h_{kn} - \delta_{kn} \sum_m w^h_{mk}
$$

Let us remember the way we perturb the transition rates:

$$
w^h_{kn}(t) = w_{kn}(t) \cdot \mathrm{exp}[\beta h f(t) \chi_{kn}] \approx w_{kn}(t) + w_{kn}(t) \beta h f(t) \chi_{kn}
$$

Such perturbation propagates to the evolution matrix in the following way

$$
W^h_{kn} = W_{kn} + \beta h f(t) [w_{kn} \chi_{kn} - \delta_{kn} \sum_m w_{mk} \chi_{mk}] + o(h)
$$

and more compactly we define a matrix $\nu_{kn}$ that you can read off combining the equations above and below:
$$
W^h_{kn}(t) - W_{kn}(t) = h \nu_{kn}(t) + o(h)
$$

The next step consists of applying time-dependent perturbation theory. If you are familiar with quantum mechanics, the same perturbatory methods apply identically to the matrix master equation above. If you are not, it takes a while to get the hang of it admittedly. You can google _interaction picture_ and _Dyson series_, though I'm sure there must be some easier explations of perturbation theory for the matrix master equation without all the jargon of quantum mechanics. Perhaps I'll make a post myself in the future about this.

At any rate to first-order time dependent perturbation theory says:

$$
G^h(t, t_0) = G(t, t_0) + h G(t, t_0) \int_{t_0}^t G^{-1}(t', t_0) \nu (t') G(t', t_0) dt' + o(h)
$$

In principle this is where we should start when analysing the linear response theory of any kind of time-dependent perturbation: $f(t)$ might be an oscillatory function or say behave logistically with time. In our case, $f(t)$ is a Dirac-delta $\delta(t-t_p)$. This allows us to kill the integral and obtain:

$$
G^h(t, t_0) = G(t, t_0) + h G(t, t_p) \nu (t_p) G(t_p, t_0) + o(h)
$$

Let us now start considering the perturbed observable:

$$
\langle M(t) \rangle_h = \sum_{k, l} M_k G^h_{kl}(t, t_0) P_l(t_0)
$$

$$
R(t) = \sum_{kl} M_k G_{ka}(t, t_p) \nu_{ab} (t_p) G_{bl}(t_p, t_0) P_l(t_0)
$$

or

$$
R(t) = \sum_{kl} M_k G_{ka}(t, t_p) \nu_{al} (t_p) P_l(t_p)
$$

plugging in the expression for $\nu$ and relabelling

$$
R(t) = \beta \sum_{klm} M_k [G_{km}(t, t_p) - G_{kl}(t, t_p)] w_{ml}(t_p) \chi_{ml} P_l(t_p)
$$

This is a fairly general expression for on-and-off switch in Markov processes as we have not specified $\chi_{ml}$ yet. For our theorem $P_l(t_p)$ is meant to be the equilibrium distribution, ie, in $t_p$ we were already at equilibrium, although of course this expression holds regardless of this fact.

We are halfway through the theorem basically, having considered the response function. Let us now move on to the correlation function of the _unperturbed_ system.

$$
C(t, t_p) = \sum_{kl} M_k M_l G_{kl}(t, t_p) P_l(t_p)
$$

$$
\frac{\partial}{\partial t_p} G_{kl}(t, t_p) = \sum_m w_{ml}[G_{kl}(t, t_p) - G_{km}(t, t_p)]
$$

$$
\frac{\partial}{\partial t_p} C(t, t_p) = \sum_{klm} M_k M_l [G_{kl}(t, t_p) - G_{km}(t, t_p)]  w_{ml}P_l(t_p) + A(t, t_p)
$$

The function $A(t, t_p)$ comes from the time derivative in $t_p$ of $P_l(t_p)$ and it's easy to see that it vanishes if at $t_p$ we are in equilibrium by enforcing detailed balance. This is our setting so we are going to write:

$$
\frac{\partial}{\partial t_p} C^{eq}(t, t_p) = \sum_{klm} M_k M_l [G_{kl}(t, t_p) - G_{km}(t, t_p)]  w_{ml}P_l^{eq}
$$

At this point we are going to make use of another part of the hypothesis, the time-independence of the transition rates $w_ml$. If this condition holds, $C^{eq}(t, t_p) = C^{eq}(t - t_p)$ and therefore:

$$
\frac{\partial}{\partial t} C^{eq}(t, t_p) = - \sum_{klm} M_k M_l [G_{kl}(t, t_p) - G_{km}(t, t_p)]  w_{ml}P_l^{eq}
$$

At this point we are essentially done. Go back to the expression for the response function, plug in $\chi_{ml} = \frac{M_m - M_l}{2}$ and after some indeces manipulation and applying once again detailed balance we shall find the thesis of the theorem:

$$
R(t) = - \beta \frac{\partial}{\partial t} C_{eq}(t, t_p)
$$

Some head-scratching might appear fairly natural here because it looks as though the theorem holds only for a very specific choice of $\chi_{ml}$, which is fine mathematically, but physically it seems to make the result rather weak. In fact this is not true because this choice is strongly suggested by the way the field usually appears in the hamiltonian (see previous post). On the other hand, it is true that more generally you could think about the field coupling say to the square of $M(X)$ say or even systems where it's not quite clear whether the hamiltonian concept even make sense. I'll admit I don't know whether in that case some version of the fluctuation-dissipation theorem still holds and I shall think about these issues (I'm fairly sure that at least part of the story consists of simply choosing the right $M(X)$ variable coupled to the field). 