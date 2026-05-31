---
layout: distill
permalink: /teaching/gamma-beams
title: Nuclear astrophysics with γ beams
description: Lecture notes for the 13th European Summer School on Experimental Nuclear Astrophysics
date: 2026-06-16

authors:
  - name: Thanassis Psaltis
    url: "mailto: thanassis.psaltis@smu.ca"
    affiliations:
      name: Saint Mary's University

bibliography: gamma-beams.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
 - name: #Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
 - name: The origin of p-nuclei, an open question for nuclear astrophysics
 #- name: γ-beam production techniques
 #- name: Major facilities
 #- name: γ-beam properties
 #- name: Detailed balance
 #- name: Stellar enhancement and partition functions
 #- name: Hauser-Feshbach
 #- name: Case study: 102Pd+γ at HIγS (TUNL)
 #- name: Summary
 - name: Broader implications and open questions
# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _sty  les block.
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


## The origin of p-nuclei, an open question for nuclear astrophysics

A small group of around 35 stable neutron--deficient nuclei with A $\geq$ 74  between selenium (Se) and mercury (Hg) cannot be produced by the two main neutron-capture processes (s- and r-process).
These are referred to as **p-nuclei** and their origin is a long-standing puzzle.

The fact that a distinct process produces these isotopes had been already identified from the early days of our field by both Cameron<d-cite key="cameron1957nuclear"></d-cite> and Burbidge et al.<d-cite key="burbidge1957synthesis"></d-cite>.
They were referred to as "excluded" nuclei, since they were "shielded" by the s- and the r-process reaction path.

<center>                                                                          
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/flow.svg" data-zoomable="">
     </div>
     <div class="caption">
      Section of the nuclear chart relevant to the production of the p-nucleus $^{102}$Pd. All coloured isotopes are stable (with origins form different processes), and the white ones are radioactive. The arrows show the photodisintegration reactions. Note that the p-nuclei cannot be reached by either the s- or r-process, since they are shielded by the stable isotopes of the same element. Figure adapted from <d-cite key="Rauscher2013"></d-cite>.
      </div>
</center>


For this reason their solar abundances<d-footnote>Note that since p-nuclei are so rare, we have not observed them in other stars other than the Sun.</d-footnote> are around one to two orders of magnitude smaller than the s- and r-counterparts, as shown in the figure below, and no single p-nucleus is the most abundant isotope of
any element.


<center>                                                                                          
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/Arnould-PhysRep-2003.png" zoomable=true>
     </div>
     <div class="caption">
     Solar abundances for s-, r-, and p-nuclei. The figure is adapted from <d-cite key="arnould2003"></d-cite>. The p-nuclei are much more rare compared to the other heavy elements, this is why their origin is so interesting!
      </div>
</center>


It is generally accepted that the p-nuclei in the solar system have been produced by more than one processes; however their synthesis mechanism is commonly referred to as **p-process**.
In the following we shall focus on one scenario operating in massive stars called the $\gamma$-process.


## $\gamma$ process nucleosynthesis

Core-collapse supernovae (ccSNe) have 


<d-cite key="Pignatari2016"></d-cite>
<d-cite key="Rauscher2013"></d-cite>
<d-cite key="Roberti2023"></d-cite>


The final abundances depend sensitively on whether a nucleus emits a neutron, proton, or α particle (see the first figure)

More recently, C-O shell mergers in the pre-explosion face as a candidate for the production of the p-nuclei via the $\gamma$ process <d-cite key="Roberti2023, Issa2026"></d-cite>.

In a similar context, rotating massive stars have been proposed as a site for the production of p-nuclei <d-cite key="Choplin2022"></d-cite>

Another viable astrophysical scenario for the production of the p-nuclei is thermonuclear supernovae (type Ia). 
In this explosion, a white dwarf is disrupted when its mass suprasses the Chandrasekhar limit, while accreting material from a companion star. 
The production of p-nuclei in type Ia supenovae has been studied in detail in the literature and it strongly depends on the initial composition of the white dwarf
<d-cite key="Travaglio2011, Battino2020"></d-cite>

$\nu$-process in core-collapse supernovae (citation)
and $\nu p$-process in proton-rich ejecta in neutrino-driven winds of ccSNe


<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/shock.png" zoomable=true>
     </div>
     <div class="caption">
     shock wave
      </div>
</center>

Accreting neutron stars via the rp-process have also been shown to produce p-nuclei, via proton captures instead of photon disintegrations, however it is not clear if they can contribute to the galactic chemical evolution due to extremely large escape velocities from a neutron star surface that hinders andy ejection of material in the interstellar medium<d-footnote>Interestingly, studies that include rotation in the neutron star have shown both a reduced production of p-nuclei but a significantly higher mass ejection than non-rotating models.</d-footnote>



Despite our ability to reproduce most of the p-nuclei abundances of the solar system to within a factor of 2, there are still a few cases where the $\gamma$-process fails to reproduce in sufficient amounts; notable examples include the light $^{92,94}$Mo, $^{96,98}$Ru, $^{113}$In, $^{115}$Sn, $^{138}La$, $^{180}$Ta that most likely have contributions from other processes.


The $\gamma$ process network is vast, involving more than 2000 nuclei (most of them radioactive) with >20,000 reactions! 

temperatures between 2-3.5 GK

## Theoretical Modeling (Hauser-Feshbach)

Given the size of the network, it is impossible to gain information for all the reactions. 
For this reason we rely heavily on theoretical estimates of the relevant nuclear reactions. 
At the intermediate and heavy mass regime, where the nuclear level densities are rather high, we can apply the Hauser-Feshbach model of nuclear reactions to extract cross-sections and reaction rates to be used in nucleosynthesis calculations.

Many codes can perform these calculations, with the most well-known in our community being:
- TALYS <d-cite key="Koning2023"></d-cite>
- NON-SMOKER
- SMARAGD
- EMPIRE and many more!

 Uncertainties propagate to nucleosynthesis predictions!

  1. optical-model potential (OmMP)
  2. $\gamma$-strength function (GSF)
  3. nuclear level density (NLD)

In the following example, we have plotted the reaction rates for the three competing reaction channels, $(\gamma,n)$, $(\gamma,p)$, and $(\gamma,\alpha)$. 
The branching from one isotopic line to the next happens when the proton or the alpha channel is stronger than the neutron.
Here the branching happens in $^{102}$Pd which is the nucleus we will study in more detail in the following.

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/branching_point.png" zoomable=true>
     </div>
     <div class="caption">
     Branching points! Figure adapted from <d-cite key="Iliadis2015"></d-cite>
      </div>
</center>

do calculations between Pd 100 and 104 and grab the decay constant at T=2.5 GK see the comparison between a, g and p channels 

## Detailed balance

\begin{equation}\label{eq:detailed_balance}
\langle \sigma v \rangle_{(p,\gamma)} = \frac{(2J_B+1)}{(2J_A+1)} \frac{E_{\gamma}^2}{(m_pc^2 kT)^{3/2}}e^{-Q/(kT)} \langle \sigma v\rangle_{(\gamma, p)}
\end{equation}


\begin{equation}
\lambda_\gamma = \frac{8\pi}{h^3 c^2}\int_0^\infty \frac{E_\gamma^2}{e^{E_\gamma/(kT)}-1} \sigma(E_\gamma)dE_\gamma
\end{equation}

## Stellar Enhancement and partition functions

<d-cite key="Rauscher2011"></d-cite>




## Enter the $\gamma$ beams



<div class="fake-img l-gutter">
  <p><b>See A. Tsantiri lecture</b></p>
</div>


### $\gamma$ beam production techniques

bremsstrahlung and laser Compton scattering (LCS) are the two main techniques to produce $\gamma$-beams in the laboratory.

### $\gamma$ beam facilities


|Facility| Energy (MeV)  |Flux ($\gamma$/s)| $\Delta E/E$ (FWHM) |  Polarization
|-------|----------------|---------------|---------------|---------------|
| HI$\gamma$S (TUNL, USA)| 1-100 | $\leq 3 \times 10^{10}$| $\sim$3-5% | Linear/Circular|
| ELI-NP (Romania)| 0.2-19.5 | $\sim 2 \times 10^{8}$| $\leq$0.5% | Linear|
| NewSUBARU (Japan)| 1-35 | $\sim 10^{7}-10^{8}$| $\sim$3% | Linear/Polarized|
| SLEGS (SSRF, China)| 0.66-21.7 | $10^{5}-10^{7}$| $\sim$6-18% | Linear|
| S-DALINAC (Germany)| Up to $\sim 30-70$| $10^{10}-10^{12}$ (integrated)| 100% (broad) | Unpolarized|

### Detectors and Observables

photonuclear cross sections as a function of $\gamma$ energy
charge-particle detection
neutron-detection (for ($\gamma,n$) reactions)
TPC (Time-Projection Chambers) or charged particle detectors (silicon)
angular distributions & polarization effects (NRF Gribble)
<d-cite key="Gribble2025"></d-cite>
<d-cite key="Iliadis2021"></d-cite>






<div class="fake-img l-body">
  <p> <b> <i class="fas fa-quote-left"></i> something I want to emphasize. </b> </p>
</div>


High Intensity $\gamma$-Ray Source (HI$\gamma$S)
[link](https://tunl.duke.edu/research/our-facilities)

---

<d-code block language='python'>
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp
</d-code>

## Case study: $^{102}$Pd+$\gamma$ at HI$\gamma$S (TUNL)



Let us now apply this knowledge using as our guide a recent experiment performed at TUNL using the HI$\gamma$S facility.

$^{102}$Pd is one of the p-nuclei 

This experiment aimed to measure the ($\gamma,x$) reactions on $^{102}$Pd which is one of the p-nuclei.
The setup consisted of the SIDAR array  which were able to detect protons and alpha particles from the ($\gamma, p$) and ($\gamma, \alpha$) channels.

Is the $^{102}$Pd a proper target to study using a $\gamma$-beam? Which is its g.s. contribution $X_0$?


The experimental data provide important information to constrain the theoretical models in the A=100-110 mass range and improve our predictions of nucleosynthesis


> this is a quote!

<d-cite key="Zilges2022"></d-cite>
<d-cite key="LaCognata2017"></d-cite>
<d-cite key="Balabanski2023"></d-cite>
<d-cite key="Utsunomiya2006"></d-cite>


## From Lab Cross Sections to Stellar Rates


## Broader implications and open questions


