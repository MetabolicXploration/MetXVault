# Cell metabolism {#MET}

::: chapterhighlights
This chapter introduces cell metabolism as a dynamical system. While the
previous chapter gave an overview of the constituents of this system,
i.e. enzymes, metabolites, etc., this chapter focuses on conceptual
abstraction of the metabolic system as a whole and how to model its
dynamics over time. The key areas introduced are:

- Conceptualizing cell metabolism as a dynamical system

- Dynamics and regulation of metabolism

- Toolbox for modeling dynamics of metabolism - biochemical reaction
  rate laws and their derivations

- Dynamics of metabolism: Examples of experimental evidence and
  model-based explanations

- Mathematical derivations and example models
:::

<figure id="MET:fig:ecoli_ccm" data-latex-placement="t!">
<div class="center">
<p><embed src=".//images/ecoli_ccm.pdf" /><br />
</p>
</div>
<figcaption>A map of central metabolism in <em>Escherichia coli</em>
bacteria – The diagram shows the reactions, metabolites, co-factors, and
enzymes, as well as a few selected carbon sources and their catabolic
pathways. </figcaption>
</figure>

## Conceptualizing cell metabolism as a dynamical system {#MET:Sec:ConceptualVies}

Cell metabolism is a dynamical process that converts available
metabolites from the environment into biomass and other products. The
metabolism of a typical cell involves thousands of biochemical reactions
and metabolites. What would be a useful way to think about such a
complex, dynamical system? We need a conceptual picture of metabolism to
help us formulate more specific ideas about how it functions, how it can
be manipulated, or even how it has evolved. Here, we first highlight a
few such 'pictures', or ways of thinking about metabolism.

Below we will switch back-and-forth between a high-level view on
metabolism, considering all of it, and a more focused, low-level view
focusing on modeling individual reactions or small sets of reaction
systems (e.g. pathways or motifs). These two viewpoints constitute two
ends of a wide spectrum, and our aim in jumping back-and-forth between
them is to allow the reader to obtain the skills to model dynamics of
reaction systems that make up metabolism, while at the same time to
invite them to think about the overall function of the metabolic system.

### Metabolism as a collection of pathways

The common and historical view of a 'metabolic system' stems from
pioneering biochemical studies from the 1930s onwards, which identified
collections of reactions as so-called 'pathways' [@Gottschalk1985].
Known mostly through the names of their discoverers, these include the
Entner--Doudoroff (ED), Embden--Meyerhof--Parnas (EMP) and
pentose-phosphate (PP) pathways involved in glucose uptake and
conversion into pyruvate, and the Krebs pathway (a.k.a. tricarboxylic
acid cycle, TCA) involved in the conversion of pyruvate into amino acid,
nucleotides, and biomass precursors [@NeidhardtIngraham1990]. This
'pathway-centric' view of cell metabolism lends itself readily to an
assembly line analogy and the notion of (linearly) connected pathways
(see Economic analogy
[\[MET:boxAssemblyLine\]](#MET:boxAssemblyLine){reference-type="ref"
reference="MET:boxAssemblyLine"}).

##### Pathways, yes, but not so linear!

The identification of well-established pathways and the subsequent focus
upon them gives the false impression that cell metabolism consists of a
series of neatly organized and serially connected pathways. This
impression is facilitated by pictures of isolated linear pathways,
common in textbooks and even research papers. In reality, these pathways
are highly interconnected with other pathways.

::: Ecoblock
We can make an analogy that presents metabolism as an assembly line in a
factory. Metabolites enter the line from outside the cell and are
processed -- i.e. acted upon by enzymes -- to create new metabolites
that are ultimately incorporated into cellular biomass. This picture is
reinforced by the common textbook illustration of metabolism as a set of
isolated pathways that are placed 'upstream' or 'downstream' of each
other, and that 'produce' or 'consume' outputs for each other. A key
shortcoming of this analogy is that it conveys a picture in which events
are strictly linear and progressive in their nature, ignoring the cyclic
and inter-connected nature of metabolism. Despite this shortcoming, this
analogy captures the point that the flux of materials through the system
can attain a 'steady-state' of equal in- and out-flux across individual
reactions (see further discussion of the steady-state concept in the
main text). One important difference however between an assembly line
and metabolism is that the rate at a given assembly stage in a factory
is not a function of how many units are waiting to be processed because
factory machines tend run at fixed rates. In metabolism, the rate of a
reaction is a function of the substrate concentration until saturated.
This leads to distinctive behavior not found in factory assembly lines.
Another important difference with a factory assembly line is that unlike
an assembly line, metabolism in some cases is able to in both directions
along the line. The most well known of these is the bidirectionality of
the glycolytic and gluconeogenic pathways.
:::

Part of these interconnections within metabolism arise from
co-substrates and specific metabolite pairs that participate in many
reactions. For example, co-substrates such as ATP and NADH link many
parts of metabolism through reactions in which they are generated or
consumed (Fig. [1.2](#MET:fig:SimpleMap){reference-type="ref"
reference="MET:fig:SimpleMap"}), while the glutamate -
$\alpha$-ketoglutarate pair is involved in the TCA cycle as well as
acting as a group donor in all amino acid biosynthesis pathways.

The pathway view provides a useful starting point to think about
metabolism, but a complete understanding of metabolism dynamics and
metabolic phenotypes requires us to come to terms with the highly
connected nature of these pathways (see below, Box
[\[MET:block:coSubstrateCycles\]](#MET:block:coSubstrateCycles){reference-type="ref"
reference="MET:block:coSubstrateCycles"}).

<figure id="MET:fig:SimpleMap" data-latex-placement="b!">
<div class="center">
<embed src=".//images/MET_SimpleMap.pdf" style="width:70.0%" />
</div>
<figcaption>A simplified map of central metabolism, particularly
highlighting interconnections among different processes (i.e. pathways)
through the NAD(P)<span class="math inline">\(^+\)</span> / NAD(P)H
co-substrate pair. </figcaption>
</figure>

### Coarse grained views of metabolism

The highly connected nature of metabolism makes it difficult to
understand its overall dynamics just from individual pathways. It also
makes it hard to conceptualize metabolism as a single, linear process,
or as serially connected pathways. Here, a coarse-grained viewpoint,
focusing on the overall function of cell metabolism, might prove
helpful. There have been several such views developed, with two
highlighted here.

##### Metabolism as biomass generator.

A widely applied coarse-grained view of metabolism considers it as a
vehicle to biomass production. In this view, metabolism is considered as
two coupled processes, one producing energy and compounds that can act
as building blocks (*e.g.* amino acids), and one that uses these to
create larger macro molecules (*e.g.* proteins and lipids) needed to
make a new cell. These two processes are called catabolic and anabolic
metabolism respectively, and their coupling presents the whole cell
metabolism
(Fig. [1.3](#MET:fig:ConceptMetabolismIC){reference-type="ref"
reference="MET:fig:ConceptMetabolismIC"} A). This coarse-grained model
is widely used
(e.g. [@NeidhardtIngraham1990; @WesterhoffHellingwerf1983]. However, it
is not always clear how to partition various pathways and reactions as
anabolic and catabolic, and the notion of metabolism organized solely to
satisfy for biomass production does not capture certain metabolic
phenotypes, such as no-growth states or excretion of high-energy
metabolites (*i.e.* metabolic overflow).

##### Metabolism as electron flow.

An alternative coarse-grained view of metabolism is obtained from a more
chemical standpoint. When one writes down an overall reaction for
cellular metabolism, considering compounds taken up from the environment
and created at the end of various metabolic processes, one realizes that
this is a redox reaction, a type of reaction where electrons are
exchanged between participating reactants (see
Fig. [1.3](#MET:fig:ConceptMetabolismIC){reference-type="ref"
reference="MET:fig:ConceptMetabolismIC"} B and Box
[\[MET:block:redoxLadder\]](#MET:block:redoxLadder){reference-type="ref"
reference="MET:block:redoxLadder"}). This means that the actual
reactions within metabolism that enable this overall reaction must
compose also of some redox reactions. In other words, we can argue that
metabolism consists of (besides other reactions) a series of redox
reactions that enable flow of electrons. Metabolism is thus an
inter-connected system of reactions that allows flow of electrons from
readily oxidized compounds (electron rich compounds with low or negative
reduction potentials) towards readily reduced compounds (electron poor
compounds with positive reduction potentials)
[@BranscombRussell2013; @ZerfassAsally2019].
(Fig. [1.3](#MET:fig:ConceptMetabolismIC){reference-type="ref"
reference="MET:fig:ConceptMetabolismIC"} B). As the Nobel laureate
Albert Szent-Györgyi (1893 -- 1986), who studied the TCA cycle and
discovered vitamin C biosynthesis pathways, once said, "Life is an
electron looking for a place to rest.".

Emphasizing its redox reactions, the metabolic system can be visualized
on a reduction potential chart, which is sometimes called a 'redox
ladder'
(Fig. [1.4](#MET:fig:RedoxChartMetabolismIC){reference-type="ref"
reference="MET:fig:RedoxChartMetabolismIC"} and box
[\[MET:block:redoxLadder\]](#MET:block:redoxLadder){reference-type="ref"
reference="MET:block:redoxLadder"}). This potential chart shows
reduction potential of redox half reactions (usually in reduction
direction) and allows us to readily visualize the thermodynamic
feasibility of redox reaction pairs. The chart is ordered in such a way
that any reduction half reaction can be paired with any other placed
below it, resulting in a thermodynamically feasible redox reaction, but
not with those above it. We notice that cell metabolism, in order to
maintain electron flows, needs to maintain thermodynamic feasibility of
the overall and all intermediate reactions. The key requirement for this
is to have access to electron donors (e.g. carbohydrates) and terminal
electron acceptors (e.g. oxygen). One must also note that the redox
ladder depicted in
Fig. [1.4](#MET:fig:RedoxChartMetabolismIC){reference-type="ref"
reference="MET:fig:RedoxChartMetabolismIC"} is derived for standard
concentrations of metabolites, whereas the reduction potentials would
depend on actual concentrations in the cell.

<figure id="MET:fig:ConceptMetabolismIC" data-latex-placement="t">
<div class="center">
<p><embed src=".//images/MET_ConceptMetabolismIC.pdf"
style="width:60.0%" /><br />
</p>
</div>
<figcaption> Coarse-grained models of cell metabolism – (A) A conceptual
drawing of cell metabolism as provider of precursors (catabolism) and
generator of biomass from those (anabolism). (B) A conceptual drawing of
cell metabolism as enabling an abstract redox reaction between a pair of
electron donors and acceptors. The electron donor can at the same time
be the carbon source for biomass generation, or there can be a separate
‘carbon-donor’. This overall redox reaction is an abstraction, in the
sense that in real metabolism electrons are not directly transferred
from the original donor to biomass precursors but rather there are many
intermediary redox reactions such as those involving key carrier
co-substrate metabolite pairs NAD(P)<span
class="math inline">\(^+\)</span>/NAD(P)H.</figcaption>
</figure>

::: Physicsblock
We can highlight the overall redox reaction implemented by the cellular
metabolism further, by writing it as two separate reactions consisting
of an oxidation reaction (involving a molecule releasing electrons) and
a reduction reaction (involving a molecule accepting electrons) (see
Fig. [1.3](#MET:fig:ConceptMetabolismIC){reference-type="ref"
reference="MET:fig:ConceptMetabolismIC"}). The feasibility of the
paired, overall redox reaction can be measured by the Gibbs' free
energy, or the closely related reduction potential, where a positive
reduction potential (or a negative Gibbs' free energy) indicates a
thermodynamically feasible reaction. Thus, a redox reaction with a
positive reduction potential implies electrons 'flowing' from a molecule
with high reduction potential towards that with a low reduction
potential -- a point that can be visualized using a "reduction ladder",
a chart of reduction potentials
(Fig. [1.4](#MET:fig:RedoxChartMetabolismIC){reference-type="ref"
reference="MET:fig:RedoxChartMetabolismIC"}). Notice that considering
redox reactions as composed of individual reduction and oxidation
reactions is merely a conceptualization, however, this provides a useful
analogy in which we can view a metabolic system as enabling the flux of
electrons across many reactions, and between an initial electron donor
and a final electron acceptor [@Gottschalk1985]. While glucose and
oxygen are possibly the most well-known electron donor and acceptor
pairs, cells, especially microbial cells, can use a wide-range of donors
and acceptors, including nitrogen and sulfur containing compounds,
thereby contributing significantly to biogeochemical cycles of these
compounds [@SchlesingerBernhardt2013].\

[]{#MET:fig:red label="MET:fig:red"}
:::

### Keeping flows in a system of interconnected fluxes

It is noticeable that both coarse-grained views presented above involve
interconnected fluxes that ultimately enable an overall flux. In the
biomass-based view, the flux between catabolism and anabolism is
connected to enable flux into biomass. In the electron-flow based view,
there is again a set of interconnected flows to enable the overall
electron flow from initial donors (e.g. glucose) to final acceptors
(e.g. oxygen).

The interconnection of fluxes in metabolism is most clearly visible in
reactions involving co-substrates, such as NAD(P)$^+$ / NAD(P)H and
ADP/ATP pairs (see below, Box
[\[MET:block:coSubstrateCycles\]](#MET:block:coSubstrateCycles){reference-type="ref"
reference="MET:block:coSubstrateCycles"}). The NAD(P)$^+$ / NAD(P)H
pairs form either the oxidation or reduction half-reaction in various
redox reactions thereby enabling the aforementioned electron flows
within the metabolic system. The ATP$^+$/ADP pair forms an energy
carrier, providing driving energy to reactions that would be
thermodynamically infeasible (see section
[1.2.1](#MET:Sec:BiochemicalReactionsAndThermodynamics){reference-type="ref"
reference="MET:Sec:BiochemicalReactionsAndThermodynamics"} below on what
we mean by this). This pair is seen as forming the flux connection
between catabolism and anabolism, where the former is considered to
result in ATP production, and the latter is considered to consume this.

Co-substrates are thus essential in connecting different fluxes, and
therefore processes, within metabolism and their dynamics must be
important to keep overall metabolic flow. It is tempting to speculate
that key co-substrates might be an evolutionary outcome that ensures
stable electron flows in the face of changing conditions. While this
possibility is difficult to prove or disprove, it is interesting to note
that the NAD(P)H/NAD(P)$^+$ pairs can attain a broad range of reduction
potentials that could enable their redox partnering with many of the
different reaction types found in cell
metabolism [@JinichFlamholz2018] - in other words, these two redox pairs
seem to be a versatile tool to connect a wide range of redox reactions
to each other and ensure electron flows.

<figure id="MET:fig:RedoxChartMetabolismIC" data-latex-placement="t">
<div class="center">
<p><embed src=".//images/MET_RedoxChartMetabolismIC_a.pdf"
style="width:50.0%" /><br />
</p>
</div>
<figcaption>Metabolism on a redox ladder – Cartoon representation
highlighting the role of electron flows through redox reactions for a
functioning metabolism, and a reduction potential chart listing key
redox reactions found in cellular metabolism. Notice that the reduction
potential chart shows reduction potentials of half-reactions in the
reduction direction and using metabolite concentrations under standard
conditions, hence the actual potentials would be different and
dynamically changing within the cells. A thermodynamically feasible
reaction would need to combine one half reaction (run in reverse,
oxidation direction) with another one lying below it (i.e. at a higher
reduction potential). Two example feasible redox pairs are shown with
the blue and red data points.</figcaption>
</figure>

### Metabolic system and recurring motifs

Within the highly inter-connected system that is metabolism, specific
reaction arrangements seem to recur frequently, so-called "reaction
motifs". We have already mentioned the cyclic reaction systems,
involving co-substrates as one such motif. Other reaction motifs that
have been highlighted include autocatalytic
cycles [@BarenholzDavidi2017] and branch points [@LaPorteWalsh1984]. As
we will discuss below, these reaction motifs can give rise to specific
nonlinear dynamics and act in auto-regulatory capacity or create
constraints on the metabolic system. In general, however, it is
difficult to ascertain the evolutionary significance of reaction motifs.
While automated approaches, involving graph theoretical analysis of
metabolic systems represented as networks, highlighted certain metabolic
motifs as significant compared to random networks, it was subsequently
shown that this result is dependent both on the original network
representation used and the randomized networks used for
comparison [@BeberFretter2012].

::: Physicsblock
The involvement of co-substrate and key metabolites results in the
coupling of many different parts of the metabolism and in the emergence
of cyclic reaction systems - for example, by connecting different parts
of the metabolism, the NAD(P)H/NAD(P)$^+$ pairs result in cycling
between their different forms. This means that in order to capture the
concentration of all the other molecules involved in these reactions, we
need to consider dynamics of a series of intertwined cyclic reaction
systems, rather than linear pathways akin to an assembly line. Indeed,
it has been argued that cyclic reaction motifs should form the basis of
developing a dynamic understanding of cell
metabolism [@ReichSelkov1981]. It must also be noted that co-substrates,
and possibly other key metabolites, can have 'conserved' concentrations
in the time scales of metabolic flux dynamics. In other words, these
metabolites form 'conserved moieties' within the system, similar to
enzymes, such that altering of the total pool size of these
co-substrates or the ratio of their different forms (e.g. the
NAD$^+$/NADH ratio) can possibly affect the flux distribution across
different pathways that they are connected to
[@HofmeyrKacser1986; @Sauro1994; @BarenholzDavidi2017; @HatakeyamaFurusawa2017; @ReichSelkov1981; @WestDelattre2022].
:::

## Reaction thermodynamics and enzyme kinetics {#MET:Sec:ThermodynamicsAndKinetics}

Independent of our conceptual views on metabolism, the fact remains that
the metabolic system involves flux of matter. A myriad of metabolites
are combined, converted, broken apart, and re-assembled. These
biochemical reactions are catalyzed by enzymes so to improve kinetic
rates, and the entire system must obey the laws of thermodynamics (more
on these later in section
[1.2.1](#MET:Sec:BiochemicalReactionsAndThermodynamics){reference-type="ref"
reference="MET:Sec:BiochemicalReactionsAndThermodynamics"}). In summary,
metabolism constitutes a 'system' of metabolites and their reactions,
together with enzymes. Its dynamics over time ensures fluxes of matter.

### Biochemical reactions and thermodynamics {#MET:Sec:BiochemicalReactionsAndThermodynamics}

Metabolism consists of individual biochemical reactions of the form:
$$\begin{equation}
 \label{MET:eqn:genericChemRxn}
    \stoich_a {\mathrm A} + \stoich_b{\mathrm B} ~ \ce{<=>} ~ \stoich_c{\mathrm C} + \stoich_d {\mathrm D}
\end{equation}$$ where $\stoich_i$ are the so-called stoichiometric
coefficients, determining the number of molecules of the *i*'th chemical
species taking part in the reaction
(Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). While these reactions are catalyzed
by enzymes, they still need to obey thermodynamic laws. We will not
provide a full treatise of the thermodynamics of chemical reactions
here - we refer the reader to excellent books on physical chemistry for
this (e.g. [@PriceDwek1997]) and also to books for a conceptual
introduction to thermodynamics (e.g. [@Ness1983]). Here, it suffices for
us to define the key thermodynamic equation, the Gibbs free energy of
reaction, involving the chemical potential of substrates and products.
Chemical potentials are related to concentrations, where the relation
depends on the ionic strength of the solution. Assuming an ideal
solution, we will write here the Gibbs free energy of reaction directly
in terms of concentrations: $$\begin{equation}
 \label{MET:eqn:genericChemRxnFreeEnergy}
\deltaG = \deltaGstd + R \cdot T \cdot \ln{
\underbrace{\frac{c^{\stoich_c}\cdot d^{\stoich_d}}{a^{\stoich_a}\cdot b^{\stoich_b}}}_{\massactionratio}
},
\end{equation}$$ where the small letters indicate the concentrations of
the substrates and products as given in the above reaction. Notice that
specifying 'products' and 'substrates' automatically specifies a
'forward' direction to the reaction
(Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). In the above expression, the term in
the natural logarithm is the ratio of the concentration of the products
to the concentration of the substrates (considering the forward
direction of the reaction) and is commonly denoted as the mass action
ratio, $\massactionratio$. The term $\deltaGstd$ is the difference
between the standard Gibbs free energy of formation of products and
substrates.

The Gibbs free energy of a reaction is the key thermodynamic equation we
introduce here, as it is this equation that determines whether a
reaction would run in the forward direction or not. If the Gibbs free
energy of reaction, for a given set of substrates and products
concentration, is negative ($\deltaG < 0$), the reaction will be
spontaneous in the forward direction as it is written (i.e. in the way
the 'substrates' and 'products' are defined). In other words, chemical
reactions proceed in the direction of lower energy - they minimize the
internal energy of the system. We will see later (in section
[1.2.3.0.6](#MET:Sec:FluxForceRelationship){reference-type="ref"
reference="MET:Sec:FluxForceRelationship"}) that Gibbs free energy will
also feature in rate laws for biochemical reactions.

It is important to introduce here the concept of thermodynamic
equilibrium, which is attained when $\deltaG = 0$. Re-arranging equation
[\[MET:eqn:genericChemRxnFreeEnergy\]](#MET:eqn:genericChemRxnFreeEnergy){reference-type="ref"
reference="MET:eqn:genericChemRxnFreeEnergy"} under this condition, we
can obtain:

$$\begin{equation}
 \label{MET:eqn:genericChemRxnEquilibirumEq}
\deltaGstd = - R\cdot T\cdot \ln{\frac{c^{\stoich_c}_{\mathrm{eq}}\cdot d^{\stoich_d}_{\mathrm{eq}}}{a^{\stoich_a}_{\mathrm{eq}}\cdot b^{\stoich_b}_{\mathrm{eq}}}},
\end{equation}$$ where the subscript "$\mathrm{eq}$" denotes the
concentrations of each species at the thermodynamic equilibrium. The
ensuing ratio is known as the equilibrium constant,
$K_{\mathrm{eq}}={\frac{c^{\stoich_c}_{\mathrm{eq}}\cdot d^{\stoich_d}_{\mathrm{eq}}}{a^{\stoich_a}_{\mathrm{eq}}\cdot b^{\stoich_b}_{\mathrm{eq}}}}$.
Re-arranging equation
[\[MET:eqn:genericChemRxnEquilibirumEq\]](#MET:eqn:genericChemRxnEquilibirumEq){reference-type="ref"
reference="MET:eqn:genericChemRxnEquilibirumEq"}, we can derive an
expression for $K_{\mathrm{eq}}$ as follows: $$\begin{equation}
    \Keq = \expe^{\frac{-\deltaGstd}{R \cdot T}}
     \label{MET:eqn:kEqEquation}
\end{equation}$$ Notice that $K_{\mathrm{eq}}$ depends only on
$\deltaGstd$, which is the difference between the standard Gibbs free
energy of formation of products and substrates involved in a reaction,
and which can be calculated from tabulated values (where available). A
good source of $K_{\mathrm{eq}}$ values of many biochemical reactions is
the eQuilibrator tool
([equilibrator.weizmann.ac.il](https://equilibrator.weizmann.ac.il))
[@NoorBarEven2012; @BeberGollub2021].

This thermodynamic treatment, showing that the equilibrium state of a
reaction is captured by a constant relating to the ratios of product and
substrate concentrations at that state, is fully supported by seminal
experimental works from the second half of 1800s conducted on chemical
reactions by Peter Waage (1833 - 1900) and Cato Guldberg (1836 - 1902),
and their contemporaries. These works were concerned with the
equilibrium, or steady-state, of chemical reactions attained under
different conditions and when initiated from various starting
concentrations of substrates. The key contribution of these studies was
the finding that the equilibrium state in a reaction, that is the ratio
of the concentration of substrates and products at steady-state, is
characterized by a constant [@Mysels1956].

This finding, referred to as the "mass action law", later gave rise to
the notion (rather erroneously) that reaction rate of a chemical
reaction at constant temperature is 'proportional to the product of the
concentrations of the reacting substances' [@Guggenheim1956]. This
derived statement actually is not a law but presents a possible rate
model that would be compatible with the experimentally observed
equilibrium state (i.e. with the mass action law of equilibrium)
[@Mysels1956; @Guggenheim1956] (see
Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"} and the Appendix
[\[MET:Sec:AppendixRateModels\]](#MET:Sec:AppendixRateModels){reference-type="ref"
reference="MET:Sec:AppendixRateModels"}).

:::::::: Physicsblock
$$\begin{equation*}
        \underbrace{\stoich_a~A ~~+~~ \stoich_b~B}_{\text{substrates}} ~~ \ce{<=>[k_+][k_-]} ~~ \underbrace{\stoich_c~C ~~+~~ \stoich_d~D}_{\text{products}}
    
\end{equation*}$$

::: center
:::

:::: minipage
::: center
**Thermodynamic interpretation**
:::

Gibbs free energy of reaction: $$\begin{equation*}
        \deltaG = \deltaGstd + R \cdot T \cdot \ln{\frac{c^{\stoich_c}\cdot d^{\stoich_d}}{a^{\stoich_a}\cdot b^{\stoich_b}}}
    
\end{equation*}$$\
At equilibrium: $$\begin{align*}
        \deltaGstd &= - R \cdot T \cdot \ln{\frac{c^{\stoich_c}_{\mathrm{eq}}\cdot d^{\stoich_d}_{\mathrm{eq}}}{a^{\stoich_a}_{\mathrm{eq}}\cdot b^{\stoich_b}_{\mathrm{eq}}}} \\
        \expe^{\frac{-\deltaGstd}{R \cdot T}} &= \frac{c^{\stoich_c}_{\mathrm{eq}} \cdot d^{\stoich_d}_{\mathrm{eq}}}{a^{\stoich_a}_{\mathrm{eq}} \cdot b^{\stoich_b}_{\mathrm{eq}}} = \Keq
    
\end{align*}$$
::::

:::: minipage
::: center
**Kinetic interpretation**
:::

Backward reaction rate: $$\begin{equation*}
        k_{-} \cdot c^{\stoich_c} \cdot d^{\stoich_d}
    
\end{equation*}$$ Forward reaction rate: $$\begin{equation*}
        k_{+}\cdot a^{\stoich_a} \cdot b^{\stoich_b}
    
\end{equation*}$$\
At equilibrium: $$\begin{align*}
        k_{+} \cdot a^{\stoich_a}_{\mathrm{eq}} \cdot b^{\stoich_b}_{\mathrm{eq}} &= k_{-} \cdot c^{\stoich_c}_{\mathrm{eq}} \cdot d^{\stoich_d}_{\mathrm{eq}} \\
        \frac{k_{+}}{k_{-}} &= \frac{c^{\stoich_c}_{\mathrm{eq}} \cdot d^{\stoich_d}_{\mathrm{eq}}}{a^{\stoich_a}_{\mathrm{eq}} \cdot b^{\stoich_b}_{\mathrm{eq}}} = \Keq
    
\end{align*}$$
::::

\
Cartoon representation of Gibbs free energy of reaction and the
thermodynamic equilibrium -- As a chemical reaction proceeds, the
concentrations of substrates and products change, which in turn affects
the 'energy in the chemical system'. We can, thus, capture the reaction
advancement in a graph, where the x-axis represents the reaction
advancement (i.e. the concentrations of substrates and products at
different times in the reaction course) and the y-axis the internal
energy of the system. The Gibbs free energy of reaction, in a way,
indicates the position of the system in this graphical representation,
where the thermodynamic equilibrium would be the energy minima. At
equilibrium, reaction Gibbs free energy would be zero, allowing us to
derive the relation between substrate and product concentrations at that
point and their free energy of formation. This relation is known as the
equilibrium constant of the reaction. The same relation can be derived
using a rate model to describe the forward and backward reactions that
make up the overall reaction. The thermodynamic result (or derivation)
shows that a given reaction (under a given temperature) would always
have the same substrate and product concentrations at equilibrium, a
point that is empirically verified by experiments and that is known as
the "mass action law". The rate-based interpretation of this
thermodynamic result (or law) is known as the "mass action rate model"
and assumes that rate of a given reaction is proportional to the
concentrations of substrates and products to the power of their
stoichiometry, and adjusted by a rate constant (shown as $k_+$ and $k_-$
above).
::::::::

### Enzymes as catalysts of biochemical reactions

We mentioned many biochemical reactions to be catalyzed by enzymes. It
is therefore worth briefly explaining enzymes. Enzymes are proteins,
chains of amino acids, that fold in the cell in various 3D structures.
For our purposes, we do not need to understand all the intricacies of
how enzymes are made or how they fold into their structures (the reader
is directed to excellent books on these
subjects [@Fersht1998; @BrandenTooze1999]). Suffice to say that in their
folded-state, enzymes can bind a set of target metabolites in such a way
that puts these metabolites in a specific physio-chemical environment
and physical orientation, where their specific biochemical reaction is
facilitated. Thus, enzymes are catalysts that facilitate a chemical
reaction among metabolites. As we will discuss further below, modeling
of biochemical reactions catalyzed by enzymes requires developing a
'mechanistic' picture of how enzymes function. Such models can be
developed based on numerous studies on enzyme structure and function.
Here, we will only state that a generally accepted model involves
enzymes binding their substrates - thereby forming a enzyme-substrate
complex - and then transitioning to a state enabling catalysis. We can
expand this model by also considering so-called allosteric binding
sites, where specific molecules (including sometimes the enzyme's own
substrate or product) can bind and alter the kinetics of either
enzyme-substrate binding or catalytic activity. These allosteric sites,
thus, provide a mechanism for regulation of enzymatic reactions
(Fig. [1.5](#MET:fig:EnzymesAndRegulation){reference-type="ref"
reference="MET:fig:EnzymesAndRegulation"}).

<figure id="MET:fig:EnzymesAndRegulation" data-latex-placement="t!">
<table>
<tbody>
<tr>
<td style="text-align: left;">(A)</td>
<td style="text-align: left;">(B)</td>
</tr>
<tr>
<td style="text-align: left;"><span
class="math display">\[\begin{equation*}
       \text{substrate} ([S])
       \ce{-&gt;[\text{flux: } \flux \approx \enzconctot \cdot
\kcat][\text{enzyme: } \enzconctot]}
       \text{product} ([P])
    
\end{equation*}\]</span></td>
<td style="text-align: left;"><embed
src=".//images/MET_EnzymesAndRegulation.pdf" style="width:50.0%" /></td>
</tr>
</tbody>
</table>
<figcaption>Enzymes and flux regulation – (A) Schematic representation
of a biochemical reaction, highlighting the involvement of a catalyzing
enzyme. For such enzyme-catalyzed reactions, the flux has an upper limit
relating to total enzyme concentration and kinetic parameters of the
enzyme (see section <a href="#MET:Sec:ModelingEnzymaticReactions"
data-reference-type="ref"
data-reference="MET:Sec:ModelingEnzymaticReactions">1.2.3</a> and
Appendix <a href="#MET:Sec:AppendixExampleModels"
data-reference-type="ref"
data-reference="MET:Sec:AppendixExampleModels">[MET:Sec:AppendixExampleModels]</a>
for enzyme catalyzed reaction rate models). (B) Cartoon representation
of enzyme structure and possible mechanisms of allosteric or competitive
regulation. Such regulation can emerge either by the substrate of the
enzyme or other metabolites binding the enzyme (left), and altering its
overall reaction rate (either through competition with the substrate or
by altering the enzyme structure and affecting its kinetic parameters,
right).</figcaption>
</figure>

### Modeling reaction fluxes - reaction rate models {#MET:Sec:ModelingEnzymaticReactions}

Metabolic reactions can involve diverse biophysical mechanisms
(uncatalyzed, enzyme-catalyzed, etc.) and can take place under diverse
biophysical conditions inside a cell (membrane-bound, cytosolic,
extracellular, coupled across membranes, etc.). As such, mechanistically
complete, biophysical representation of all metabolic reactions in
dynamic, mathematical models might never be possible [@Beard2011].
Dynamical models of metabolic systems, as with all mathematical models,
must therefore balance abstraction of real mechanistic features of a
system with achieving a still useful and insight-providing model. At the
core of all dynamical metabolic models are rate laws that aim to capture
the kinetics of biochemical reactions.

##### Non-enzymatic reactions - the reversible and irreversible mass action rate models {#MET:Sec:NonEnzymaticReactions}

All rate models used in metabolic modeling are based on the so-called
'mass action law' described in
Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"} above. As discussed in that section,
the "mass action law", which is derived from thermodynamic principles,
is compatible with a rate model that assumes reaction rate of a chemical
reaction at constant temperature to be 'proportional to the product of
the concentrations of the reacting substances'
[@Guggenheim1956; @Mysels1956] (see
Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). This 'mass action rate model' is
commonly used, especially in the context of elementary reactions
(i.e. reactions involving one single step), and has been shown
empirically to apply in the case of some non-elementary reactions
[@Mysels1956]. According to the mass action model, the net rate of any
reaction of the form given in
Eq. ([\[MET:eqn:genericChemRxn\]](#MET:eqn:genericChemRxn){reference-type="ref"
reference="MET:eqn:genericChemRxn"}) is given by; $$\begin{equation}
 \label{MET:eqn:genericChemRxnReversibleRate}
v = k_+\cdot a^{\stoich_a}\cdot b^{\stoich_b} - k_-\cdot c^{\stoich_c}\cdot d^{\stoich_d},
\end{equation}$$ where small letters denote concentration of the
relevant species of the same letter, $\stoich_i$ denote the
stoichiometric coefficient for species $i$ (as introduced above), and
$k_+$ and $k_-$ denote kinetic rate constants relating substrate
concentrations to reaction rate.

The mass action rate expression is such that if the first term is larger
than the second then $\flux > 0$, and more reactant will convert to
product than product converting to reactant
(Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). This situation will continue until
some point, where the second term will be larger than the first, and the
opposite will occur. Consequently, this expression makes the system
converge towards an equilibrium point, or steady-state, where
$\flux = 0$. As long as the reagents are free to move, they will collide
and interconvert (in both directions) at the microscopic level, even
when the equilibrium is reached. However, at equilibrium, the amount of
reactant converting to product equals the amount of product converting
to reactant per unit of time, therefore there is no net consumption and
production of metabolites
(Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). When we have the concentrations that
lead to the thermodynamic equilibrium of the reaction, i.e. equilibrium
concentrations, we will have; $$\begin{align*}
\flux &= 0 = k_+\cdot a^{\stoich_a}\cdot b^{\stoich_b} - k_-\cdot c^{\stoich_c}\cdot d^{\stoich_d}
\\[5pt]
\frac{k_+}{k_-} &= \frac{c^{\stoich_c}\cdot d^{\stoich_d}}{a^{\stoich_a}\cdot b^{\stoich_b}}
\end{align*}$$ This ratio is known as the reaction's equilibrium
constant $\Keq$ and hence the 'mass action rate model' is consistent
with the empirical observations of Waage and Guldberg. As we have shown
in
Eq. ([\[MET:eqn:kEqEquation\]](#MET:eqn:kEqEquation){reference-type="ref"
reference="MET:eqn:kEqEquation"}) above, the equilibrium constant is
equivalent to the reaction's Gibbs free energy under standard
conditions. Note that when considering a biochemical system (rather than
a chemical one), it is customary to report Gibbs free energies for
standard conditions adjusted for a pH of 7, and denoted with superscript
$\circ'$. Thus, we can write; $$\begin{equation}
 \label{MET:eqn:EquilibriumConstantMassAction}
\frac{k_+}{k_-} = \Keq = \expe^{-\frac{\deltaGstd}{R \cdot T}}
\end{equation}$$ where $\deltaGstd$ is the Gibbs free energy under
biological standard conditions, and $R$ and $T$ denote the molar gas
constant[^1] and temperature (in Kelvin) respectively (see
Box [\[MET:block:massAction\]](#MET:block:massAction){reference-type="ref"
reference="MET:block:massAction"}). It is important to note here that,
given $\Keq$ is a constant determined by thermodynamics, the parameters
$k_+$ and $k_-$ cannot be chosen independently, i..e $k_- = \Keq / k_+$.

Following on from this last point, it is important to consider a
reaction with large $\Keq$, i.e. a reaction for which $\deltaGstd$ is
highly negative. In this case, the value of $k_-$ can become small to
the extent that the reverse reaction can be negligible. In this case the
reaction could be considered as effectively irreversible and the rate
model can be approximated by; $$\begin{equation}
    \flux = k_+\cdot a^{\stoich_a}\cdot b^{\stoich_b}
\end{equation}$$

##### Enzymatic reactions

The mass action rate discussed above forms also the basis of modeling
enzymatic reactions. This approach is justified by considering each
enzymatic reaction as a series of 'elementary steps', each obeying the
mass action rate model. To this end, many alternative elementary steps,
or 'enzyme mechanisms', can be considered to 'capture' an enzymatic
reaction and subsequently many alternative assumptions can be made to
simplify the resulting system of steps. It is also possible to include
allosteric regulation or other types of inhibition or activation steps
within these elementary steps, allowing generation of a rich variety of
enzymatic models and rate laws. Here, we will cover some of the most
common of such models, noticing that the construction of these models
follows the same general principles of (i) drawing up elementary
reactions, (ii) writing down mass action based kinetic rates for the
system, and (iii) simplifying the system with assumptions on kinetic
parameters (see Appendix
[\[MET:Sec:AppendixRateModels\]](#MET:Sec:AppendixRateModels){reference-type="ref"
reference="MET:Sec:AppendixRateModels"}). The reader can consult
additional books (e.g. [@Cornish-Bowden2012]) for more specific,
elaborate enzymatic reaction schemes, or can attempt them as an
exercise.

##### Single substrate, irreversible enzymatic rate model (Michaelis-Menten model) {#MET:Sec:SingelSubstrateIrreversible}

A possible representation of an enzyme mediated reaction consisting in
the conversion of a reactant S to a product P could be the following
reaction scheme: $$\begin{equation*}
    {\mathrm{S}} + \mathrm{E} \ce{<=>[k_{1}][k_{2}]} \mathrm{E}{\mathrm{S}} \ce{->[\kcat]} {\mathrm{P}} + \mathrm{E}.
\end{equation*}$$ This reaction scheme is rather specific, for example,
it ignores the possibility that substrate bound enzyme can be converted
into product, while remaining bound on the enzyme. Thus, the above
reaction scheme is derived from a more complete and more complex
reaction scheme through application of several assumptions relating to
individual reactions. The resulting rate model from the above scheme is
usually known as the Michaelis-Menten model, named after the biochemists
Leonor Michaelis and Maud Menten who studied enzyme kinetics in the
early 1900's, but several studies of that time and afterwards arrived at
a similar model using different assumptions. Implementation of the
specific assumptions, as we detailed in Appendix
[\[MET:Sec:AppendixExampleModels\]](#MET:Sec:AppendixExampleModels){reference-type="ref"
reference="MET:Sec:AppendixExampleModels"}, allows one to arrive at the
above reaction system, which can be represented by a reduced ODE system,
compared to the full system. In this reduced ODE system, the ODE
describing the rate of formation of the product, which is equivalent to
reaction rate, becomes: $$\begin{equation}
  \label{MET:eqn:michaelis_menten}
    \flux = \dfrac {\metconc \cdot \etot \cdot \kcat}{\km + \metconc}
\end{equation}$$ where $\etot$ represents the total enzyme
concentration, $\kcat$ is known as the catalytic rate of an enzyme, and
$\km$ is known as the Michaelis-Menten coefficient of the enzyme and is
equal to $(k_2 + \kcat)/k_1$ (we note that depending on the assumptions
used, the expression for $\km$ can vary). Plotting the above rate of
formation of product against increasing substrate concentration (see
Figure [1.6](#MET:fig:MichaelisMentenCurve){reference-type="ref"
reference="MET:fig:MichaelisMentenCurve"}) shows that the rate is a
'saturating function' of substrate, i.e. the rate approaches a threshold
point - given by $\vmax = \etot \cdot \kcat$ as substrate concentration
increases. Thus, we can see that the enzymatic nature of the reaction
introduces a limiting factor on the reaction rate that depends on
$\vmax$, i.e. total enzyme concentration and enzyme's catalytic rate.
This fact underpins the regulation of metabolic flux through regulation
of enzyme levels or enzyme's catalytic rate, and is a key conceptual
point for the constraint-based methods discussed later in this book.

<figure id="MET:fig:MichaelisMentenCurve" data-latex-placement="t!">

<figcaption>Michaelis-Menten rate law – The x- and y-axis show the
substrate concentration (normalized by <span
class="math inline">\(\km\)</span>) and reaction flux (normalized by
<span class="math inline">\(\vmax\)</span>) respectively. The dashed
horizontal line corresponds to <span
class="math inline">\(\vmax\)</span>, i.e. <span
class="math inline">\(\etot \cdot \kcat\)</span>.</figcaption>
</figure>

##### Single substrate, reversible enzymatic rate model (Haldane model) {#MET:Sec:SingelSubstrateReversible}

Considering that all chemical reactions are --- at least, in theory ---
reversible, it is also possible to express the rate of an
enzyme-mediated reaction as a function of the concentration of both
substrate and product. A method to do so has been introduced by Haldane
[@Haldane1965]. It considers the following reaction scheme:
$$\begin{equation*}
    {\mathrm S} + {\mathrm E} \ce{<=>[k_{1}][k_{2}]} {\mathrm {ES}} \ce{<=>[k_{3}][k_{4}]} {\mathrm {EP}} \ce{<=>[k_{5}][k_{6}]} {\mathrm P} + {\mathrm E}.
\end{equation*}$$ Deriving the rate law for this reaction scheme is
slightly more involved, but it follows the same strategy as explained
above, of creating elementary steps, treating them as obeying mass
action rate, and making additional simplifying assumptions. As shown in
Appendix
[\[MET:Sec:AppendixRateModels\]](#MET:Sec:AppendixRateModels){reference-type="ref"
reference="MET:Sec:AppendixRateModels"}, we can follow this strategy to
derive the reversible rate law as follows: $$\begin{equation}
    \flux = \etot\cdot \dfrac{\kcatplus}{\kmS}\cdot \dfrac{\metconc - p\cdot \dfrac{\kcat^-/\kmP}{\kcatplus/\kmS}}{1 + \dfrac{p}{\kmP} + \dfrac{\metconc}{\kmS}}
\end{equation}$$ where $\kmS$ and $\kmP$ are composite constants
relating to the substrate and product binding to the enzyme, and
$\kcatplus$ and $\kcat^-$ are Haldane coefficients (again, composite
parameters of other kinetic constants) describing catalytic rate of the
enzyme (see Appendix
[\[MET:Sec:AppendixRateModels\]](#MET:Sec:AppendixRateModels){reference-type="ref"
reference="MET:Sec:AppendixRateModels"} for further details of these
parameters).

As done in the above section on kinetics of the non-enzymatic reversible
reaction, we can consider the equilibrium condition for this enzymatic
reversible reaction. This would allow us to derive the corresponding
relation between $\Keq$ and reaction Gibbs free energy. Recognizing the
relation between the Haldane composite parameters and $\Keq$ (see
Appendix
[\[MET:Sec:AppendixRateModels\]](#MET:Sec:AppendixRateModels){reference-type="ref"
reference="MET:Sec:AppendixRateModels"}) and the flux-force relation
(see below), we can then re-formulate the reversible rate law as:
$$\begin{equation}
 \label{MET:eqn:factorized_gibbs_energy}
    \flux  = \etot\cdot \kcatplus \cdot \dfrac{\metconc / \kmS}{1 + p/\kmP + \metconc/\kmS}\cdot \left(1 - \expe^{\frac{\deltaG}{R\cdot T}}\right)
\end{equation}$$ where $\deltaG$ is the Gibbs free energy of reaction
for a given substrate and product levels under biological conditions and
considering the forward direction of the reaction. This rate law shows
that forward reaction rate will be independent of thermodynamics, when
the reaction free energy is highly negative (i.e. when the reaction is
far from thermodynamic equilibrium, $\deltaG \ll 0$). However, as the
reaction Gibbs free energy gets close to zero, the reaction rate will
decrease, and as such, there will be a dependence of reaction rate on
reaction free energy.

Another way of writing equation
[\[MET:eqn:factorized_gibbs_energy\]](#MET:eqn:factorized_gibbs_energy){reference-type="ref"
reference="MET:eqn:factorized_gibbs_energy"} is this one:
$$\begin{equation}
    \flux  = \etot\cdot \kcatplus \cdot \dfrac{\metconc/\kmS \cdot \left(1 - \expe^{\frac{\deltaG}{R\cdot T}}\right)}{1 + \metconc/\kmS \cdot \left(1 + \dfrac{\kcatplus}{\kcat^-} \cdot \expe^{\frac{\deltaG}{R\cdot T}} \right)}
\end{equation}$$ where we replace $p/\kmP$ with an expression that
depends on $\metconc$ and $\deltaG$. This alternative expression,
developed in the context of modeling microbial metabolism
[@HohCord-Ruwisch1996; @GrosskopfSoyer2016], can be useful because it
shows us that when the reaction is far from equilibrium
($\deltaG \ll 0$), the term $\expe^{\deltaG / (R\cdot T)}$ will approach
zero and the above formula can be approximated by the irreversible
Michaelis-Menten rate law (Equation
[\[MET:eqn:michaelis_menten\]](#MET:eqn:michaelis_menten){reference-type="ref"
reference="MET:eqn:michaelis_menten"}). In this case, we further notice
that the Haldane coefficient $\kmS$ becomes equivalent to $\km$
introduced above in the irreversible reaction scheme (see section
[1.2.3.0.3](#MET:Sec:SingelSubstrateIrreversible){reference-type="ref"
reference="MET:Sec:SingelSubstrateIrreversible"}).

It is important to note that many reactions within cell metabolism are
experimentally shown to be reversible, indicating that they operate
close to thermodynamic equilibrium
[@CanelasRas2011; @ParkRubin2016; @NoorBarEven2012].

##### Rate models for representing allosteric effects

Rate models for representing allosteric effects, i.e. binding of
additional molecules - or their own substrates - on the enzyme and
affecting the enzyme-mediated reaction rate, can be created either by
adjusting the rate laws given above empirically, or by considering the
additional binding events at 'allosteric sites' of the enzyme and
deriving a new 'mechanistic' rate model. To give an example of the
former strategy, we can consider a Michaelis-Menten rate model adjusted
for an inhibitory effect of the substrate on the enzymatic reaction
rate. This adjusted rate model can be expressed as: $$\begin{equation}
  \label{MET:eqn:michaelis_menten_allosteric}
    \flux = \frac {\vmax \cdot \metconc}{\km + \metconc + \metconc^2/\ki}
\end{equation}$$ where $\ki$ represents the saturation coefficient for
the binding of the substrate at an allosteric site on the enzyme. Notice
that we used such a model in the small multi-stable system example
introduced above (section
[1.3.3](#MET:Sec:MultiStable){reference-type="ref"
reference="MET:Sec:MultiStable"}) and discussed in Appendix
[\[MET:Sec:AppendixExampleModels\]](#MET:Sec:AppendixExampleModels){reference-type="ref"
reference="MET:Sec:AppendixExampleModels"}.

For the same example, the alternative approach (the latter case
mentioned above) would be to develop a mechanistic model involving
multiple binding reaction on an enzyme. The resulting elementary
reactions and their mass action implementation can be then carried out.
This process would result in a set of ODEs, which can then be further
simplified to draw a rate model for the proposed allosteric regulation.
An example of this type model is developed in the context of
multi-substrate binding enzymes, and shown to lead to multi-stability
under certain parameter conditions [@HayesFeliu2022].

##### Flux-force relationship {#MET:Sec:FluxForceRelationship}

All chemical reactions, including biochemical reactions, must obey
thermodynamic laws. This fact manifests itself in several ways in
dynamical modeling. Firstly, reaction direction (or, rather,
feasibility) is determined by the sign of the reaction Gibbs free
energy. Second, the kinetic constants associated with the elemental
reaction steps are constrained by thermodynamics (section
[1.2.3](#MET:Sec:ModelingEnzymaticReactions){reference-type="ref"
reference="MET:Sec:ModelingEnzymaticReactions"}). To see the third
relation arising from thermodynamics, we consider again the simple
non-enzymatic mass action model we used above -- reaction schematic
given in
Eq. ([\[MET:eqn:genericChemRxn\]](#MET:eqn:genericChemRxn){reference-type="ref"
reference="MET:eqn:genericChemRxn"}) and the reaction Gibbs free energy
given by
Eq. ([\[MET:eqn:genericChemRxnFreeEnergy\]](#MET:eqn:genericChemRxnFreeEnergy){reference-type="ref"
reference="MET:eqn:genericChemRxnFreeEnergy"}).

We now re-consider the net rate of reaction as given above in
Eq. ([\[MET:eqn:genericChemRxnReversibleRate\]](#MET:eqn:genericChemRxnReversibleRate){reference-type="ref"
reference="MET:eqn:genericChemRxnReversibleRate"}), and break this into
its components of forward reaction rate (or flux) and reverse reaction
rate (or flux), which are given by; $$\begin{align*}
\flux_+ &= k_+\cdot a^{\stoich_a}\cdot b^{\stoich_b} 
\\
\flux_- &= k_-\cdot c^{\stoich_c}\cdot d^{\stoich_d}
\end{align*}$$ and then, we can express the net forward flux (*J*) as:
$$\begin{align*}
\fluxJ  &= \flux_+ - \flux_- 
= \flux_+ \cdot \left(1 - \frac{\flux_-}{\flux_+}\right) 
= \flux_+ \cdot \left(1 - \frac{k_-\cdot c^{\stoich_c}\cdot d^{\stoich_d} }{k_+\cdot a^{\stoich_a}\cdot b^{\stoich_b} }\right) 
= \flux_+ \cdot \left(1 - \frac{k_-}{k_+}\cdot \massactionratio \right)
\end{align*}$$ In this re-organized form of the net forward flux, we
notice that the expression in parentheses on the right hand side can be
re-expressed in terms of reaction free energy (using
Eq. ([\[MET:eqn:EquilibriumConstantMassAction\]](#MET:eqn:EquilibriumConstantMassAction){reference-type="ref"
reference="MET:eqn:EquilibriumConstantMassAction"})) as follows:
$$\begin{align*}
\fluxJ  &= \flux_+\cdot \left(1 - \frac{k_-}{k_+}\cdot \massactionratio \right) = \flux_+ \cdot \left(1 - \frac{\massactionratio}{\Keq} \right) = \flux_+ \cdot \left(1 - \expe^\frac{\deltaG}{R \cdot T} \right)
\end{align*}$$ Thus, we find that the net forward flux of the reaction
is given by the forward reaction rate multiplied by a thermodynamic
factor. When the reaction is energetically favored, i.e. has large
negative Gibbs free energy, the thermodynamic factor diminishes and the
net forward flux is fully determined by forward reaction rate alone (see
Figure [1.7](#MET:fig:FluxForceCurve){reference-type="ref"
reference="MET:fig:FluxForceCurve"}). When the reaction is closer to
equilibrium, i.e. small negative or near-zero Gibbs free energy, then
the net forward flux will be determined by a combination of forward and
reverse flux rates. This relation between net forward flux and
thermodynamics is referred to as the flux-force relation
[@BeardQian2007; @NoorFlamholz2013] and holds also for the enzymatic
reversible reaction model described above (see section
[1.2.3.0.4](#MET:Sec:SingelSubstrateReversible){reference-type="ref"
reference="MET:Sec:SingelSubstrateReversible"}).

<figure id="MET:fig:FluxForceCurve" data-latex-placement="t!">

<figcaption>The ratio of net forward flux (<span
class="math inline">\(\fluxJ\)</span>) to forward reaction rate (<span
class="math inline">\(\flux_+\)</span>) as a function of the negative
reaction Gibbs free energy</figcaption>
</figure>

##### A note on choosing a reaction rate model

In the above sections, we have introduced several biochemical reaction
rate models. These models fall into two main categories, namely those
that model enzyme action (i.e. enzymatic models) and those that ignore
the enzyme action (i.e. non-enzymatic models). Notice that derivation of
both categories of models rely on the mass action law. In the
non-enzymatic case, we model reactions as single-step forward and
backward reactions using mass action, while in the enzymatic case, we
consider multi-step reaction mechanisms, but still use the mass action
for each individual step. For each category, we can consider the
reaction thermodynamics and model reactions as reversible, but -- as we
discussed above -- we can also choose to approximate reactions as
'irreversible' when the overall reaction's Gibbs free energy is very
negative (i.e. when $\Keq$ is large).

In a given modeling context and metabolic system, it would be a valid
question to ask -- which model should one use? This question can be
answered in parts. In the first instance, we can make a decision about
the use of reversible or irreversible rate models. As already mentioned,
this decision should be based on the value of $\Keq$ -- a reaction with
a very large $\Keq$ can be modeled as irreversible, as long as the
product concentrations are known not to reach very high levels (in a
cell). However, to represent a metabolic reaction as irreversible is not
without consequences even if the reaction always runs in the same
direction (notice that the assumption of irreversible reaction means
that the reaction rate cannot go negative). Reversible kinetics can
capture the negative feedback of reaction products on reaction rate, and
irreversible reaction models would lose this feature
[@Cornish-BowdenCardenas2001]. A recent study by Shen et
al [@ShenKohlhaas2020] showed how important it can be to include product
inhibition to create a predictive metabolic model.

In the case of lower $\Keq$ value -- in combination with a consideration
of possible product concentration -- the modeler should opt for the
reversible rate models, which are thermodynamically consistent. The
decision about use of enzymatic or non-enzymatic reaction models can be
made in a practical manner. If the enzyme associated with the modeled
reaction has measured kinetic rates, it would be sensible to opt for a
enzymatic model (noting that *in vivo* enzyme kinetics might differ from
those measured *in vitro* and that many enzyme kinetics studies use
parameter derivations assuming an irreversible Michaelis-Menten model).
Consequently, it may not be possible to find all the required parameters
in the literature, so to model a reaction using reversible rate model.
In the absence of measured enzyme parameters, the modeler can use
'guesstimated' parameters, based -- for example -- on the distribution
of known enzyme kinetic parameters, or alternatively, use the
non-enzymatic model.

Given the discussion in the preceding paragraph, it is a useful exercise
to consider when the non-enzymatic and enzymatic models might behave in
the same way. We have introduced above the concept of flux-force
relationship, where we have shown that the net flux in a reversible
reaction would be given by the forward flux multiplied by a
thermodynamic factor: $$\begin{align*}
    \fluxJ  &= \flux_+\cdot \left(1 - \frac{\massactionratio}{\Keq} \right)
\end{align*}$$ If we consider this equation for the reversible
non-enzymatic and enzymatic models, we would notice that the
thermodynamic factor would show the same behavior for both models,
depending only on reaction $\Keq$ value and substrate and product
concentrations. Where the models would differ, would be in the behavior
of the $v_+$ term, which takes the form:

For the reversible enzymatic case: $$\begin{align*}
    \flux_+ = \etot \cdot \kcatplus \cdot (\metconc/\kmS) / (1 + \metconc/\kmS + p/\kmP)
\end{align*}$$ And, for the reversible non-enzymatic case:
$$\begin{align*}
    \flux_+ = \metconc \cdot k_+
\end{align*}$$ Where $\kcat$, $\kmS$, and $\kmP$ are the enzyme kinetic
parameters for the enzymatic model and $k_+$ is the forward reaction
rate coefficient for the non-enzymatic model. Thus, the two models would
behave in a similar way, when there is correspondence between these two
terms, which are sometimes referred to as "saturation terms"
[@NoorFlamholz2013]. By re-arranging the above terms, we can show that
correspondence between the two models can be expressed as:
$$\begin{align*}
    \etot \cdot \kcatplus \cdot (1/\kmS) / (1 + \metconc/\kmS + p/\kmP) \approx k_+
\end{align*}$$ We can see that in the regime, where $\metconc \ll \kmS$
and $p \ll \kmP$, both models would behave in a linear fashion and their
behavior would correspond exactly with the right choice of parameters
(i.e. assuming $(\etot \cdot \kcat^+ / \kmS) = k_+$). Outside of this
regime, correspondence would be dependent on both parameters and
concentration of $S$ and $P$. One interesting case to consider is when
total amount of $S$ and $P$ would be conserved, for example, with
cycling reaction schemes. In this case, we can introduce a new parameter
$C$ to describe the total pool of the cycled metabolite (e.g. $C = S+P$)
and the correspondence would be expressed as: $$\begin{align*}
    (\etot \cdot \kcatplus / \kmS) / (1 + (\metconc \cdot \kmS - \metconc \cdot \kmP) / (\kmS \cdot \kmP) + C/\kmP) \approx k_+
\end{align*}$$ Thus, in this case of the sum of substrate and product
concentrations being conserved, we can have correspondence between the
non-enzymatic and enzymatic models when $S$ is small or when
$\kmS = \kmP$.

## Dynamics and regulation of metabolism {#MET:Sec:DynamicsAndItsRegulation}

As explained so far in this chapter, cell metabolism involves
biochemical reactions involving metabolites (and often catalyzed by
enzymes). Thus, understanding metabolism involves studying the dynamics
of this system, trying to predict how metabolite levels will go up or
down, or settle to a steady state as cell physiology changes in response
to external or internal processes (e.g. cells encountering glucose or
undergoing division). Obtaining such understanding requires us to
develop models of biochemical reaction systems and predict the
'dynamics' of those systems. In the previous section, we learned how to
model one biochemical reaction. Now we will see how we can readily
expand these models to capture multi-reaction systems. The 'art' of
developing and analyzing dynamical models falls under the branch of
mathematics known as calculus and nonlinear dynamics. Many introductory
books to these subjects are available, but we find that two particularly
useful ones are those by Silvanus Thompson on calculus [@Silvanus1914]
and by Steven Strogatz on nonlinear dynamics [@Strogatz2000]. Here, we
will not re-introduce these topics but focus solely on various reaction
rate models for metabolic systems that have been developed based on
ODEs. We will highlight relations between these models and reaction
thermodynamics and explore their possible limitations and applications
in different cases. There are also books that are solely dedicated to
models of biochemical reaction kinetics and enzyme kinetics more
broadly - the reader is advised to further explore the topic with the
help of such books, particularly
[@Fersht1998; @Cornish-Bowden2012; @Sauro2012]

### Stoichiometric matrix and ordinary differential equations

As mentioned above, metabolic systems consists of many reactions. When
describing multiple reactions in a biochemical 'system', it is
convenient to represent the stoichiometries of individual reactions in a
compact form called the stoichiometric matrix, $\Stoichmat$. The rows
and columns of this matrix corresponds to $m$ species (i.e. the
metabolites), and to $n$ reactions, found in the system respectively:
$$\begin{equation*}
    \Stoichmat \text{ is a } m \times n\ \mathrm{matrix}
\end{equation*}$$ The intersection of a row and column in the matrix
indicates whether the species represented by that row takes part in the
particular reaction represented by that column, or not. The sign of the
element determines whether there is a net loss or gain of substance, and
the magnitude describes the relative quantity of substance taking part
in the reaction. It is important to appreciate that the elements of the
stoichiometry matrix *do not* concern themselves with the rate of
reaction, and just indicate the quantities taking part in the reaction.

A full description of a biochemical network, including the time-varying,
dynamical behavior of metabolite concentrations, will augment the
stoichiometry matrix with a rate vector, $\fluxv$, forming a so-called
system equation: $$\begin{equation}
    \frac{\intd{\metconcv}}{\intd t}
    = \Stoichmat \, \fluxv (\metconcv)
    \label{MET:eqn:SystemEquation}
\end{equation}$$ This equation represents a system of ordinary
differential equations (ODEs) that describe the time evolution of the
species, $\metconcv$. In other words, the ODE for species $\metconc$
describes the rate of change in the concentration of $\metconc$ with a
given (infinitesimal) change in time. The ODEs can be solved numerically
(i.e. simulated) by computer or studied analytically.

Notice that in mathematics, the time varying entities in a dynamical
systems - in our context, the concentrations of chemical species - are
known as 'variables', while any elements of the system that stay
constant over time are known as 'parameters'. For an insightful and
accessible mathematical treatment of differential equations and system
dynamics, the reader is referred to these two excellent books
[@Silvanus1914; @Strogatz2000], while for a metabolic view of variables
and parameters, the article on the Control of Flux, by Kacser and Burns,
offers a valuable perspective [@KacserBurns1995].

### Dynamic steady state

As stated above, the ODEs describe the time evolution of all variables
$\metconcv$ in the system. An informative approach to any dynamical
system is to consider its steady state, a state where consuming and
generating processes on each variable would have the same rate, i.e. the
ODEs are equal to zero, and there would be no change in the variable
amounts. For example, a water tank filling at a constant rate but
emptying at a rate proportional to the height of water in the tank will
eventually reach a steady-state where the output flow equals the inflow
of water (Fig. [1.8](#MET:fig:SteadyState){reference-type="ref"
reference="MET:fig:SteadyState"}). Under these conditions the height of
water remains constant, or at a steady state.

<figure id="MET:fig:SteadyState" data-latex-placement="t!">
<p>(A) Thermodynamic steady state<br />
<span class="math display">\[\begin{equation*}
        \stoich_a~A ~~+~~ \stoich_b~B ~~ \ce{&lt;=&gt;} ~~ \stoich_c~C
~~+~~ \stoich_d~D
    
\end{equation*}\]</span></p>
<div class="center">

</div>
<p>(B) Dynamic steady states – non-equilibrium thermodynamics<br />
</p>
<div class="center">
<embed src=".//images/MET_SteadyState.pdf" style="width:65.0%" />
</div>
<figcaption> Illustration of thermodynamic equilibrium and dynamical
steady state – (A) Thermodynamic steady state. (B) Dynamic steady states
– non-equilibrium thermodynamics. While the former happens only at
chemical equilibrium, the latter can arise in systems that are far from
chemical equilibrium. A cartoon of a flowing water through a tank and a
reaction involving co-substrate cycling are shown as examples of systems
that can attain dynamical steady states.</figcaption>
</figure>

It is important to note that the thermodynamic equilibrium mentioned
above is also a type of steady-state, but this does not mean that
steady-state is only attained at thermodynamic equilibrium. In other
words, there can be a steady-state where the system is out of
thermodynamic equilibrium but the concentrations of metabolites are not
changing. An example of this would be a linear metabolic pathway of
connected reactions, with influx and outflux of an initial and endpoint
metabolite (as seen in
Fig. [1.8](#MET:fig:SteadyState){reference-type="ref"
reference="MET:fig:SteadyState"}). In such a system, we can readily
consider a scenario where there is influx of the first metabolite,
outflux of the last metabolite, and forward flux through each of the
reactions in the pathway. Thus, we would have a situation where all
reactions are out of thermodynamic equilibrium, but all metabolite
concentrations in the pathway attain a dynamic steady-state, where their
influx and outflux are equal
(Fig. [1.8](#MET:fig:SteadyState){reference-type="ref"
reference="MET:fig:SteadyState"}). The distinction between systems that
are both at steady-state and thermodynamic equilibrium, and those that
are at steady-state but out of thermodynamic equilibrium, is an
important one. It has been shown that complex dynamics, such as
bistability and oscillations (as discussed below) are only possible in
the latter case [@PrigogineLefever1969; @BeardQian2007; @Goldbeter2018].

Mathematically speaking, the steady-state is defined when the ODE
system, i.e. the system equation, is set to zero: $$\begin{equation}
\frac{\intd{\metconcv}}{\intd t} = {\Stoichmat\ \fluxv (\metconcv)} = \mathvectorfont{0} \label{MET:eqn:SystemEquation:StedyState}
\end{equation}$$ For simple systems, such as a tank of water filling and
emptying, there is only one unique steady-state. This is perhaps better
illustrated with a simple biochemical example. Consider a two step
pathway where the first step has a constant rate $k_1$ and the second
step a variable rate determined by a first-order reaction rate, $k_2$.
$$\begin{equation}
    \ce{->[\flux_0 = k_1] S ->[\flux_1 = k_2 \cdot \metconc]}
\end{equation}$$ The differential equation describing the concentration
of metabolite S is given by: $$\begin{equation}
    \frac{\intd \metconc}{\intd t} = k_1 - k_2\cdot \metconc
\end{equation}$$ Setting this equation to zero and solving for
$\metconc$ yields the steady-state level of $S$: $$\begin{equation}
    \metconc = \frac{k_1}{k_2}
\end{equation}$$ This solution indicates there is only a single
steady-state for this system dependent on the parameters ${k_1}$ and
${k_2}$.

### Multiple steady-states and oscillations {#MET:Sec:MultiStable}

In the previous section it was shown that a simple two step pathway
admitted a single steady-state. There can be, however, metabolic systems
that can show multiple steady states. As a simple example, consider the
system shown in
Figure [1.9](#MET:fig:SimplePathway){reference-type="ref"
reference="MET:fig:SimplePathway"}. This shows a linear pathway of two
reactions, with the first reaction activated by the species $x$.

<figure id="MET:fig:SimplePathway" data-latex-placement="t!">
<p><br />
</p>
<figcaption>Cartoon of a simple pathway that features allosteric enzyme
regulation and that can show multiple steady-state solutions (see
Appendix <a href="#MET:Sec:AppendixRateModels" data-reference-type="ref"
data-reference="MET:Sec:AppendixRateModels">[MET:Sec:AppendixRateModels]</a>).
The metabolite ‘x’ positively regulates the first step, <span
class="math inline">\(\flux_1\)</span>. The resulting positive feedback
can result in a bistable system under a certain parameter
regime.</figcaption>
</figure>

Under certain parameter and model choices, such a system can admit three
steady-states. Details of a model that can be simulated can be found in
Appendix
[\[MET:Sec:AppendixExampleModels\]](#MET:Sec:AppendixExampleModels){reference-type="ref"
reference="MET:Sec:AppendixExampleModels"}). Other examples of metabolic
systems with multiple steady-states will be given below. In bi-, or
multi-stable systems, there can be multiple sets of steady state
concentrations and flux rates that the system can settle at. Which set
of steady-states is realized is usually determined by initial
concentrations or can be caused by a change in one of the concentrations
or parameters. Thus, the system can change its steady-state value
abruptly at a threshold value of a specific parameter of the system. For
a metabolic system displaying bistability, we can expect a rapid switch
in multiple fluxes with changes in the concentration of one or few
metabolites [@Strogatz2000]. Furthermore, when bistability is combined
with noise in some parameters (e.g. enzyme expression level) there can
be a multi-modal distribution of flux states across genetically
identical cells (e.g. see [@SimsekKim2018; @RosenthalQi2018] and
section [\[MET:Sec:SelectedExperimentalObservations\]](#MET:Sec:SelectedExperimentalObservations){reference-type="ref"
reference="MET:Sec:SelectedExperimentalObservations"}).

## Concluding remarks

In this chapter, we set out to introduce cellular metabolism as a
dynamical system. We have seen that metabolism comprises many
biochemical reactions, that are historically cataloged and described
into pathways. These pathways are usually not linear, composing of
serial conversions of metabolites, but rather display branching points
and inter-connections through metabolites participating in many
reactions. This inter-connected nature of metabolic systems, together
with the large numbers of participating metabolites and reactions, makes
them a complex system to study and conceptualize.

We have introduced both simplified, coarse-grained viewpoints for
describing metabolism, and mechanistic approaches for detailed dynamical
modeling of it at the level of single reactions. The former can be used
to guide specific ideas on how to study metabolism, or to develop
analogies to other disciplines, while the latter can provide a toolbox
for constructing dynamical models of small or large metabolic systems.
We have provided specific examples of such dynamical models and shown
how they can allow us to relate system behavior - steady state or
temporal behavior - to specific reaction mechanisms or parameters
(e.g. allosteric interactions between metabolites and enzymes, cyclic
reaction schemes, branching points).

There are many challenges remaining in the analysis and understanding of
metabolism as a dynamical system. Recent studies found for example that
many fluxes, where measured, are lower than predicted from a enzymatic
irreversible reaction rate model (introduced in
Eq. ([\[MET:eqn:michaelis_menten\]](#MET:eqn:michaelis_menten){reference-type="ref"
reference="MET:eqn:michaelis_menten"})) [@DavidiNoor2016], and changes
in flux patterns with changing conditions cannot be explained by enzyme
levels alone [@GerosaHaverkornVanRijsewijk2015]. These findings lead to
the question on what determines/limits reaction fluxes and how reaction
fluxes are regulated besides regulation of enzyme levels. There are
several possible answers, including effects relating to allosteric
interactions between metabolites and enzymes, reaction thermodynamics,
and substrate-related effects. The experimental study and model
incorporation of these possibilities is ongoing in systems biology, with
increasing interest to include also more of the physico-chemical aspects
of the cellular environment into the study of metabolism - such as
diffusion of molecules, involvement of radical chemistry (especially
generation of oxygen radicals in respiration) and membrane potential
[@BeardQian2008; @Beard2011]. As such, we are increasingly hoping to
move from metabolic reactions studied in isolation, to cell-scale models
and physico-chemical concepts that unite cell metabolism and physiology.
Some of this emerging movement is captured in subsequent chapters of
this book.

## Recommended readings {#recommended-readings .unnumbered}

##### Enzyme kinetics and reaction models

- "Enzymes" by J. B. S. Haldane [@Haldane1965]. Historically important
  book on enzyme kinetics and enzymatic reaction models.

- "Fundamentals of Enzyme Kinetics" by A. Cornish-Bowden
  [@Cornish-Bowden2012]. General introductory book on enzymes and enzyme
  catalysis.

- "Enzyme Kinetics for Systems Biology" (2012) by H. M
  Sauro [@Sauro2012]. In addition to covering enzyme kinetics, this book
  also discusses stochastic kinetics and the kinetics of gene regulatory
  systems with an emphasis on systems biology models.

- "Structure and Mechanism in Protein Science: Guide to Enzyme Catalysis
  and Protein Folding" by A. Fersht [@Fersht1998]. General introductory
  book on enzymes and enzyme catalysis.

##### Thermodynamics and physical chemistry

- "Understanding thermodynamics" by H. C. van Ness [@Ness1983]. An
  excellent book that de-mystifies thermodynamics. It provides a
  conceptual treatise, leaving the mathematics to the side and focusing
  on what actually the thermodynamic laws mean.

- "Principles and Problems in Physical Chemistry for Biochemists"
  by N. C. Price [@PriceDwek1997]. An introductory book on
  thermodynamics, physical chemistry, and biochemistry.

##### Metabolic system dynamics

- "Energy metabolism of the cell : a theoretical treatise" by J. G.
  Reich and E. E. Sel'kov [@ReichSelkov1981]. Provides an early view of
  the importance of reaction dynamics as a 'self-regulatory' element in
  metabolism. Emphasizes the importance of cyclic reaction schemes and
  interconnections among metabolic processes.

- "Chemical Biophysics: Quantitative Analysis of Cellular Systems"
  by D. A. Beard and H. Qian [@BeardQian2008]. Provides a rare approach
  of attempting to combine - co-study the more physical aspects of cell
  physiology, including membrane potential and compartmentalization,
  with metabolism dynamics.

- "Systems Biology: An Introduction to Metabolic Control
  Analysis" (2018) by H. M Sauro [@Sauro2018]. Discusses biochemical
  network dynamics from the perspective of metabolic control analysis.

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
[]{#MET:Exerc:1 label="MET:Exerc:1"}

1.  Write the reaction scheme for an irreversible enzymatic reaction
    with two substrates. Assume both substrates bind the enzyme
    simultaneously (forming one complex $ES_1S_2$), and both products
    are released simultaneously from this complex (*i.e.* without
    intermediary $EP_1P_2$ stage).

2.  Find the rate of product production for this system.
:::

::: exercise
[]{#MET:Exerc:2 label="MET:Exerc:2"}

1.  Write the reaction scheme for a reversible enzymatic reaction with
    two substrates. Assume both substrates bind the enzyme
    simultaneously (forming one complex $ES_1S_2$), and both products
    are released/absorbed simultaneously from/into this complex (*i.e.*
    without intermediary $EP_1P_2$ stage).

2.  Find the rate of product production for this system.
:::

::: exercise
[]{#MET:Exerc:3 label="MET:Exerc:3"}

1.  Write the reaction scheme for an irreversible enzymatic reaction
    with two substrates. Assume the substrates bind sequentially
    (forming complexes $ES_1$ and $ES_1S_2$), and both products are
    released simultaneously from $ES_1S_2$ (*i.e.* without intermediary
    $EP_1P_2$ stage).

2.  Find the rate of product production for this system.
:::

::: exercise
[]{#MET:Exerc:4 label="MET:Exerc:4"}

1.  Write the reaction scheme for an irreversible enzymatic reaction
    with two substrates. Assume the substrates bind the enzyme in any
    order (forming complexes $ES_1$, $ES_2$ and $ES_1S_2$), and both
    products are released simultaneously from this $ES_1S_2$ (*i.e.*
    without intermediary $EP_1P_2$ stage).

2.  Find the rate of product production for this system. Note that
    symbolic math tools such as [Mathematica]{.smallcaps},
    [Maple]{.smallcaps} or the [SymPy]{.smallcaps} Python library will
    be helpful for this question (though not essential).
:::

[^1]: The *molar gas constant* (also known simply as the *gas constant*)
    is the molar equivalent to the Boltzmann constant, expressed in
    units of energy per temperature increment per amount of substance
    (quantified in moles rather than single particles). Its value is
    about $8.31$ $\text{J} \cdot \text{K}^{-1} \cdot \text{mol}^{-1}$.
