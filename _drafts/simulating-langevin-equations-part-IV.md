---
layout: post
title: "Handling Langevin equations 101, Part IV: Stochastic Differential Equations"
tags: simulation stochastic-equations
---

So why is the symbolic notation for stochastic equations useful at all? It's meaningless if taken literally and it really just seems like a placeholder for something with actual content.

In practice, what they are actually used for is to find the momenta of the $x$ variable. Notice first that although $\frac{dx}{dt}$ makes no sense, $\frac{d}{dt} \langle x \rangle$, $\frac{d}{dt} \langle x^2 \rangle$ and so on are perfectly defined. The idea is that it's easier to use the stochastic equation to find analytical expression for the evolution of the momenta instead of considering finite difference each time, _provided you respect some basic rules_.

To illustrate, let us rewrite our differential in a way that is more convenient for analytical computations

$$
dx_t = A(x_t)dt + B(x_t)dW_t
$$

The noisy part of the differential is expressed in terms of brownian increments, so that $dW_t = W_{t+dt} - W_t = \eta \sqrt{dt}$. Summing up all the $dx_t$ gives $x_t$ and in the limit of small $dt$ the sum becomes an integral

$$
x_t = x_0 + \int_0^t A(x_s)ds + \int_0^t B(x_s)dW_s
$$

There's nothing mystical about the second integral, replace it with a discrete sum in your mind and you see that is perfectly defined. Different discretization schemes will give different results, but each sum is well-defined. The notation above describes the Euler-Ito discretization procedure. Stratonovich-like choices will be described instead by writing:

$$
\eqalign{
dx_t &= A\left(x_t+\alpha dx_t\right)dt + B\left(x_t+\alpha dx_t\right)dW_t \\
        &= A(x_t)dt + \alpha B'(x_t)B(x_t)dt + B(x_t)dW_t \\
        &= A(x_t)dt + B(x_t) \circ dW_t
}
$$

$B(x_t) \circ dW_t$ describes the noisy part of the differential using the Stratonovich computation.

$$
x_t = x_0 + \int_0^t A(x_s)ds + \int_0^t B(x_s) \circ dW_s
$$


One way of making computations about the momenta is to manipulate these integrals. To be fair, this is only slightly more sophisticasted than considering finite difference, but I think it's instructive and it helps understand stochastic equations later. 

Computations in the Ito's scheme
---------------------------------

Let's consider the simplest non-trivial example, $\langle (x_t - x_0)^2 \rangle$ using the Ito scheme. Simply start by multiply the equation above for $x_t - x_0$ and take the average:

$$
\langle (x_t - x_0)^2 \rangle = \langle \left( \int_0^t A(x_s)ds \right)^2 \rangle + \int_0^t \int_0^t \langle B(x_s) dW_s B(x_u) dW_u \rangle
$$

The cross-term cancels because $\langle dW_s \rangle = 0$. It's tempting to split $\langle B(x_s) dW_s B(x_u) dW_u \rangle$ right away, but one must be careful. Without loss of generality, consider $s>u$: then $B(x_s)$ is correlated with $dW_u$ and these two terms cannot be split for instance. Still in this case, one can say

$$
\langle B(x_s) dW_s B(x_u) dW_u \rangle = \langle B(x_s) dW_u \rangle \langle B(x_u) \rangle \langle dW_s\rangle
$$

which is zero once again because $\langle dW_s \rangle = 0$. An identical argument holds for $s$ less than $u$. Therefore it seems that in the integral only the strip $s=u$ matters. In that case you can split 

$$
\langle B(x_s) dW_s B(x_u) dW_u \rangle = \langle B(x_s)^2 \rangle \langle dW_s^2 \rangle = \langle B(x_s)^2 \rangle dt
$$

so that all in all:

$$
\langle (x_t - x_0)^2 \rangle = \langle  \left( \int_0^t A(x_s)ds \right)^2 \rangle + \int_0^t \langle B(x_s)^2 \rangle ds
$$

Finally it is easy to prove that you can turn this integral equation into a differential equation:

$$
\frac{d}{dt}\langle (x_t - x_0)^2 \rangle =  2 \langle (x_t-x_0) A(x_t) \rangle + \langle B(x_t)^2 \rangle
$$

Let us now consider the same computation, but using stochastic derivatives. We simply use Ito's lemma:

$$
\frac{d}{dt} x_t^2 = 2 x \frac{dx}{dt} + B(x)^2
$$

then take the average and use $\frac{dx}{dt} = A(x_t) + B(x_t)\xi_t$ to obtain:

$$
\frac{d}{dt} x_t^2 = 2 \langle x_t A(x_t) \rangle + \langle x_t B(x_t) \xi_t \rangle \langle B(x_t)^2 \rangle
$$

At this point everything hinges on how you compute averages like $ \langle f(x_t) \xi_t \rangle $. For Ito's trajectories the prescritpion should be:

$$ 
\langle f(x_t) \xi_t \rangle = \langle f(x_t) \rangle \langle \xi_t \rangle = 0
$$

so that for instance in the case above we re-obtain the result computed by manipulating integrals

$$
\langle \frac{d}{dt} x_t^2 \rangle = 2 \langle x_t A(x_t) \rangle + \langle B(x_t)^2 \rangle
$$

Note how much shorter the computation becomes using stochastic derivative, provided you know the basic rules.

Computations in the Stratonovich's scheme
------------------------------------------

With Stratonovich, you can again make computations with the integrals, but at this point we have learned that it should be much easier to work with stochastic derivatives.  Consider again $x_t^2$, use the ordinary rules of calculus to compute its stochastic derivative with Stratonovich and take the average

$$
\frac{d}{dt} x_t^2 = 2 \langle x_t A(x_t) \rangle + \langle \left [x_t B(x_t) \right] \circ \xi_t \rangle
$$

In this case what matters is the average $\langle f(x_t) \circ \xi_t \rangle$. It is easy to prove that:

$$
\langle f(x_t) \circ \xi_t \rangle = \frac{1}{2}  \langle \frac{\partial f}{\partial x} B(x_t) \rangle
$$

and therefore

$$
\frac{d}{dt} x_t^2 = 2 \langle x_t A(x_t) \rangle + \langle \frac{1}{2}B'(x_t)B(x_t)x \rangle + \langle B(x_t)^2 \rangle
$$

as expected considering for the instance the way Stratonovich's calculus connects to Ito's calculus. Note also that the big fuss that is sometimes made about the 'loss of causality' in the Stratonovich case is really overblown. $\langle x_t \xi_t \rangle$ is said to violate causality performing computations the Stratonovich way, but that is just because we are actually performing $\langle x_t \circ \xi_t \rangle$, implying the presence of $dx_t$ in the average sign and then obviously $dx_t$ and $\xi_t$ correlate.

All in all after these examples we have a fairly good practical understanding of how to use \xi_t to extract information from the stochastic differential equation. Essentially, the idea here is to use it only under average sign and use the simple rules outlined above to perform calculations. It really is introduced mostly to perform symbolic manipulations, but as we have seen, these really are useful. At any rate, whenever you feel confused, just use $\xi_t dt$ which is just $dw_t$, ie, a brownian increment in $dt$. I should clarify a little bit what happens when you consider averages of quantities at different times, such $\langle x{t_1} x_{t_2} \rangle$, $\langle x{t_1}  \xi_{t_2} \rangle$, but I'll leave that for another post.

Solutions of SDEs
------------------

I'll conclude with a very simple remark. So far, I have emphasised stochastic differential equations (SDEs) as a tool to obtain differential equations for the momenta or as a compact summary of the way trajectories are simulated. It seems perfectly natural to ask if there is a analytical solution concept that arises from the stochastic differential equation:

$$
\frac{dx}{dt} = A(x(t)) + B(x(t)) \xi(t)
$$

The answer is yes, the solution to the above equation will be a random variable expressed as a function of the noisy 'source' $W_t$. Ideally, we would like to have $x_t = f(W_t)$, ie, the random variable $x_t$ depends only on the random variable $W_t$ and not also $W_s$ with $s$ less than $t$. This is the case for instance for the noisy exponential growth described by

$$
\frac{dN}{dt} = kN(t) + D N(t)\xi(t)
$$

which has the solution

$$
N(t) = N_0 \exp \left[ (k-\frac{D}{2})t + D W_t \right]
$$

Given this equation, since we know the distribution of $W_t$, we will be able to compute all the statistical properties of $N(t)$ by the usual transformation methods. In general, though, the solution will depend on all the past values of $W_t$.

Are there general techniques to attack SDEs in order to obtain full solutions? I am not really an expert and I should look into it. Just to get a taste of them, it seems that one simple technique consists of trying to rewrite the differential equation in such a way that:

$$
\frac{d}{dt} f(N_t) = \xi_t
$$

for some function $f$, remembering Ito's lemma when you do this. Then you obtain an implicit equation:

$$
f(N_t) - f(N_0) = W_t
$$

and try to extract $N_t$ from there. You can apply this method for the noisy exponential growth above, for example. At any rate, looking for SDEs solutions seems a very sophisticated field and just looking at the [wiki page](<https://en.wikipedia.org/wiki/Stochastic_differential_equation>) of the number of concepts and techniques involved.
