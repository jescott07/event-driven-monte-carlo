# Event Driven Monte Carlo Simulation

The classical Monte Carlo simulation tends to reject new configurations when the new configuration energy is biger than the original one, it is particularly visible in low temperature systems. On the other hand the event driven monte carlo simulation correct this bias by not reject any configurational change evaluation. We can do this by choosing a free parameter that evaluates the energy samples, first we will generate a sequenc of configurations ($c_1,c_2,\ldots,c_N$), that in the stationary regime, the probrability of find the system in some configuration $c$ in equilibrium $P_{eq}(c)$ is porportional to the energy of this configuration $E(c)$, in this way:

<p align='center'>
$P_{eq}(c) \propto e^{-\beta E(c)}$
<p/>

where, setting $k_b = 1$ then $\beta = \frac{1}{T}$.

Defining the transition rate of one atual configuration $c$ to another configuration $c'$ as $R(c',c)$, the total rate of changing the $c$ configuration is:

<p align='center'>
$R(c) = \Sigma_{c_i} R(c_i,c)$
<p/>

So, the mean permanence time of the $c$ configuration is:

<p align='center'>
$T(c) = \frac{1}{R(c)}$
<p/>

