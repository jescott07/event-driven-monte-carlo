# Event Driven Monte Carlo Simulation

The classical Monte Carlo simulation tends to reject new configurations when the new configuration energy is biger than the original one, it is particularly visible in low temperature systems. On the other hand the event driven monte carlo simulation correct this bias by not reject any configurational change evaluation. We can do this by choosing a free parameter that evaluates the energy samples, first we will generate a sequenc of configurations ( $c_1,c_2,\ldots,c_N$ ), that in the stationary regime, the probrability of find the system in some configuration $c$ in equilibrium $P_{eq}(c)$ is porportional to the energy of this configuration $E(c)$ as:

<p align='center'>
$P_{eq}(c) \propto e^{-\beta E(c)}$
<p/>

where, setting $k_b = 1$ then $\beta = \frac{1}{T}$.

Defining the transition rate of one current configuration $c$ to another configuration $c'$ as $R(c',c)$. The total rate of changing the $c$ configuration is:

<p align='center'>
$R(c) = \Sigma_{c'} R(c',c)$
<p/>

So, the mean permanence time of the $c$ configuration is:

<p align='center'>
$T(c) = \frac{1}{R(c)}$
<p/>

From the the principle of detailed balance:

<p align='center'>
$R(c',c)P_{eq}(c) = R(c,c')P_{eq}(c')$
<p/>

We can represent this as:

<p align='center'>
$R(c',c) = \frac{r}{P_{eq}(c)} [P_{eq}(c') P_{eq}(c)]^{\alpha}$
<p/>

Where $r$ is a constante and $\alpha \geq 0$. So:

<p align='center'>
$R(c) = \frac{r}{P_{eq}(c)} \Sigma_{c'} [P_{eq}(c') P_{eq}(c)]^{\alpha}$
<p/>

Using that:

<p align='center'>
$P_{eq}(c) = \frac{1}{Z} e^{-\beta E(c)}$
<p/>

Since $Z$ is a constant, to calculate $R(c)$ we can ignore its value. Considering that:

<p align='center'>
$E(c') = E(c) + \Delta E$
<p/>

Where $\Delta E$ is the variation of energy from one configuration ( $c$ ) to another ( $c'$ ). So we can represent the sum over the configuration as a sum over the variation of energy, as:

<p align='center'>
$\Sigma_{c'} = \Sigma_{\Delta E'} N(\Delta E', c)$
<p/>

Where $N(\Delta E',c)$ is the number of transitions of the $c$ configuration given the variation of energy $\Delta E'$. Thus:


<p align='center'>
$R(c) =  r e^{\beta E(c)}  \Sigma_{\Delta E'} N(\Delta E', c) e^{-\alpha \beta (E(c) + \Delta E')} e^{-\alpha \beta E(c)}$
<p/>

<p align='center'>
$\Rightarrow R(c) =  r e^{\beta(1- 2 \alpha)E(c)}  \Sigma_{\Delta E'} N(\Delta E', c) e^{-\alpha \beta \Delta E'} = \frac{1}{T(c)}$
<p/>

Thus, the next transition will will happen in the time $t + T(c)$ and 

<p align='center'>
$P(c',c) = \frac{R(c',c)}{\Sigma_{c''} R(c'',c)} = \frac{e^{- \alpha \beta \Delta E}}{\Sigma_{\Delta E'} N(\Delta E',c) e^{-\alpha \beta \Delta E'}}$
<p/>

Notice that, for $\alpha = 0$ $P(c',c)$ is independent of $\Delta E$, thus we will have a poor sample for low energies.

We can choose $c'$ from the probability configuration:

<p align='center'>
$P(c',c) = \frac{e^{-\alpha \beta \Delta E(c)}}{\Sigma_{\Delta E'} N(\Delta E', c) e^{- \beta \Delta E'}} \equiv \frac{e^{-\alpha \beta \Delta E(c)}}{Q} $
<p/>

we know that all configurations $c'$ for the same $\Delta E$ are equally probable, thus:

<p align='center'>
$P(\Delta E,c) = \frac{ N(\Delta E', c) e^{-\alpha \beta \Delta E(c)}}{Q} $
<p/>

Lets take te minimum value of $\Delta E$ ( $\Delta E_{min}$ ). From a random number $Z$, where $Z \in [0,1)$ we evaluate:

if $Z < P(\Delta E_min,c)$ then $\Delta E = \Delta E_{min}$

else if $Z < P(\Delta E_min,c) - P(\Delta E_min + 1,c)$ then $\Delta E = \Delta E_{min} + 1$

$\cdots$

else if $Z < P(\Delta E_{min},c) - P(\Delta E_{min} + 1,c) + \ldots + P(\Delta E_{max},c)$ then $\Delta E = \Delta E_{max}$

From these steps we evaluate $\Delta E$, and them we choose a random value of $N(\Delta E,c)$. Thus we have our new configuration $c'$.

To implement this, we need a list with the folowing informations:

1) The position of the occupied particle
2) The direnction of the transitions, for exemple, up, down, right left
3) The number of transitions of each $\Delta E$, where the maximum number of transitions is $2L^2$ where every transition has the same $\Delta E$



