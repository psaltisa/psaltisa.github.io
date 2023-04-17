---
layout: distill
permalink: /teaching/reaction-networks
title: An introduction to thermonuclear reaction network calculations
description: Lecture notes for the 2nd Frontiers Summer School
date: 2023-05-16

authors:
  - name: Thanassis Psaltis
    url: "mailto: psaltis.tha@duke.edu"
    affiliations:
      name: TUNL, NC State University

bibliography: networks.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: The ingredients
  - name: Solving the network
  - name: The codes

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

## Introduction

or what is a reaction network and why does it matter?

You might have not realized it, but if you are working in nuclear astrophysics, your work is very closely related to nuclear reaction networks. Before we get into the specifics, let me give you some practical examples:

- Student A works in low energy experimental nuclear physics and she measured the cross section of an astrophysically interesting reaction for her dissertation,
- Student B is an observational astronomer and has measured the abundances of Galactic metal-poor stars
- Postdoc C works in nuclear theory and has implemented a new Equation of State (EoS) to be used in NS and SN simulations

GCE, new yields


What do they all have in common? Their results are inteconnected using nuclear reaction networks!

Networks can be found everywhere, they are groups of interconnected things. The most common example is *social networks*, your family, friends, colleagues and the rest of the people you are interacting socially (nowadays there are also virtual counterparts of these networks).

Similarly, thermonuclear reaction networks connect nuclei via (you guessed it) nuclear reactions (or other nuclear processes).

We will discuss how these reactions enter the network, when they matter and when they don't.

these reactions are called *thermonuclear* since they are caused by the thermal motion
of the involved nuclei, which obey a Maxwellian distribution.
<d-cite key="iliadis2017nuclear"></d-cite>
<d-cite key="rolfs1988cauldrons"></d-cite>

The thermonuclear reaction rates we studied in the previous
section are used to calculate the abundance evolution of
nuclear species and the energy release by these reactions
in an astrophysical environment. A system of
first-order coupled differential equations, which describes
this abundance evolution and energy generation
is called a nuclear reaction network.
The size of these networks can vary according to the
astrophysical environment, with quiescent stellar burning being much
smaller compared to explosive burning. For example, a $\nu
p$-process nucleosynthesis network can include 5,000 nuclei and
around 50,000 reactions. In this section we shall
introduce nuclear reaction networks.

To begin, the abundance, or number fraction, $Y_i = n_i/(\rho N_A)$, of
the nuclear species $i$ in an astrophysical
environment is a dynamical quantity, dependent on the nuclear
processes that occur. It is more convenient to use abundances rather than
number densities $n_i$ in reaction network calculations since the
latter quantity changes with both the number of the species $i$ and
the volume of the astrophysical system <d-cite key="lippuner2017"></d-cite>.
Most reactions can be grouped into three
functional categories, according to the number of interacting nuclei:
reactions involving a single nucleus, such as decays and electron/positron
captures, two (*e.g* $\isotope[7][]{Be}(\alpha,\gamma)\isotope[11][]{C}$) and three
(*e.g* $\mathrm{^4He(\alpha \alpha,\gamma)^{12}C}$ -- triple--$\alpha$ reaction) nuclei<d-cite key="hix1999computational"></d-cite>. We can write a generalized abundance evolution equation for $Y_i$, or rate equation,
as follows

$$
  \frac{dY_i}{dt} = \underbrace{\sum_j \lambda_j Y_j}_{\text{decays}}
  +\underbrace{\sum_{j,k}  \lambda_{jk}
      Y_j Y_k}_{\text{2-body reactions}} + \underbrace{\sum_{j,k,l}
      \lambda_{jkl} Y_j Y_k Y_l}_{\text{3-body reactions}}
$$

we can also express the same relation, more generally as:
$$
\dot{\mathbf{y}} = f(\mathbf{y})
$$
where $\mathbf{y}$ is the vector of all the abundances $Y_i$ in the network.

where the quantities $\lambda_j$, $\lambda_{j,k}$ and $\lambda_{j,k,l}$ are
the rates of these reactions, which are related to the thermonuclear reaction
rates we calculated earlier in this chapter. For the case of a two-body
reaction, we can write



In the special case of Nuclear Statistical Equilibrium (NSE),
where all nuclides are in equilibrium via strong and
electromagnetic interactions, the reaction network is greatly
simplified and the abundance, $Y_i$, of each species can be
calculated in terms of the free protons, $Y_p$, and neutrons,
$Y_n$, by applying the Saha equation

$$
\frac{dY_i}{dt} &= 0 \\
    Y_i &= G_i \left(\rho N_A\right)^{A_i-1} \frac{A_i^{3/2}}{2_i^A} \left( \frac{2\pi \hbar^2}{m kT}\right)^{\frac{3}{2}(A_i-1)} e^{B_i/kT} Y_n^{N_i} Y_p^{Z_i}
$$

where $G_i$ and $B_i$ is the partition function and binding
energy of species $i$, $A$ is its mass number, $N$ the number of neutrons, $Z$ the number of protons and $\rho$ and $T$
are the density and temperature of the environment. The unique
solution of the network for ($T,\rho,Y_e$) can be obtained
using two constraints, namely mass and charge conservation

$$
\sum_i A_i Y_i &= 1 \\
\sum_i Z_i Y_i &= Y_e
$$


The energy released by nuclear reactions in an astrophysical
environment, $\mathrm{\epsilon_{nuclear}}$, can be calculated using
Equation~\ref{ch2:eq19}
\begin{equation}\label{ch2:eq19}
    \epsilon_{nuclear}= - \sum_i N_A m_i c^2 \frac{dY_i}{dt}~\text{(MeV/g s})
\end{equation}
where $m_i c^2$ is the rest mass energy of species $i$ in MeV.

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

***
## The rate equation

Let us now discuss an example of a very simple network that has only three
nuclei, conveniently named as a, b and c.

Our simple network has only three reactions:

$$ a + b \rightleftharpoons c + \gamma$$

$$ b \rightarrow a$$

The fusion of $a$ and $b$ produce $c$ and a $\gamma$ ray (similarly the photodissociation of $c$ creates $a$ and $b$), and $b$ can decay to $a$.

Let's write down the differential equation that describes the time evolution of the abundance of nucleus $a$:

$$ \frac{d n_a}{dt} = - n_a n_b \langle \sigma v \rangle $$

Imagine doing the same exercise for thousands of nuclei that are connected with tens of thousands of reactions!
<div class="fake-img l-gutter">
  <p>This is a typical $r$-process reaction network!</p>
</div>

***
## Thermonuclear reaction rates

\begin{equation}\label{therm}
    N_A \langle \sigma v \rangle_{ab} = \left( \frac{8}{\pi \mu}\right)^{1/2} (kT)^{-3/2} N_A \int_0^\infty \sigma(E) E  e^{-E/kT} dE
\end{equation}

Equation~\ref{therm} is a general expression for the thermonuclear reaction
rate. In principle, the only missing piece for its calculation
is the energy--dependent reaction cross section, $\sigma(E)$. Once this
quantity is either measured experimentally, or estimated theoretically,
Equation~\ref{ch2:eq6}
can be integrated numerically and then evaluated at the temperature of
interest.



Hauser-Feshbach estimates of reaction rates
<div class="fake-img l-gutter">
  <p>See G. Perdikakis lecture</p>
</div>




***
## The ingredients

To solve the rate equation numerically we will need some input. First and foremost, we need the nuclear physics information about the isotopes in the network; that is mainly their reaction rates, reaction Q-values, half-lifes (if they are radioactive), fission fragment distributions (if they are fissionable) and partition functions, the sum of thermally populated levels. You might ask here why I did not mention nuclear masses, which many people try to measure experimentally.
<div class="fake-img l-gutter">
  <p>See A. Kankainen lecture</p>
</div>
The nuclear masses enter the rate equation via the reaction Q-value. Another nuclear input that is used when solving a thermonuclear reaction network is the Equation Of State (EOS), which gives us the relation between temperature, pressure, and density in the plasma. In some special cases, where the neutrino properties are of interest, for example in neutrino-driven wind ejecta, we also need to know the evolution of neutrino-related quantities, such as their luminosity.

As far as the astrophysics input is concerned we are mainly interested in the time evolution of the temperature and density of the plasma and in many cases its electron fraction $Y_e$.


astrophysical conditions, mainly the time evolution of temperature and density, for some special cases the evolution of
neutrino-related quantities,



- tracer particles
- parametric trajectories

the nuclear physics input: mainly reaction rates, partition functions, half-lifes, fission fragment distributions, nuclear masses and more


<d-cite key="jiang2021nuclear">D et al.</d-cite>
<d-cite key="hix2006thermonuclear"></d-cite>

typical networks (for hydrodynamics codes)
$\alpha$-nuclei reaction network from He to Ni
$\mathrm{^4He, ^{12}C, ^{16}O, ^{20}Ne, ^{24}Mg, ^{28}Si, ^{32}S, ^{36}Ar, ^{40}Ca, ^{44}Ti, ^{48}Cr, ^{52}Fe, ^{56}Ni}$
connected mainly by $(\alpha,\gamma)-(\gamma,\alpha)$ reactions, the triple-$\alpha$ reaction and the heavy ion reactions
$\mathrm{^{12}C+^{12}C, ^{12}C+^16}O, ^{16}O+^{16}O}$


***
## Solving the network


integrate the rate equation


Various numerical techniques can be used to solve (integrate)
such networks. Reaction network codes, such as NuGrid
NuPPN, employ
mostly the
backward (implicit) Euler method, "Wagoner's method" <d-cite key="wagoner1969synthesis"></d-cite>,
Gear's method <d-cite key="gear1971automatic"></d-cite> or
the Bader-Deuflhard semi-implicit method <d-cite key="bader1983semi"</d-cite>. For more details on the
integration of nuclear reaction networks, we refer
the reader to the work of <d-cite key="timmes1999integration"> and of <d-cite key="longland2014performance"></d-cite>.




***

## The codes

After all this discussion about reaction networks, do you want to run some calculations? That's great! 😁 There are many codes in the nuclear astrophysics community that are used for different nucleosynthesis processes; some of them are open-source, others are not. A non-exhaustive list of such codes include the following<d-footnote>If there are codes that I am missing, please
<a href="mailto:psaltis.tha@duke.edu">contact me</a> and I will include them!</d-footnote>:


| Name      | Description | Is it open-source? |
| ----------- | ----------- | -------------------------------------|
| NuPPN      | Title       | |
| WinNet   | Text        | |
| SkyNet [<i class="fas fa-external-link-alt"></i>](https://bitbucket.org/jlippuner/skynet)   | Text        | |
| GSINet   | Text        | |
| PRISM   | Text        |  |
| NucNet-Tools [<i class="fas fa-external-link-alt"></i>](https://sourceforge.net/p/nucnet-tools/home/Home/)   | Text |  |
| Torch [<i class="fas fa-external-link-alt"></i>](https://cococubed.com/code_pages/burn.shtml)  | Text        |  |
| XNet  [<i class="fas fa-external-link-alt"></i>](https://github.com/starkiller-astro/XNet)  | Text        |   |





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

<d-code block language="javascript">
  var x = 25;
  function(x) {
    return x * x;
  }
</d-code>

**Note:** `<d-code>` blocks do not look good in the dark mode.
You can always use the default code-highlight using the `highlight` liquid tag:



The main text column is referred to as the body.
It is the assumed layout of any direct descendants of the `d-article` element.

<div class="fake-img l-body">
  <p>.l-body</p>
</div>

For images you want to display a little larger, try `.l-page`:

<div class="fake-img l-page">
  <p>.l-page</p>
</div>

All of these have an outset variant if you want to poke out from the body text a little bit.
For instance:

<div class="fake-img l-body-outset">
  <p>.l-body-outset</p>
</div>

<div class="fake-img l-page-outset">
  <p>.l-page-outset</p>
</div>

Occasionally you’ll want to use the full browser width.
For this, use `.l-screen`.
You can also inset the element a little from the edge of the browser by using the inset variant.

<div class="fake-img l-screen">
  <p>.l-screen</p>
</div>
<div class="fake-img l-screen-inset">
  <p>.l-screen-inset</p>
</div>

The final layout is for marginalia, asides, and footnotes.
It does not interrupt the normal flow of `.l-body` sized text except on mobile screen sizes.

<div class="fake-img l-gutter">
  <p>This is a sidenote</p>
</div>


Colons can be used to align columns.

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |


> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote.

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-2 mt-md-0">
            {% include figure.html path="https://cococubed.com/images/net_integration/aprox13.svg" class="img-fluid" zoomable=true caption="Graphic representation of a Jacobian matrix. The non-coloured squares are zero elements in the matrix. Figure [source](https://cococubed.com/pix_pages/sparse.shtml)." %}
        </div>
    </div>
</center>

***
## Sensitivity studies using reaction networks

One of the awesome things we can do using thermonuclear reaction networks, given the capabilities of modern computers, is multiple (>thousands) calculations of the same profile (astrophysical condition). What can we learn from that? By changing individual nuclear parameters, for example a reaction rate, one can see the effect in the final elemental or even isotopic abundance pattern. Through the years researchers in our field have taken different approaches for these sensitivity studies. In the 2000s it was common to vary individually reaction rates within their uncertainty: a typical example is the seminal work of Iliadis *et al* <d-cite key="iliadis2002nova"></d-cite> on classical novae nucleosynthesis. In that study the authors varied 175 reaction rates (out of 1265) in a 142 species network, from the then most recent evaluations. The goal was to find reactions which *rate uncertainty* affects isotopic abundances in classical novae. They found ~20 reactions - $(p,\gamma)$ and $(p,\alpha)$ which affect isotopic abundances in CO and ONe novae. The work of Ref.<d-cite key="iliadis2002nova"></d-cite> motivated a series of experimental measurements through the 2000s and 2010s, both direct and indirect, that reduced the uncertainties of the highlighted reaction rates.

During the 2010s researchers start using Monte Carlo (MC) algorithms to perform sensitivity studies. In this class of works - some notable examples for different nucleosynthesis scenarios are listed in Table - reaction rates are randomly sampled from a distribution in every calculation. The reactions that influence abundances are also identified by the *correlation* between the factor by which the rate was changed and the effect in the abundance.


| Scenario        |Reference           | Cool  |
| ------------- |:-------------:| -----:|
| weak $r$-process      | Bliss et al.  | $1600 |
| $r$-process      | Mumpower et al.      |   $12 |
| $\nu p$-process | Nishimura et al.      |    $1 |
| $\gamma$-process | Rauscher et al.      |    $1 |
| $rp$-process | Parikh et al. Cyburt et al.      |    $1 |
| $i$-process | Denissenkov et al.      |    $1 |
| $s$-process | Hirschi et al.     |    $1 |
| BBN | Coc et al. Iliadis et al.    |    $1 |

Markov Chain Monte Carlo (MCMC) techniques have also being used for nuclear inputs (see the work of Ref.<d-cite key="vassh2021mcmc"></d-cite>)
