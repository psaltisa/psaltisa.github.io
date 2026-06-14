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
 - name: How to produce the p-nuclei
 - name: The nuclear physics of the $\gamma$-process
   subsections:
        - name: The Hauser-Feshbach (HF) statistical model
        - name: Detailed balance- Connecting forward and reverse reactions
        - name: Stellar enhancement and partition functions
 - name: Why $\gamma$-beam experiments matter
 - name: $\gamma$-ray beam production techniques
 - name: Case study- $^{102}$Pd+$\gamma$ at HI$\gamma$S (TUNL)
   subsections:
        - name: Why $^{102}$Pd?
        - name: Experimental setup
        - name: Model expectations
        - name: Results and interpretation
 - name: Broader implications and open questions
   subsections:
       - name: Key open questions in the γ-process
       - name: Future perspectives
 - name: Conclusions
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

<div class="fake-img l-body">
  <p> <b> A companion Jupyter notebook can be found in <a href="https://github.com/psaltisa/gamma-beams"><i class="fab fa-github"></i></a> and <a target="_blank" href="https://colab.research.google.com/github/psaltisa/gamma-beams/blob/main/notebook.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></b></p>
</div>

## The origin of p-nuclei, an open question for nuclear astrophysics

A small group of around 35 stable neutron--deficient nuclei with A $\geq$ 74 between selenium (Se) and mercury (Hg) cannot be produced by the two main neutron-capture processes (s- and r-process).
These are referred to as **p-nuclei** and their origin is a long-standing puzzle.

The fact that a distinct process produces these isotopes had been already identified from the early days of our field by both Cameron<d-cite key="cameron1957nuclear"></d-cite> and Burbidge et al.<d-cite key="burbidge1957synthesis"></d-cite>. They were referred to as "excluded" nuclei, since they were "shielded" by the s- and the r-process reaction path.

<center>                                                                          
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/flow.png" data-zoomable="">
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


## How to produce the p-nuclei

Core-collapse supernovae (ccSNe) explosions are the last evolutionary stage of massive stars with $M \sim 8~M_{\odot}$.
During the explosion, the shock-wave that propagates towards the outer layers of the star induces the production of p-nuclei through *photodisintegration* reactions.
For this reason, this scenario is referred to as $\gamma$-process<d-cite key="Rauscher2013, Pignatari2016, Roberti2023"></d-cite>.

<div class="fake-img l-body">
  <p> <b> The $\gamma$ process network is vast, involving more than 2,000 nuclei (most of them radioactive) with >20,000 reactions!
 </b> </p>
</div>

The initial seeds are isotopes produced previously during the s-process in the AGB phase of the massive star, or even r-process isotopes that polluted the nebula that produced the massive star. For this reason, knowing this seed distribution accurately (and the neutron-producing reactions!) is a key uncertainty in $\gamma$-process modeling.
<div class="fake-img l-gutter">
  <p><b>See lectures by M. Busso and M. Pignatari</b></p>
</div>

As we can see from the top figure, the main drivers of the $\gamma$-process are $(\gamma,n)$, $(\gamma,p)$ and $(\gamma,\alpha)$ reactions.
Of importance are the branching points, where the flow moves to lower mass isotopes.
In this cases, the competition between $(\gamma,n)$ and the other two channels can change the reaction flow, and eventually the final p-nuclei abundances.


In the $\gamma$–process each mass region is produced at a different peak temperature: intermediate mass p–nuclei (A~ 92–136) are produced at $T \sim 2.5 − 3$ GK while the heavy p–nuclei (A > 140) at $T < 2.5$ GK.
For this reason it is important to have a good understanding of the temperature and density profiles of the shock wave as it propagates through the outer layers of the star, which is still a major uncertainty in $\gamma$-process modeling.

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/shock.png" zoomable=true>
     </div>
     <div class="caption">
     1D shock wave profiles from different radii of an exploding star <d-cite key="rapp2006apj"></d-cite>. Note that the peak temperature decreases as the shock moves outward, losing energy due to the interaction with the free-falling outer layers.
      </div>
</center>

More recently, C-O shell mergers in the pre-explosion phase have been proposed as a candidate for the production of the p-nuclei <d-cite key="Roberti2023, Issa2026"></d-cite>.
In a similar context, rotating massive stars have been proposed as a site for the production of p-nuclei <d-cite key="Choplin2022"></d-cite>.

ccSNe are also hosts for two additional processes that produce a small subset of the p-nuclei via reactions that involve neutrinos. The $\nu$-process has been shown to produce some rare species, such as $^{152}$Gd, $^{164}$Er, $^{180}$Ta <d-cite key="Heger2005"></d-cite> while the $\nu p$-process in the proton-rich ejecta of the neutrino-driven ejecta (close to the stellar remnant) can produce the light p-nuclei <d-cite key="Frohlich2006"></d-cite>. Nevertheless, the latter scenario is still very sensitive to the astrophysical conditions and the underlying nuclear physics input.

Another viable astrophysical environment for the production of the p-nuclei is thermonuclear supernovae (type Ia).
In this explosion, a white dwarf is disrupted when its mass surpasses the Chandrasekhar limit, while accreting material from a companion star.
The production of p-nuclei in type Ia supernovae has been studied in detail in the literature and it strongly depends on the initial composition of the white dwarf <d-cite key="Travaglio2011, Battino2020"></d-cite>

Accreting neutron stars via the rp-process have also been shown to produce p-nuclei, via proton captures instead of photon disintegrations, however it is not clear if they can contribute to the galactic chemical evolution due to extremely large escape velocities from a neutron star surface that hinder any ejection of material into the interstellar medium<d-footnote>Interestingly, studies that include rotation in the neutron star have shown both a reduced production of p-nuclei but a significantly higher mass ejection than non-rotating models.</d-footnote>.

Despite our ability to reproduce most of the p-nuclei abundances of the solar system to within a factor of 2, there are still a few cases where the $\gamma$-process fails to reproduce in sufficient amounts; notable examples include the light $^{92,94}$Mo, $^{96,98}$Ru, $^{113}$In, $^{115}$Sn, $^{138}$La, $^{180}$Ta that most likely have contributions from other processes<d-cite key="Roberti2023"></d-cite>.


## The nuclear physics of the $\gamma$-process

### The Hauser-Feshbach (HF) statistical model

Given the vast size of the $\gamma$-process network (>2,000 nuclei), we cannot directly measure all the relevant reactions at the temperatures of interest.
Thankfully, theoretical calculations bridge this gap.
The **Hauser-Feshbach (HF) model** is the standard approach for calculating photodisintegration (and radiative capture) cross sections in the intermediate- to heavy-mass regime where level densities are high.

In a photodisintegration reaction, a $\gamma$-ray is absorbed by a nucleus, forming a **compound nucleus** in an excited state.
The compound nucleus then decays through one or more exit channels (neutron, proton, alpha emission, or $\gamma$-ray emission) *independently* of how it was formed.
The assumption that the compound nucleus "forgets" its formation mechanism underlies the HF model.

The HF model expresses the cross section as:

\begin{equation}
\sigma(E) = \pi \hbar^2 \sum_{J,\pi} g(J^\pi) \frac{T_\mathrm{in}(E) T_\mathrm{out}(E)}{T_\mathrm{tot}(E)}
\end{equation}

where:
- $g(J^\pi)$ is the density of states (or transmission coefficient weighting) for angular momentum $J$ and parity $\pi$
- $T_\mathrm{in}(E)$ is the **transmission coefficient** for the entrance channel (photon absorption)
- $T_\mathrm{tot}(E)$ is the total transmission (sum over all competing channels, *e.g.* proton, neutron and alpha)

Each output is weighted by its own transmission coefficient, which depends on the **nuclear level density (NLD)** and **$\gamma$-ray strength function ($\gamma$SF)**, which are the three main sources of uncertainty in HF predictions:

1. **Optical-model potential (OMP):** The complex potential describing nucleon scattering in the nucleus. Different parameterizations (e.g., Koning–Delaroche, RIPL-3) can differ by factors of 2–3 in transmission coefficients, especially for neutrons.

2. **$\gamma$-ray strength function ($\gamma$SF):** The probability for a nucleus to emit (or absorb) a photon at a given energy. The $\gamma$SF is constrained by photon scattering experiments (NRF), but extrapolation to higher energies carries large uncertainties. Different models (*e.g.*, Lorentzian, Brink-Axel, microscopic) can differ significantly.

3. **Nuclear level density (NLD):** The number of available quantum states per unit energy. For low excitation energies, individual levels are resolved; at higher energies (where the $\gamma$-process operates), the density grows rapidly.
The NLD is often parameterized by Fermi-gas models, with parameters that differ between codes.

As you can imagine, the uncertainties in these three ingredients propagate to the predicted thermonuclear reaction rates, and as a result to the final $\gamma$-process abundance predictions through nucleosynthesis calculations.
A factor of 2 error in a single reaction rate can alter the final p-nucleus abundances by orders of magnitude at branching points <d-cite key="Rauscher2013"></d-cite>.
<div class="fake-img l-gutter">
  <p><b>See lecture by A. Tsantiri</b></p>
</div>

Many codes can perform these calculations, with the most well-known in our community being:
- TALYS <d-cite key="Koning2023"></d-cite>
- NON-SMOKER (SMARAGD)
- EMPIRE

For the first two, you can access database results for different reactions in [NON-SMOKERweb](https://nucastro.org/interface_expl.html) and [TALYS world](https://nds.iaea.org/relnsd/talys/talys.html).


Let us now explore how we can use these theoretical nuclear physics calculations to study the $\gamma$-process.
In the following example, we have plotted the reaction rates for the three competing reaction channels, $(\gamma,n)$, $(\gamma,p)$, and $(\gamma,\alpha)$ in the palladium isotopic hain.
The branching from one isotopic line to the next happens when the proton or the alpha channel is stronger than the neutron.
Here the branching happens in $^{102}$Pd which is the nucleus we will study in more detail in the following.
Note that we haven't included any uncertainties in these calculations, meaning that the branching point might change if we change the nuclear physics input, which is why experiments are so important to constrain the models.

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/branching_point.png" zoomable=true>
     </div>
     <div class="caption">
     Branching points in the palladium (Pd) isotopic chain. Figure adapted from <d-cite key="iliadis2017nuclear"></d-cite>. The $(\gamma,\alpha)$ channel dominates in $A=102$. All calculations were made using the TALYS code<d-cite key="Koning2023"></d-cite> with the default settings.
      </div>
</center>


### Detailed balance- Connecting forward and reverse reactions

The detailed balance principle allows us to extract photodisintegration cross sections from radiative capture data. For a reaction $A + a \leftrightarrow B + b$, detailed balance relates the forward reaction rate to the reverse:

\begin{equation}\label{eq:detailed_balance}
\langle \sigma v \rangle_{(p,\gamma)} = \frac{(2J_B+1)}{(2J_A+1)} \frac{E_{\gamma}^2}{(m_pc^2 kT)^{3/2}}e^{-Q/(kT)} \langle \sigma v\rangle_{(\gamma, p)}
\end{equation}

Here, $Q = (m_A + m_p - m_B - m_\gamma)c^2$ is the Q-value (negative for endothermic reactions). The temperature dependence $T^{-3/2}$ reflects the thermal distribution of particles in the plasma (Maxwell-Boltzmann). The spin factors $(2J+1)$ account for the different quantum states available in each channel.

At higher temperatures, the exponential factor $e^{-Q/(kT)}$ grows, making the photodisintegration rate larger compared to radiative capture. This is why the $\gamma$-process is efficient in core-collapse supernovae, where temperatures exceed GK!

### Stellar enhancement and partition functions

In the astrophysical environment, nuclei are not confined to their ground states. Thermal excitation populates excited levels, and the *effective* cross section seen in a stellar plasma depends on:

- **Partition function:** The fraction of nuclei in excited states is given by the partition function:
   \begin{equation}
   G(T) = \sum_i (2J_i+1) e^{-E_i/(kT)}
   \end{equation}
   where the sum runs over all accessible excited levels. At low $T$, only the ground state contributes; at high $T$, many levels are populated.

- **Stellar enhancement factor:** The ratio of the stellar rate to the ground-state rate is approximately:
   \begin{equation}
   \frac{\langle \sigma v \rangle_\star}{\langle \sigma v \rangle_{g.s.}} \approx \frac{\sum_i (2J_i+1) \sigma_i(T) e^{-E_i/(kT)}}{(2J_{g.s.}+1)\sigma_{g.s.}(T)}
   \end{equation}

 Different excited states have different spins and resonance strengths. A measurement targeting only the ground state can miss significant contributions from excited levels. This is particularly important near energy thresholds, where ground-state contributions might be suppressed but excited-state contributions could be substantial <d-cite key="Rauscher2011"></d-cite>.

For more details on how to calculate partition functions and apply them to astrophysical rates, see <d-cite key="Rauscher2011"></d-cite> and <d-cite key="iliadis2017nuclear"></d-cite>.

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/excited.png" zoomable=true>
     </div>
     <div class="caption">
     The difference between reactions in the lab and in teh star. In the latter case, we have contributions from excited states that can significantly enhance the reaction rate. Figure adapted from <d-cite key="iliadis2017nuclear"></d-cite>.
      </div>
</center>


## Why $\gamma$-beam experiments matter

As we have discussed already, the $\gamma$-process network is vast (>2,000 nuclei, >20,000 reactions), making it impossible to measure all reaction rates directly. For photodisintegration reactions (the reverse of radiative capture), direct measurements are particularly challenging, but very important.
<div class="fake-img l-gutter">
  <p><b>See lectures by G. Gyürky and  A. Tsantiri</b></p>
</div>

Typically, we can use the time-reversal symmetry of nuclear interactions to get the photodisintegration rates. If we measure the *forward* reaction (e.g., $p + ^{101}\mathrm{Rh} \rightarrow \gamma + ^{102}\mathrm{Pd}$)<d-footnote>In this case the target would be radioactive, which makes the "forward" reaction also challenging!</d-footnote>, we can extract the *reverse* photodisintegration rate via detailed balance. This is why $\gamma$-beam experiments on the ground states of unstable nuclei produced in reactions like $(p,\gamma)$ are crucial.

In stellar environments, nuclei exist in excited states due to the high temperatures. The competition between different exit channels—$(\gamma,n)$ vs. $(\gamma,p)$ vs. $(\gamma,\alpha)$—depends sensitively on *where* the compound nucleus has strength (resonances). Monoenergetic $\gamma$-beams allow us to scan through these resonances systematically.

The HF model relies on inputs like the optical-model potential, $\gamma$-ray strength function, and nuclear level density. By measuring cross sections at energies relevant to the $\gamma$-process, we can constrain these inputs and reduce uncertainties in theoretical predictions.


<div class="fake-img l-body">
  <p> <b> $\gamma$-beam experiments DO NOT provide the full stellar rate, but are used to constrain the HF model inputs!
 </b> </p>
</div>


## $\gamma$-ray beam production techniques

Two main techniques are used to produce intense monochromatic $\gamma$-ray beams:

**Bremsstrahlung radiation:**
A high-energy electron beam strikes a high-Z target, producing a continuous spectrum of photons via Coulomb deceleration in the nuclear field. The spectrum is broad, requiring post-acceleration collimation to select a narrow energy band.

Advantages:
- Simple, robust technique
- High integrated flux in broad energy range

Disadvantages:
- Energy resolution typically 100% (very broad)
- Only a small fraction of photons end up in the selected energy window

**Compton backscattering:**
A low-energy laser photon is scattered off a relativistic electron beam. By tuning the electron energy and collision geometry, one can produce nearly monochromatic photons via the Compton formula:
\begin{equation}
E_\gamma = E_e \left(1 - \cos\theta\right) \frac{2E_\mathrm{laser}}{m_e c^2} / \left[1 + \frac{2E_e}{m_e c^2}(1-\cos\theta)\right]
\end{equation}

Advantages:
- Excellent energy resolution (< 1% FWHM)
- Tunable beam energy by adjusting electron energy
- Narrow energy spread allows threshold measurements

Disadvantages:
- More complex infrastructure (linac + laser + collision geometry)
- Lower absolute photon flux compared to bremsstrahlung
- Higher operational cost


### Major $\gamma$-ray beam facilities worldwide

The following table summarizes the key facilities used for photonuclear research in astrophysics:

|Facility| Country | Energy Range (MeV)  |Flux ($\gamma$/s)| $\Delta E/E$ (FWHM) |  Polarization | Technique
|-------|---------|----------------|---------------|---------------|--------|----------|
| HI$\gamma$S (TUNL) | USA | 1–100 | $\leq 3 \times 10^{10}$| 3–5% | Linear/Circular | Compton backscattering |
| ELI-NP | Romania | 0.2–19.5 | $\sim 2 \times 10^{8}$| $\leq$0.5% | Linear | Laser Compton Scattering |
| NewSUBARU | Japan | 1–35 | $\sim 10^{7}$–$10^{8}$| $\sim$3% | Linear/Pol. | Laser Compton Scattering|
| S-DALINAC | Germany | 5–70 | $10^{10}$–$10^{12}$ (integrated)| ~100% (broad) | Unpolarized | Bremsstrahlung |

The choice of facility depends on the physics questions:
- **High flux, broad energy range:** S-DALINAC or HI$\gamma$S for measuring integrated cross sections
- **Excellent energy resolution:** ELI-NP for threshold measurements and nuclear resonance fluorescence (NRF)
- **Polarization studies:** HI$\gamma$S for studying angular distributions and multipole decomposition

### Detectors and Observables

To extract astrophysical information from $\gamma$-beam experiments, we need to measure:

- **Photonuclear cross sections $\sigma(E_\gamma)$ as a function of energy:**
   Direct measurement of the reaction probability is the primary goal. By scanning the $\gamma$ energy across the relevant range (typically MeV–tens of MeV), one can identify resonances and measure threshold behavior. For the $\gamma$-process, typical threshold energies are 5–20 MeV (corresponding to the negative Q-values)<d-cite key="Utsunomiya2006"></d-cite>.

- **Particle detection:** The outgoing nuclei and/or neutrons from $(\gamma,n)$, $(\gamma,p)$, and $(\gamma,\alpha)$ reactions must be detected with:
   - **Silicon detectors** for charged particles: Excellent energy and position resolution; provides particle identification via $\Delta E$–$E$ techniques
   - **Neutron detectors:** Scintillators or time-projection chambers (TPCs) for measuring neutron energies and multiplicities
   - **CdZnTe or similar:** Fast timing for coincidence measurements to identify multi-nucleon ejection

- **Angular distributions $\frac{d\sigma}{d\Omega}$:**
   The angular distribution of outgoing particles constrains the multipolarity (E1, E2, M1, etc.) of the $\gamma$-ray interaction. This provides nuclear structure information beyond just the cross section magnitude <d-cite key="Iliadis2021"></d-cite>.

- **Nuclear resonance fluorescence (NRF):**
   When a $\gamma$ ray elastically scatters off a nucleus, it reveals the position and width of excited states. NRF is particularly useful for identifying low-lying resonances that feed the ground state <d-cite key="Gribble2025, Zilges2022"></d-cite>; this is crucial for understanding stellar enhancement factors.

**Example: The SIDAR array at HIγS** <d-cite key="Munch2020"></d-cite> uses silicon detector rings to measure the energy and angle of protons and alpha particles. By reconstructing the missing energy, one can extract the neutron binding energy and identify which reaction channel (p, α, or n ejection) occurred.

---

## Case study- $^{102}$Pd+$\gamma$ at HI$\gamma$S (TUNL)

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/higs.png" zoomable=true>
     </div>
     <div class="caption">
     Layout of the <a href= 'https://tunl.duke.edu/research/our-facilities'>HIγS</a> facility at TUNL<d-cite key="Weller2009"></d-cite>. The HI$\gamma$S facility uses Compton backscattering to produce intense, polarized $\gamma$-beams.
      </div>
</center>

### Why $^{102}$Pd?

$^{102}$Pd is one of the ~35 p-nuclei and plays a crucial role in $\gamma$-process nucleosynthesis for several reasons: At this nucleus, the reaction flow branches between $(\gamma,n)$ leading to $^{101}$Pd and $(\gamma,p)$ leading to $^{101}$Rh (or  $(\gamma,\alpha)$). The competition between these two channels directly affects whether the reaction flow continues to lighter p-nuclei or remains in the Pd isotope chain.

The solar system abundances of light p-nuclei (including Pd and Rh isotopes) are difficult to reproduce with standard $\gamma$-process models. Understanding the branching at $^{102}$Pd is essential for solving this discrepancy.

The ($\gamma,p$) reaction to $^{101}$Rh has $Q = -7.81$ MeV (endothermic). This threshold is within the energy range of modern $\gamma$-beam facilities like HIγS (up to 100 MeV), making direct measurements feasible.

$^{102}$Pd is a stable nucleus with a long half-life, so it can be produced as a pure target without complications from radioactive decay.

**Astrophysical relevance:** In core-collapse supernovae, $^{102}$Pd experiences peak temperatures of ~2.5–3 GK. At these temperatures, the thermal population of excited states in $^{102}$Pd affects the branching ratio. Direct measurements constrain the ground-state contribution, which can then be extrapolated to excited states using nuclear models.

### Experimental setup

The recent $^{102}$Pd$(\gamma,x)$ experiment (where x = p and α) at HIγS utilized:

- **$\gamma$-ray beam:** Monochromatic, collimated beam produced via Compton backscattering. The beam is scanned from slightly above the threshold (~10 MeV) up to ~19 MeV to map out the excitation function.

- **Target:** A thin $^{102}$Pd 78% enriched target (1.8 mg/cm$^2$ thickness) positioned at the center of the detector array.

- **Silicon Detector Array (SIDAR):** <d-cite key="Munch2020"></d-cite>
   - Multiple silicon detectors arranged in rings around the target (~38% of 4π coverage)
   - Measures the energy and angle of outgoing protons and alpha particles
   - Energy resolution: ~100 keV (dominated by target thickness)
   - Angular resolution: ~2.5° (allows extraction of angular distributions if desired)

- **Detector logic:** A charged particle is identified by:
   - Its energy loss in the silicon ($dE/dx$, related to charge and mass)
   - Its residual energy after passing through the detector
   - The combination determines whether it's a proton, alpha, or heavier fragment

**Measured quantities:**
- Differential cross section $\frac{d\sigma}{dE_\gamma}$ for ($\gamma,p$) and ($\gamma,\alpha$) as functions of $E_\gamma$
- Angular distributions $\frac{d\sigma}{d\Omega}$ (if measured with sufficient angular resolution)
- Total $\gamma$-induced reaction cross sections by integrating over angles

<center>                                                                
       <div class="col-sm mt-2 mt-md-0">
           <img class="img-fluid"
            src="{{ site.baseurl }}/assets/img/sidar.png" zoomable=true>
     </div>
     <div class="caption">
     Schematic of the silicon detector array (SIDAR) <d-cite key="Munch2020"></d-cite>.
      </div>
</center>

### Model expectations

Before the experiment, theoretical predictions (using TALYS) made specific predictions for the cross sections. The predictions depended on the choice of nuclear physics inputs that we discussed previously (OMP, $\gamma$SF and NLD).

Typical HF predictions:
- ($\gamma,p$) cross section: ~1–10 mb near 10 MeV above threshold
- ($\gamma,\alpha$) cross section: Smaller (~0.1–1 mb) but non-negligible

**Uncertainties:** HF predictions for this nucleus carry typical uncertainties of factors of 2–3 (sometimes more) due to the nuclear physics inputs. This is why direct measurements are essential.

### Results and interpretation

The experimental data (provided in the companion notebook as `pd102gp.dat`) show the ($\gamma,p$) cross section as a function of $\gamma$-energy. Key observations include the threshold behavior, the energy dependance and its comparison with the the HF predictions. The cross section rises sharply above the 7.81 MeV threshold, reaching peak values of a few millibarns at ~10 MeV. The opening of the neutron channel at ~10.5 MeV is not as pronounced as expercted. Above ~15 MeV, the cross section behavior seems to flatten out. We can now use the measured cross sections to constrain the HF model inputs. If the measurement differs from theory, it suggests that one or more of the OMP, GSF, or NLD parameters needs refinement.

**How does this feed back to nucleosynthesis?**

Using the measured cross section $\sigma(E_\gamma)$ and detailed balance, one can calculate the stellar reaction rate:

\begin{equation}
\lambda_\gamma = \frac{8\pi}{h^3 c^2}\int_0^\infty \frac{E_\gamma^2}{e^{E_\gamma/(kT)}-1} \sigma(E_\gamma) \, dE_\gamma
\end{equation}

This integral weights the cross section by the thermal photon distribution (Planck function). At high stellar temperatures (T = 2–3 GK, relevant for the $\gamma$-process), the Planck function shifts weight to higher energies, emphasizing the cross section above ~15 MeV.

The updated rates, combined with the competing ($\gamma,n$) rates, determine the branching ratio in the astrophysical environment. This directly predicts the final abundance of $^{101}$Rh vs. the flux of nuclei progressing toward lighter p-nuclei. The notebook guides you through this calculation step by step.


## Broader implications and open questions

### Key open questions in the γ-process

- **Light p-nuclei discrepancy:** Standard $\gamma$-process calculations struggle to reproduce the observed abundances of light p-nuclei (A ~ 90–120). This may indicate:
   - Missing physics in the supernova models (e.g., rotation, magnetic fields, 3D effects)
   - Contributions from alternative sites (e.g., C–O shell mergers, νp-process)
   - Systematic uncertainties in nuclear reaction rates that haven't been fully explored

- **Role of excited-state contributions:** Most direct measurements target ground states. The contribution of excited states at astrophysical temperatures remains poorly constrained.

- **The importance of (γ,α) reactions:** While ($\gamma,n$) dominates the reaction
flow, ($\gamma,\alpha$) channels can open up new reaction paths or suppress certain isotopes. Precise measurements of ($\gamma,\alpha$) cross sections are still lacking for many nuclei.

- **Rare isotope beams:** Many reaction for the $\gamma$-process involve unstable isotopes. Next-generation facilities (*e.g.*, FRIB, GSI-FAIR) have very recently started to perform experiments on radioactive beams, allowing direct measurements on unstable nuclei <d-cite key="Dellmann2025,Tsantiri2025"></d-cite>.

### Future perspectives

Some ideas about the future directions in our field regarding the $\gamma$-process:

- **New generation of $\gamma$-ray sources:**
   - Higher intensity beams (increased flux by orders of magnitude)
   - Improved energy resolution for better threshold studies
   - Wider energy ranges to probe different astrophysical regimes
   - Improved polarization capabilities for nuclear structure studies

- **Advanced detector technologies:**
   - Fast, large-volume TPCs for neutron detection and energy reconstruction
   - $\gamma$-ray spectrometers for coincident photon detection

- **Collaboration with astrophysical observations:**
   - Solar abundances still set strong constraints on nucleosynthesis models
   - Meteoritic data (presolar grains, isotope anomalies) provide complementary evidence
   - Astronomical observations (s-process abundances in AGB stars, r-process signatures in neutron star mergers)

- **Bridging theory and experiment:**
   - Uncertainty quantification to propagate nuclear physics uncertainties through nucleosynthesis
   - Bayesian approaches to constraining reaction rates from multiple experimental inputs
   - Integrated frameworks combining nuclear physics, hydrodynamics, and observational constraints

## Conclusions

The $\gamma$-process remains a fundamental open problem in nuclear astrophysics. Understanding where the p-nuclei come from requires inputs from different perspectives: state-of-the-art astrophysical modeling, careful nuclear measurements with $\gamma$-beams (or capture reactions), and theoretical nuclear physics to extrapolate beyond what we can measure. Each piece contributes to piecing together this complex cosmic puzzle.

Feel free to play with the companion notebook and get some hands-on experience with the data analysis and calculations that lie at the heart of this field. By working through the detailed balance calculations and rate conversions, you will gain insight into how laboratory measurements can help us understand the origin of the elements in the cosmos.
