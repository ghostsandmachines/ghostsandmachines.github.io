---
layout: post
title: "Cas"
date: 2019-04-11
tags: statistical-mechanics cas
--- 
 
> In condensed matter physics, there is a clear separation between the rules that govern the time evolution of the system and the state of the system itself. [..] The mathematical reason for this is that the governing equation does not depend on the solution of the equation. The evolution operator is independent of the state of the system. In biology, however, the situation is different. The rules that govern the time evolution of the system are encoded in abstractions, the most obvious of which is the genome itself. As the system evolves in time, the genome itself can be altered; thus, the governing rules are themselves changed. From a computer science perspective, one might say that the physical world can be thought of as being modeled by two distinct components: the program and the data. But in the biological world, the program is the data, and vice versa. For example, the genome encodes the information which governs the response of an organism to its physical and biological environment. At the same time, this environment actually shapes genomes, through gene transfer processes and phenotype selection. Thus, we encounter a situation where the dynamics must be self-referential: the update rules change during the time evolution of the system, and the way in which they change is a function of the state and thus the history of the system. 
>
> -- <cite>Nigel Goldenfeld and Carl Woese</cite>

> Let us consider a collection of classical nodes or entities (e.g., spins, agents) connected by links (interactions). Each node can be in one of a number of possible states described by a scalar, vector, matrix, or other mathematical object. [..] We first consider a ‘simple’ (not complex)
system; e.g., a random network or a regular lattice. Denoting the state of a node by $\sigma_i$,
one may describe its evolution by a system of equations
>$\frac{d \sigma_i}{dt} = F(\\{\sigma_i\\}, \mathbf{M}) \; \forall \, i$
> , where $N$ is the number of agents, $\mathbf{M}$ is the interaction matrix with elements $M_{ij}^{\alpha}$ that span all pairs of agents and the index $\alpha$ accounts for possible different types of interactions. The function F can be stochastic or deterministic. [..] For a complex (as opposed to a complicated) system, the states of the nodes again determine the state of the system but they also influence the interactions between the nodes. In other words, the microstates (nodes) and the nature of the interactions \mathbf{M} dynamically update each other. The evolution of such a system is therefore governed by a system of equations
>$\frac{d \sigma_i}{dt} = F(\\{\sigma_i\\}, \mathbf{M}) \; \forall \, i$ ,
>$\frac{d M_{ij}^{\alpha}}{dt} = G(\\{\sigma_i\\}, \mathbf{M}) \; \forall \, ij$ .
>
> --<cite>Yurij Holovatch, Ralph Kenna and Stefan Thurner</cite>

> How does evolution produce increasingly fit organisms in environments which are highly uncertain for individual organisms?
What kinds of economic plan can upgrade an economy's performance in spite of the fact that relevant economic data and utility measures must be obtained as the economy develops?
How does an organism use its experience to modify its behavior in beneficial ways (i .e., how does it learn or "adapt under sensory guidance") ?
How can computers be programmed so that problem-solving capabilities are built "what is to be done" rather than "how to do it" ?
What control procedures can improve the efficiency of an ongoing process, when details of changing component interactions must be compiled and used concurrently ?
> There is no collective name for such problems, but whenever the term adaptation (ad + aptare, to fit to) appears it consistently singles out the problems of interest.
>
> --<cite>John H. Holland</cite>

>The crux of the problem for the adaptive plan is that initially it has incomplete information about which structures are most fit. To reduce this uncertainty the plan must test the performance of different structure in the environment. The 'adaptiveness' of the plan enters when different environment cause different sequences of structures to be generated and tested. [..]
A characteristic of the environment can be unknown (from the adaptive plan's point of view) only if alternative outcomes of the plan's tests are allowed for. Each distinct combination of alternatives is a distinct environment E in which the plan may have to act. 
> --<cite>John H. Holland</cite>

> Among the specific obstacles confronting an adaptive plan are the following:
1. The space of the possible structure of the system is large so that there are many alternatives to be tested.
2. The structures in such space are complicated so that it is difficult to determine which substructures or components (if any) are responsible for good performance.
3. The performance measure is a complicated function with many interdependent parameters (e.g., it has many dimensions and is nonlinear, exhibiting local optima, discontinuities, etc.).
4. The performance measure varies over time and space so that given adaptations are only advantageous at certain places and times.
5. The environment E presents to the adaptive plan a great flux of information (including performances) which must be filtered and sorted for relevance.
>
> --<cite>John H. Holland</cite>