---
layout: post
title: Historic Papers 1 - Breit & Wigner, Phys. Rev. (1936)
date: 2022-02-05
description:
inline: false
author:
tags: [nuclear-astrophysics, historic-papers]
category: article
---

*"Historic Papers" is a series of posts, in which we explore famous scientific papers that were the stepping stones for the advent of nuclear astrophysics, and we also learn about the life of the scientists involved.* <br>


For the first paper of the series, I chose *"Capture of slow neutrons"* by Gregory Breit and Eugene Wigner, published at [Physical Review](https://journals.aps.org/pr/abstract/10.1103/PhysRev.49.519){:target="\_blank"} in 1936. Firstly, let's put this work into perspective; the quantum revolution was at full swing a decade ago, and now the fruits of this theory tree are starting to fall one after the other. One of the most important discoveries was that of the neutron - the third ingredient of an atom, along with the proton and the electron - by James Chadwick at the Cavendish Laboratory four years ago (1932). Around three years after this paper was published, in December 1938, Lise Meitner, Otto Hahn and others, discovered nuclear fission, which will bring humanity one step closer to nuclear energy and unfortunately the horror of atomic bombs. As far as politics are concerned, since the early 1930s, scientists from Germany are fleeting mainly towards the United States, due to the rise of the Nazi regime.

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-2 mt-md-0">
            {% include figure.html path="/assets/img/breit-wigner-1936.png" class="img-fluid" zoomable=true caption="The abstract of the paper published in Physical Review (1936)." %}
        </div>
    </div>
</center>

Breit and Wigner were set out to tackle an important question regarding interactions between neutrons and nuclei. Experiments had showed that the interaction probability (or **cross section**) can be "anomalously large", however the current theories could not account for that. This paper set the theoretical framework for these special interactions that resemble the workings of a radio station and a pocket radio (or musical instruments):

#### When the **frequency** of the **receiver** is tuned to the **frequency** of a **radio station** then **we can listen to the station**.

If we change *frequency* to **energy**, *receiver* to **interacting particle**,
*radio station* to **nuclear state** and *we can listen to the station* to **the interaction cross section is enhanced**,
you have the basic idea behind resonances in nuclei.



<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="/assets/img/bw-equation.png" class="img-fluid" zoomable=true caption="The famous Breit-Wigner formula as presented in their paper." %}
        </div>
    </div>
</center>

Even though Breit and Wigner studied the resonant interaction considering neutrons, their formula can be used for other species, such as protons or helium nuclei. Now let's play a bit with this formula, to get a better understanding of its parts. We can write it down in a more simplified form:

$$\sigma(E) \propto \frac{\Gamma_1 \Gamma_2}{(E_r-E)^2+(\Gamma/2)^2}$$

where $$\Gamma_1, \Gamma_2$$ are the widths of different cross section channels, $$E_r$$ is the resonance energy and $$\Gamma = \Gamma_1+\Gamma_2$$. The effect of changing $$E_r$$ is
that we essentially change our nuclear level (or radio station).

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="/assets/img/bwigner-e.svg" class="img-fluid" zoomable=true caption="The effect of changing the resonance energy to the interaction cross section." %}
        </div>
    </div>
</center>

Now we will keep the same resonance energy and change the resonance width $$\Gamma$$.

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="/assets/img/bwigner-g.svg" class="img-fluid" zoomable=true caption="The effect of changing the resonance width to the interaction cross section." %}
        </div>
    </div>
</center>

You see that when we increase the $$\Gamma$$ factor, our distribution becomes wider.

### The importance of the paper

Towards the end of paper one can find a very interesting paragraph:

><i class="fas fa-quote-left"></i> Bombardment of light nuclei with charged particles has also shown the existence of resonances.
Thus there are resonances for the emission of γ-rays in proton bombardment of Li, C, F and
similarly there are the well known resonances in
disintegrations produced by α particles. Experimental methods have not been very suitable so
far for the detection of resonance regions on account of the scarcity of monochromatic sources
and the necessity of using thin films.

In the years following this work, experimental physicists will start measuring resonances of interacting
nuclei in a wide variety of energies. Breit and Wigner provided the important theoretical background to
explain the resonant structure of nuclear reactions. Later in the twentieth century, we will learn that
such resonances also occur inside stars and are responsible for the light that we from the sun and other stars and
the creation of the elements that make up the universe.


### Meet the scientists


**Eugene Wigner** was awarded the Nobel prize for Physics in 1963 *"for his contributions to the theory of the atomic nucleus and the elementary particles, particularly through the discovery and application of fundamental symmetry principles"*. Originally from Hungary, Wigner worked in Germany (Berlin and
Göttingen) and moved to the United States in 1930 to work at Princeton University. He was an integral part, along with Leó Szilárd and Albert Einstein
for the famous letter to President Roosvelt regarding the use of fission to create nuclear weapons, which led to the Manhattan Project. Wigner was also
a member of the *Martians* gang, along with Leó Szilárd, Johnny von Neumann, Edward Teller and others. To quote the famous science fiction writer Isaac Asimov "*There is a rumor in America that there are two intelligent races on Earth: Humans and Hungarians*".


**Gregory Breit** was born in Russia, close to Odessa and emigrated to the United States at 16. He was selected to supervise the design of the atomic bomb, which would later become the Manhattan project, however he resigned in 1942, and eventually Robert Oppenheimer led this effort.


<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="/assets/img/breit-wigner.jpg" class="img-fluid" zoomable=true caption="G. Breit (left) and E. Wigner (right). Credit: AIP Emilio Segrè Visual Archives, Physics Today Collection" %}
        </div>
    </div>
</center>

---
[G. Breit and E. Wigner, Phys. Rev., **49** 519 (1936)](https://journals.aps.org/pr/abstract/10.1103/PhysRev.49.519){:target="\_blank"}

[Gregory Breit: Bibliographical Memoir by McAllister Hull](https://web.archive.org/web/20050421092901/http://stills.nap.edu/html/biomems/gbreit.html){:target="\_blank"}
