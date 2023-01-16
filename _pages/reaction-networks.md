---
layout: distill
permalink: /teaching/reaction-networks
title: An introduction to thermonuclear reaction network calculations
description: Lecture notes for Frontiers Summer School 2023
date: 2022-01-01

authors:
  - name: Thanassis Psaltis
    url: "mailto: apsalti@ncsu.edu"
    affiliations:
      name: TUNL, NCSU

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
## The ingredients

astrophysical conditions, mainly the time evolution of temperature and density, for some special cases the evolution of
neutrino-related quantities,

- tracer particles
- parametric trajectories

the nuclear physics input: mainly reaction rates, partition functions, half-lifes, fission fragment distributions, nuclear masses and more


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

<d-cite key="jiang2021nuclear">D et al.</d-cite>
<d-cite key="hix2006thermonuclear"></d-cite>

some are open-source, others not

- NuPPN
- WinNet
- SkyNet [<i class="fas fa-external-link-alt"></i>](https://bitbucket.org/jlippuner/skynet)
- GSINet
- PRISM (Portable Routines for Integrated nucleoSynthesis Modeling)
- NucNet-Tools [<i class="fas fa-external-link-alt"></i>](https://sourceforge.net/p/nucnet-tools/home/Home/)
- Torch [<i class="fas fa-external-link-alt"></i>](https://cococubed.com/code_pages/burn.shtml)
- XNet (reduced and full post-processing) [<i class="fas fa-external-link-alt"></i>](https://github.com/starkiller-astro/XNet)
- ReNet (reduced)
- pynucastro

and many others


### The solvers

- Intel MKL
- SuperLU
- BLAS
- Pardiso
- Armadillo
- Trilinos
- LAPACK

etc..
<d-footnote>I made a footnote.</d-footnote>


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
            {% include figure.html path="https://cococubed.com/images/net_integration/jac_3zones.svg" class="img-fluid" zoomable=true caption="Graphic representation of a Jacobian matrix." %}
        </div>
    </div>
</center>

***
## Sensitivity and impact studies
