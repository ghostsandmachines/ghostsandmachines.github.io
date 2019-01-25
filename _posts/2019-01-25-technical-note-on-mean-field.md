---
layout: post
title: "A technical note on approximating the mean of the function with the function of the mean"
date: 2019-01-25
tags: mean-field art-of-approximation 
---

I want to write a small technical note of how to approximate the mean of a function with the function of the mean and how to quantify the error of the approximation.  It happens quite often that we know something about a certain underlying random variable and we want to know the implication of such knowledge on other observables.

Let us consider $f(M)$ and write its mean:
	
$$
\langle f \rangle = \int P(M) f(M) dM
$$
	
We taylor-expand $f(M)$ around the mean $\langle M \rangle$:
	
$$
f(M)  = f\left(\langle M \rangle \right) + (M-\langle M \rangle) f'\left(\langle M \rangle \right) + \frac{1}{2}(M-\langle M \rangle)^2 f''\left(\langle M \rangle \right) + ..	
$$
	
It's immediate to obtain:
	
$$
\langle f \rangle = f\left(\langle M \rangle \right) + \frac{ \sigma_M^2 }{2}f''\left(\langle M \rangle \right) + \frac{ \sigma_M^3 \gamma_M}{3!}f'''\left(\langle M \rangle \right) + \frac{ \sigma_M^4 K_M}{4!}f''''\left(\langle M \rangle \right) + ..
$$
	
with $\sigma_M$, $\gamma_M$, $K_M$ being the standard deviation, the skewness and the kurtosis.
	
It is apparent that the goodness of the approximation $ \langle f \rangle \approxeq f\left(\langle M \rangle \right) $ depends both on the shape of the underlying distribution $P(M)$ and the specific form of the function $f(M)$. In particular if $f(M)$ is close to being linear, the approximation is rather good.
	
Let us consider a function that is as far from a linear function as possible, i.e., an exponential. If $f(M) = \exp \left (M/\tau \right )$, then
	
$$
\langle f \rangle = f\left(\langle M \rangle \right) \left [1 + \frac{ \sigma_M^2 }{2 \tau^2} + \frac{ \sigma_M^3 \gamma_M}{3! \tau^3} + \frac{ \sigma_M^4 K_M}{4! \tau^4} + .. \right ] 	
$$
	
Often, it's tempting to consider the observable $M$ distributed according to a gaussian distribution. In this case, the skewness is $0$, the kurtosis is $3$ and all that matters effectively is the ratio $\frac{\sigma_M}{\tau}$. The latter statement applies whenever the skewness and the kurtosis are of order $o(1)$. On the other hand, already gaussian mixtures complicate things. Consider bimodality for instance: in a simple symmetric gaussian mixture skewness obeys $\sigma^3 \gamma = \frac{3}{2} \Delta \mu \frac{\sigma_2^2 - \sigma_1^2}{2}$ and $\sigma^2 = \frac{\sigma_1^2 + \sigma_2^2}{2} + \frac{(\Delta \mu )^2}{4}$, meaning skewness picks up a contribution from the mixture. Despite this, it seems highly likely that when we consider $\gamma$ by performing the appropriate ratio of these two quantities we obtain something of order $o(1)$ at worst because $(\Delta \mu )^2$ is most likely bigger than $\Delta \mu (\sigma_2^2 - \sigma_1^2)$.
	
We turn to analyse the meaning of the ratio $\frac{\sigma_M}{\tau}$. It is apparent that $\tau$ gives the scale after which the change in the observabme $f$ becomes exponential. $\sigma_M$ is the scale of the fluctuations of the underlying random variable. Round $\langle M \rangle$, the values that matter are within an interval of length $\sigma_M$. If $\sigma_M \ll \tau$, it is possible to approximate $f(M)$ linearly along this interval to $f\left(\langle M \rangle \right) + (M-\langle M \rangle) f'\left(\langle M \rangle \right)$ and therefore approximating the mean of the function with the function of mean is allowed.
	
This example illustrates a generic principle: it is true that $ \langle f \rangle \approxeq f\left(\langle M \rangle \right) $ if $f(M)$ is approximately linear around $\langle M \rangle$ in a region of length $\sigma_M$ or greater. This criterium is major refinement over simply stating that $f(M)$ must be linear everywhere. Possible exceptions to this rule emerge with highly skewed or fat-tailed distributions. It is useful in general to think of a $\tau$ defined as the intrinsic scale of $f(M)$ within which is possible to approximate linearly around $\langle M \rangle$. 
	
Finally let us consider the power-law case
	
$$
f(M) = c M^{\alpha}
$$

with $\alpha \leq 2$. In this case the following relation holds
	
$$
\langle f \rangle \approxeq f\left(\langle M \rangle \right) + \frac{ \sigma_M^2 }{2} \frac{c \alpha (\alpha -1)}{\langle M \rangle^{2-\alpha} }
$$
	
which is more instructive when written
	
$$
\langle f \rangle \approxeq f\left(\langle M \rangle \right) \left [1+  \left(\frac{\sigma_M}{\langle M \rangle}\right)^2 \alpha (\alpha-1) \right]
$$
	
The sign of the correction depends on whether the power-law is sublinear or superlinear. Superlinear laws require a bigger correction. To get a feel for the numbers, consider a quadratic scaling and $\frac{\sigma_M}{\langle M \rangle} = 0.1$, then $\langle f \rangle \approxeq f\left(\langle M \rangle \right)$ up to a 2% underestimation, a very good approximation. If $\frac{\sigma_M}{\langle M \rangle} = 1$, $f\left(\langle M \rangle \right) = \frac{1}{3} \langle f \rangle$, which is instead a sever underestimation, about 66%. The main lesson to draw out of this numerical analysis is that the spread of the underlying distribution matters more than the particular exponent in the case of power-laws.