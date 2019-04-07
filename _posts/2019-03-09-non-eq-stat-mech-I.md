---
layout: post
title: "A primer on non-equilibrium statistical physics, Part I"
date: 2019-03-09
tags: statistical-mechanics non-equilibrium-series time-reversibility
---

I remember coming across the notion of thermodynamic equilibrium in the standard undergraduate thermodynamics classes and spending entire afternoons trying to find once and for all a definition that was both intuitive and rigorous, but embarassingly I failed. Abstract definitions involving thermodynamic potentials seem rigorous, but they either give little physical intuition or are downright circular. More supposedly concrete definitions seem riddled with exceptions and poorly-defined underlying concepts. In the end I settled for some vague notion of time independence of the system macro-observables, shut up and went through the required exercises for the exam. I did notice that I wasn't quite alone in my confusion, despite the subject being almost 200 hundred years old, as for one all kinds of questions on the axioms of thermodynamics pop up regularly on physics stackexchange and for another reservations about the notion of thermodynamic equilibrium are made all the time, as the wiki page summarizes well. I made a note of coming back to the issue and think about it through the years.


The simple starting point of this series is the fact that equilibrium is not  stationarity. It's not just things being time independent. Non-equilibrium stationary states (NESS) are entirely possible and quite common in nature in fact and I don't think this is emphasised enough. Rather, equilibrium has something to do with the notion of time reversibility and this is what we are going to refresh. 

Time-reversibility in deterministic systems
------------------------------------------

Much of modelling consists of writing down a differential equation for our variable of interest $x$ (possibly a vector of multiple variables):

$$
\frac{dx}{dt} = f(x(t))
$$

Roughly-speaking, it is tempting to say that the system satisfies time reversibility if for any solution $x(t)$, there is a solution $x(-t)$. This is quite a sloppy way of putting it, though. A dynamical solution is defined by both the evolution equation and the initial conditions. A better way of formalizing the idea of reversibility is to say that for given solution $\\{x_0, x(t)\\}$, there is $x_0^{\ast}$ such that $\\{x_0^{\ast}, x(-t)\\}$ is a solution. But notice that $x_0^{\ast}$ cannot be anywhere on the $x(t)$ trajectory or it will simply follow the forward solution instead of going back (assuming uniqueness). If that is the case, it is not possible to move from $x_0^{\ast}$ to $x(-t)$, not right after $t=0$ at any rate preserving continuity. This suggests that the correct way of formalizing time reversibility is to say that for given solution $\\{x_0, x(t)\\}$, there is $x_0^{\ast}$ such that $\\{x_0^{\ast}, x^{\ast}(-t)\\}$ is a solution.

This definition seems a bit disappointing at first because the 'asterisk' operation seem fairly arbitrary. Let us consider the classic example to clear up some confusion. Let $x = (\mathbf{q}, \mathbf{p})$, ie, the positions and momenta of a system of particles obeying the usual laws of classical mechanics. Start from $(\mathbf{q_0}, \mathbf{p_0})$, evolve with $(\mathbf{q}(t), \mathbf{p}(t))$ until time $T$. Then, we know that if we take as initial conditions $(\mathbf{q}(T), -\mathbf{p}(T))$, we will have $(\mathbf{q}(T-t), -\mathbf{p}(T-t))$ as a solution. In this case, the 'asterisk' operation is the sign flip of the velocities. Note that acting twice on the state $x = (\mathbf{q}, \mathbf{p})$ gives the original state, ie, the 'asterisk' operation is an involution.

If we describe such operation with the use of an operator $\pi$ acting on the state space, we can finally say quite generally that a dynamical system is time-reversible if its time evolution operator $U_t$, such that $U_t x_0 = x_t$ satisfies the equation

$$
U_{-t} =  \pi U_t \pi
$$

To prove this equation, simply translate the steps illustrated above in the operator language. A bit loosely, this equation says that going back from a state is like going forward from another state. As you see, the notion of reversibility feels quite intuitive, but a precise definition is fairly abstract.

There are lots of cool properties about time-reversible dynamical systems. For instance given a fixed point

$$
x_{fp}= U_t x_{fp} \qquad \forall t
$$

act on it with the operator $\pi$ and obtain

$$
\pi x_{fp} = \pi U_t x_{fp} = U_{-t} \pi x_{fp}
$$

which proves that $\pi x_{fp}$ is also a fixed point (just act with $U_t$ on both sides now). A related simple question that is natural to ask is whether fixed points can exist at all for time-reversible systems. Attracting fixed points go a little bit against our untrained intuition of time-reversibility for instance, as many initial conditions collapse eventually onto the same state. It turns out that it's completely possible to have such fixed points in time-reversible systems. The absence of attracting fixed points requires additional structure, such as the presence of conserved quantities along the trajectories. This tells us once again that time-reversibility presents a number of subtleties and one must be careful.

Time-reversibility in stochastic systems
------------------------------------------

In a probabilistic setting, time reversibility is interestingly easier to define formally. The idea is simply that any trajectory and its time-reversed version have identical probabilities, whether the time-reversed version involves an involution operation or not (that'll depend on the problem):

$$
P(x_0, t_0; x_1, t_1; .. ; x_k, t_k) = p(x_k, t_0; x_{k-1}, t_1; .. ; x_0, t_k)
$$

$$
P(x_0, t_0; x_1, t_1; .. ; x_k, t_k) = p(x_k^{\ast}, t_0; x_{k-1}^{\ast}, t_1; .. ; x_0^{\ast}, t_k)
$$

If you break down the stochastic evolution of the system into a determistic part and a noisy one, it's apparent that the first equation makes sense only because of the noisy part. Otherwise we can apply the argument made before and argue that different initial conditions cannot possibly evolve over the same trajectory. 

If the system is Markovian, the joint probability factors into a product of conditional probabilities and one can prove easily that the above conditions is equivalent to 

$$
P(x', t_1 | x, t_0)P(x, t_0) = P(x, t_1 | x', t_0)P(x', t_0)
$$

or even better consider infinitesimal time differences

$$
w(x', x)P(x, t) = w(x, x')P(x', t)
$$

with $w(x', x)$ being the rates fixing Markovian evolution. Finally let us recall that for Markovian systems $P(x, t)$ obey the master's equation:

$$
\frac{\partial}{\partial t} P(x, t) = \sum_{x'} w(x, x')P(x', t) - w(x', x)P(x, t)  
$$

therefore if the equation for time reversibility is satisfied, we find ourselves automatically in a stationary state. This stationary state is peculiar precisely because of the equation:

$$
w(x', x)P_{eq}(x) = w(x, x')P_{eq}(x')
$$

which is the celebrate detailed-balance condition. Any stationary state satisfying this condition is called an equilibrium state, but as you can see the master's equation has in principle stationary solutions NOT satisfying detailed balance and in that case we will speak of non-equilibrium stationary states (NESS).

Some other important observations:

1. In order to check for detailed balance, it is not actually necessary to find the stationary distribution. [Kolmogorov's criterion](<https://en.wikipedia.org/wiki/Kolmogorov%27s_criterion>) gives a way to verify detailed balance solely through the knowledge of the transitions rates. Detailed balance is a dynamical property of the system.
2. To check whether or not we find ourselves at equilibrium, we always need dynamical measurements. The knowledge of P_s(x) is not sufficient as equilibrium is a property of  the probability distribution of the full trajectories.

An elementary example of the second point is given in the figure below.

<figure>
<img src="{{ site.url }}/img/irreversibility.png" alt="irreversibility">
</figure>

Both graphs represent 3-state markov processes. In the first case, transitions occur in any directions, in the second one only in the clockwise direction (the system is stochastic in the holding times). Let us assume that the stochastic nature of the jumps is captured by a single parameter only, a timescale effectively. Holding times are identical for all states, jumps are equally likely in any directions. It is immediate to prove that both processes end up in the uniform stationary state $P(A) = P(B) = P(C) = \frac{1}{3}$. Yet only only in the first process the stationary state is genuinely equilibrium as detailed balance is satisfied. The static marginal statistics are identical, but dynamically the processes are quite different.

I think that it should be much clearer conceptually what equilibrium actually means now. It is still an open question to characterize more physically the distinction between a system in equilibrium and out of equilibrium. What phenomena are common in one situation and uncommon in the other one? What is impossible in one case and what becomes possible in the other? In particular, what kind of phases are there in out-of-equilibrium systems? What kind of phase transitions? What kind of universality classes? How do such systems respond to slight perturbations? We've seen already that sometimes identical distribution can characterize simultaneously equilibrium and out-of-equilibrium systems, so we also know that even identifying out-of-equilibrium systems isn't necessarily trivial. In the next post, I will talk about what is perhaps the most important signature of equilibrium systems, the fluctuation-dissipation theorem. 