---
layout: distill
permalink: /teaching/reaction-networks
title: An introduction to thermonuclear reaction networks
description: Lecture notes for the 2nd Frontiers Summer School
date: 2023-05-16

authors:
  - name: Thanassis Psaltis
    url: "mailto: psaltis.tha@duke.edu"
    affiliations:
      name: TUNL & NC State University

bibliography: reaction-networks.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
 # - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Thermonuclear reaction rates
  - name: Solving the network
  - name: The codes

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbbbbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white !important;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

<div class="fake-img l-body">
  <p> <b><i class="fa fa-desktop"></i> For the lecture slides click this link <a
  href='{{base_url}}/assets/talks/Frontiers-lecture' target="_blank"><i class="fas
  fa-external-link-alt"></i> </a></b> </p>
</div>


### What is a reaction network and why should I care?

If you work in nuclear astrophysics, you may not have realized the close
connection between your work and nuclear reaction networks. Let us examine
some examples:

- Student A works in low-energy experimental nuclear physics and 
she measured the cross section of an astrophysically interesting reaction 
for her dissertation,
- Postdoc B is an observational astronomer and has measured the elemental 
abundances of Galactic metal-poor stars,
- Student C works in nuclear theory and has implemented a new Equation of
State (EoS) to be used in Neutron Star (NS) and Supernovae (SNe) simulations,
- Postdoc D wants her Galactic Chemical Evolution (GCE) code to include
  the contribution of a specific nucleosynthesis process for which she
  requires its yields. 

What do they all have in common? Their results are inteconnected using nuclear reaction networks!

Networks are groups of things that are connected in some way, and we can find them
everywhere. The most common example is *social network*: your family,
friends, colleagues and the rest of the people you are interacting socially 
(nowadays we can find virtual counterparts of these networks). A network
consists of nodes (in our social network example, people), and edges (social connections). 
There is a very active academic field which studies networks and their
interactions, called *network science*. 

 <center>  
   <div class="col-sm mt-2 mt-md-0">
        <img
    src="{{ site.baseurl }}/assets/talks/images/net0.svg"
    class="img-fluid" data-zoomable="">
		<div class="caption">
	A simple network. The nodes are connected with the edges.
	</div>
	</div>
 </center>


Similarly, thermonuclear reaction networks connect nuclei via nuclear
processes, such as reaction and decays.
An additional complexity is that the reaction networks we will study in this
lecture evolve over time, according to the thermodynamical conditions of the
environment (mainly temperature, $T(t)$ and density, $\rho(t)$).
In this lecture we will discuss how these reactions enter the network, when they matter and when they don't.
We call these reactions *thermonuclear* because they are caused by the thermal motion
of the involved nuclei, which *almost always* obey a Maxwellian
distribution<d-cite key="iliadis2017nuclear, rolfs1988cauldrons"></d-cite>.

 <center>                                                                                       
 <div class="col-sm mt-2 mt-md-0">
    <img class="img-fluid"
    src="{{ site.baseurl }}/assets/talks/images/net1.svg" data-zoomable="">
	</div>
	<div class="caption">
	A visualization of a nuclear reaction network based on the Reaclib
    database. There are ~8,000 isotopes (nodes) and ~77,000 nuclear processes 
	(edges) connecting them. There are regions in the network where more nuclear
    reactions take place than others (red rectangle versus blue rectangle). 
	The figure is adapted from Jiang <em>et al.</em> (2021) <d-cite key="jiang2021nuclear"></d-cite>.
	</div>
</center>
 
---

## Thermonuclear reaction rates 

Let us consider a simple stellar gas, which initially consists only of two 
charged-particle species $a$ and $b$. In this environment, only three nuclear
processes can occur, namely

$$ a + b \rightarrow c + \gamma$$

$$ c + \gamma \rightarrow a + b $$

$$ b \rightarrow a$$

that is, the fusion of $a$ and $b$ to produce a new species $c$ and a $\gamma$ ray 
(known as a *radiative capture* - similarly the photodissociation of $c$
produces $a$ and $b$), and the decay of $b$ to $a$.

 <div class="row justify-content-sm-center">                                                                                          
        <div class="col-sm mt-2 mt-md-0">
            <img class="img-fluid"
             src="{{ site.baseurl }}/assets/talks/images/stellar-gas.svg" data-zoomable="">
	    </div>
	    <div class="caption">
	        A visualization of our stellar gas, made out of the fictionary
            particles $a$ and $b$. As time moves forward, nuclear
            reactions create particle $c$ and $\gamma$ rays, and decays 
			and photodisintegrations also occur.	
		</div>
</div>


Before delving into a full reaction network, let's explore
the first nuclear process, which we can write conveniently as
$a(b,\gamma)c$. The rate of this reaction, which we can define as the number
of reactions per volume and unit time, can be writen as follows<d-footnote>In
case of identical particles, we can generalize Equation
\ref{eq:1} to $r_{ab} = \frac{n_an_b \langle \sigma v
\rangle_{ab}}{(1+\delta_{ab})}$, 
where $\delta_{ab}$ is the Kronecker symbol.</d-footnote>

\begin{equation}\label{eq:1}
r_{ab} =  n_a n_b \langle \sigma v \rangle_{ab}
\end{equation}

where $n_a$ and $n_b$ are the concentrations, or number densities, of species
$a$ and $b$ per unit volume (usually expressed in
cm<sup>-3</sup>). These are *dynamical quantities* regulated by the nuclear
processes that involve them. $\langle \sigma v \rangle_{ab}$ is the
average value of the reaction cross section $\sigma$ (usually expressed in 
barns, where 1 b $\equiv$ 10<sup>-24</sup> cm<sup>2</sup>) and the
relative velocity distribution of the interacting particles $a$ and $b$.

Number density can change if the gas expands or contracts (remember that it
is species *per unit volume*). For this reason, we need a conserved quantity 
which reflects the nuclear transformations that occur in the gas. There are two 
such quantities that are commonly used in astrophysics, the **mass fraction**,
$X_i$ and the **abundance**, $Y_i$. The three quantities, number density, 
mass fraction and abundance are related through the following expression

\begin{equation}\label{eq:2}
n_i =  \frac{\rho N_A X_i}{A_i} = \rho N_A Y_i
\end{equation}

where $A_i$ is the atomic mass of species $i$ in amu (for example $A_{\mathrm{^{4}He}}$=
4.0026 amu) and $N_A$ is the Avogadro constant ($N_A = 6.022 \times 10^{23}$ mol<sup>-1</sup>).

If we apply the nucleon number conservation in the
environment<d-footnote>Remember that nuclear reactions generate energy! The
mass is not conserved, but rather the number of nucleons.</d-footnote>, we can get the following 
useful expressions for the mass fractions and the abundances, respectively

\begin{equation}\label{eq:3}
\sum_i X_i = 1
\end{equation}

\begin{equation}\label{eq:4}
\sum_i A_i Y_i = 1
\end{equation}

Now that we have convinced ourselved that we are measuring the change of
the constituents of the gas that is caused by nuclear processes, we can move 
on to the calculation of the thermonuclear reaction rate $\langle \sigma v \rangle_{ab}$. 

In a stellar gas, like in our example, the temperature is high enough
to ionize completely the constituent atoms (bare nuclei), such that they do not experience
any long range electronic interactions. The relative velocity of
the interacting particles can be described by the Maxwell-Boltzmann
distribution

\begin{equation}\label{eq:5}
P(v) dv = \left( \frac{\mu}{2\pi kT} \right)^{3/2} e^{-\mu v^2/(2kT)} 4\pi v^2 dv
\end{equation}

which expresses the probability that the relative velocity of
charged-particles $a$ and $b$ lies between $v$ and $v+dv$. 
$\mu = m_a m_b/ (m_a+m_b)$ is the reduced mass of the system, 
$k$ is the Boltzmann constant, with a value of $k= 8.6173 \times 10^{-5}$ eV/K 
and T is the gas temperature expressed in Kelvin. The Maxwell-Boltzmann
distribution shows the following behavior: it increases 
linearly with energy E at low energies, E $\ll$ kT, reaches a
maximum value at E = kT and decreases exponentially at high energies, E $\gg$ kT. 
This behavior is crucial when considering at which energies the
astrophysically interesting reactions take place.

We can express the Maxwell-Boltzmann particle velocity distribution as an
energy distribution (convert using $E= \frac{1}{2} \mu v^2$) and obtain 
the reaction rate in the center-of-mass energy (in units of cm<sup>3</sup>  mol<sup>-1</sup> s<sup>-1</sup>)

\begin{equation}\label{eq:6}
    N_A \langle \sigma v \rangle_{ab} = \left( \frac{8}{\pi \mu}\right)^{1/2} (kT)^{-3/2} N_A \int_0^\infty \sigma(E)~E~e^{-E/kT} dE
\end{equation}

Equation \ref{eq:6} is a general expression for the thermonuclear reaction
rate. In principle, the only missing piece for its calculation
is the energy--dependent reaction cross section, $\sigma(E)$. Once this
quantity is either measured experimentally, or estimated theoretically,
It can then be integrated numerically and evaluated at the temperature of
interest.

In general, there are few cases in which Equation \ref{eq:6} can be solved
analytically, because the cross section has a relatively simple energy
dependence. A smooth (**non-resonant**) and a strong (**resonant**) energy dependence
of the cross-section are encountered frequently in nuclear astrophysics<d-cite
key="longland2010npa"></d-cite>.

For non-resonant reactions, the cross section $\sigma(E)$ can be re-written as
\begin{equation}\label{eq:7}
\sigma(E) = \frac{S(E)}{E} e^{-2\pi \eta}
\end{equation}

where $S(E)$ is called the *astrophysical S-factor* and it is a slowly varying
functions of energy that removes the strong $1/E$ energy dependence of
$\sigma(E)$. Substituting Equation \ref{eq:7} to \ref{eq:6} gives us

\begin{equation}\label{eq:8}
N_A \langle \sigma v \rangle_{ab} = \left(\frac{8}{\pi \mu}\right)^{1/2}
(kT)^{-3/2} N_A \int_0^\infty S(E) e^{-2\pi \eta} e^{-E/KT} dE
\end{equation}

The integrant of the above expression exhibits a very interesting energy
dependence. Multiplying the transmission probability through the Coulomb
barrier, $e^{-2\pi \eta}$, which increases with increasing energy, with the
Maxwell-Boltzmann factor, which decreases with increasing energy, results in a 
peak which defines an energy region where *it is more probable for nuclear
reactions to occur* in a stellar gas. The peak is commonly referred to as the
*Gamow peak*.

For resonant reactions, the cross section can be described by the single-level
Breit-Wigner formula<d-footnote>Note that this description is valid for
resonances which have approximately constant partial widths over the total
resonance withd (Γ(E)/Er < 0.1, called <em>narrow</em>) and in addition do not
overlap significantly with other resonances (<em>isolated</em>)</d-footnote>:

\begin{equation}\label{eq:9}
\sigma(E) = \frac{\lambda}{4\pi} \frac{(2J+1)}{(2j_a+1)(2j_b+1)}
(1+\delta_{ab}) \frac{\Gamma_1(E) \Gamma_2(E)}{(E_r-E)^2+(\Gamma(E)/2)^2}
\end{equation}

where $\lambda$ is the de Broglie wavelength, which expresses the wave nature of the interact-
ing particles, $j_i$ are the spin of projectile and target, $J$ and $E_r$ are the spin and energy
of the resonance respectively, $Γ_i$ are the partial widths for entrance and exit channels
and $\Gamma$ is the sum of all the partial widths $\Gamma_i$, which correspond to the energetically
allowed decay channels.

Using Equation \ref{eq:9} we can solve analytically Equation \ref{eq:6}. In
the case of many resonances, we can add them incoherently and write the 
thermonuclear reaction rate as follows
\begin{equation}\label{eq:10}
N_A \langle \sigma b \rangle = N_A \left(\frac{2\pi}{\mu kT}\right)^{3/2}
\hbar^2 \sum_i (\omega \gamma)_i e^{-E_i/kT}
\end{equation}

where $\omega = (2J+1)/(2j_a+1)(2j_b+1)$ is the nuclear spin factor and 
$\omega \gamma$ is called the *resonance strength*, $\omega \gamma \equiv
\omega \frac{\Gamma_1 \Gamma_2}{\Gamma}$, and it is proportional to the area
under the resonance cross section, or the product of the total resonance width
and the cross section at the resonance energy, $\Gamma \cdot \sigma(E=E_r)$.

For nucleosynthesis processes that involve exotic nuclei, reaction rates are 
usually based on theoretical estimates for $\sigma(E)$. For example, in the $r$-process we 
rely on calculations based on the Hauser-Feshbach statistical model of nuclear
reactions for the $(n, \gamma)$ reactions on exotic neutron-rich species. 
<div class="fake-img l-gutter">
  <p><b>See G. Perdikakis lecture</b></p>
</div>

This model is used to describe cross sections in higher excitation energies of 
intermediate and heavy nuclei, where the density of nuclear levels
is high enough to take an average of many Breit-Wigner resonances. It assumes
that the compound nucleus formed in a reaction undergoes a sequence of
statistical decays, where the excitation energy is partitioned among the
available degrees of freedom of the system, such as nucleons, $\gamma$-rays, and other particles.

To calculate thermonuclear reaction rates, one needs to solve Equation
\ref{eq:6} numerically or analytically. Given that reaction rates carry 
uncertainty from many different factors, such as resonance energies, resonance
strengths *etc.*, we need a statistically meaningful way to treat them. One
of the ways used in the nuclear astrophysics community is to treat each
nuclear physics input as a (lognormal) distribution and sample thousands of
times using a Monte Carlo technique, solving Equation \ref{eq:6} every time. 
That way, one calculates a thermonuclear reaction rate with temperature dependent uncertainty
(essentially for every temperature point, you get a distribution for the
reaction rate, and from the 16th (lower) and 84th (high) percentile).
The code `RatesMC`, which was developed by R. Longland (NCSU/TUNL) performs such
calculations.<d-footnote>You can find RatesMC in Github 
<a href="https://github.com/rlongland/RatesMC"><i class="fab fa-github"></i></a>.</d-footnote>



More recently, Bayesian statistics along with Markov Chain Monte Carlo (MCMC)
algorithms have been used to calculate S-factors of astrophysically important 
reactions<d-cite key="iliadis2016apj, odell2022prc"></d-cite>.


The thermonuclear reaction rates we discussed 
are used to calculate the abundance evolution of
nuclear species and the energy release by these reactions
in an astrophysical environment. A nuclear reaction network
is a system of first-order coupled differential equations, 
which describes the abundance evolution and energy generation, and depends
only on the nuclear reaction rates and the local thermodynamical
conditions<d-cite key="arnett1996supernovae, hix2006thermonuclear, travaglio2013"></d-cite>. 
The size of these networks can vary according to the astrophysical 
environment, with quiescent stellar burning being much smaller compared to explosive burning. 


<div class="fake-img l-body">
  <p> <b> <i class="fas fa-quote-left"></i> A nuclear reaction network
is a system of first-order coupled differential equations, 
which describes the abundance evolution and energy generation, and depends
only on the nuclear reaction rates and the local thermodynamical conditions. </b> </p>
</div>



***
## <i class="fas fa-project-diagram"></i> The rate equations

Let us return to our stellar gas example and try to write the differential 
equations that describe the abundance evolution for species $a$, $b$ and $c$.
Particle $a$ is destroyed by the $a(b,\gamma)c$ reaction, and created by the
$c(\gamma,b)a$ photodissociation and the decay of particle $b$. Using
Equations \ref{eq:1} and \ref{eq:2} we can write

\begin{equation}
\frac{dY_a}{dt} = - \rho N_A Y_a Y_b \langle \sigma v \rangle_{ab} +
\lambda_\gamma Y_c + \lambda_b Y_b
\end{equation}

Similarly, particle $b$ is destroyed by the $a(b,\gamma)c$ reaction and its decay, and created by the                                 
$c(\gamma,b)a$ photodissociation:

\begin{equation}
\frac{dY_b}{dt} = - \rho N_A Y_a Y_b \langle \sigma v \rangle_{ab} - \lambda_b
Y_b +  \lambda_\gamma Y_c 
\end{equation}

Particle $c$ is created by the $a(b,\gamma)c$ reaction and destroyed by the reverse:

\begin{equation}
\frac{dY_c}{dt} =  - \lambda_\gamma Y_c + \rho N_A \langle \sigma v \rangle_{ab} Y_a Y_b   
\end{equation}


Imagine doing the same exercise for thousands of nuclei that are connected
with tens of thousands of reactions!<d-footnote>
This is the size of a typical $r$-process reaction network!</d-footnote>

Most reactions can be grouped into three
functional categories, according to the number of interacting nuclei:
reactions involving a single species, such as decays and electron/positron
captures, two (*e.g.* our fictitious $a(b,\gamma)c$) and three
(*e.g.* $\mathrm{^4He(\alpha \alpha,\gamma)^{12}C}$ -- triple--$\alpha$
reaction) nuclei<d-cite key="hix1999computational"></d-cite>. 
We can write a generalized abundance evolution equation for $Y_i$, or rate
equation, as follows

$$
\begin{aligned}
  \frac{dY_i}{dt} &= \underbrace{\sum_j \mathcal{N}_j^i \lambda_j
  Y_j}_{\text{decays}} \\
 &+\underbrace{\sum_{j,k} \mathcal{N}_{j,k}^i \rho  N_A \langle \sigma v
 \rangle_{jk} Y_j Y_k}_{\text{2-body reactions}} \\
 &+ \underbrace{\sum_{j,k,l}
     \mathcal{N}_{j,k,l}^i (\rho  N_A)^2 \langle \sigma v \rangle_{jkl} Y_j Y_k Y_l}_{\text{3-body reactions}}
\end{aligned}
$$

where $\lambda_j$ is called the decay constant (just imagine solving only the
first part of the equation and $\lambda_j$ will show up as an exponential
factor, similar to a radioactive decay), $\langle \sigma v \rangle_{jk}$ and $\langle \sigma v \rangle_{jkl}$ are
the thermonuclear reaction rates for 2- and 3-body reactions. Note that in the
latter we multiplied by $(\rho N_A)^2$ to account for the third particle. The $\mathcal{N}$s are used to specify
how many particles are created or destroyed in a reaction, and take also into
account double-counting, in case of identical interacting particles. Specifically:

$\mathcal{N}_j^i$ = $N_i$ 

$$\mathcal{N}_{j,k}^i$$ = $$\frac{N_i}{ \prod_{m=1}^{n_{j,k}} \mid N_m \mid!}$$

$$\mathcal{N}_{k,k,l}^i$$ = $$\frac{N_i}{\prod_{m=1}^{n_{j,k,l}} \mid N_m \mid!}$$

We can also express the same relation, more generally as
\begin{equation}
\dot{\mathbf{y}} = f(\mathbf{y})
\end{equation}

where $\mathbf{y}$ is the vector of all the abundances $Y_i$ (or mass
fractions $X_i$) in the network ($Y_1$, $Y_2$, $\cdots$, $Y_N$), and $f$ is 
a function which depends on the abundances $Y_i$ and the thermodynamical 
properties of the environment, $T(t), \rho(t), \cdot$.


***
## <i class="fas fa-clipboard-list"></i> The ingredients

To solve the rate equation numerically we need some input. First and
foremost, we need the nuclear physics information about the isotopes in the
network; that is their reaction rates, reaction Q-values, half-lifes
(if they are radioactive), fission fragment distributions (if they are
fissionable) and partition functions, the sum of thermally populated levels. 

You might wonder why we did not mention nuclear masses, which many researchers measure experimentally.
The nuclear masses enter the rate equation via the Q-value (for example in
neutron captures, photodissociation rates and $\beta$-decays). If a new
mass measurement is made, that updates the Q-value in the network. 
<div class="fake-img l-gutter">
  <p><b>See A. Kankainen lecture</b></p>
</div>

For example, in the $r$-process, $(\gamma, n)$ rates depend on the mass
difference, or *neutron separation energy* $S_n$ as follows<d-cite
key="mumpower2016ppnp"></d-cite>

\begin{equation}
\lambda_\gamma \propto
T^{3/2} \exp\left[ -\frac{S_n(Z,N)}{kT} \right]  \langle \sigma v \rangle_{(Z, N-1)} 
\end{equation}

Another nuclear input that is used when solving a thermonuclear reaction
network is the Equation Of State (EOS), which gives us the relation between 
temperature, pressure, and density in the gas. In some special cases, where 
the neutrino properties are of interest (*e.g.* in neutrino-driven wind
ejecta) we also need to know the evolution of neutrino-related quantities, 
such as their luminosity.

As far as the astrophysics input is concerned we are mainly interested 
in the time evolution of the temperature and density of the plasma and 
in many cases its electron mole fraction $Y_e \equiv n_p (n_p+n_n)^{-1}$ -
$Y_e$ = 1 only protons, $Y_e$= 0 only neutrons<d-footnote>The
neutrons will start to decay, so that state cannot remain for long!</d-footnote>.

The properties of the astrophysical environment can be obtained from hydrodynamic
simulations. For explosive nucleosynthesis processes, a common technique is to
use "tracer particles" <d-cite key="travaglio2004nucleosynthesis"></d-cite>,
which are mass packets advected with the flow of the gas and follow the
evolution of key parameters as a function of time (*e.g.* temperature and density).
It is also common to create "parametric profiles" if there is a
simple time dependence of temperature/density (see for example the work of 
Iliadis *et al* (2018)<d-cite key="iliadis2018apj"></d-cite>), which is
computationally less expensive and it also allows for the exploration of 
the relevant parameter phase space.


***
## <i class="fas fa-pen"></i> Solving the network

To find the abundance $Y_i$ for each species $i$ in our reaction network, we
need to solve (integrate) the Rate equation. The main challenge comes from the nature of
the thermonuclear reactions, where some of them are much faster (slower) than
others.

Thermonuclear reaction networks are
known to be very *stiff*, meaning that their solution is
numerically unstable, and as such, smaller steps of
integration must be used. Stiffness in a network arises from
the fact that its differential equations include very slow and
very fast reactions simultaneously. For this reason, it is
computational challenging to include many species in a stellar
evolution hydrodynamic code since it causes a slowdown on
its performance, and thus post-processing nucleosynthesis
calculations are preferred.



These systems are known to be *stiff* given to that property. Let us examine 
an example of a stiff equation:

\begin{equation}\label{eq:stiff}
\dot{x} = -21 x(t) + e^{-t}
\end{equation}

with boundary condition $$ x(0) = 0$$.

<d-code block language='python'>
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Define the function for the stiff equation
def stiff_eq(t, y):
     return  -21 * y + np.exp(-t) 
# Set the initial condition and time range for the solution
y0 = [0]
t_span = [0, 10]

# Define a function to track the step size used by the solver
def track_step_size(t, y):
    if sol.t_events is not None:
        track_step_size.steps.append(np.abs(sol.t_events[0][0] - t))
    return 0

# Initialize an empty list to store the step sizes
track_step_size.steps = []

# Use solve_ivp to solve the equation numerically
sol = solve_ivp(stiff_eq, t_span, y0, method='Radau', 
	  dense_output=True, events=lambda t, y: track_step_size(t, y))

# Create an array of times to evaluate the step size at
t_eval = np.linspace(0, 10, len(track_step_size.steps))

# Evaluate the solution at the desired times
y = sol.sol(t_eval).T

# Plot the solution and the step size in subplots
fig, axs = plt.subplots(2, sharex= True)
fig.subplots_adjust(hspace=0)

axs[0].plot(t_eval, y, color='k')
axs[0].set_ylabel('x(t)')
axs[0].tick_params(direction='in', which='both', right=True, top=True)
axs[0].minorticks_on()

axs[1].plot(t_eval, track_step_size.steps, color='k')
axs[1].set_ylim(1e-3,20)
axs[1].set_xlabel('t')
axs[1].set_ylabel('Step size')
axs[1].set_yscale('log')
axs[1].tick_params(direction='in', which='both', right=True, top=True)
axs[1].minorticks_on()

fig.align_ylabels()

plt.show()
</d-code>


<center>
        <div class="col-sm mt-2 mt-md-0">
            <img
    src="{{ site.baseurl }}/assets/img/stiff.svg"
    class="img-fluid" zoomable=true>
	<div class="col three caption">                                                                                                
     (Top) The solution of the differential equation \ref{eq:stiff} as a function of
        time. (Bottom) The step size used by the solver to reach to the
        solution. At early times $\Delta t \ll 1$ and at later times $\Delta t
        \approx t $.
    </div>
	</div>
</center>


Various numerical techniques can be used to solve (integrate)
such networks. Reaction network codes, such as NuGrid
NuPPN, employ
mostly the
backward (implicit) Euler method, "Wagoner's method" <d-cite key="wagoner1969synthesis"></d-cite>,
Gear's method <d-cite key="gear1971automatic"></d-cite> or
the Bader-Deuflhard semi-implicit method <d-cite key="bader1983semi"></d-cite>. For more details on the
integration of nuclear reaction networks, we refer
the reader to the work of <d-cite key="timmes1999integration"> and of <d-cite key="longland2014performance"></d-cite>.

### The Jacobian matrix

Another way to define stifness in a system of equations it to 
take the ratio of the real part of the largest eigenvalue $\lambda_{max}$
of the Jacobian 
In the networks that are common for nuclear astrophysics we get
$\lambda_{max}/\lambda_{min} > 10^{15}$ due to the wide range in timescales
between strong, electromagnetic and weak interactions
(example of p+p and some other reaction)

<d-cite key="travaglio2013"></d-cite>

<center>
        <div class="col-sm mt-2 mt-md-0">
            <img
    src="https://cococubed.com/images/net_integration/torch127_jac.svg"
    class="img-fluid" zoomable=true>
	<div class="col three caption">                                                                                                
     Graphic representation of a
    Jacobian matrix. The non-coloured squares are zero elements in the
    matrix.  <a href="https://cococubed.com/net_pages/net_torch.shtml">[Fig. source]</a> 
    </div>
        </div>
</center>



***
## <i class="fas fa-burn"></i> Energy generation

As we have already discussed, nuclear reactions release energy from the
conversion of nucleons. The energy released by nuclear reactions in an astrophysical
environment, $\mathrm{\epsilon_{nuclear}}$, can be calculated using

\begin{equation}
    \epsilon_{nuclear}= - \sum_i N_A m_i c^2 \frac{dY_i}{dt}~\text{(MeV/g s})
\end{equation}
where $m_i c^2$ is the rest mass energy of species $i$ in MeV.

The following table shows the energy release from different burning stages<d-cite key="arnett1996supernovae"></d-cite>.


|Process| Burning stage  |q (MeV/nucleon)|
|-------|----------------|---------------|
| $\mathrm{ H \rightarrow ^4He}$ | Hydrogen buning | 5-7 |
| $\mathrm{ 3\alpha \rightarrow ^{12}C}$ | Hydrogen buning | 0.606 |
| $\mathrm{ 4\alpha \rightarrow ^{16}O}$ | Helium buning | 0.902 |
| $\mathrm{ 2^{12}C \rightarrow ^{24}Mg}$ | Helium buning | 0.52 |
| $\mathrm{ 2^{20}Ne \rightarrow ^{16}O+^{24}Mg}$ | Neon buning | 0.11 |
| $\mathrm{ 2^{16}O \rightarrow ^{32}Si}$ | Oxygen buning | 0.52 |
| $\mathrm{ ^{28}Si \rightarrow ^{56}Ni}$ | Silicon buning | 0-0.31 |

typical networks (for hydrodynamics codes)
$\alpha$-nuclei reaction network from He to Ni
$\mathrm{^4He, ^{12}C, ^{16}O, ^{20}Ne, ^{24}Mg, ^{28}Si, ^{32}S, ^{36}Ar, ^{40}Ca, ^{44}Ti, ^{48}Cr, ^{52}Fe, ^{56}Ni}$
connected mainly by $(\alpha,\gamma)-(\gamma,\alpha)$ reactions, the triple-$\alpha$ reaction and the heavy ion reactions
$\mathrm{^{12}C+^{12}C, ^{12}C+^16}O, ^{16}O+^{16}O}$



***
##  Two special cases

In general we jsut need to solve the network equation for every different
astrophysical conditions, however there are two special cases, where
the network can be solved very easily.

### Steady-state
- Steady-state [e.g. hydrogen burning through the CNO cycle]

\begin{equation}
Y_i^{steady} = \frac{P_i}{D_i}
\end{equation}


example? (Iliadis or Arnett)


### Nuclear Statistical Equilibrium (NSE)

In the special case of Nuclear Statistical Equilibrium (NSE),
where all nuclides are in equilibrium via strong and
electromagnetic interactions, the reaction network is greatly
simplified and the abundance, $Y_i$, of each species can be
calculated in terms of the free protons, $Y_p$, and neutrons,
$Y_n$, by applying the Saha equation

\begin{equation}
    Y_i = G_i \left(\rho N_A\right)^{A_i-1} \frac{A_i^{3/2}}{2_i^A} \left( \frac{2\pi \hbar^2}{m kT}\right)^{\frac{3}{2}(A_i-1)} e^{B_i/kT} Y_n^{N_i} Y_p^{Z_i}
\end{equation}

where $G_i$ and $B_i$ is the partition function and binding
energy of species $i$, $A$ is its mass number, $N$ the number of neutrons, 
$Z$ the number of protons and $\rho$ and $T$ are the density and 
temperature of the environment. The unique solution of the network for 
($T,\rho,Y_e$) can be obtained using two constraints, namely mass (Equation
\ref{eq:3} or \ref{eq:4}) and charge conservation

\begin{equation}\label{eq:0}
\sum_i Z_i Y_i = Y_e
\end{equation}

where $Y_e = n_p/(n_p+n_n)$ is called the **electron mole fraction**. If $Y_e
< 0.5$ we have a neutron-rich gas, and in the case of $Y_e>0.5$
we have a neutron-deficient one. This is very important for some
nucleosynthesis processes.


<center>
        <div class="col-sm mt-2 mt-md-0">
            <img
    src="{{ site.baseurl }}/assets/img/nse-iliadis.png"
    class="img-fluid" zoomable=true>
		<div class="col three caption">
		 Abundances of the dominant species versus neutron excess parameter $\eta$ 
		 (or electron mole fraction $Y_e$) in a nuclear statistical equilibrium composition at
		 T = 3.5 GK and ρ = 10<sup>7</sup> g/cm<sup>3</sup> . The abundances
        on either side of $\eta$ = 0 ($Y_e$ = 0.5) show a different behavior. 
		</div>
	</div>
</center>



***
## <i class="fas fa-code"></i> The codes

After all this discussion about reaction networks, do you want to run some
calculations? That's great! 😁 There are many codes in the nuclear
astrophysics community that are used for different nucleosynthesis processes;
some of them are open-source, others are not. I have compiled a
non-exhaustive list of such codes in the following table<d-footnote>If there are codes that I am missing, please
<a href="mailto:psaltis.tha@duke.edu">contact me</a> and I will include them!</d-footnote>

| Name  | Description | Is it open-source? | Reference  |
|:----- |:-----------:|:------------------:|:---------------------------:|
| GSINet | <i class="fas fa-code-branch"></i> of BasNet| <i class="fas fa-times"></i>   | Mendoza-Temis *et al.* (2015) <d-cite key="mendoza2015prc"></d-cite>   | 
| NucNet [<i class="fas fa-external-link-alt"></i>](https://sourceforge.net/p/nucnet-tools/home/Home/)  | example text |    <i class="fas fa-check"></i>  | Meyer (2012) <d-cite key="meyer2012webnucleo"></d-cite> |
| NuPPN [<i class="fas fa-external-link-alt"></i>](https://nugrid.github.io/content/codes_collab)  | example text | Within the NuGrid collaboration    | Pignatari *et al.* (2016) <d-cite key="pignatari2016apjs"></d-cite>  |
| PRISM  |    r-process mainly              |   <i class="fas fa-times"></i>   | Sprouse *et al.* (2021) <d-cite key="sprouse2021prc"></d-cite>  | 
| SkyNet [<i class="fas fa-external-link-alt"></i>](https://bitbucket.org/jlippuner/skynet) | Text   | <i class="fas fa-check"></i> | Lippuner and Roberts (2017) <d-cite key="lippuner2017"></d-cite>|
| torch [<i class="fas fa-external-link-alt"></i>](https://cococubed.com/code_pages/burn.shtml)        | Text | <i class="fas fa-check"></i>   | Timmes (1999) <d-cite key="timmes1999integration"></d-cite>   |
| WinNet   | <i class="fas fa-code-branch"></i> of BasNet  |   <i class="fas fa-times"></i>       |  Winteler *et al.* (2012) <d-cite key="winteler2012apjl"></d-cite>               |
| XNet  [<i class="fas fa-external-link-alt"></i>](https://github.com/starkiller-astro/XNet)           | Both post-processing and reduced network                                          |   <i class="fas fa-check"></i>                 | Hix and Meyer (2006) <d-cite key="hix2006thermonuclear"></d-cite>               |





### The solvers

For those that are interested in the nitty-gritty of ODE solvers for thermonuclear reaction networks, I have compiled a short list of the most commonly used ones:
- Intel MKL
- SuperLU
- BLAS
- Pardiso
- Armadillo
- Trilinos
- LAPACK



Syntax highlighting is provided within `<d-code>` tags.
An example of inline code snippets: `<d-code language="html">let x = 10;</d-code>`.
For larger blocks of code, add a `block` attribute:

**Note:** `<d-code>` blocks do not look good in the dark mode.
You can always use the default code-highlight using the `highlight` liquid tag:



The main text column is referred to as the body.
It is the assumed layout of any direct descendants of the `d-article` element.

<div class="fake-img l-body">
  <p>Nuclear reaction networks is an indispensable tool for a nuclear
  astrophysicist. Learn how it works and use it to your advantage!</p>
</div>



***
## <i class="fas fa-cogs"></i>  Sensitivity studies using reaction networks

One of the awesome things we can do using thermonuclear reaction networks, given the capabilities of modern computers, is multiple (>thousands) calculations of the same profile (astrophysical condition). What can we learn from that? By changing individual nuclear parameters, for example a reaction rate, one can see the effect in the final elemental or even isotopic abundance pattern. Through the years researchers in our field have taken different approaches for these sensitivity studies. In the 2000s it was common to vary individually reaction rates within their uncertainty: a typical example is the seminal work of Iliadis *et al* <d-cite key="iliadis2002nova"></d-cite> on classical novae nucleosynthesis. In that study the authors varied 175 reaction rates (out of 1265) in a 142 species network, from the then most recent evaluations. The goal was to find reactions which *rate uncertainty* affects isotopic abundances in classical novae. They found ~20 reactions - $(p,\gamma)$ and $(p,\alpha)$ which affect isotopic abundances in CO and ONe novae. The work of Ref.<d-cite key="iliadis2002nova"></d-cite> motivated a series of experimental measurements through the 2000s and 2010s, both direct and indirect, that reduced the uncertainties of the highlighted reaction rates.

During the 2010s researchers start using Monte Carlo (MC) algorithms to
perform sensitivity studies. In this class of works - some notable examples
for different nucleosynthesis scenarios are listed in the table below -
reaction rates are randomly sampled from a distribution, which reflects their
uncertainty, in every calculation. The reactions that influence abundances 
are identified by the *correlation* between the factor by which the 
rate was changed and the effect in the abundance.


| Scenario         | Reference                   |  Notes |
|------------------|:---------------------------:|------:|
| BBN              | Iliadis and Coc (2020) <d-cite key="iliadis2020apj"></d-cite>  | MC study using Bayesian rates   |
| Nova nucleosynthesis | Iliadis *et al* (2002)<d-cite key="iliadis2002nova"></d-cite> | Individual rates change |
| $s$-process      | Cescutti *et al.* (2018) <d-cite key="cescutti2018mnras"></d-cite>              | MC study    |
| $i$-process      | Denissenkov *et al.* (2021) <d-cite key="denissenkov2021mnras"></d-cite> | MC study of $(n, \gamma)$ rates   |
| weak $r$-process | Bliss *et al.* (2020) <d-cite key="bliss2020prc"></d-cite>, Psaltis *et al.* (2022) <d-cite key="psaltis2022apj"></d-cite>| MC study of $(\alpha, n)$ rates   |
| $\nu p$-process  | Wanajo *et al* (2011) <d-cite key="wanajo2011apj"></d-cite>, Nishimura *et al.* (2019) <d-cite key="nishimura2019mnras"></d-cite>     | Individual rates, MC study   |
| $r$-process      | Mumpower *et al.* (2016) <d-cite key="mumpower2016ppnp"></d-cite>            | MC study on nuclear masses, β-decay halflives and $(n,\gamma)$ rates    |
| $\gamma$-process | Rauscher *et al.* (2016) <d-cite key="rauscher2016mnras"></d-cite>            | MC study   |
| $rp$-process     | Parikh *et al.* (2008) <d-cite key="parikh2008apj"></d-cite>,  Cyburt *et al.* (2016) <d-cite key="cyburt2016apj"></d-cite> | Individual rates change  |
| Type Ia nucleosynthesis | Parikh *et al* (2013) <d-cite key="parikh2013aa"></d-cite>, Nishimura *et al.* (2018) <d-cite key="nishimura2018mnras"></d-cite> | Individual rates change, MC study   |


Markov Chain Monte Carlo (MCMC) techniques have also being used for nuclear inputs (see the work of Ref.<d-cite key="vassh2021mcmc"></d-cite>)

## <i class="fas fa-exclamation"></i> Take-home message

If there is one thing you should remember from this lecture, it is the following:

> Nuclear reaction networks are an indispensable tool for a nuclear astrophysicist. Learn how it works and use it to your advantage!
