---
layout: post
title: "A primer on non-equilibrium statistical physics Part II, The Fluctuation-Dissipation Theorem"
date: 2019-03-20
tags: statistical-mechanics non-equilibrium-series fluctuation-dissipation-theorem
--- 

I am going to describe the fluctuation-dissipation theorem in the abstract context of Markov chains because I think it's both simple and general enough to let people understand how far-reaching are these concepts. They are helpful when handling all kinds of system beyond the usual collections of particles you deal with in the traditional statistical mechanics curriculum.

It is true that the fluctuation-dissipation theorem (FDT) is an equilibrium result, but as far as I know any 'measure of non-equilibrium' is usually based on quantifying the extent to which the FDT is broken, so it is crucial to understand well the theorem.  

Notation for Markov chains
---------------------------

Let us label a state $X$ of the system with a discrete of numbers, $k$, $l$, $n$, etcetera. The fundamental object of any Markov process is the probability:

$$
G_{kl}(t, t_0) = \mathrm{Pr} ( X=k, t | X=l, t_0)
$$ 

Out of this conditional probability, one can in principle obtain any statistical distribution related to our system. In particular, the probability of being in state $k$ will be

$$
P_k(t, t_0) = \sum_l G_{kl}(t, t_0) P_l(t_0)
$$

To conclude this mini-review of Markov processes, let us write down the master's equation

$$
\frac{\partial}{\partial t} G_{kl} (t, t_0) = \sum_n w_{kn}(t) G_{nl}(t,t_0) - w_{nk}(t)G_kl(t, t_0)
$$

using the following matrix notation

$$
G_{kl}(t, t_0) \rightarrow G(t, t_0)
$$

$$
w_{kn}(t) - \delta_{kn} \sum_m w_{mk}(t) \rightarrow W(t)
$$

so that we obtain

$$
\frac{\partial}{\partial t} G(t, t_0) = W(t) G(t, t_0)
$$

This is not only a compact notation for a Markov process, it has also the advantage of highlighting the analogy with the Schrondinger's equation and suggesting the use of any technique we've learned in that context to attack this particular problem. Let us also note that the matrix $W$ depends on the time, ie, the transition rates depend on time, precisely because we want to model the switching on and off of a perturbation. Formally, perturbing the system means changing the transitions rates and therefore the elements of the matrix.

Perturbing the system
----------------------

How exactly shall we perturb the system, ie, how shall we modify the transition rates? This is not trivial in principle. Keep in mind, though, that in fact we are not interested in results that are highly-dependent on the particular details of the perturbation. The fluctuation-dissipation theorem should be a rather general result. 

In physics, perturbations are often modelled as external fields inducing a bias on the system, say a magnetic field $h(t)$ acting on ferromagnetic material and pushing the spins to align in the direction of the field. The hamiltonian changes to $H(X) \rightarrow H(X) - h(t)M(X)$ with $M(X)$ being the magnetization of the system.

Detailed-balance holds for equilibrium systems, implying that several different types of dynamics generate the same stationary state. In physics, this state is the boltzmann distribution $\frac{1}{Z(\beta)} \mathrm{exp}(-\beta H(X))$ and therefore transition rates obey the equation:

$$
\frac{w(X', X)}{w(X, X')} = \mathrm{exp}[-\beta \Delta H(X', X)]
$$

As an example consider the transition rates used in the classic Metropolis algorithm
$$
w(X', X) \propto \mathrm{min} [1, \mathrm{exp}(-\beta \Delta H)]
$$

When we add the field $h$, we can write the new transition rates in terms of the old one in the following way:

$$
w^h(X', X) = w(X', X) \mathrm{exp}[\beta h \frac{\Delta M}{2} ]
$$

Notice that this choice is consistent with the new hamiltonian, ie, $\frac{w^h(X', X)}{w^h(X, X')} = \mathrm{exp}[-\beta (\Delta H - h\Delta M)]$. All of this suggests a particular way to perturb the transition rates with a clear physical interpretation. Going further, we aren't actually interested in general perturbation anyway, but only small perturbation, ie, $h \rightarrow 0$. All in all, we are going to perturb the transition rates in the following way:

$$
w^h_{kn}(t) = w_{kn}(t) + \beta h f(t) \chi_{kn} w_{kn}
$$

$f(t)$ can be anything in principle, but it's best to think of it as a function with a narrow support around a single time, indicating a quick switching on and switching off of the perturbation. $\chi_{kn}$ encodes the physical meaning of the perturbation, for instance in the previous case $\chi_{kn} = \frac{M_k - M_n}{2}$ and therefore if $h > 0$ the system transits more easily toward higher magnetization states. As you can see, this is a very general way of perturbing the system; perhaps only the multiplicative way of doing the perturbation seems arbitrary but as we've seen before it allows a direct connection with the hamiltonian for physical systems.

Measuring the perturbation
---------------------------

We've described what we mean by perturbing the system formally, but in practice people don't measure transition rates. Rather, they focus on some observable $M(t)$ and consider the way it changes switching on the field:

$$
\langle M_h(t) \rangle - \langle M_0(t) \rangle
$$

Let us remember that the field $h$ itself is dependent on time. The situation we have in mind is the one with the field switched off for $t \rightarrow -\infty$ and therefore the difference above is zero, then the field is switched on and the difference shoots up and finally the field is switched off again and therefore we slowly go back to zero.

As we are interested in the small perturbation limit, what characterizes the system is the derivative in $h$ for $h=0$. We define the response function:

$$
R(t) = \frac{\partial}{\partial h} [\langle M_h(t) \rangle_{h} - \langle M_0(t) \rangle]_{h=0}
$$

This is still not completely defined and to be absolutely clear, let's recall that for any observable

$$
\langle O(t) \rangle = \sum_k O_k P_k(t)
$$

with the evolution of $P_k(t)$ determined both by the transition matrix AND the particular P_k(t_0). While computing the averages above the transition matrix changes as for $\langle M_h(t) \rangle_{h}$ we consider the perturbed transition matrix, while in $ \langle M_0(t) \rangle $ we use the original matrix. On the other hand, we always use the stationary distribution with the field switched off as $P_k(t_0)$. Therefore $\langle M_0(t) \rangle$ won't depend on time for instance.

The whole idea is that the system is initially in the stationary distribution, not in any distribution, and then we switched on and off the perturbing field.

The fluctuation-dissipation theorem
------------------------------------

Before deriving the theorem, we are going to state it clearly. In this version of the fluctuation-theorem we assume:

1. our system evolves in time in a Markovian fashion with a unique stationary states.
2. the transition rates of the Markov process are time-independent.
3. the detailed-balance condition holds. 
4. the perturbation takes the form $w^h_{kn}(t) = w_{kn} + \beta h f(t) \chi_{kn} w_{kn}$ with $f(t)$ representing an on-off switch around a time $t_p$, a kind of dirac delta, and $\chi_{kn} = \frac{M_k - M_n}{2}$. Keep in mind what we've said above; this form might look very specific but it's actually not.

Then:

$$
R(t) = - \beta \frac{\partial}{\partial t} C_{ss}(t, t_p)
$$

$$
C_{ss}(t, t_p) := \langle M(t) M(t_p) \rangle
$$

ie, the correlation function at stationarity of the UNPERTURBED state, the field is switched off in these averages. More explicitly

$$
C_{ss}(t, t_p) = \sum_{kn} M_k M_n P(X=k, t; X=n, t_p) = \sum_{kn} M_k M_n G_{kn}(t, t_p) P_{ss}(n)
$$

Therefore, the response function of the system to the perturbation is related to the correlation function of the unperturbed system. Note that if we take the covariance $ \langle M(t) M(t_p) \rangle - \langle M(t) \rangle \langle M(t_p) \rangle $ for $C_{ss}(t, t_p)$ nothing changes because the latter term does not depend on time.

It seems that quite often what you know, either experimentally or analytically, is actually the response function and not the correlation function. But in equilibrium systems the two are related so the knowledge of one implies the other. Imagine for instance that the correlation function has an exponential behavior:

$$
C_{ss}(\tau) = \mathrm{Var M} \cdot \mathrm{exp}(-\lambda \tau)
$$

In this case you can infer the equilibrium fluctuations of the unperturbed system from the response function as:

$$
\mathrm{Var M} = \frac{R(0)}{\lambda \beta}
$$

Another cool formula you can derive to obtain the variance from the response function is 

$$
\mathrm{Var M} = k_B T \int_{t_p}^{\infty} R(t) dt  
$$

More generally, note how the strength of the response is monotonic in the strength of the fluctuations. In particular if the fluctuations diverge, for instance at criticality, the response diverges as well.

A simple example from biophysics
------------------------------------

As we've said before, binding processes are fundamental in any molecular account of living matter. The simplest phenomenological model of binding consists of considering a single binding site and a fixed, uniform concentration of ligands around it and say that the probability of a binding event is proportional to such concentration. 

Let $p$ the probability of having the binding site occupied. Modelling binding with a two-state markov processes, the master's equation gives

$$
\frac{\partial}{\partial t} p(t) = c k_{+} (1-p) - k_{-}p
$$

whose solution is

$$
p(t) = p_{ss} + (p_0 - p_{ss})\mathrm{exp}(-\lambda t)
$$

with $\lambda = c k_{+} + k_{-}$ and $p_{ss} = \frac{c k_{+}}{c k_{+}+k_{-}}$. This process clearly obeys detailed-balance and is completely solved which is helpful to check the result of the fluctuation-dissipation theorem. Consider now $n(t) \in [0, 1]$ the random variable describing the occupation number of the binding site and let's write down the equation in the mean:

$$
\frac{\partial}{\partial t} \langle n \rangle = c k_{+} (1-\langle n \rangle) - k_{-}\langle n \rangle
$$

Let us call $\bar{n}$ the stationary equilibrium value of the occupation number and consider $\langle \delta n \rangle = \langle n \rangle - \bar{n}$. Having in mind the response function, we perturb the rates according to $c k_{+} \rightarrow c k_{+}(1+\frac{\beta h}{2})$ and $k_{-} \rightarrow k_{-}(1-\frac{\beta h}{2}) $ with $h$ dependent  on time. After some algebra we obtain:

$$
\frac{\partial}{\partial t} \langle \delta n \rangle = - \lambda \langle \delta n \rangle + h(t) \beta \lambda \bar{n} (1-\bar{n})
$$

Understand what's going on here: we are computing the response function and in order to do that, we only need an equation in the mean rather than manipulating the entire master's equation; from this mean equation only, we will be able to compute the equilibrium fluctuations through the fluctuation-dissipation theorem. All of this highlights how the FTD is a great computational tool as well and if in this case you could calculate the fluctuations directly from the master's equation solution, it's easy to imagine situations where that isn't possible.

We are going to solve for the response function in a somewhat hand-wavy way. 

<figure>
<img src="{{ site.url }}/img/response.png" alt="response">
<figcaption><b>Fig.1 </b> The typical form of the response function in the limit of an infinitely fast on-and-off switch of the perturbation at time $t_p$.</figcaption>
</figure>

In the case of interest, the field $h(t)$ is turned on at time $t_p$ and turned off quickly after that in a dirac-delta type of fashion. Before the system in the stationary state therefore $ \langle \delta n \rangle = 0$. Around $t_p$:

$$
\langle \delta n \rangle = \int_{t_p - \epsilon}^{t_p + \epsilon} h(t) \beta \lambda \bar{n} (1-\bar{n}) dt = h \beta \bar{n} (1-\bar{n})
$$

meaning there is a sudden jump at $t_p$. After that the field is switched off and the dynamics is purely relaxational, ie $\frac{\partial}{\partial t} \langle \delta n \rangle = - \lambda \langle \delta n \rangle$, with $\langle \delta n \rangle$ starting with the value given by the jump. Putting it all together:


$$
\langle \delta n (t) \rangle = \cases{
0 &  $ t \leq t_p$ \\
h \beta \lambda \bar{n} (1-\bar{n}) \mathrm{exp}[-\lambda (t-t_p)] &   $t > t_p$
}
$$

which gives us the response function

$$
R(t) = \cases{
0 &  $ t \leq t_p$ \\
\beta \lambda \bar{n} (1-\bar{n}) \mathrm{exp}[-\lambda (t-t_p)] &  $ t > t_p$
}
$$

In this particular case, one can easily compute the correlation function from the solution of the master's equation and you can check the validity of the fluctuation-dissipation theorem. If we hadn't been able to compute the correlation function directly, we wouldn't have had to worry because we could obtain it anyway from perturbing the equation of the mean.

I'll end by mentioning the two main sources for this blogpost, both articles go into much more detail and I'd suggest you go through them if you are interested in the subject:

- Bialek W., Setayeshgar S., Physical limits to biochemical signalling, _PNAS_ (2005)

- Diezemann G., Fluctuation-dissipation relations for Markov processes, _PRE_ (2005)