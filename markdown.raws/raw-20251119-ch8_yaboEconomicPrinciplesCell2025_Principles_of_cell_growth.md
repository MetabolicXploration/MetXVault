# Principles of cell growth {#SMA}

::: chapterhighlights
- A comprehensive description of fundamental growth laws in microbial
  growth, elucidating the core principles that govern biological growth
  patterns.

- A detailed exploration of the contrasts between coarse-grained and
  fine-grained modeling is presented, offering insights into the varying
  levels of detail that each approach encompasses.

- A thorough breakdown of the key assumptions in the modeling of
  metabolic systems is provided, underlining the foundational premises
  that are crucial for accurately representing these complex systems.

- The process of deriving fundamental growth laws by modeling key
  assumptions is meticulously demonstrated, enabling a clear
  understanding of how theoretical constructs translate into biological
  realities.
:::

## Introduction {#SMA:Sec:Introduction}

A key feature of living systems is that they are able to grow and
reproduce. The reproductive success in a given environment defines the
fitness of a living system. The study of the growth of bacteria and
other microorganisms is crucial for better understanding their capacity
to cause diseases in humans or for better exploiting their use in
biotechnological or environmental processes. Beyond their interest for a
variety of applications, bacteria and other microorganisms have shown
themselves ideal model systems for investigating fundamental questions
on the relation between growth, fitness and characteristics of the
environment.

One of the first to systematically and quantitatively study the growth
of bacterial cultures was Jacques Monod in the 1940s. He performed
so-called diauxic growth experiments, in which bacteria were cultured in
a medium containing two different limiting carbon sources. He showed
that the bacteria first deplete one carbon source before starting to
assimilate the second carbon source. The order in which the primary and
secondary carbon source were consumed was determined by the growth rate
they support: the preferred carbon source allows the culture to grow at
a higher rate. Further work on the molecular basis of diauxic growth led
to the discovery that cells inhibit the expression and activity of
functions for the use of secondary carbon sources when a preferred
carbon source is present, a global regulatory mechanism known as carbon
catabolite repression [@jacob1961genetic; @magasanik1961catabolite].

Monod characterized bacterial growth by means of batch culture
experiments in a well-defined growth medium allowing bacteria to reach a
state of balanced growth, where the accumulation of biomass can be
described by a single constant, the exponential growth rate. Together
with the chemostat, a device allowing continuous culture of
microorganisms at a predefined growth rate [@novick1950description],
these methods have become standard in microbial physiology. They notably
underlie the discovery of a number of so-called growth laws, relating
the growth rate to a variety of properties of the physiology of growing
bacteria. The growth laws are conserved across different organisms and a
broad range of experimental conditions. Here, we list three well-known
growth laws [@jun2018fundamental; @scott2011bacterial]:

1.  *Dependency of the growth rate on nutrient availability*
    [@monod1949growth]: In his characterization of bacterial growth,
    Monod discovered the first growth law. He observed that the growth
    rate of bacteria depends upon the nutrient concentration in the
    medium in a hyperbolic fashion
    (Fig. [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}A).

2.  *Correlation between growth rate and nutrient uptake rate*
    [@pirt1965maintenance]: In continuous cultures, the growth rate was
    shown to vary linearly with the nutrient uptake rate
    (Fig. [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}B). The slope of this linear relation
    is called the biomass yield and the offset the 'maintenance energy',
    as it is assumed to be derived from the energy spent on processes
    required to maintain the basic processes of the cell, in the absence
    of growth [@vanBodegom07].

3.  *Correlation between growth rate and cellular composition*
    [@schaechter1958dependency; @bremer2008modulation]: In 1959,
    Schaechter, Maaløe and Kjeldgaard showed that RNA, DNA and the
    number of nuclei in *Salmonella typhimurium* linearly correlate with
    the growth rate. Later, it was further shown that other
    physiological parameters, such as the mass fraction of ribosomes in
    growing populations, also linearly correlate with the growth rate
    [@bremer2008modulation]
    (Fig. [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}C). Initially, it was believed that
    the correlation between ribosomal mass fraction and growth was
    strictly positive, however, Scott et al. [@scott2010interdependence]
    showed that when growth is inhibited through translation-inhibiting
    drugs, growth rate and ribosomal mass fraction exhibit a negative
    (near-)linear relation.

<figure id="SMA:fig:GrowthLaws" data-latex-placement="t">
<p>(A) (B) (C)<br />
</p>
<div class="center">

</div>
<figcaption>Bacterial growth laws – (A) Monod growth law: growth rate
dependency on nutrient availability (data from <span class="citation"
data-cites="monod1949growth"></span>). (B) Correlation between growth
rate and nutrient uptake rate (data from <span class="citation"
data-cites="kayser2005metabolic"></span>). (C) Correlation between
growth rate and cellular composition (data from <span class="citation"
data-cites="bremer2008modulation"></span>).</figcaption>
</figure>

The conserved nature of the growth laws has led scientists to ask
whether there are fundamental principles governing bacterial growth. To
answer this question, different types of mathematical models have been
developed. One approach aims at integrating all known molecular
constituents of the cell and the reactions involving these constituents
into a big model, an *in-silico* copy, or 'digital twin', of the cell.
Such models, known as fine-grained models, can be useful to predict
emergent phenotypes, but they are difficult to construct and maintain,
and their complexity makes it hard to grasp certain principles that
underpin growth. In this chapter, we will focus on coarse-grained models
of bacterial growth. Rather than assembling individual reactions in a
bottom-up manner, these models are based on the top-down definition of a
limited number of basic cellular functions or processes involved in
growth, described by appropriate macro-reactions
(Fig. [1.2](#SMA:fig:CoarseGrainModeling){reference-type="ref"
reference="SMA:fig:CoarseGrainModeling"}). Coarse-grained models are
smaller and therefore easier to construct and analyze. The lack of
molecular detail can make their predictions less accurate, but their
simplicity allows a focus on how basic cellular functions and their
interactions shape bacterial growth.

How much detail is included in a model depends on the specific
scientific question asked, and similarly, models may vary in their
underlying assumptions. Oftentimes, assumptions are based on biochemical
principles governing intracellular reactions, on physical limitations
faced by cells, on optimality principles, or on a combination of these.

In this chapter, we show how to understand and, ultimately, how to
develop coarse-grained models of cellular growth. We present a number of
coarse-grained models with increasing levels of granularity. The models
have been chosen to also represent a variety of commonly used
assumptions, for example, based on growth rate maximization or on
phenomenological or mechanistic constraints. Despite these differences,
however, models we discuss generally recover the basic growth laws, and
we show how the latter can be derived from solving two of the simplest
coarse-grained models. The goals of this chapter are:

1.  To enable the reader to understand and analyze any model of
    microbial growth from the literature.

2.  To enable the reader to develop their own coarse-grained model of a
    metabolic system that is directed at their specific scientific
    question.

3.  To provide the reader with a new perspective on modeling of complex
    systems and specifically the biological cell.

<figure id="SMA:fig:CoarseGrainModeling" data-latex-placement="t">
<div class="center">
<p><embed src=".//images/SMA_CoarseGrainModeling.pdf" /><br />
</p>
</div>
<figcaption>Coarse-grained modeling of cellular growth – Compared to
genome-scale FBA and whole-cell models (Chapters , , , coarse-grained
models zoom out of the molecular detail and focus on key
processes.</figcaption>
</figure>

## Fundamental modeling assumptions of microbial growth {#SMA:Sec:MainAssumptionsAndConstraints}

The models of microbial growth we consider here are based on fundamental
assumptions that follow from biochemical and biophysical constraints. In
this section, we discuss and mathematically define assumptions that are
found, explicitly or implicitly, in most coarse-grained models of
microbial growth. The assumptions are formulated in an abstract manner
to hold for any self-replicating biological system, irrespective of the
specifics of the underlying molecular mechanisms. In the next section,
we use these assumptions to construct increasingly complex models of
microbial growth and show how the latter can be used to derive the
experimentally observed growth laws presented in the introduction of
this chapter.

The growth of microorganisms consists of the uptake of nutrients from
the environment and the conversion of these nutrients into new microbial
cells through a number of coupled metabolic processes
(Fig. [1.2](#SMA:fig:CoarseGrainModeling){reference-type="ref"
reference="SMA:fig:CoarseGrainModeling"}). This description brings out
the self-replicating or autocatalytic nature of microbial growth: cells
transform nutrients from the environment into new cells. In what
follows, we consider growth on the population level, that is, an
increase in the total amount of cells or, equivalently in many
situations, an increase of the biomass of the population. This leads to
the well-known model of microbial growth, where the change in biomass
over time is proportional to the amount of biomass
(Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}A): $$\begin{equation}
 \label{SMA:eq1.1}
        \frac{\intd B}{\intd t} = \lambda B,
    
\end{equation}$$ where $t$ \[h\] denotes time, $B$ in gram dry weight
\[gDW\] the biomass and $\lambda$ \[1/h\] the population growth rate.

If the growth rate is constant, the solution to
Eq. ([\[SMA:eq1.1\]](#SMA:eq1.1){reference-type="ref"
reference="SMA:eq1.1"}) describes exponential growth of the biomass:
$$\begin{equation}
 \label{SMA:eq1.2}
         B=B_0~ \expe^{\lambda t},
    
\end{equation}$$ where $B_0$ \[gDW\] is the initial biomass at $t = 0$.

The growth rate is a key parameter that is often used as a proxy for the
fitness of microorganisms. It is dependent on the metabolic processes,
that is, how a cell utilizes the nutrients to synthesize new biomass
(self-replication). The simplest description of metabolism is that it
takes up a nutrient, breaks it down into metabolites (catabolism), and
then utilizes these metabolites to produce new biomass (anabolism)
(Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}B). Catabolic and anabolic
processes comprise a variety of biochemical reactions that are carried
out by different sets of proteins and enzymes. The reaction rates of
these processes are limited biochemically and biophysically. We
formulate these limitations as modeling assumptions and define them as
mathematical constraints, four of which we briefly review below.

<figure id="SMA:fig:WModelComplexity" data-latex-placement="t!">
<p><embed src=".//images/SMA_ModelComplexity.pdf"
style="width:100.0%" /><br />
</p>
<figcaption>Coarse-grained models of metabolic systems with increasing
complexity – (A) A self-replicating system. (B) The simplest description
of a metabolic system: coupled catabolic and anabolic reactions. (C) A
metabolic system that can catabolize two different nutrient sources.
</figcaption>
</figure>

### Conservation of mass and quasi-steady-state assumption

Dry biomass is often a more readily measurable quantity than cell
volume. The latter relates absolute abundances of cell components to
their intracellular concentrations. Yet, because bacterial cells have
been observed to maintain approximately constant cell density across
various growth conditions
[@kubitschek1983buoyant; @kubitschek1984independence] (though transient
exceptions have been observed at the single-cell level
[@oldewurtel2021robust]), biomass can be regarded a proxy for volume and
is therefore assumed to be proportional to cell volume in many growth
models. All models considered in this chapter are based on the
assumption of constant cell density and approximate the concentration
$x$ of a cellular component x (we use normal font for cell components
and italic font for their concentrations) by its absolute abundance
divided by the cell mass.

According to the law of mass conservation, the change of mass is equal
to the inflow minus the outflow of mass. As a consequence, the change in
concentration of a cell component, for example a metabolite pool, is
determined by the sum of the rates of the reactions consuming and
producing this cell component
(Fig. [1.4](#SMA:fig:WModelingAssumptions){reference-type="ref"
reference="SMA:fig:WModelingAssumptions"}A). The mass balance for any
cell component x is given by the following equation: $$\begin{equation}
 \label{SMA:eq1.3}
\frac{\intd x}{\intd t}
=\sum _{\substack{y}}  r_{y \rightarrow x} \,- 
\sum_{\substack{k}} r_{x \rightarrow k},
\end{equation}$$ where $r_{y \rightarrow x}$ denotes the rate of the
reaction converting cell component y into cell component x (production
of x), and $r_{x \rightarrow k}$ the rate of the reaction converting
cell component x into cell component k (consumption of x). Typically,
cell component concentrations have units mg/gDW or mmol/gDW, so that
rates of metabolic reactions are expressed in units mg/(gDW h) or
mmol/(gDW h).

In the simple system shown in
Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}B, there are two reactions: one
converting the nutrient source N into a metabolite X and one utilizing
the metabolite for the synthesis of biomass. According to
[\[SMA:eq1.3\]](#SMA:eq1.3){reference-type="eqref"
reference="SMA:eq1.3"}, the flux balance of metabolite pool $x$ is given
by $\intd x/\intd t = r_{n \rightarrow x}-r_{x \rightarrow B}$.

A key assumption is that intracellular concentrations are in
quasi-steady state. This means that cell component pools remain
constant: $$\begin{equation}
 \label{SMA:eq1.4}
\frac{\intd x}{\intd t} = 0, \ \text{for all cell components } x.
\end{equation}$$ The quasi-steady-state assumption simplifies the
mathematical analysis of the system significantly and holds for balanced
growth of the microbial population. In this chapter, we focus mostly on
situations in which the quasi-steady-state assumption applies, but also
give an example of a model with metabolic dynamics. In metabolic
modeling, the rates of reactions at steady state are called fluxes,
denoted by the symbol $J$. With the quasi-steady-state assumption,
Eq. ([\[SMA:eq1.3\]](#SMA:eq1.3){reference-type="ref"
reference="SMA:eq1.3"}) becomes $$\begin{equation}
 \label{SMA:eq1.5}
\sum _{\substack{y}}  J_{y \rightarrow x} = \sum_{\substack{k}} J_{x \rightarrow k}
\end{equation}$$ that is, for every cell component, the sum of
production fluxes equals the sum of consumption fluxes. In the example
system, we have $J_{n \rightarrow x} = J_{x \rightarrow B}$.

### Proteome allocation assumption

The biochemical reactions breaking down nutrients into intracellular
metabolites, and the reactions utilizing these metabolites for the
synthesis of new biomass, do not occur spontaneously. The reactions are
catalyzed mostly by protein complexes, in particular metabolic enzymes
and ribosomes. In coarse-grained models, well-defined sets of
biochemical reactions are grouped together into macro-reactions. The
cell components that are necessary to catalyze the individual steps of a
macro-reaction are grouped together into a corresponding so-called
proteome sector. A proteome sector includes mostly proteins that
catalyze metabolic reactions but also ribosomes catalyzing the reaction
of protein biosynthesis. Proteins constitute most of the biomass of the
cell [@Neidhardt1996]. Therefore, as a first approximation, the sum of
the proteome sectors equals the total biomass of the growing population
measured in units of $g$
(Fig. [1.4](#SMA:fig:WModelingAssumptions){reference-type="ref"
reference="SMA:fig:WModelingAssumptions"}B): $$\begin{equation}
 \label{SMA:eq1.6}
    %\sum _{\substack{\text{%proteome}\\\text{sectors}}} P_{x \rightarrow y}=B
    \sum_{r\in \{x\rightarrow y\}} P_r = B,
\end{equation}$$ where $P_{x \rightarrow y}$ is the proteome sector
catalyzing the macro-reaction that transforms cell component x into cell
component y. The proteome sectors as defined above are extensive
quantities, summed over the entire growing population, like the total
biomass $B$. For the models, we are rather interested in intensive
quantities, the amount of a proteome sector relative to the total amount
of biomass (protein), corresponding to protein concentrations or protein
fractions. Dividing the left-hand and right-hand sides of
Eq. ([\[SMA:eq1.6\]](#SMA:eq1.6){reference-type="ref"
reference="SMA:eq1.6"}) by $B$, we thus obtain: $$\begin{equation}
 \label{SMA:eq1.7}
    \sum_{r\in \{x\rightarrow y\}} p_{r}=1
\end{equation}$$ where $p_{x \rightarrow y}$ is the fraction of the
proteome converting x into y, defined by
$p_{x \rightarrow y}=P_{x \rightarrow y} / B$. Proteome fractions are
dimensionless and sum to one.

In the simple example system in
Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}B, we distinguish two
macro-reactions: a catabolic reaction and an anabolic reaction (biomass
synthesis). We therefore define two proteome sectors, corresponding to
enzymes and ribosomes, respectively, with fractions
$p_{n \rightarrow x}$ and $p_{x \rightarrow B}$, respectively. In later
examples in the chapter, the catabolic and anabolic processes are
further broken down into smaller macro-reactions and so are the proteome
sectors.

### Mathematical description of reaction fluxes

The rate at which a reaction is converting one cell component, e.g., a
metabolite, into another is determined by the proteome fraction, the
concentrations of the substrates of the reaction and possible regulation
by other cell components in the system. While mass-action kinetics
provide a principled framework to develop rate equations for biochemical
reactions, in practice, various approximations based on mechanistic
assumptions are often used to obtain simplified equations
[@heinrich2012regulation]. Below there are a few examples of rate laws
defining the fluxes in coarse-grained models:

1.  *Excess substrate and no allosteric interactions.* The simplest
    relation of the flux $J$ to the relevant proteome sector is linear,
    such that

    $$\begin{equation}
     \label{SMA:eq1.8}
           J_{x \rightarrow y} = p_{x \rightarrow y}\, \beta_{x \rightarrow y},
         
    \end{equation}$$ where $\beta_{x \rightarrow y}$ is a parameter
    describing the efficiency of proteome sector $p_{x \rightarrow y}$
    in generating a flux from $x$ to $y$. This expression assumes
    substrate x is in excess and disregards any regulation of the flux
    by allosteric interactions of the enzymes and other cell components.

2.  *Limited substrate and allosteric interactions.* A more complex
    relation is obtained when the substrate is in excess and allosteric
    interactions involving a cell component n play a role in the
    modulation of the flux. The expression of the flux is multiplied by
    two regulatory functions $f(x)$ and $g(n)$ describing the modulation
    of the flux by the substrate and the allosteric cell component,
    respectively: $$\begin{equation}
     \label{SMA:eq1.9}
            J_{x \rightarrow y} =p_{x \rightarrow y}\, \beta_{x \rightarrow y}\, f(x)\, g(n).
        
    \end{equation}$$ It is important to note that that both $f(x)$ and
    $g(n)$ return values between $0$ and $1$, and that the flux remains
    linear in the proteome fraction. Typically, a Michaelis-Menten
    relation is taken for the effect of the concentration of substrate x
    on the flux, such that $f(x)=x/(k_{x \rightarrow y}+x)$
    (Fig. [1.4](#SMA:fig:WModelingAssumptions){reference-type="ref"
    reference="SMA:fig:WModelingAssumptions"}D). When the concentration
    $x$ is in excess, such that $x \gg k_{x \rightarrow y}$, the
    function $f(x)$ becomes approximately $1$. Other types of regulatory
    functions can be used depending on the macroreactions concerned and
    the growth conditions.

### Volume and surface area assumptions

The intracellular volume as well as the surface area of the cell are
limited (Fig. [1.4](#SMA:fig:WModelingAssumptions){reference-type="ref"
reference="SMA:fig:WModelingAssumptions"}C). Obviously, the total volume
occupied by the components of the cell, in particular proteins, cannot
be larger than the cell volume. As such, the total volume of the cell is
larger than the sum of the volume of the proteome sectors that are
functioning inside the cell plus some constant volume taken up by other
cell components such as DNA. This gives the following constraint:
$$\begin{equation}
 \label{SMA:eq1.10}
\text{Cell volume} \geq  \sum_{r\in \{x\rightarrow y\}}  p_{r} v_{r} + v_0
\end{equation}$$ where $v_{x \rightarrow y}$ is the volume of proteome
sector $p_{x \rightarrow y}$ and $v_0$ is some constant volume filled by
other cell components. Similarly, the total surface occupied by proteins
and lipids making up the cell membrane has to equal the surface area of
the cell. This constraint gives: $$\begin{equation}
 \label{SMA:eq1.11 }
 \text{Cell surface area} \geq  \sum_{r\in \{x\rightarrow y\}}  p_{r} s_{r} + l_0 
\end{equation}$$ where $s_{x \rightarrow y}$ is the surface area of
proteome sector $p_{x \rightarrow y}$ and $l_0$ is the surface area of
the lipids in the cell membrane.

<figure id="SMA:fig:WModelingAssumptions" data-latex-placement="t!">
<p><embed src=".//images/SMA_ModelingAssumptions.pdf"
style="width:100.0%" /><br />
</p>
<figcaption>Fundamental assumptions in the modeling of microbial growth
– (A) Conservation of mass and steady-state assumption: The change in
concentration of a cell component is equal to the incoming flux minus
the outgoing flux. At steady state, the concentration of the cell
component is constant. (B) Proteome allocation assumption: the proteome
is divided into different proteome sectors. The number of proteome
sectors in a model depends on the model granularity. The sum of all the
proteome sectors always equals 1. (C) Volume and surface area
assumption: The volume of the cell is limited and is filled with
intracellular cell components such as proteins. The sum of the volumes
of the intracellular cell components is equal to the cell volume.
Similarly, the surface area of the cell is limited and contains membrane
cell components such as lipids. The sum of the surface areas of membrane
cell components is equal to the cell surface area. (D) Example of flux
assumption according to Michaelis-Menten kinetics: the reaction <span
class="math inline">\(x \rightarrow y\)</span> is carried out by
proteome sector <span class="math inline">\(p_{x \rightarrow
y}\)</span>. The maximal rate is reached for saturating substrate
concentrations and is determined by the size of the proteome
sector.</figcaption>
</figure>

## Growth laws derived from basic modeling assumptions {#SMA:Sec:Exm}

In the following section, we will build upon the fundamental assumptions
discussed earlier to construct models of microbial metabolism with
increasing complexity. We will introduce additional assumptions as
necessary to solve each model, and use them to derive one of the growth
laws presented in the introduction of this chapter that have been
experimentally observed in microorganisms.

##### Example 1 - Basic metabolic system with saturating substrate concentrations

In this example, we will use the basic metabolic model to derive the
relationship between the concentration of ribosomes and the growth rate
in microorganisms. The most basic metabolic model involves the uptake of
a single nutrient from the environment, the catabolism of that nutrient
into a metabolite x, and the use of this metabolite in anabolic
processes to synthesize biomass
(Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}B). This model consists of two
reactions and two proteome sectors. According to the proteome allocation
constraint, the sum of the proteome sectors must sum to one (according
to Eq. ([\[SMA:eq1.7\]](#SMA:eq1.7){reference-type="ref"
reference="SMA:eq1.7"})):

$$\begin{equation}
 \label{SMA:eq1.12}
        p_{n \rightarrow x} + p_{x \rightarrow B} = 1.
    
\end{equation}$$

For simplicity, we assume that the rate of each reaction is proportional
to the allocation of the proteome to that reaction (according to
Eq. ([\[SMA:eq1.8\]](#SMA:eq1.8){reference-type="ref"
reference="SMA:eq1.8"})), so that: $$\begin{equation}
 \label{SMA:eq1.13}
        J_{n \rightarrow x} = p_{n \rightarrow x}\beta_{n \rightarrow x} ;\quad J_{x \rightarrow B} = p_{x \rightarrow B}\beta_{x \rightarrow B}.
    
\end{equation}$$

The mass conservation constraint, with the assumption of a steady state
for metabolite x, gives (according to
Eq. ([\[SMA:eq1.5\]](#SMA:eq1.5){reference-type="ref"
reference="SMA:eq1.5"})): $$\begin{equation}
 \label{SMA:eq1.14}
    J_{n \rightarrow x} = J_{x \rightarrow B}.
        
\end{equation}$$

Finally, due to conservation of mass, the biomass synthesis flux equals
the growth rate: $$\begin{equation}
 \label{SMA:eq1.15}
        \lambda = J_{x \rightarrow B}.
    
\end{equation}$$

Solving equations [\[SMA:eq1.12\]](#SMA:eq1.12){reference-type="eqref"
reference="SMA:eq1.12"}-[\[SMA:eq1.15\]](#SMA:eq1.15){reference-type="eqref"
reference="SMA:eq1.15"} gives a prediction for the growth rate:
$$\begin{equation}
 \label{SMA:eq1.16}
        \lambda = \frac{\beta_{x \rightarrow B}\beta_{n \rightarrow x}}{\beta_{x \rightarrow B}+\beta_{n \rightarrow x}}.
    
\end{equation}$$

Solution [\[SMA:eq1.15\]](#SMA:eq1.15){reference-type="eqref"
reference="SMA:eq1.15"} for the growth rate is based solely on
*mechanistic assumption* - that is, assumptions that are based on the
mechanistic properties of the biochemical reactions in the cell. In this
case, that is that the fluxes are linear to the relevant proteome
sector. Because we have taken a steady state approximation and the rates
of the two reactions must be equal, the growth rate is determined by the
relative values of the catalytic constants.

Using this model, we can now derive the relationship between the
concentration of ribosomes and the growth rate. Combining
Eq. [\[SMA:eq1.12\]](#SMA:eq1.12){reference-type="eqref"
reference="SMA:eq1.12"} and
[\[SMA:eq1.14\]](#SMA:eq1.14){reference-type="eqref"
reference="SMA:eq1.14"} gives: $$\begin{equation}
 \label{SMA:eq1.17}
        \lambda = p_{x \rightarrow B}\beta_{x \rightarrow B}
    
\end{equation}$$

This shows that the growth rate is linearly proportional to the anabolic
sector. Given that the anabolic sector is composed mostly of ribosomes,
this fits well with the experimentally observed linear relationship
between the concentration of ribosomes and the growth rate, which was
first described by Schaechter *et al.* [@schaechter1958dependency] and
later confirmed by Bremer *et al.* [@bremer2008modulation]. It is
important to notice that this relation is due to the assumption that the
biomass synthesis flux is linear in the ribosomal proteome sector.

In summary, we have derived the linear relationship between the
concentration of ribosomes and the growth rate using only basic
assumptions about the properties of the biochemical reactions in the
cell and the conservation of mass. This relationship is one of the
experimentally observed growth laws in microbial systems.

##### Example 2 - Growth on two nutrient sources

In this example, we consider a metabolic system that grows on two
different nutrient sources, $n_1$ and $n_2$
Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}C. We use the fundamental
assumptions outlined in Section 1.2 and an additional assumption of
growth-rate maximization to demonstrate how cells may exhibit catabolite
repression - a phenomenon in which cells utilize only one nutrient even
when multiple nutrients are available in the environment
[@magasanik1961catabolite].

The metabolic system in this example catabolizes both nutrient sources
to the same metabolite x, but at different efficiencies. The anabolic
reaction is the same as in Example 1. There are now three proteome
sectors in this model: two for catabolism of the nutrients and one for
anabolism. Thus, according to the proteome allocation constraint
(Eq. [\[SMA:eq1.7\]](#SMA:eq1.7){reference-type="ref"
reference="SMA:eq1.7"}), we have: $$\begin{equation}
 \label{SMA:eq1.18}
        p_{n_1 \rightarrow x} + p_{n_2 \rightarrow x} + p_{x \rightarrow B} = 1.
    
\end{equation}$$ As before, we assume a linear correlation between
reaction rates and proteome sector fractions (according to
Eq. ([\[SMA:eq1.8\]](#SMA:eq1.8){reference-type="ref"
reference="SMA:eq1.8"})). The different efficiencies of the catabolic
sectors is represented as $\beta_{n_2}>\beta_{n_1}$. Applying the mass
conservation assumption for metabolite x, combined with the steady state
assumption, gives $$\begin{equation}
 \label{eq1.19}
        J_{n_1 \rightarrow x} + J_{n_2 \rightarrow x} = J_{x \rightarrow B}.
    
\end{equation}$$ The growth rate is again equal to biomass synthesis
flux, as in Example 1: $$\begin{equation}
 \label{SMA:eq1.20}
        \lambda = J_{x \rightarrow B}.
    
\end{equation}$$ Given that there are more variables than constraints in
this example, solving Eqs.
[\[SMA:eq1.18\]](#SMA:eq1.18){reference-type="ref"
reference="SMA:eq1.18"} -
[\[SMA:eq1.20\]](#SMA:eq1.20){reference-type="ref"
reference="SMA:eq1.20"} reveals that there is no unique solution for the
growth rate, but rather a solution space with one free variable
$p_{n_1 \rightarrow x}$: $$\begin{equation}
 \label{SMA:eq1.21}
        \lambda = \frac{\beta_{x \rightarrow B} \beta_{n_2 \rightarrow x}}{\beta_{x \rightarrow B} + \beta_{n_2 \rightarrow x}} + p_{n_1 \rightarrow x} \left(\frac{\beta_{n_1 \rightarrow x} - \beta_{n_2 \rightarrow x}} {\beta_{x \rightarrow B} +  \beta_{n_2 \rightarrow x}} \right) \beta_{x \rightarrow B}.
    
\end{equation}$$ The solution shows that the metabolic system has a
decision to make regarding how much of the proteome to invest in sector
$p_{n_1 \rightarrow x}$. To solve this system, we introduce an
additional assumption of *growth rate maximization* -- that is, to
maximize its fitness, the metabolic system maximizes the growth rate in
a given condition. In this example, to maximize the growth rate, the
cell uses only the more efficient catabolic system, setting
$p_{n_1 \rightarrow x}=0$ and the solution for the growth rate is as in
example 1. The model predicts that the cells will only utilize the
nutrient source with the higher efficiency, even if both nutrient
sources are available in the environment. This solution fits the
catabolic repression experimental result presented in the introduction
in which in which the metabolic system represses the use of a less
efficient nutrient source in favor of a more efficient one.

##### Example 3 - Multiple energy generating pathways

In this example, we focus on a classic question in cell physiology known
as overflow metabolism [@stouthamer1975determination; @xu1999modeling].
Within the cell, two primary energy-generating pathways exist: the
oxygen-requiring respiration pathway and the oxygen-independent
fermentation pathway. It is established that, in the presence of oxygen,
the respiration pathway fully oxidizes available nutrients, rendering it
more nutrient-efficient in contrast to the fermentation pathway
[@nelson2008lehninger]. Utilization of the fermentation pathway is
marked by the secretion of byproducts, such as acetate in *E. coli* or
ethanol in yeast, making it inherently wasteful. Intriguingly,
experimental observations reveal a counterintuitive phenomenon: even
under oxygen-rich conditions, cells often opt for the less efficient
fermentation pathway. Under growth rates surpassing a critical
threshold, the secretion rate of byproducts, indicating an increased
reliance on the fermentation pathway, exhibits a linear rise
[@basan2015overflow; @vemuri2006overflow; @elsemman2022whole]. This
counterintuitive preference for fermentation has long presented a
profound question in bacterial physiology.

Based on previous studies [@basan2015overflow], we present a
coarse-grained model to elucidate this observed phenomenon
(Fig. [1.3](#SMA:fig:WModelComplexity){reference-type="ref"
reference="SMA:fig:WModelComplexity"}D). The model postulates
steady-state growth on a single nutrient source, denoted as $n$. This
nutrient is taken up from the environment, and channeled towards biomass
through the proteome sector $p_{n \rightarrow B}$. Additionally, it
serves as a precursor for energy generation, either through the
respiration pathway catalyzed by proteome sector $p_{n \rightarrow r}$
or the fermentation pathway catalyzed by proteome sector
$p_{n \rightarrow f}$. Thus, according to the proteome allocation
constraint (Eq. [\[SMA:eq1.7\]](#SMA:eq1.7){reference-type="ref"
reference="SMA:eq1.7"}), we have:

$$\begin{equation}
 \label{SMA:eq1.22}
        p_{n \rightarrow B} + p_{n \rightarrow r} + p_{n \rightarrow f} = 1.
    
\end{equation}$$

Diverging from earlier models presented in this chapter, our model
necessitates two precursors for biomass generation: energy and a carbon
precursor. Carbon assimilation is coarse-grained into the biomass
generation pathway $n \rightarrow B$, while energy is generated through
the energy-producing pathways of respiration $n \rightarrow r$ and
fermentation $n \rightarrow f$. Consequently, two mass balance equations
are requisite -- one for carbon flux and another one for energy flux.
The carbon mass balance equates the carbon uptake rate coming from
nutrient uptake $J_{in}^C$ to the carbon fluxes utilized for cell
biosynthesis $J_{n \rightarrow B}^C$, fermentation
$J_{n \rightarrow f}^C$ and respiration $J_{n \rightarrow r}^C$:

$$\begin{equation}
 \label{SMA:eq1.23}
        J_{in}^C= J_{n \rightarrow B}^C + J_{n \rightarrow f}^C + J_{n \rightarrow r}^C.
    
\end{equation}$$

Similarly, the energy balance equation asserts that the energy generated
by fermentation $J_{n \rightarrow f}^E$ and respiration
$J_{n \rightarrow r}^E$ equals the energy utilized for the biomass
synthesis reaction $J_{n \rightarrow B}^E$:

$$\begin{equation}
 \label{SMA:eq1.24}
        J_{n \rightarrow B}^E = J_{n \rightarrow f}^E + J_{n \rightarrow r}^E.
    
\end{equation}$$

Consistent with prior examples in this chapter, we maintain a linear
correlation between reaction rates and proteome sector fractions (as per
Eq. [\[SMA:eq1.8\]](#SMA:eq1.8){reference-type="ref"
reference="SMA:eq1.8"}).

Both fermentation and respiration reactions utilize a carbon substrate
and produce energy, with a key distinction lying in their nutrient
utilization efficiency. The ratio of carbon utilized in these reactions
to energy generated is expressed as:

$$\begin{equation}
 \label{SMA:eq1.25}
        J_{n \rightarrow r}^E = \epsilon_{n \rightarrow r} J_{n \rightarrow r}^C; \hspace{0.2cm}  J_{n \rightarrow f}^E = \epsilon_{n \rightarrow f} J_{n \rightarrow f}^C.
    
\end{equation}$$

Given that the respiration pathway exhibits higher nutrient efficiency
than the fermentation pathway:
$\epsilon_{n \rightarrow r} > \epsilon_{n \rightarrow f}$.

Concluding the model description, we incorporate the cellular
requirements for growth precursors (energy and carbon) and the proteome.
Under carbon limitation, the proteome fraction dedicated to cell
biosynthesis $p_{n \rightarrow B}$ exhibits a linear growth rate
dependence
[@basan2015overflow; @hui2015quantitative; @scott2010interdependence; @you2013coordination]:

$$\begin{equation}
 \label{SMA:eq1.26}
        p_{n \rightarrow B} = p_{0} + \sigma_{n \rightarrow B}\lambda.
    
\end{equation}$$

The growth rate correlates with the flux of growth precursors, adhering
to a fixed stoichiometry of the metabolic network
[@varma1994metabolic; @neidhardt1990physiology]:

$$\begin{equation}
 \label{SMA:eq1.27}
        J_{n \rightarrow B}^E=\sigma_E\lambda; \hspace{0.2cm}  J_{n \rightarrow B}^C=\sigma_C\lambda.
    
\end{equation}$$

Another key assumption of the model posits that, while the respiration
pathway is more nutrient-efficient, utilizing less nutrients per energy
unit generated, the fermentation pathway is more proteome-efficient,
requiring a smaller proteome fraction per energy unit generated. This
assumption is embodied in the efficiency parameters of the reaction
fluxes: $\beta_{n \rightarrow f} > \beta_{n \rightarrow r}$.

To validate the efficacy of our model in capturing the experimentally
observed linear increase in acetate secretion with high growth rates, we
endeavored to predict acetate secretion as a function of growth rate.
The acetate secretion rate is governed by the flux through the
fermentation pathway, represented by
$J_{ac}=S_{ac} J_{n \rightarrow f}^C$, where $S_{ac}$ is determined by
the involved stoichiometry. Solving
Eqs [\[SMA:eq1.22\]](#SMA:eq1.22){reference-type="ref"
reference="SMA:eq1.22"} -
[\[SMA:eq1.27\]](#SMA:eq1.27){reference-type="ref"
reference="SMA:eq1.27"} for acetate secretion yields an expression that
increases linearly with the growth rate:

$$\begin{equation}
 \label{SMA:eq1.28}
        J_{ac} = \frac{S_{ac}}{\epsilon_{n \rightarrow f}} \beta_E (p_E - \lambda( \sigma_{x \rightarrow B} + \frac{\sigma_E}{\beta_{x \rightarrow r}})).
    
\end{equation}$$

where
$\beta_E = \frac{\beta_{n \rightarrow r} \beta_{n \rightarrow f}}{\beta_{n \rightarrow r} - \beta_{n \rightarrow f}}$
and $p_E = 1 - p_0$. The negative value of $\beta_E$, arising from the
higher proteome efficiency of the fermentation pathway, results in a
positive slope and a negative intercept on the $J_{ac}$-axis. The model
provides a good quantitative fit to the experimental observation
[@basan2015overflow]. The critical growth rate $\lambda_{cr}$,
signifying the growth rate at which the cell activates the fermentation
pathway, occurs when $J_{ac}=0$, giving
$\lambda_{ac}= \frac{p_E}{\sigma_{n \rightarrow B} + \sigma_E/\beta_{n \rightarrow r}}$.

It is crucial to highlight the key assumption underlying this solution,
which lies in the relative efficiencies of the energy-generating
pathways. At high growth rates, the cell encounters inhibition not only
in its ability to rapidly extract energy from the nutrient but, more
significantly, it is constrained by the available proteome.
Consequently, the cell shifts to utilize the more efficient fermentation
pathway.

It is also noteworthy to identify the assumptions overlooked by the
model. For instance, the model excludes the proteome sector for nutrient
uptake, coarsely integrating it into the biomass biosynthesis and energy
generation pathways. While this assumption is reasonable for growth on a
single nutrient, a model considering multiple nutrients with varying
uptake efficiencies necessitates the inclusion of proteome sectors for
nutrient uptake. Further analysis of the model can be found in
[@basan2015overflow; @golan2023metabolic].

## Mechanistic links between cellular trade-offs, gene expression, and growth

This section presents a coarse-grained cell model that describes the
dynamic adaptation of global mechanisms driving the growth of bacterial
cells. Compared to the models previously described in this chapter, this
model is dynamic, i.e. not based on steady-state assumptions, and it has
a higher level of granularity. It is also based on explicit mechanisms,
which allows extension with additional mechanisms of interest, for
example, the effects of antibiotics or of heterologous gene expression
on cellular growth.

Energy metabolism and protein production are the main pillars of biomass
production and cell growth, and form the basis of the growth model. A
set of ordinary differential equations describes the dynamic interplay
of (i) nutrient internalization and catabolism, (ii) transcription, and
(iii) and translation (see
Fig. [1.5](#SMA:fig:WModel){reference-type="ref"
reference="SMA:fig:WModel"}). A key assumption of the model is that
biomass is dominated by proteins, and so the cellular growth rate
corresponds to the total rate of protein synthesis via translation. All
processes are part of a feedback loop in which the final protein
products act as catalyzers of the model reactions, creating a
self-replicating system.

<figure id="SMA:fig:WModel" data-latex-placement="t!">
<embed src=".//images/SMA_WModel.pdf" style="width:60.0%" />
<figcaption>Schematic of the dynamic growth model – The model focuses on
key cellular processes: nutrient uptake, transcription and translation.
Enzymes (shown in blue and dark green) import and metabolize
extracellular nutrient (shown in orange), which yields energy (yellow).
Availability of energy impacts transcription and translation, however,
it is assumed that energy consumption is dominated by translation. The
different species of mRNA compete for ribosomes (light green), and their
translation consumes energy. Assuming that biomass is dominated by
protein, the total rate of translation determines the rate of growth
(lower right). Four classes of proteins are modelled: ribosomes,
nutrient transporters, enzymes and other house-keeping proteins (red).
</figcaption>
</figure>

In its basic form, the growth model includes 14 intracellular variables:
internal nutrient, $s_i$; energy molecules, $a$; and four types of
proteins along with their corresponding free ($m_x$) and ribosome-bound
mRNAs ($c_x$). Of the four types of proteins considered, there are three
groups of catalyzing molecules: transporters ($e_t$), metabolic enzymes
($e_m$) and ribosomes ($r$), and one group of housekeeping proteins
($q$). As the model does not assume steady state, the different
reactions are defined in terms of reaction rates instead of reaction
fluxes. A simplified description of the main reaction rates of the model
is shown in Table [1.1](#SMA:tab:rates){reference-type="ref"
reference="SMA:tab:rates"}. For details on all reactions and parameters,
readers are referred to the supplementary information of
[@weisse2015mechanistic]. In what follows, the focus will be on the
conceptual aspects underlying the prediction of cellular growth rate,
and some examples of model applications.

Building on the assumptions of mass balance and proteome allocation
described in
Section [1.2](#SMA:Sec:MainAssumptionsAndConstraints){reference-type="ref"
reference="SMA:Sec:MainAssumptionsAndConstraints"} of this chapter, the
model centers around three fundamental constraints, namely $(i)$ a
finite pool of cellular energy that fuels protein biosynthesis, $(ii)$ a
finite pool of ribosomes for which mRNAs compete for translation, and
$(iii)$ a finite cell mass. As a result, the model predicts the dynamic
allocation of internal resources and its emergent impact on cellular
growth rate without the need to assume growth rate maximisation.

:::: center
::: {#SMA:tab:rates}
  Description                Reaction                                  Reaction rate
  -------------------------- ----------------------------------------- ------------------------------------------
  Nutrient internalisation   ${s \rightarrow s_i}$                     $e_t \cdot\frac{v_t s}{(K_t + s)}$
  Nutrient metabolism        ${s_i \rightarrow n_s a}$                 $e_m\cdot\frac{ v_m s_i}{(K_m + s_i)}$
  Transcription              ${\varnothing \rightarrow m_x}$           $\omega_x \cdot\frac{a}{(\theta_x + a)}$
  Ribosome binding           ${m_x + r \leftrightarrow c_x}$           $k_b\cdot m_xr$, $k_u\cdot c_x$
  Translation                ${c_x + n_x a \rightarrow x + m_x + r}$   $c_x \cdot \frac {\gamma(a)}{n_x}$

  : Summary of main model reactions and their accompanying rates. The
  four proteins represented in the model are denoted in the reactions by
  $x$, $x \in r, e_t, e_m,q$, $\gamma(a)$ is the rate of translational
  elongation, defined as $\frac{\gamma_{max} a}{K_\gamma + a}$, and
  $n_x$ is the average length of a protein molecule in amino acids. The
  parameter $n_s$ represents nutrient quality and determines the yield
  of energy per catabolized nutrient.
:::
::::

### Model definitions

##### Growth rate and biomass synthesis

Based on the assumption that biomass is dominated by protein, and other
contributions are negligible, the biomass $B$ of a cell can be
calculated by summing over the coarse-grained proteome,
$$\begin{equation}
\label{eq:biomass}
    B =  \sum_x n_x x + n_r \sum_x c_x, \qquad x\in{r,e_t,e_m,q},
\end{equation}$$ which sums over all proteins ($x$) and mRNA-bound
ribosomes ($c_x$), with $n_r$ and $n_x$ denoting the lengths of proteins
in terms of amino acids. Equation
[\[eq:biomass\]](#eq:biomass){reference-type="eqref"
reference="eq:biomass"} is equivalent to the mass balance assumption
described in section 1.2.1 of this chapter. As a consequence, the
proteome allocations, defined by $\phi_x = {x}/{B}$ for
$x\in\{e_m, e_t, r,q\}$ sum to 1, i.e. $\sum_x \phi_x = 1$.

Similar to the previous examples in this chapter (Section
[1.3](#SMA:Sec:Exm){reference-type="ref" reference="SMA:Sec:Exm"}), the
model correlates the growth rate with biomass production, which depends
on translating ribosomes and their translation elongation rate
$\gamma(a)$. Importantly, the rate of elongation depends on the energy
produced in the catabolic processes described in the model, which
dynamically couples protein synthesis with metabolism. Defining the
number of translating ribosomes $R_t=\sum_x c_x$, the change in cellular
biomass over time becomes $$\begin{equation}
    \frac{dB}{dt} = \gamma(a) R_t - \lambda B.
\end{equation}$$ The second term, $\lambda B$, accounts for dilution via
redistribution of mass to daughter cells at division. In homeostatic
conditions, that is when $B$ is in steady state and so
$\frac{dB}{dt}=0$, it then follows that $\lambda^*$ is proportional to
the rate of protein synthesis. To define growth dynamically,
$$\begin{align}
    \lambda(t) &:= \frac{\gamma(a) R_t}{B_0}, \quad B_0>0.
    \label{3} 
\end{align}$$ Setting $B_0$ to the typical biomass of a cell in
mid-exponential growth ensures that cells will have a steady-state
biomass of $B^*=B_0$.

##### Rate of translation

In actively growing bacteria, protein synthesis, and in particular
translation-associated processes, account for a major part of the energy
budget. The model assumes a simplified mechanism to derive the
dependence of the translation rates on the energy levels of the cell. It
is assumed that each elongation step of translation consumes a fixed
amount of energy
(Figure [1.6](#SMA:fig:Translation){reference-type="ref"
reference="SMA:fig:Translation"}), and further that intermediate
reactions are in quasi-steady state. It can then be shown that the net
rate of translation elongation takes the form $$\begin{align}
    \gamma(a) &= \frac{\gamma_{\max} a}{K_{\gamma}+a}.
\end{align}$$ Here, $\gamma_{\max}$ denotes the maximal rate of
translation elongation per ribosome and $K_{\gamma}$ the energy
threshold of half-maximal elongation. For any protein $x$, the rate of
its translation is then given by $$\begin{align}
    \nu_x(c_x,a) = c_x\frac{\gamma(a)}{n_x} ,
\end{align}$$ where $c_x$ denotes ribosomes bound to mRNA of type $x$
and division by $n_x$ accounts for the number of elongation steps to
take place for the production of one $p_x$.

<figure id="SMA:fig:Translation" data-latex-placement="t!">
<p><embed src=".//images/SMA_Translation.pdf"
style="width:85.0%" /><br />
</p>
<figcaption>Mechanistic derivation of the translational elongation rate
– The model assumes that each elongation step consumes a fixed amount of
energy. In a first step, energy reversibly binds the mRNA-ribosome
complex, upon which elongation takes place. Once the peptide reaches
it’s final length, the protein is released and ribosome and mRNA are
freed up. </figcaption>
</figure>

##### Rate of transcription

The model assumes that transcription is energy-dependent, but that its
consumption is negligible compared to that of translation. Analogous to
translation, under the assumption of fixed energy consumption per
elongation step, the rate of transcription takes the same shape and is
defined by $$\begin{equation}
    \omega_x(a) = \frac{\omega_x a}{\theta_x + a}, \qquad x \in {r,e_t,e_m}.
\end{equation}$$ Here, the energy threshold of half-maximal
transcription, $\theta_x$, is specific for each proteome sector $x$,
which dynamically links the proteome allocations $\phi_x$ with different
growth conditions. In particular, $\theta_r\gg \theta_x$ for $x\neq r$
ensures that the ribosomal sector increases in rich growth conditions
(cf. growth laws in Fig. [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
reference="SMA:fig:GrowthLaws"}C).

In addition, the model assumes that the transcription of household genes
is negatively auto-regulated to maintain near constant levels across
different conditions. Therefore $$\begin{equation}
    \omega_{q}(q,a)  =  \frac{w_{q} a}{\theta_q+a} \cdot \mathcal{I}(q),\qquad {with} \quad \mathcal{I}(q) :=\frac{1}{1+(q/K_q)^{h_q}},
\end{equation}$$ where $\mathcal{I}$ is the auto-inhibition function
with threshold $K_q$ and Hill-coefficient $h_q$.

### Model predictions

The model recovers the bacterial growth laws through the automodulation
of finite cellular resources in response to changing environments. It
robustly fits empirical data
(Fig. [1.7](#SMA:fig:Laws){reference-type="ref"
reference="SMA:fig:Laws"}), suggesting the growth laws are an emerging
property of the constraints integrated into the modeling approach.

<figure id="SMA:fig:Laws" data-latex-placement="t!">
<embed src=".//images/SMA_Laws.pdf" style="width:55.0%" />
<figcaption>Mechanistic cell model – Experimental data (coloured
circles) and model simulations (lines) depicting the relationship
between growth rate and cellular composition. The data describes the
ribosomal fraction of the proteome <span
class="math inline">\(\phi_r\)</span> in different growth conditions.
Each colour represents a different media composition, with increasing
drug-free growth going from red to green. The numbers within the circles
indicate the addition of the antibiotic chloramphenicol to the growth
media at a certain concentration [in <span class="math inline">\(\mu
M\)</span>]. Although this antibiotic inhibits translation, an increase
in <span class="math inline">\(\phi_r\)</span> can be observed through
all media compositions. The model fit to the experimental data
demonstrates the capacity of this model to describe two of the growth
laws. (Inset) Model simulation. Besides the composition, varying the
amount of external nutrient in the growth media increases the
steady-state growth rate up to a saturation point. This reproduces
Monod’s growth law. </figcaption>
</figure>

The model predicts a hyperbolic dependence of the growth rate on
nutrient availability as described by Monod's law
(Fig. [1.7](#SMA:fig:Laws){reference-type="ref"
reference="SMA:fig:Laws"} inset), derived using the conservation of mass
assumption and when $\phi_r\ll \phi_q$. Energy is created from the
metabolism of internalized nutrients and determines the rates of
transcription ($\omega_x(a)$) and translation ($\gamma(a)$). In the
absence of antibiotics, the latter is proportional to the growth rate of
the cell as described in Eq. [\[3\]](#3){reference-type="eqref"
reference="3"}. As the nutrient quality is increased, more energy will
be available and therefore more transcription will occur. Due to the
relationship between transcription thresholds ($\theta_r\gg \theta_x$),
the transcription of ribosomes is increased comparatively more, leading
to an increase in the ribosomal mass fraction as seen in
Fig. [1.7](#SMA:fig:Laws){reference-type="ref"
reference="SMA:fig:Laws"}.

In a fixed nutrient condition, inhibiting translation by the addition of
an antibiotic increases intracellular energy levels as fewer ribosomes
can translate. Again, with $\theta_r\gg \theta_x$, this energy increase
leads to a proportionally larger increase in transcription of ribosomal
mRNAs and so to a larger $\phi_R$. In contrast to the scenario without
antibiotics, fewer ribosomes can actively translate and therefore the
growth rate will be lower. Consequently, a negative dependence of
$\phi_R$ and growth rate arises.

### Applications of the model

Due the coarse-grained modeling of mechanisms and the use of non-steady
state dynamics, the model lends itself to modular extension for a range
of applications. For example, to reproduce the negative correlation
between growth rate and ribosome content amid translational inhibition
(Fig. [1.7](#SMA:fig:Laws){reference-type="ref"
reference="SMA:fig:Laws"}), the model was extended to account for
inhibitory actions of the antibiotic chloramphenicol on ribosomes.
Similarly, mechanisms that account for drugs with other modes of action
could also be included. Further, in [@weisse2015mechanistic], it was
shown that the model can be extended to study a number of applications:

Firstly, the model was extended to account for expression of a
heterologous gene circuit and predict constraints between heterologous
circuit expression, circuit function, and the growth of the host. This
has applications in areas such as chemical production in biotechnology,
where host-circuit interactions are not understood and where synthetic
circuits have to operate robustly in different growth conditions. In
this context, the model can serve to quantify host-circuit interactions
for a more host-aware design of synthetic gene circuits.

In another application, the model's ability to dynamically predict
growth rate emergently from intracellular mechanisms was used as a proxy
for evolutionary 'fitness' to study when gene regulation was
evolutionarily stable. This was done by augmenting the cell model with
population growth, assuming that all cells of a population are
identical, and modeling competitive interactions between a resident and
mutant strain.

Finally, in [@weisse2015mechanistic] it was shown how to use the model
to study specific mechanisms within a wider cellular context. With the
example of gene-dosage compensation, where the effects of a gene
deletion can be reduced by increasing the expression of a paralogous
gene, it was shown how and when global regulatory mechanisms caused
compensation. The example showed that the constraints underpinning the
growth laws can also cause global negative feedbacks on proteins
affecting growth.

## Concluding remarks

In this chapter, we delved into the intricate world of coarse-grained
modeling of microbial growth. We began by describing key experimental
evidence that has led to what is known as bacterial growth laws. These
laws are derived from growth measurements and are deemed to be conserved
for various organisms. We then mathematically described the fundamental
assumptions necessary to model bacterial growth. Using basic modeling
systems, we showed how to analyze such a system and derive fundamental
conclusions for bacterial growth. These models reproduce the bacterial
growth laws, providing a link between theoretical models and
experimental results. Finally, we introduced a more complex model that
includes various cell processes such as translation, transcription, and
the cellular growth process. Overall, this chapter highlights the power
of coarse-grained modeling in unraveling the complexities of microbial
growth and offers a framework for exploring a wide range of biological
questions.

While this chapter lays a foundation for research on various topics in
biology, many areas remain to be explored. For example, the effects of
changing environmental conditions such as dynamic changes in nutrient
availability, acidity, or temperature are not discussed. Furthermore,
various cellular processes such as protein degradation and membrane
assembly are not covered in the chapter. Including these processes in a
coarse-grained model could potentially lead to the discovery of other
growth laws.

In the next chapter, you will explore models that further refine the
biological cell and bridge between coarse-grained models and
genome-scale models. These models incorporate several of the assumptions
discussed here but utilize more knowledge of the metabolic network.

## Recommended readings {#recommended-readings .unnumbered}

**Growth laws in microbiology:**

- Monod, The growth of bacterial cultures, *Annual Review of
  Microbiology*, 1949 [@monod1949growth]. Classical reference for the
  quantitative modeling of microbial growth.

- Schaechter, Maaløe, and Kjeldgaard, Dependency on medium and
  temperature of cell size and chemical composition during balanced
  growth of *Salmonella typhimurium*, *Microbiology*, 1958
  [@schaechter1958dependency]. Classical article that introduced the
  growth law for ribosomes.

- Scott, Gunderson, Mateescu, Zhang, and Hwa. Interdependence of cell
  growth and gene expression: origins and consequences, *Science*, 2010
  [@scott2010interdependence]. Article that renewed interest in growth
  laws for the quantitative study of microbial physiology.

- Jun, Si, Pugatch, and Scott, Fundamental principles in bacterial
  physiology -- history, recent progress, and the future with focus on
  cell size control: a review, *Reports on Progress in Physics*, 2018
  [@jun2018fundamental]. A very complete review of growth laws in
  microbiology.

**Coarse-grained modeling of microbial growth:**

- Hinshelwood, On the chemical kinetics of autosynthetic systems,
  *Journal of the Chemical Society*, 1952 [@Hinshelwood52]. Historical
  reference for coarse-grained modeling of microbial growth.

- Kafri, Metzl-Raz, Jonas and Barkai, Rethinking cell growth models,
  *FEMS Yeast Research*, 2016 [@Kafri16]. Review of coarse-grained
  models of microbial growth.

- de Jong *et al.*, Mathematical modeling of microbes: metabolism, gene
  expression and growth, *J. R. Soc. Interface*, 2017 [@deJong17].
  Review comparing coarse-grained models of microbial growth with other
  modeling frameworks.

- Bruggeman, Planqué, Molenaar, and Teusink, Searching for principles of
  microbial physiology, *FEMS Microbiology Reviews*, 2020
  [@Bruggeman20]. Review summarizing biological insights obtained from
  coarse-grained models.

**Examples of coarse-grained models:**

- Molenaar, van Berlo, de Ridder and Teusink, Shifts in growth
  strategies reflect tradeoffs in cellular economics, *Molecular Systems
  Biology*, 2009 [@Molenaar09]. Influential article illustrating the
  explanatory capacity of coarse-grained models.

- Weiße *et al.*, Mechanistic links between cellular trade-offs, gene
  expression, and growth, *Proceedings of the National Academy of
  Sciences of the USA*, 2015 [@weisse2015mechanistic]. Article
  describing how growth laws for ribosomes can be recovered from
  coarse-grained model of microbial growth.

- Basan *et al.*, Overflow metabolism in *Escherichia coli* results from
  efficient proteome allocation, *Nature*, 2015 [@basan2015overflow].
  Article describing how proteome allocation constraints can account for
  overflow metabolism in bacteria.

- Zavřel *et al.*, Quantitative insights into the cyanobacterial cell
  economy, *eLife*, 2019 [@Zavrel19]. Example of the use of
  coarse-grained models for explaining physiological principles
  underlying growth of less-studied (photosynthetic) microorganisms.

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
A system is composed of a set of 2 linear reactions: nutrient -\>
metabolite $x_1$ -\> metabolite $x_2$ -\> biomass. Using the same
approximations as in example 1, solve for the growth rate. What would be
the solution for a system composed of $N$ reactions? Show that the least
efficient reaction determines the growth rate.
:::

::: exercise
Solve example 1 when the nutrients are not available in excess. Use
Michaelis-Menten relations for both reactions. First, derive the
concentration of metabolite $x$ as function of catabolic sector proteome
size. What is the minimal size for the catabolic sector? What happens if
the catabolic sector is smaller than that? Next, determine the proteome
allocation that maximizes the growth rate.
:::

::: exercise
Solve Example 2 when the nutrients are not available in excess. Use
Michaelis-Menten relations for the catabolic reaction. At what point
does the metabolic system switch to use the other nutrient source?
:::

::: exercise
A metabolic system is growing in an environment with one nutrient
available. The system allosterically regulates its catabolic reaction
according to the concentration of metabolite x. Assume Michaelis-Menten
kinetics for all reactions. What is the growth rate as function of
catabolic sector proteome size? This is a complex solution, don't solve
it analytically and plot a numerical solutions instead. What is the
catabolic sector proteome size that maximizes the growth rate?
:::

::: exercise
Consider the model from section 1.3, example 3. Solve the model for the
nutrient uptake rate as function of growth rate for:

1.  Growth rates above the onset of acetate secretion

2.  Growth rates below the onset of acetate secretion
:::

::: exercise
Simple coarse-grained models can generally be solved analytically.
However, for models with a higher level of granularity, like the one
presented in this section, reaching an analytical solution to the model
equations is highly complex. Computational approaches that allow
numerically solving high-dimensional systems are of great value.

1.  With the help of the provided code and following the detailed
    description of the ODE system in the SI of [@weisse2015mechanistic],
    implement and solve the system of ODEs. Using this implementation,
    reproduce Monod's law, as seen in the inset of Figure
    [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}.

2.  The nutrient composition of the growth media is the main driver of
    increasing growth rates. Simulate the model to steady state for
    different values of nutrient qualities. What model species are most
    impacted by an increase in nutrient quality?

3.  As seen in Figure [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}, the addition of a drug that
    inhibits protein synthesis results in an upregulation of the
    ribosomal fraction $\phi_R$. Reproduce Figure
    [1.1](#SMA:fig:GrowthLaws){reference-type="ref"
    reference="SMA:fig:GrowthLaws"}. How do the observed results relate
    to your answer in question 2?
:::
