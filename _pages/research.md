---
layout: page
permalink: /research/
title: research
description: our framework
nav: true
---

<style>
    #controls { display: flex; align-items: center; gap: 12px; justify-content: center; margin: 6px 0 8px; }
    #downloadBtn {
      border: 0; border-radius: 10px; padding: 10px 14px; font-weight: 700; cursor: pointer;
      background: #9D2235; color: white; box-shadow: 0 6px 16px rgba(30,144,255,.25);
    }
    #downloadBtn:hover { filter: brightness(1.05); }

    #periodic-table { display: flex; justify-content: center; margin: 8px 0; }
    svg { width: 100%; height: auto; display: block; }

    .tooltip {
      position: absolute; padding: 12px; background: #fff; border: 1px solid #ddd; border-radius: 8px;
      pointer-events: none; font-size: 14px; box-shadow: 3px 3px 10px rgba(0,0,0,.2); max-width: 300px; z-index: 10; color: #333;
    }
    .element-cell { stroke: #333; stroke-width: .5; transition: all .2s; }
    .element-cell:hover { stroke-width: 2; stroke: #000; filter: brightness(1.06); }

    .legend {
      display: flex; justify-content: center; flex-wrap: wrap; gap: 10px 14px; margin-top: 8px; padding: 10px;
      background: #f8f9fa; border-radius: 10px;
    }
    .legend-item { display: flex; align-items: center; gap: 8px; }
    .legend-color { width: 18px; height: 18px; border-radius: 3px; border: 1px solid #ddd; }

    footer { text-align: center; margin-top: 6px; padding: 8px; color: var(--muted); font-size: .9rem; }

    @media (max-width: 640px) {
      .legend { flex-direction: column; align-items: flex-start; gap: 8px; }
      #controls { justify-content: space-between; }
    }
</style>

In our research in nuclear astrophysics, we take a **systems approach** to understanding how the elements are made in the Cosmos.
We begin by identifying the most important nuclear processes that shape the evolution of stars and stellar explosions, using **nucleosynthesis calculations** based on advanced stellar models.
To probe these critical reactions, we carry out **experiments with radioactive ion beams** at leading facilities around the world.
These measurements help reduce uncertainties in the models and sharpen our picture of how the rarest elements are formed.
Finally, we compare our predictions with the latest **astronomical observations**, which both test our theories of nucleosynthesis and guide the direction of future experiments and modeling.

You can explore more in our [publications]({{ site.baseurl }}/publications) and [presentations]({{ site.baseurl }}/talks).
If you want to discuss further, don't hesitate to [contact](mailto:{{site.email}}).

---

### <i class="fa fa-search" aria-hidden="true"></i>&nbsp; Research Interests
nuclear astrophysics • radiative capture reactions with recoil separators • nuclear reaction networks • large-scale nuclear sensitivity studies • charged–particle spectroscopy • in–beam and activation γ-ray spectroscopy • experimental studies with stable and radioactive ion beams

---
### The origin of the elements

<div class="container">

<div id="periodic-table"></div>

<div class="legend" id="legend">
    <div class="legend-item"><div class="legend-color" style="background:#8A2BE2"></div><span>Big Bang nucleosynthesis</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#FF4500"></div><span>Cosmic Ray Spallation</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#1E90FF"></div><span>Massive stars</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#FFD700"></div><span>Exploding massive stars</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#9D2235"></div><span>Neutron Star Mergers or ν-driven ejecta</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#6B8E23"></div><span>Dying low- and intermediate-mass stars</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#808080"></div><span>Exploding white dwarfs</span></div>
    <div class="legend-item"><div class="legend-color" style="background:#ffffff; border: 1px solid #ccc;"></div><span>Man-made, artificial (or decay products)</span></div>
</div>
<div class="caption">
Motivated by Christian Iliadis' (UNC/TUNL) <a href="https://iliadis.web.unc.edu/elements/">version</a>.
</div>
<div id="controls">
    <button id="downloadBtn">Download the periodic table!</button>
</div>

</div>

<script>
// === CONFIG ===
const origins = {
    "Big Bang nucleosynthesis": "#8A2BE2",
    "Cosmic Ray Spallation": "#FF4500",
    "Massive stars": "#1E90FF",
    "Exploding massive stars": "#FFD700",
    "Neutron Star Mergers or ν-driven ejecta": "#9D2235",
    "Dying low- and intermediate-mass stars": "#6B8E23",
    "Exploding white dwarfs": "#808080",
    "Man-made, artificial": "#ffffff",
};

// Multi-origin compositions
const multiOrigins = {
    3:[{origin:"Big Bang nucleosynthesis",fraction:.5},{origin:"Cosmic Ray Spallation",fraction:.5}],
    6:[{origin:"Massive stars",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    7:[{origin:"Massive stars",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    9:[{origin:"Massive stars",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    14:[{origin:"Massive stars",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    16:[{origin:"Massive stars",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    19:[{origin:"Massive stars",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    21:[{origin:"Massive stars",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    23:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    24:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    25:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    26:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    27:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Massive stars",fraction:.25},{origin:"Exploding massive stars",fraction:.25}],
    28:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Exploding massive stars",fraction:.5}],
    29:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Massive stars",fraction:.25},{origin:"Exploding massive stars",fraction:.25}],
    30:[{origin:"Exploding white dwarfs",fraction:.5},{origin:"Massive stars",fraction:.25},{origin:"Exploding massive stars",fraction:.25}],
    31:[{origin:"Massive stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    32:[{origin:"Massive stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    34:[{origin:"Massive stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    35:[{origin:"Massive stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    36:[{origin:"Massive stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    37:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Massive stars",fraction:.25},{origin:"Dying low- and intermediate-mass stars",fraction:.25}],
    41:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    44:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    46:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    48:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    49:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    59:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    60:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    70:[{origin:"Dying low- and intermediate-mass stars",fraction:.5},{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5}],
    72:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    73:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    74:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    80:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    81:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
    83:[{origin:"Neutron Star Mergers or ν-driven ejecta",fraction:.5},{origin:"Dying low- and intermediate-mass stars",fraction:.5}],
};

// Elements data
const elements = [
    {number:1,name:"Hydrogen",symbol:"H",x:1,y:1,origin:"Big Bang nucleosynthesis",fact:"Most of it was made 3 minutes after the Big Bang nucleosynthesis!"},
    {number:2,name:"Helium",symbol:"He",x:19,y:1,origin:"Big Bang nucleosynthesis",fact:"About 25% of the mass of the universe is helium!"},
    {number:3,name:"Lithium",symbol:"Li",x:1,y:2,origin:"Big Bang nucleosynthesis",fact:"The lightest metal, produced in the Big Bang and in stars."},
    {number:4,name:"Beryllium",symbol:"Be",x:2,y:2,origin:"Big Bang nucleosynthesis",fact:"Rare element produced by cosmic ray spallation."},
    {number:5,name:"Boron",symbol:"B",x:14,y:2,origin:"Big Bang nucleosynthesis",fact:"Also produced by cosmic ray spallation."},
    {number:6,name:"Carbon",symbol:"C",x:15,y:2,origin:"Dying low- and intermediate-mass stars",fact:"Basis of all known life, formed in aging stars."},
    {number:7,name:"Nitrogen",symbol:"N",x:16,y:2,origin:"Dying low- and intermediate-mass stars",fact:"Most nitrogen in the universe is synthesized in stars."},
    {number:8,name:"Oxygen",symbol:"O",x:17,y:2,origin:"Dying low- and intermediate-mass stars",fact:"The third most abundant element in the universe."},
    {number:9,name:"Fluorine",symbol:"F",x:18,y:2,origin:"Dying low- and intermediate-mass stars",fact:"Formed in asymptotic giant branch stars."},
    {number:10,name:"Neon",symbol:"Ne",x:19,y:2,origin:"Dying low- and intermediate-mass stars",fact:"Abundant in the universe but rare on Earth."},
    {number:11,name:"Sodium",symbol:"Na",x:1,y:3,origin:"Exploding massive stars",fact:"Created in supernovae through fusion and neutron capture."},
    {number:12,name:"Magnesium",symbol:"Mg",x:2,y:3,origin:"Exploding massive stars",fact:"Eighth most abundant element in the universe."},
    {number:13,name:"Aluminum",symbol:"Al",x:14,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Most abundant metal in Earth's crust."},
    {number:14,name:"Silicon",symbol:"Si",x:15,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Makes up about 27% of Earth's crust."},
    {number:15,name:"Phosphorus",symbol:"P",x:16,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Essential for life, found in DNA and ATP."},
    {number:16,name:"Sulfur",symbol:"S",x:17,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Abundant in the universe and essential for life."},
    {number:17,name:"Chlorine",symbol:"Cl",x:18,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Most chlorine on Earth is in the oceans."},
    {number:18,name:"Argon",symbol:"Ar",x:19,y:3,origin:"Dying low- and intermediate-mass stars",fact:"Third most abundant gas in Earth's atmosphere."},
    {number:19,name:"Potassium",symbol:"K",x:1,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Essential mineral for nerve function in animals."},
    {number:20,name:"Calcium",symbol:"Ca",x:2,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Most abundant metal in the human body."},
    {number:21,name:"Scandium",symbol:"Sc",x:4,y:4,origin:"Dying low- and intermediate-mass star",fact:"Rare earth element found in stars."},
    {number:22,name:"Titanium",symbol:"Ti",x:5,y:4,origin:"Exploding massive stars",fact:"Ninth most abundant element in Earth's crust."},
    {number:23,name:"Vanadium",symbol:"V",x:6,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Added to steel for strength and wear resistance."},
    {number:24,name:"Chromium",symbol:"Cr",x:7,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Hard, corrosion-resistant metal."},
    {number:25,name:"Manganese",symbol:"Mn",x:8,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Essential for steel production and biological processes."},
    {number:26,name:"Iron",symbol:"Fe",x:9,y:4,origin:"Dying low- and intermediate-mass stars",fact:"Most abundant element on Earth by mass."},
    {number:27,name:"Cobalt",symbol:"Co",x:10,y:4,origin:"Exploding massive stars",fact:"Used in batteries and magnetic alloys."},
    {number:28,name:"Nickel",symbol:"Ni",x:11,y:4,origin:"Exploding massive stars",fact:"Fifth most abundant element on Earth."},
    {number:29,name:"Copper",symbol:"Cu",x:12,y:4,origin:"Exploding massive stars",fact:"First metal used by humans, over 10,000 years ago."},
    {number:30,name:"Zinc",symbol:"Zn",x:13,y:4,origin:"Exploding massive stars",fact:"Essential mineral for human health."},
    {number:31,name:"Gallium",symbol:"Ga",x:14,y:4,origin:"Exploding massive stars",fact:"Melts just above room temperature."},
    {number:32,name:"Germanium",symbol:"Ge",x:15,y:4,origin:"Exploding massive stars",fact:"Important semiconductor material."},
    {number:33,name:"Arsenic",symbol:"As",x:16,y:4,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Notorious poison but essential trace element for some species."},
    {number:34,name:"Selenium",symbol:"Se",x:17,y:4,origin:"Exploding massive stars",fact:"Essential nutrient but toxic in large amounts."},
    {number:35,name:"Bromine",symbol:"Br",x:18,y:4,origin:"Exploding massive stars",fact:"One of only two liquid elements at room temperature."},
    {number:36,name:"Krypton",symbol:"Kr",x:19,y:4,origin:"Exploding massive stars",fact:"Noble gas used in lighting and photography."},
    {number:37,name:"Rubidium",symbol:"Rb",x:1,y:5,origin:"Exploding massive stars",fact:"Soft, silvery-white metallic element."},
    {number:38,name:"Strontium",symbol:"Sr",x:2,y:5,origin:"Dying low- and intermediate-mass stars",fact:"Gives red color to fireworks."},
    {number:39,name:"Yttrium",symbol:"Y",x:4,y:5,origin:"Dying low- and intermediate-mass stars",fact:"Used in LEDs and superconductors."},
    {number:40,name:"Zirconium",symbol:"Zr",x:5,y:5,origin:"Dying low- and intermediate-mass stars",fact:"Resistant to corrosion, used in nuclear reactors."},
    {number:41,name:"Niobium",symbol:"Nb",x:6,y:5,origin:"Exploding massive stars",fact:"Used in jet engines and particle accelerators."},
    {number:42,name:"Molybdenum",symbol:"Mo",x:7,y:5,origin:"Dying low- and intermediate-mass stars",fact:"Essential trace element for animals and plants."},
    {number:43,name:"Technetium",symbol:"Tc",x:8,y:5,origin:"Exploding massive stars",fact:"First artificially produced element."},
    {number:44,name:"Ruthenium",symbol:"Ru",x:9,y:5,origin:"Exploding massive stars",fact:"Rare transition metal."},
    {number:45,name:"Rhodium",symbol:"Rh",x:10,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"One of the rarest and most valuable metals."},
    {number:46,name:"Palladium",symbol:"Pd",x:11,y:5,origin:"Exploding massive stars",fact:"Used in catalytic converters and jewelry."},
    {number:47,name:"Silver",symbol:"Ag",x:12,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Best electrical conductor of all elements."},
    {number:48,name:"Cadmium",symbol:"Cd",x:13,y:5,origin:"Exploding massive stars",fact:"My first nuclear astrophysics project was about a reaction with cadmium!"},
    {number:49,name:"Indium",symbol:"In",x:14,y:5,origin:"Exploding massive stars",fact:"Used in touch screens and LCD displays."},
    {number:50,name:"Tin",symbol:"Sn",x:15,y:5,origin:"Dying low- and intermediate-mass stars",fact:"Alloyed with copper to make bronze."},
    {number:51,name:"Antimony",symbol:"Sb",x:16,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Known since ancient times."},
    {number:52,name:"Tellurium",symbol:"Te",x:17,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Rare, silvery-white metalloid."},
    {number:53,name:"Iodine",symbol:"I",x:18,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Essential for thyroid function."},
    {number:54,name:"Xenon",symbol:"Xe",x:19,y:5,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in high-intensity lamps and anesthesia."},
    {number:55,name:"Caesium",symbol:"Cs",x:1,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Most electropositive element."},
    {number:56,name:"Barium",symbol:"Ba",x:2,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in X-ray imaging."},
    {number:71,name:"Lutetium",symbol:"Lu",x:4,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in nuclear control rods."},
    {number:72,name:"Hafnium",symbol:"Hf",x:5,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in nuclear control rods."},
    {number:73,name:"Tantalum",symbol:"Ta",x:6,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Highly corrosion-resistant."},
    {number:74,name:"Tungsten",symbol:"W",x:7,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Highest melting point of all elements."},
    {number:75,name:"Rhenium",symbol:"Re",x:8,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"One of the rarest elements in Earth's crust."},
    {number:76,name:"Osmium",symbol:"Os",x:9,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Densest naturally occurring element."},
    {number:77,name:"Iridium",symbol:"Ir",x:10,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Second-densest element after osmium."},
    {number:78,name:"Platinum",symbol:"Pt",x:11,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Precious metal used in jewelry and catalytic converters."},
    {number:79,name:"Gold",symbol:"Au",x:12,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Most malleable of all metals."},
    {number:80,name:"Mercury",symbol:"Hg",x:13,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Only metal that is liquid at room temperature."},
    {number:81,name:"Thallium",symbol:"Tl",x:14,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Extremely toxic, used in rat poison."},
    {number:82,name:"Lead",symbol:"Pb",x:15,y:6,origin:"Dying low- and intermediate-mass stars",fact:"Heavy metal known since ancient times."},
    {number:83,name:"Bismuth",symbol:"Bi",x:16,y:6,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Heaviest mostly stable element."},
    {number:84,name:"Polonium",symbol:"Po",x:17,y:6,origin:"Man-made, artificial",fact:""},
    {number:85,name:"Astatine",symbol:"At",x:18,y:6,origin:"Man-made, artificial",fact:""},
    {number:86,name:"Radon",symbol:"Ra",x:19,y:6,origin:"Man-made, artificial",fact:""},
    {number:87,name:"Francium",symbol:"Fr",x:1,y:7,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Most electropositive element."},
    {number:88,name:"Radium",symbol:"Ra",x:2,y:7,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Most electropositive element."},
    {number:103,name:"Lawrencium",symbol:"Lr",x:4,y:7,origin:"Man-made, artificial",fact:""},
    {number:104,name:"Rutherfordium",symbol:"Rf",x:5,y:7,origin:"Man-made, artificial",fact:""},
    {number:105,name:"Dubnium",symbol:"Db",x:6,y:7,origin:"Man-made, artificial",fact:""},
    {number:106,name:"Seaborgium",symbol:"Sg",x:7,y:7,origin:"Man-made, artificial",fact:""},
    {number:107,name:"Bohrium",symbol:"Bh",x:8,y:7,origin:"Man-made, artificial",fact:""},
    {number:108,name:"Hassium",symbol:"Hs",x:9,y:7,origin:"Man-made, artificial",fact:""},
    {number:109,name:"Meitnerium",symbol:"Mt",x:10,y:7,origin:"Man-made, artificial",fact:""},
    {number:110,name:"Darmstadtium",symbol:"Ds",x:11,y:7,origin:"Man-made, artificial",fact:""},
    {number:111,name:"Roentgenium",symbol:"Rg",x:12,y:7,origin:"Man-made, artificial",fact:""},
    {number:112,name:"Copernicium",symbol:"Cn",x:13,y:7,origin:"Man-made, artificial",fact:""},
    {number:113,name:"Nihonium",symbol:"Nh",x:14,y:7,origin:"Man-made, artificial",fact:""},
    {number:114,name:"Flerovium",symbol:"Fl",x:15,y:7,origin:"Man-made, artificial",fact:""},
    {number:115,name:"Moscovium",symbol:"Mc",x:16,y:7,origin:"Man-made, artificial",fact:""},
    {number:116,name:"Livermorium",symbol:"Lv",x:17,y:7,origin:"Man-made, artificial",fact:""},
    {number:117,name:"Tenessine",symbol:"Ts",x:18,y:7,origin:"Man-made, artificial",fact:""},
    {number:118,name:"Oganesson",symbol:"Og",x:19,y:7,origin:"Man-made, artificial",fact:""},
    {number:57,name:"Lanthanum",symbol:"La",x:4,y:9,origin:"Dying low- and intermediate-mass stars",fact:"First element in the lanthanide series."},
    {number:58,name:"Cerium",symbol:"Ce",x:5,y:9,origin:"Dying low- and intermediate-mass stars",fact:"Most abundant of the rare earth elements."},
    {number:59,name:"Praseodymium",symbol:"Pr",x:6,y:9,origin:"Exploding massive stars",fact:"Used in aircraft engines."},
    {number:60,name:"Neodymium",symbol:"Nd",x:7,y:9,origin:"Exploding massive stars",fact:"Makes powerful magnets."},
    {number:61,name:"Promethium",symbol:"Pm",x:8,y:9,origin:"Man-made, artificial",fact:"Radioactive and rare."},
    {number:62,name:"Samarium",symbol:"Sm",x:9,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in cancer treatments."},
    {number:63,name:"Europium",symbol:"Eu",x:10,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Makes red phosphors in TV screens."},
    {number:64,name:"Gadolinium",symbol:"Gd",x:11,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in MRI contrast agents."},
    {number:65,name:"Terbium",symbol:"Tb",x:12,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Makes green phosphors."},
    {number:66,name:"Dysprosium",symbol:"Dy",x:13,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in nuclear reactors."},
    {number:67,name:"Holmium",symbol:"Ho",x:14,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Has the highest magnetic strength."},
    {number:68,name:"Erbium",symbol:"Er",x:15,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Used in fiber optics."},
    {number:69,name:"Thulium",symbol:"Tm",x:16,y:9,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Rarest rare earth element."},
    {number:70,name:"Ytterbium",symbol:"Yb",x:17,y:9,origin:"Exploding massive stars",fact:"Used in atomic clocks."},
    {number:89,name:"Actinium",symbol:"Ac",x:4,y:10,origin:"Man-made, artificial",fact:""},
    {number:90,name:"Thorium",symbol:"Th",x:5,y:10,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Radioactive, potential nuclear fuel."},
    {number:91,name:"Protactinium",symbol:"Pa",x:6,y:10,origin:"Man-made, artificial",fact:""},
    {number:92,name:"Uranium",symbol:"U",x:7,y:10,origin:"Neutron Star Mergers or ν-driven ejecta",fact:"Fuel for nuclear power plants."},
    {number:93,name:"Neptunium",symbol:"Np",x:8,y:10,origin:"Man-made, artificial",fact:""},
    {number:94,name:"Plutonium",symbol:"Pu",x:9,y:10,origin:"Man-made, artificial",fact:""},
    {number:95,name:"Americium",symbol:"Am",x:10,y:10,origin:"Man-made, artificial",fact:""},
    {number:96,name:"Curium",symbol:"Cm",x:11,y:10,origin:"Man-made, artificial",fact:""},
    {number:97,name:"Berkelium",symbol:"Bk",x:12,y:10,origin:"Man-made, artificial",fact:""},
    {number:98,name:"Californium",symbol:"Cf",x:13,y:10,origin:"Man-made, artificial",fact:""},
    {number:99,name:"Einsteinium",symbol:"Es",x:14,y:10,origin:"Man-made, artificial",fact:""},
    {number:100,name:"Fermium",symbol:"Fm",x:15,y:10,origin:"Man-made, artificial",fact:""},
    {number:101,name:"Mendelevium",symbol:"Md",x:16,y:10,origin:"Man-made, artificial",fact:""},
    {number:102,name:"Nobelium",symbol:"Nb",x:17,y:10,origin:"Man-made, artificial",fact:""},
];

// Synthetic discovery years to fill empty facts
const synthesisYears = new Map([
    [84,1898],[85,1940],[86,1900],[89,1899],[91,1913],[93,1940],[94,1940],[95,1944],[96,1944],
    [97,1949],[98,1950],[99,1952],[100,1952],[101,1955],[102,1958],[103,1961],[104,1964],
    [105,1968],[106,1974],[107,1981],[108,1984],[109,1982],[110,1994],[111,1994],[112,1996],
    [113,2003],[114,1998],[115,2003],[116,2000],[117,2010],[118,2002]
]);

// Fill in empty facts using the above years
elements.forEach(e => {
    if (!e.fact || !e.fact.trim()) {
        const year = synthesisYears.get(e.number);
        if (year) e.fact = `Synthetic element first synthesized in ${year}.`;
        else e.fact = "Synthetic element."; // fallback
    }
});


        // === D3 Rendering ===
        const tableRoot = d3.select('#periodic-table');
        const svg = tableRoot.append('svg');
        const tooltip = d3.select('body').append('div').attr('class','tooltip').style('opacity',0);

        function getLayout() {
            // Grid spans 19 columns; compute a cell size that fits the container comfortably
            const containerWidth = document.querySelector('.container').clientWidth;
            const maxCols = 19;
            const padX = 8; // minimal, will be extended below

            // Let the cell be up to 50px; lower on small screens
            const cellSize = Math.max(24, Math.min(50, Math.floor((containerWidth - 2*24) / (maxCols + 2))));
            const left = Math.max(12, Math.floor(cellSize * 2));
            const top = Math.max(10, Math.floor(cellSize * 1));
            const maxY = d3.max(elements, d => d.y); // includes lanth/actinide rows
            const width = left + maxCols*cellSize + left;
            const height = top + maxY*cellSize + top;

            // Typography proportional to cell size
            const font = {
                number: Math.max(8, Math.round(cellSize * 0.22)),
                symbol: Math.max(10, Math.round(cellSize * 0.42)),
                name:   Math.max(6, Math.round(cellSize * 0.18)),
            };
            return {cellSize, left, top, width, height, font};
        }

        function getGradientId(n){ return `gradient-${n}`; }

        function createMultiColorGradient(defs, element) {
            const parts = multiOrigins[element.number];
            if (!parts) return null;
            const id = getGradientId(element.number);
            const g = defs.append('linearGradient')
                .attr('id', id)
                .attr('x1','0%').attr('y1','0%').attr('x2','100%').attr('y2','0%');
            let cum = 0;
            parts.forEach(p => {
                g.append('stop').attr('offset', `${cum*100}%`).attr('stop-color', origins[p.origin]);
                cum += p.fraction;
                g.append('stop').attr('offset', `${cum*100}%`).attr('stop-color', origins[p.origin]);
            });
            return id;
        }

        function fillFor(element) {
            if (multiOrigins[element.number]) return `url(#${getGradientId(element.number)})`;
            return origins[element.origin];
        }

        function tooltipHTML(d) {
            let text = `<b>${d.name} (${d.symbol})</b><br>Atomic Number: ${d.number}`;
            if (d.fact) text += `<br><br>${d.fact}`;
            if (multiOrigins[d.number]) {
                text += '<br><br><b>Origin Composition:</b>';
                multiOrigins[d.number].forEach(p => {
                    text += `<br>${p.origin}: ${(p.fraction*100).toFixed(0)}%`;
                });
            } else {
                text += `<br><br><b>Origin:</b> ${d.origin}`;
            }
            return text;
        }

        function draw() {
            // Clear prior drawing
            svg.selectAll('*').remove();

            const {cellSize, left, top, width, height, font} = getLayout();

            // Responsive SVG via viewBox
            svg.attr('viewBox', `0 0 ${width} ${height}`)
               .attr('width', width)
               .attr('height', height);

            const defs = svg.append('defs');
            elements.forEach(el => { if (multiOrigins[el.number]) createMultiColorGradient(defs, el); });

            // Cells
            svg.selectAll('rect.element-cell')
                .data(elements)
                .enter()
                .append('rect')
                .attr('class','element-cell')
                .attr('width', cellSize)
                .attr('height', cellSize)
                .attr('rx', Math.max(2, Math.round(cellSize*0.06)))
                .attr('x', d => (d.x-1)*cellSize + left)
                .attr('y', d => (d.y-1)*cellSize + top)
                .attr('fill', d => fillFor(d))
                .on('mouseover', function(event, d){
                    tooltip.transition().duration(150).style('opacity', .95);
                    tooltip.html(tooltipHTML(d));
                })
                .on('mousemove', function(event){
                    tooltip.style('left', (event.pageX + 12) + 'px')
                           .style('top', (event.pageY - 28) + 'px');
                })
                .on('mouseout', function(){
                    tooltip.transition().duration(200).style('opacity', 0);
                });

            // Numbers
            svg.selectAll('text.element-number')
                .data(elements)
                .enter()
                .append('text')
                .attr('class','element-number')
                .attr('x', d => (d.x-1)*cellSize + left + 2)
                .attr('y', d => (d.y-1)*cellSize + top + Math.round(font.number+1))
                .style('font-size', font.number + 'px')
                .style('font-weight', 700)
                .text(d => d.number);

            // Symbols
            svg.selectAll('text.element-symbol')
                .data(elements)
                .enter()
                .append('text')
                .attr('class','element-symbol')
                .attr('x', d => (d.x-1)*cellSize + left + cellSize/2)
                .attr('y', d => (d.y-1)*cellSize + top + Math.round(cellSize/2))
                .attr('text-anchor','middle')
                .attr('dominant-baseline','middle')
                .style('font-weight', 800)
                .style('font-size', font.symbol + 'px')
                .text(d => d.symbol);

            // Names
            svg.selectAll('text.element-name')
                .data(elements)
                .enter()
                .append('text')
                .attr('class','element-name')
                .attr('x', d => (d.x-1)*cellSize + left + cellSize/2)
                .attr('y', d => (d.y-1)*cellSize + top + cellSize - Math.max(3, Math.round(cellSize*0.08)))
                .attr('text-anchor','middle')
                .style('font-size', font.name + 'px')
                .text(d => d.name);
        }

        // Initial draw + resize handling (debounced)
        draw();
        let resizeTimer;
        window.addEventListener('resize', () => {
            clearTimeout(resizeTimer);
            resizeTimer = setTimeout(draw, 120);
        });

        // === PNG Download (SVG + Legend) ===
        document.getElementById('downloadBtn').addEventListener('click', () => {
          const svgNode = document.querySelector('#periodic-table svg');
          const legendNode = document.querySelector('#legend');
          if (!svgNode) return alert('No table found to export.');

          // Clone SVG
          const clone = svgNode.cloneNode(true);
          if (!clone.getAttribute('xmlns')) clone.setAttribute('xmlns', 'http://www.w3.org/2000/svg');

          // Dimensions from viewBox
          let vb = clone.getAttribute('viewBox');
          let width = clone.getAttribute('width');
          let height = clone.getAttribute('height');
          if (vb) {
            const parts = vb.split(/\s+/).map(Number);
            if (parts.length === 4) { width = parts[2]; height = parts[3]; }
          }
          width = Number(width) || 1200;
          height = Number(height) || 800;

          // Add style for fonts
          const styleEl = document.createElementNS('http://www.w3.org/2000/svg','style');
          styleEl.textContent = `text { font-family: 'Raleway', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; }`;
          const defs = clone.querySelector('defs') || clone.insertBefore(document.createElementNS('http://www.w3.org/2000/svg','defs'), clone.firstChild);
          defs.appendChild(styleEl);

          // Serialize SVG
          const serializer = new XMLSerializer();
          const svgString = serializer.serializeToString(clone);
          const svgBlob = new Blob([svgString], {type: 'image/svg+xml;charset=utf-8'});
          const url = URL.createObjectURL(svgBlob);

          const img = new Image();
          img.onload = () => {
            const scale = 2;
            // Canvas: add space for legend below
            const legendHeight = legendNode.offsetHeight || 100;
            const canvas = document.createElement('canvas');
            canvas.width = Math.round(width * scale);
            canvas.height = Math.round((height + legendHeight + 30) * scale); // +30 padding
            const ctx = canvas.getContext('2d');

            // White background
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Draw the SVG
            ctx.drawImage(img, 0, 0, width * scale, height * scale);

            // Render legend as plain text + colored boxes
            // Render legend with title
            const items = legendNode.querySelectorAll('.legend-item');

            // Layout parameters
            const margin = 40;
            const lineHeight = 36 * scale;   // slightly smaller row height
            const gapX = 40 * scale;         // horizontal gap between items
            const gapY = 10 * scale;         // reduced vertical gap
            let yStart = height * scale + margin;

            // --- Title ---
            ctx.font = `${24 * scale}px Raleway, Arial`;
            ctx.textAlign = 'center';
            ctx.fillStyle = '#000';
            ctx.fillText("The origin of the elements", canvas.width / 2, yStart);
            ctx.textAlign = 'left';

            // Update yStart after title
            yStart += 40 * scale;

            // --- Legend items ---
            ctx.font = `${18 * scale}px Raleway, Arial`;
            ctx.textBaseline = 'middle';

            let x = margin, y = yStart;

            items.forEach(item => {
              const colorBox = item.querySelector('.legend-color');
              const label = item.querySelector('span').textContent;

              // Measure text width
              const textWidth = ctx.measureText(label).width;
              const itemWidth = 30 * scale + textWidth + gapX;

              // Wrap to next line if too wide
              if (x + itemWidth > canvas.width - margin) {
                x = margin;
                y += lineHeight + gapY;
              }

              // Draw color box
              ctx.fillStyle = colorBox.style.backgroundColor || '#ccc';
              ctx.fillRect(x, y - 12 * scale, 24 * scale, 24 * scale);
              ctx.strokeStyle = '#333';
              ctx.strokeRect(x, y - 12 * scale, 24 * scale, 24 * scale);

              // Draw text
              ctx.fillStyle = '#000';
              ctx.fillText(label, x + 34 * scale, y);

              // Move x forward
              x += itemWidth;
            });



            // Save PNG
            canvas.toBlob(blob => {
              const link = document.createElement('a');
              link.href = URL.createObjectURL(blob);
              link.download = 'periodic_table_origins.png';
              document.body.appendChild(link);
              link.click();
              document.body.removeChild(link);
              setTimeout(() => URL.revokeObjectURL(link.href), 500);
            }, 'image/png');

            URL.revokeObjectURL(url);
          };

          img.onerror = () => {
            URL.revokeObjectURL(url);
            alert('Failed to render image for download.');
          };

          img.src = url;
        });

    </script>
