---
layout: post
title: "Hitting times and recurrence times"
date: 2019-01-13
---

Let us define 

$$
\Pi_1(t, \mathbf{x_0}, \mathbf{x})
$$

as the probability of reaching, or hitting, position $\mathbf{x}$ for the first time at time $t$ starting from position $\mathbf{x_0}$. This time $t$ is also called called first-passage time. This is a very different object from $P(t, \mathbf{x_0}, \mathbf{x})$ the probability of being at position $\mathbf{x}$ at time $t$ starting from position $\mathbf{x_0}$. First of all, time is the random variable in the former, position in the latter. Second of all, being at position $\mathbf{x}$ at time $t$ does not mean that the particle couldn't have been in $\mathbf{x}$ at a previous time, but this is precisely what we require with $\Pi_1(t, \mathbf{x_0}, \mathbf{x})$. It's a much more stringent condition on the trajectories that allows us to realize the desired event.

<video class='center' width="500" height="375" controls>
  <source src="{{ site.url }}/blog/img/random_walk_video.mp4" type="video/mp4">
</video>

In addition to first-passage times, we can consider recurrence times and define

$$
\Omega(t, \mathbf{x})
$$

as the probability distribution of the time $t$ at which the particle comes back to position $\mathbf{x}$, starting from the same position. What is the relationship between first-passage times and recurrence times? Well, clearly a recurrent time is nothing more than the time it takes to get from the neighborhood of $\mathbf{x}$ to $\mathbf{x}$. Then:

$$
\Omega(t, \mathbf{x})  = \sum_{\mathbf{x'} \in B(\mathbf{x})} \Pi(t, \mathbf{x'}, \mathbf{x})
$$

so first-passage times distributions encode also the recurrence time distribution.

Beyond first-passage times, we can consider second-passage times, third-passage times and so on, in the form of $\Pi_2(t, \mathbf{x_0}, \mathbf{x})$, $\Pi_3(t, \mathbf{x_0}, \mathbf{x})$, .. More generally 

$$
\Pi_n(t, \mathbf{x_0}, \mathbf{x})
$$

is the probability that the particles goes through position $\mathbf{x}$ for the $n$-th time at time $t$. It's quite obvious that the knowledge of $\Pi_1(t, \mathbf{x_0}, \mathbf{x})$ is sufficient to derive all the other $n$-th distribution times. For instance

$$
\Pi_2(t, \mathbf{x_0}, \mathbf{x}) = \int_0^t\Pi_1(s, \mathbf{x_0}, \mathbf{x}) \Omega(t-s, \mathbf{x}) ds
$$

meaning we obtain higher passage times distribution by convolving n-times the first-passage time distribution with the recurrence time:

$$
\Pi_n(t, \mathbf{x_0}, \mathbf{x}) = \Pi * \left[\Omega^{*n-1} \right]  (t)
$$

Hitting times are interesting by itself and in a plethora of applications. The time it takes for a particle random walking to bind to a static receptor will be described by the a first-passage time distribution for instance. We can go a little further though and think of two particles random walking and ask when they will collide. If you imagine two particles, then it's tempting to say that $\Pi_1(t, \mathbf{x_0}, \mathbf{x}) \cdot \Pi_1(t, \mathbf{x_0'}, \mathbf{x})$ is the probability of the two particle meeting at time $t$ in position $\mathbf{x}$ starting from their respective initial conditions. In fact this is slightly wrong. The right expression for this probability is the following:

$$
P_{COL}(t, \mathbf{x}, \mathbf{x_0}, \mathbf{x_0'}) = \sum_{n, m} \Pi_n(t, \mathbf{x_0}, \mathbf{x}) \Pi_m(t, \mathbf{x_0'}, \mathbf{x})
$$

as for instance, it could that one particle goes through position $\mathbf{x}$ before the other particle, but then it goes through once again at the same time as the other particle and this case is encoded by $\Pi_2(t, \mathbf{x_0}, \mathbf{x}) \Pi_1(t, \mathbf{x_0}, \mathbf{x})$. Taking into account all possibilities gives the sum in the equation above. It's clear on the other hand that $\Pi_1(t, \mathbf{x_0}, \mathbf{x}) \cdot \Pi_1(t, \mathbf{x_0'}, \mathbf{x})$ works as a lowest order approximation of the collision probability. It's also quite obvious that if I want to consider more than two particles, the time it takes before any one collision will be given by a distribution made of as many terms as the ones above for each pair, plus also higher order terms considering the possibility of many-body collisions, eg, three particles in the same position. Now, technically we are assuming a collision model in which the subsequent dynamics after collision isn't affected. This isn't obvious, but I feel like it's probably a good zeroeth approximation in many cases.

Finally it's sometimes useful to think of first-passage time distribution as

$$
\Pi_1(t, \mathbf{x_0}, \mathbf{x}) = \frac{\text{# of trajectories reaching x in t steps}}{\text{# of possible trajectories t-steps long}}
$$

as it allows to make hypothesis on $\Pi$ based on our intuition about the number of trajectories.

Note that many of these definitions and relations are quite general and not confined to simple random walk. Next, we are going to analyse what happens in a $d$-dimensional simple random walk.