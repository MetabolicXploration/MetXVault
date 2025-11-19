# The enzyme cost of metabolic fluxes {#PAT}

::: chapterhighlights
- In this chapter we discuss why certain pathway designs have been
  selected by evolution, by hypothesizing that some are more beneficial
  than others -- based on several possible criteria and optimization
  goals: minimizing the number of reactions, maximizing product yield,
  increasing reaction turnover rates, and avoiding small thermodynamic
  driving forces.

- It turns out that all these criteria are related to a single
  objective: minimizing enzyme demand per product production rate or,
  equivalently, maximizing "enzyme productivity".

- We first focus on simple unbranched pathways with predefined flux
  distributions. We discuss several feasibility and optimality problems
  where metabolite concentrations are independent variables and solve
  for the minimal enzyme demand. In this setting, we see how enzyme
  productivity can be assessed or predicted and how it depends on
  different system parameters such as kinetics, thermodynamics, and
  concentrations of enzymes and metabolites.

- We discuss the difference between growth rate and yield. We then
  illustrate it by comparing between pathway options for glycolysis.
:::

## What guides evolution to select one pathway over another? {#PAT:Sec:WhatGuidesEvolution}

In the previous chapters, we asked what flux distributions are possible
in a network, and which are most profitable for a certain task. Now we
shall ask, more specifically, what led to the choice of existing
pathways, or what makes a pathway variant favorable over another one
that exists, or may have existed, in evolution. Of course, the same
question plays also an important role in metabolic engineering, when new
pathways are added to an organism, typically with the goal of achieving
a maximal production, while imposing the smallest possible burden on the
cell.

The chemical space is vast and many options exist for the same process,
even if we consider only reactions with known enzyme mechanisms and
impose thermodynamic constraints. Hence, while evolution had a choice
between many pathway variants, only a tiny fraction of these possible
variants is actually realized in nature, and a core part of central
metabolism almost always follows the exact same design. The few
exceptions that exist actually prove the rule, such the two natural
variants of glycolysis discussed later in this chapter. How can we
understand why a certain variant is used in a certain organism or
situation? And why are many variants not used at all? Moreover, some
very successful pathways show features that might appear strange at
first glance [@BarEvenFlamholz2012]: in glycolysis, an initial
investment of ATP is required, and only later it is recovered in higher
amounts leading to a net gain. Is this just an evolutionary accident,
i.e. a case where the pathway that evolved first is the one that stuck
around although it is not necessarily better than all the alternatives?
Or, rather, evolution did manage to find the optimal solution and
therefore we should try to explain what the advantages of these
"engineered" features are?

In this chapter, we assume that it was a selection for functional
features, not chance, that determined these pathway "choices", and ask:
what guides evolution to select one pathway over another? What are the
criteria that make pathways "efficient" or "profitable" for a cell or,
alternatively, for a metabolic engineer? To compare pathways, we assume
that each pathway comes with a predefined flux distribution, and
therefore a predefined product yield, and alternative pathways (yielding
the same product) are compared at equal product production rates.

When people talk about natural ecosystems, diversity is usually the
first topic discussed. Indeed, evolution through natural selection is
almost guaranteed to create diversity where species evolve to occupy
biological niches while exploring the vast space of possible phenotypes.
Similarly, the world of biochemistry is a vast space of possible
reactions. Metabolic enzymes participate in a network of pathways that
supply cells with energy, and building blocks for biomass. Scientists
have been studying these biochemical reactions for nearly 300 years
[@GrueningRalser2021] -- so far tens of thousands such reactions have
been classified; certainly many more exist in nature. Here are a few
online databases where biochemical reaction data are collected or
predicted: [MetaNetX](https://www.metanetx.org/),
[KEGG](https://www.kegg.jp/), [MetaCyc](https://metacyc.org/),
[BiGG](http://bigg.ucsd.edu/), [ModelSEED](https://modelseed.org/),
[ATLAS of biochemistry](https://lcsb-databases.epfl.ch/pathways/atlas/).

To study the choice between pathways variants, we consider alternative
pathways leading from A to B (or having a certain net sum formula) and
their respective advantages and disadvantages. For simplicity, let us
focus on biosynthesis pathways whose main task is more or less clear:
producing a precursor molecule. Thus, the theoretical question would be:
if a cell needs to make B from A, which pathway should it use? More
specifically, how should the metabolic reactions be chosen and in what
order? What should their kinetics and how should they be regulated?

If the pathway variant found in nature is due to selection for "good
functioning", then what are the features that make existing pathway
designs successful? In short, what are criteria for "good" pathways? One
possible criterion seems to be simplicity, that is, choosing a short
route from pathway substrate and pathway product.

::: Philblock
The notion of "pathways" is common in cell biology to describe a set of
reactions, proteins, or processes that form a functional unit. However,
there is no general definition: in practice, a pathway is often just a
subregion of interest within a larger network. In metabolism, "pathways"
often lead from some important substrate to some important product, with
a simple and predefined flux distribution that consumes substrate(s),
generates product(s), and may or may not make use of co-factors.
Considering fluxes in specific pathways (instead of flux distributions
in the entire network) is often a practical choice and, importantly, a
choice that assumes that we can model, understand, manipulate, or
engineer such a pathway without strongly affecting the rest of the cell.
This has a number of benefits: (i) Instead of studying a huge network,
we can look at pathways separately; (ii) there are reasons to believe
that the flux distributions in enzyme-efficient metabolic states must be
elementary flux modes (see Chapter ). Since EFMs often entail discrete
choices between different pathways, it can make sense to study these
pathways separately (iii) once we understand the costs and benefits of
single pathways (with a single, scalable flux mode), we can apply the
same thinking to analysing flux distribution on the entire metabolic
network. Thus, in the rest of this chapter, all results about "pathways"
will also hold generally for entire networks, as long as a (scalable)
flux mode is given. Instead of comparing alternative pathways, we can
compare alternative flux modes. In the following chapter, we use this
for optimizing over the set of all possible flux modes that a given
network can support.
:::

In contrast to the huge diversity that is allowed by the catalytic
capabilities of enzymes, a few metabolic pathways are extremely
ubiquitous and exist virtually in every living cell. For example,
glycolysis is a general term for pathways that convert glucose to
pyruvate while producing ATP [@BarEvenFlamholz2012]. One variant of
glycolysis, named after Gustav Embden, Otto Fritz Meyerhof, and Karol
Parnas (or the EMP pathway for short, see Figure
[1.1](#PAT:fig:emp_vs_ed_map){reference-type="ref"
reference="PAT:fig:emp_vs_ed_map"}), was the first metabolic pathway to
be discovered by scientists [@GrueningRalser2021]. Often, the pyruvate
is reduced to lactate or ethanol, which makes the pathway redox
balanced. Therefore, it one of the most common way for producing ATP
anaerobically (i.e. without oxygen to serve as an electron acceptor).
Another common variant was discovered in 1952 by Nathan Entner and
Michael Doudoroff [@Conway1992] (ED for short). For example, *E. coli*
is capable of metabolizing glucose through both the EMP or the ED
variants, and often does so simultaneously
[@GerosaHaverkornVanRijsewijk2015].

<figure id="PAT:fig:emp_vs_ed_map" data-latex-placement="t">
<div class="center">
<embed src=".//images/PAT_EMPversusEDMap.pdf" style="width:50.0%" />
</div>
<figcaption>Two natural variants of the glycolysis pathway, named after
their discoverers: Embden-Meyerhof-Parnas (EMP) and Entner-Doudoroff
(ED) – The pathways are part of the core metabolism shown in Figure
.</figcaption>
</figure>

More generally, the overall reaction describing glycolysis is:
$$\begin{equation}
\label{PAT:eqn:glycolysis_formula}
    \ce{Glucose + 2 NAD(P)+ + n ADP + n Phosphate -> 2 Pyruvate + 2 NAD(P)H + n ATP + n H2O}
\end{equation}$$ where the value of $n$ for the EMP pathway is 2.
@NgWang2019 explored the space of all possible glycolyses (with
different values of $n$), by exhaustively enumerating all glycolytic
pathway variants. In order to generate the variants, they adapted a
computational method first introduced by @BarEvenNoor2010 for finding
alternative carbon fixation cycles -- metabolic cycles whose net
reaction converts CO$_2$ into organic compounds. You start by collecting
a database of known biochemical reactions (e.g. from a database such as
KEGG [@KanehisaFurumichi2016]) and then use a linear-programming
algorithm to identify the set of reactions with the minimal sum of
fluxes that conform to the predefined net reaction
(e.g. [\[PAT:eqn:glycolysis_formula\]](#PAT:eqn:glycolysis_formula){reference-type="ref"
reference="PAT:eqn:glycolysis_formula"}). The objective is somewhat
arbitrary, but since solving the LP requires setting an objective, we
chose the min-flux as a reasonable proxy for the simplicity of the
pathway. In any case, we will soon see how one can iterate through all
possible solutions. @NgWang2019 used this algorithm with the
stoichiometry from
[\[PAT:eqn:glycolysis_formula\]](#PAT:eqn:glycolysis_formula){reference-type="ref"
reference="PAT:eqn:glycolysis_formula"} to find all possible glycolysis
pathways comprising known enzymatic reactions (see Box
[\[PAT:box:IntegerCuts\]](#PAT:box:IntegerCuts){reference-type="ref"
reference="PAT:box:IntegerCuts"}).

::: MathDetailblock
The linear problem can be described by: $$\begin{align}
\label{PAT:eqn:pathway_search_lp}
    \begin{split}
        \text{minimize} ~~~& \sum_i \fluxi \\
        \text{subject to} ~~~ & \Stoichmatint \fluxv = 0 \\
        & \forall i ~~~ 0 \leq \fluxi \leq \beta \\
        & \flux_\text{glycolysis} = -1
    \end{split}
\end{align}$$ where $\fluxv$ is the flux variable, and $\Stoichmattot$
is comprised of the universal stoichiometric matrix , and in addition
one reaction (whose flux is denoted $\flux_\text{glycolysis}$) which has
the stoichiometry of
Eq. ([\[PAT:eqn:glycolysis_formula\]](#PAT:eqn:glycolysis_formula){reference-type="ref"
reference="PAT:eqn:glycolysis_formula"}). The constraint
$\flux_\text{glycolysis} = -1$ ensures that the sum of all active
reactions except for $\flux_\text{glycolysis}$ will together form a full
glycolysis pathway, since their net reaction has to balance the
stoichiometry of $\flux_\text{glycolysis}$ given the mass balance
constraint $\Stoichmatint \fluxv = 0$. $\beta$ given the upper bound on
the flux for all reactions. For simplicity, we assume that all fluxes
are positive and that reversible reactions are split into their two
opposing directionalities . $\beta$ is a tunable parameter that is an
upper bound on all the fluxes in the solution pathways. Setting it too
low would exclude solutions with complex stoichiometries. On the other
hand, a very high value would increase the complexity of the search and
lead to very long run-times. Typically, we choose $\beta = 10$ which is
a good balance between the two extremes. Finally, we set the objective
function ($\sum_i \fluxi$) to minimize the sum of fluxes. As we will
explain shortly, we can iterate through all possible solutions and
therefore the objective will only determine the order at which we find
them.

To find all possible glycolysis pathways comprising known enzymatic
reactions, @NgWang2019 iteratively introduced constraints in order to
exclude all previous solutions and find the next optimal one
[@PharkyaBurgard2004]: to exclude a solution, they add an *integer cut*,
which is an inequality constraint ensuring that the number of active
reactions is strictly larger than the sum over their indicator variables
(boolean variables that are equal to 1 if the reaction is active,
i.e. carries a nonzero flux). Therefore, at least one of those reactions
must be inactive in all future solutions. This is quite similar to
constrained Minimal Cut Sets (cMCS) which were introduced in Chapter as
a way of exploring the flux space.

Formally, if $\{P_0, P_1 \ldots P_m\}$ are the set of solutions already
discovered by our algorithm (where
$\forall j \, P_j \subseteq \{0, \ldots, n\}$, i.e. each solution is a
set of integers which correspond to indices of active reactions) then
the added constraints will be: $$\begin{align}
    \begin{split}
        \forall i ~~~&~~~ z_i \in \{0, 1\} \\
        \forall i ~~~&~~~ \fluxi - \beta z_i \leq 0 \\
        \forall j ~~~&~~~ \sum_{i \in P_j} z_i < \|P_j\|
    \end{split}
\end{align}$$ where $\|P_j\|$ is the length of pathway $j$ (i.e. the
number of reactions). The $z_i$ are boolean reaction indicators,
i.e. $z_i$ must be equal to 1 if a reaction is active ($\fluxi > 0$).
The final set of constrains eliminate $P_j$ and any pathway which is a
superset of $P_j$ from the solution space. Using this extra set of
constraints iteratively, each time generating the *next* pathway and
adding it to the excluded list, will eventually go through all possible
solutions (by increasing order of their sum of fluxes). It is important
to note that using integer cuts requires switching to an MILP
(Mixed-Integer Linear Program) solver, which is computationally much
more demanding and typically requires a commercial license.
:::

The objective set by the linear problem
([\[PAT:eqn:pathway_search_lp\]](#PAT:eqn:pathway_search_lp){reference-type="ref"
reference="PAT:eqn:pathway_search_lp"}) is minimizing the sum of fluxes,
which corresponds to pathways with fewer reactions and low fluxes in
each one. As discussed in , this objective is only a crude proxy for the
efficiency of a pathway, and its only purpose is to get the pathway
solutions in a relatively logical order. Although we have discussed
global enzyme constraints in previous chapters (such as molecular
crowding and proteome allocation), when comparing pathways we will focus
only on the efficiency of the pathway itself. This will allow us to
compare pathways without thinking about the rest of the cell or a
specific metabolic context. But how can one quantify the efficiency of a
pathway? The next section will be dedicated to exactly this question.

## Pathway efficiency - some notions and thoughts {#PAT:Sec:PathwayEfficiency}

For glycolysis alone, @NgWang2019 found 11,916 alternatives that produce
at least one mole of ATP per mole of glucose. These include, of course,
the EMP pathway. Although evolution can explore these options, natural
selection typically converges on one or a few efficient variants. This
does not mean that every single pathway observed in nature must be
optimal, but we generally expect cells hosting highly inefficient
pathways to eventually become extinct. @IacomettiMarx2022 tested this
experimentally by knocking out the EMP pathway from *E. coli* and
forcing the cells to use the alternatives that naturally exist in this
bacterium. In all cases, growth rates were slower than in the wild-type.

Before we discuss other examples for metabolic pathways, we need to
define what we mean by "efficiency". There are several criteria one
should consider:

- Low consumption rate of the substrate

- High generation rate of the product

- High regeneration rate or low consumption rate of the co-factor

- Small number of steps [@NoorEden2010]

- Higher thermodynamic forces
  [@FinleyBroadbelt2009; @BarEvenFlamholz2012b]

- High enzyme turnover numbers

- High enzyme saturation levels

Some of these criteria refer to the cost (or investment) of the pathway,
while others reflect the benefit (or profit) to the cell. By considering
two common scenarios -- single nutrient limitation or exponential growth
in rich media -- we can focus on two simple criteria which provide good
measures of efficiency.

When the availability of a single nutrient is limiting growth,
maximizing the molar yield (i.e. the number of moles of product
generated for each mole of the nutrient) becomes the important feature.
Yield is rather straightforward to calculate, as it is a direct outcome
of the stoichiometry of the pathway. For example, anaerobic fermentation
is often compared to respiration and deemed inefficient since it yields
two moles of ATP per glucose, instead of $\approx$`<!-- -->`{=html}30
[@Rich2003].

On the other hand, when conditions are good, such as during exponential
growth in rich media, minimizing the total number of proteins required
is often the objective which determines growth rate. . Here, we will be
using the enzyme demand (e.g. in grams of protein) per unit of flux
(typically, in mmol per hour per gram of cell dry weight). In fact, the
enzyme demand per flux, as an objective, takes into consideration both
the cost (protein) and the benefit (flux). Importantly, these two
criteria scale linearly with respect to each other: doubling the amount
of all enzymes without changing any of the metabolite concentrations
would directly double the flux in the pathway. Therefore, this measure
of efficiency is independent of the magnitude of the flux in the
pathway. But, as we will see shortly, enzyme demand is a non-linear
function, making it trickier to compute compared to other
constraint-based problems such as ones we've seen in previous chapters.

Notably, these two measures of efficiency are not only useful for
evolutionary processes, but for bioengineering as well. Obviously, the
molar yield has economical implications when, for example, producing
ethanol from sugar. However, the rate of a bioprocess is important as
well due to the costs involved, e.g. for maintaining an operational
bioreactor. One can imagine a computational model that accurately
predicts the enzyme demand per flux of a pathway. Choosing the pathways
with the lowest demand would be a good strategy for increasing the
overall rate of bioproduction [@KlamtMuller2018].

We define the enzyme demand per unit flux as the total amount of enzyme
(in grams of protein) that is required to catalyze all of the pathway
reactions at their required rates. We start by deriving a formula for
the demand of a single enzymatic reaction. Consider an enzyme-catalyzed
reaction: $$\begin{equation}
    \textrm{S} \ce{<=>} \textrm{P}
\end{equation}$$ where $s$ and $p$ will be the concentrations of the
substrate ($\textrm{S}$) and product ($\textrm{P}$) respectively, and
$E$ the concentration of the enzyme which catalyzes this reaction (for
simplicity, we drop the *tot* subscript from $E_\textrm{tot}$). Here, we
will be using the factorized rate law (Eq. ), but other kinetic rate
laws would produce similar results. The rate of a reaction is given by:
$$\begin{equation}
    \flux = \enzconc \cdot \kcatplus \cdot \frac{s/\kmS}{1 + p/\kmP + s/\kmS}\cdot \left(1 -   \expe^{\deltaG/RT}\right)
\end{equation}$$ where $\kcatplus$ is the forward turnover rate, $\kmS$
and $\kmP$ are the Michaelis-Menten constants for the $\textrm{S}$ and
product $\textrm{P}$, and $\deltaG$ is the Gibbs free energy. So, the
minimal amount of enzyme that is required for reaching a given rate
$\flux$ is: $$\begin{equation}
 q \equiv \flux \cdot h\cdot \frac{1}{\kcatplus} \cdot \frac{1 + p/\kmP + s/\kmS}{s/\kmS} \cdot \left(1 -   \expe^{\deltaG/RT}\right)^{-1},
\end{equation}$$ where $h$ is a number converting enzyme concentration
$\enzconc$ into enzyme amount $q$ (for example, the enzyme molecular
mass). For an illustration, see Figure
[1.2](#PAT:fig:efficiencies){reference-type="ref"
reference="PAT:fig:efficiencies"} . Summing up the demand across all the
reactions in the pathway (each with its own rate, kinetic parameters,
and substrate/product concentrations) will produce the total enzyme
demand. Looking at this function, we can already make some interesting
observations. First, the kinetic parameters ($\kcatplus$, $\kmP$, and
$\kmS$) can be treated as constants since they change only in
evolutionary timescales, and we often assume that existing enzymes
already have near-optimal kinetics (although that's not always the
case). Since we care about the demand *per pathway flux* one can,
without loss of generality, set $\flux$ to 1. However, if the pathway
requires a non-trivial ratio between some reactions, the value of
$\flux$ can be different based on the stoichiometry. Finally, the
thermodynamic term, i.e. $1 -   \expe^{\deltaG/RT}$ (which we will
discuss in more detail in the following section,
[1.3](#PAT:Sec:Thermodynamics){reference-type="ref"
reference="PAT:Sec:Thermodynamics"}), is a function of the metabolite
concentrations and the $\Keq$, which is another constant. So, generally
speaking, enzyme demand is defined by a set of constants that are unique
to each pathway, and variables that represent the metabolite
concentrations. Since these concentrations are subject to change
depending on the growth conditions, we often treat them as optimization
variables and try to find the minimal demand possible within certain
constraints. In Section [1.4](#PAT:Sec:Optimizing){reference-type="ref"
reference="PAT:Sec:Optimizing"}, we will see a general method for
finding the minimal value using convex optimization.

<figure id="PAT:fig:efficiencies" data-latex-placement="t!">
<div class="center">
<table>
<tbody>
<tr>
<td style="text-align: left;">(A)</td>
<td style="text-align: left;">(B)</td>
<td style="text-align: left;">(C)</td>
</tr>
</tbody>
</table>
<embed src=".//images/PAT_Efficiencies.pdf" style="width:100.0%" />
</div>
<figcaption>Enzyme cost in metabolism – (A) Enzyme-specific flux depends
on a number of physical factors. Under ideal conditions, an enzyme
molecule catalyses its reaction at a maximal rate given by the enzyme’s
forward catalytic constant (blue). The rate is reduced by microscopic
reverse fluxes (magenta) and by incomplete saturation with substrate,
causing waiting times between reaction events, or by enzyme inhibition
or incomplete activation (red). (B-C) On a logarithmic scale, catalytic
rates and enzyme demand can be split into sums of efficiency terms. With
lower catalytic rates, larger amounts of enzyme are required for
realizing the same metabolic flux.</figcaption>
</figure>

::: MathDetailblock
According to
Eq. ([\[PAT:eq:factorized\]](#PAT:eq:factorized){reference-type="ref"
reference="PAT:eq:factorized"}), reversible rate laws can be factorized
into five terms that depend on metabolite concentrations in different
ways [@NoorFlamholz2013]. For a reaction S $\rightleftharpoons$ P with
reversible Michaelis-Menten kinetics
Eq. ([\[PAT:eq:mmratelaw\]](#PAT:eq:mmratelaw){reference-type="ref"
reference="PAT:eq:mmratelaw"}), a driving force
$\drivingforce = -\deltaG / RT$, and a prefactor for non-competitive
inhibition, the rate law can be written as $$v \;=\; {\color{c1}e}
    \;\cdot\; {\color{c2}k_{\rm cat}^+}
    \;\cdot\; \underbrace{{\color{c3}[1- \mathrm{e}^{- \theta}]}}_{\etarev}
    \;\cdot\; \underbrace{{\color{c4}\frac{s/K_{\mathrm S}}{1+s/K_{\mathrm S}+p/K_{\mathrm P}}}}_{ \etakin}
    \;\cdot\; \underbrace{{\color{c4}\frac{1}{1+x/K_{\mathrm I}}}}_{\etareg}$$
with inhibitor concentration $x$. The product of the first two terms,
$E$ and $\kcatplus$, represents the maximal velocity, i.e. the rate at
full substrate-saturation without backward flux and without enzyme
inhibition. The following factors decrease this velocity for different
reasons: $\etarev$ describes a decrease due to backward fluxes,
$\etakin$ -- the decrease due to incomplete substrate saturation, and
$\etareg$ -- the decrease due to small-molecule regulation (see Figure
[1.2](#PAT:fig:efficiencies){reference-type="ref"
reference="PAT:fig:efficiencies"} b). While $\kcatplus$ is an
enzyme-specific constant (yet, dependent on conditions such as pH, ionic
strength, or molecular crowding in cells), the efficiency factors are
concentration-dependent, unitless, and can vary between 0 and 1. The
thermodynamic factor $\etarev$ depends on the driving force (and thus,
indirectly, on metabolite concentrations), and the equilibrium constant
is required for its calculation. The saturation factor $\etakin$ depends
directly on metabolite levels and contains the $\km$ values as
parameters. Enzyme regulation by small molecules yields additive or
multiplicative terms in the rate law denominator, which in our example
and can be captured by a separate factor $\etareg$. The enzyme cost for
a flux $\flux$, with an enzyme burden $h_{e}$, can be written as

$$q =
    {\color{c5}h_{e}} \cdot {\color{c1}e} =
    {\color{c5}h_{e}} \cdot v
    \cdot {\color{c2}\frac{1}{k_{\rm cat}^+}}
    \cdot \underbrace{{\color{c3}\frac{1}{[1- \mathrm{e}^{- \theta}]}}}_{1/ \etarev}
    \cdot \underbrace{{\color{c4}\frac{1+s/K_{\mathrm S}+p/K_{\mathrm P}} {s/K_{\mathrm S}} }}_{1/ \etakin}
    \cdot \underbrace{{\color{c4} [1+x/K_{\rm I}]}}_{1/ \etareg}$$

and contains the terms from the rate law in inverse form. The first
factors, $h_{e} \,v/\kcatplus$, define a minimum enzyme cost, which is
then increased by the following efficiency factors. By omitting some of
these factors, one can construct simplified enzyme cost functions with
higher specific rates, or lower enzyme demands (compare Figure
[1.2](#PAT:fig:efficiencies){reference-type="ref"
reference="PAT:fig:efficiencies"}b). For a closer approximation, the
factors may be substituted with constant numbers between $0$ and $1$.
:::

Most of the proposed criteria for good pathways have either to do with
material investments (such as substrate, cofactor, or energy demand) or
with "machine investments", that is, enzyme demands. Enzyme demands, in
turn, depend on pathway length, enzyme masses, and enzyme efficiency,
and therefore on rate laws (where $\kcat$ values, thermodynamic forces,
and metabolite concentrations come into play). In fact, many criteria
which we discussed earlier as indicators of efficiency are actually an
approximation of the enzyme demand under certain assumptions. For
example, the number of steps is proportional to the total demand if all
enzymes have exactly the same $\kcatplus$, saturation, and
thermodynamics. Therefore, it is quite a useful rule-of-thumb in case
not much else is known about the enzymes themselves. A better
approximation, denoted *Pathway Specific Activity*, was used by
[@BarEvenNoor2010] to compare CO$_2$ fixation cycles. If we assume that
all enzymes are fully saturated and irreversible, the demand would be a
direct function of the individual enzyme specific activities
(specifically, proportional to the sum of all their reciprocal values).
But even if we know nothing about the enzyme kinetic parameters,
thermodynamics alone can provide us with useful information with which
to grade pathways. Specifically, the $\Keq$ of a reaction is a universal
constant that is not affected by enzymes, but rather determined solely
by the chemical structures of the substrates and products.

In the following sections, we will focus on enzyme use efficiency as a
main objective and consider a thermodynamic approximation, relating
enzyme demands to thermodynamic forces. For linear metabolic pathways,
optimal enzyme profiles (and the associated metabolite profiles and
enzyme costs) can be computed with closed formulae. We will also discuss
a way to compute optimal enzyme profiles numerically, for networks of
any shape and size, as long as the flux mode is known.

## The role of thermodynamics {#PAT:Sec:Thermodynamics}

In general, when considering larger metabolic networks, thermodynamic
feasibility can play an important or even crucial role in determining
which pathways are used. In this section we will discuss this role more
explicitly and see how thermodynamics can still give us useful insights
about pathway efficiency even when no other kinetic data is available.

Why are thermodynamic driving forces a meaningful criterion for good
pathways? In brief, the driving forces, defined as
$\drivingforce \equiv -\deltaG/RT$, play a double role: first, they
determine whether or not a pathway flux is feasible at all, given the
metabolite concentrations at the pathway boundary (i.e. the metabolites
that form connections to the broader metabolic network); and second, in
case the pathway *is* feasible, driving forces can affect enzyme
efficiency and, consequently, the enzyme demand for a given desired
pathway flux. In Chapter , we learned that $\deltaG$, and hence the
driving force $\drivingforce$, depends on the equilibrium constant
$\Keq$ of the reaction and on the substrate and product concentrations.
We also learned that for a flux in forward direction, the driving force
must be positive. Beyond that, the efficiency of an enzyme is
proportional to
$\etarev( \drivingforce) = 1 -  \expe^{- \drivingforce}$, a function
that ranges between 0 (for $\drivingforce = 0$, reactions in
thermodynamic equilibrium) and 1 ($\drivingforce \gg 1$, reactions far
from equilibrium). Let us now see how this non-equilibrium relation
affects pathway efficiency.

### Enzyme kinetics and driving forces

We should remind ourselves some of the lessons learned in Chapter .
Specifically, recall the factorized rate law [@NoorFlamholz2013] with a
reversibility term that is an explicit function of the Gibbs energy
(Eq. ): $$\begin{align}
    \label{PAT:eqn:factorized_multi}
    \flux = \enzconc \cdot \kcatplus \cdot \frac{\prod_i s_i^{\stoich_i} / \kmS}{1 + \prod_j p_j^{\stoich_j} / \kmP + \prod_i s_i^{\stoich_i} / \kmS}\cdot (1 -   \expe^{\deltaG/RT})\,.
\end{align}$$ The enzyme mechanism behind this formula assumes fast
binding and unbinding of substrate and product, and a slow reversible
conversion step (of bound substrate into bound product). Note that here
we generalize the rate law for cases with more than one substrate and
one product, where $\stoich_i$ and $\stoich_j$ are the stoichiometric
coefficients of substrates and products, respectively[^1]. This
generalization is one out of many, and corresponds to the assumption
that all reactants bind independently to the enzyme (and at random
order). We focus on this rate law because it is one of the simplest, but
the theoretical results in this chapter apply to most other
generalizations as well (e.g. convenience kinetics
[@LiebermeisterKlipp2006]).

According to the definition of $\kcatplus$, and also by noticing that
the middle and rightmost terms in
Eq. ([\[PAT:eqn:factorized_multi\]](#PAT:eqn:factorized_multi){reference-type="ref"
reference="PAT:eqn:factorized_multi"}) are each smaller than $1$, the
rate of an enzymatic reaction is bounded by
$\flux \le \enzconc \cdot \kcatplus$ (see Mathematical Details Box
[\[PAT:box:FactorizedRateLaws\]](#PAT:box:FactorizedRateLaws){reference-type="ref"
reference="PAT:box:FactorizedRateLaws"} for a detailed explanation).
However, the additional terms are often much lower than $1$, which means
that the rate does not reach its maximum. If we try to measure the
apparent catalytic rate by dividing the rate by the enzyme abundance
($\kapp = \flux / \enzconc$) we would typically get a value that is
lower than $\kcatplus$, while only in rare "ideal" cases, $\kapp$ would
approach the $\kcatplus$. In fact, this reasoning was used by
@DavidiNoor2016 to estimate the $\kcatplus$ values of more than $100$
enzymes in *E. coli*, where they sampled many growth conditions and took
the maximum $\kapp$ as the estimate.

As discussed in Section , the factorized rate law has a thermodynamic
perspective based on the flux-force relationship, where we view the
reversibility term as a "penalty" for the fact that by lowering the
energy barrier, enzymes must catalyze reactions in both directions. When
the driving force ($\drivingforce$) is low, the reverse reaction flux
can become significant and lower the net flux. On the other hand, if the
driving force is large enough, this term can be ignored and the rate law
resembles irreversible kinetics .

So far we've seen that increasing the driving force of a single reaction
translates to a better enzyme efficiency and lower demand. If we
consider whole pathways, ones whose overall driving force is larger have
more of it to distribute among the reactions and therefore should also
have higher efficiencies overall. However, using "too much" driving
force can also have downsides. Using a larger amount of the Gibbs energy
to drive the pathway reactions means that less of that energy would go
for building biomass or currency metabolites such as ATP. An example for
this trade-off between the efficiency of single enzymes (in terms of
backward rates) and the overall pathway efficiency (in terms of ATP
yield) was demonstrated by @FlamholzNoor2013 who analyzed two versions
of the famous glycolytic pathway (see Figure
[1.1](#PAT:fig:emp_vs_ed_map){reference-type="ref"
reference="PAT:fig:emp_vs_ed_map"} below).

### Driving forces should not be too small

<figure id="PAT:fig:ThermoEfficiency" data-latex-placement="t">
<p>(A) (B)<br />
</p>
<div class="center">

</div>
<figcaption>The thermodynamic efficiency term <span
class="math inline">\(\etarev\)</span> and some approximations – (A) In
a given reaction, the thermodynamic efficiency term <span
class="math inline">\(\etarev=1-  \expe^{- \drivingforce}\)</span>
(solid line) can vary between 0 and 1 depending on the driving force
<span class="math inline">\(\drivingforce\)</span>. Small driving forces
make the enzyme inefficient, since <span class="math inline">\(\etarev
\rightarrow 0\)</span>, while for large forces, thermodynamics does not
play a role as <span class="math inline">\(\etarev \rightarrow
1\)</span>. The dashed lines show two linear approximation that hold
always as bounds, but can also be used as good approximations for small
or large <span class="math inline">\(\drivingforce\)</span> values,
respectively: <span class="math inline">\((1-  \expe^{- \drivingforce})
&lt;  \drivingforce\)</span> and <span
class="math inline">\((1-  \expe^{- \drivingforce}) &lt; 1\)</span>. (B)
The reciprocal value <span class="math inline">\(1/\etarev\)</span> is
one of the factors determining enzyme demand. The solid line shows the
thermodynamic demand factor <span
class="math inline">\(1/\etarev\)</span>, while the dashed lines show
the resulting approximations <span class="math inline">\(1/\etarev &gt;
1/ \drivingforce\)</span> and <span class="math inline">\(1/\etarev &gt;
1\)</span>, corresponding respectively to the enzyme demand
approximations <span class="math inline">\(\enzconc\ge
\frac{\flux}{\kcat  \drivingforce}\)</span> and <span
class="math inline">\(\enzconc\ge
\frac{\flux}{\kcat}\)</span>.</figcaption>
</figure>

With the factorized rate law
[\[PAT:eqn:factorized_multi\]](#PAT:eqn:factorized_multi){reference-type="ref"
reference="PAT:eqn:factorized_multi"}, we can approximate the reaction
rates by $\flux \le \enzconc \,\kcat\,(1- \expe^{- \drivingforce})$
(where we assume positive fluxes by convention). The thermodynamic
efficiency $\etarev=1- \expe^{- \drivingforce}$ plays a prominent role.
As shown in Figure [1.3](#PAT:fig:ThermoEfficiency){reference-type="ref"
reference="PAT:fig:ThermoEfficiency"}, this formula yields two important
approximations: for small forces $\drivingforce$, that is, close to
equilibrium, we obtain $\etarev\approx  \drivingforce$, while for large
forces, that is, for strongly forward-driving reactions, we obtain
$\etarev\approx 1$. In fact, both approximations also serve as upper
bounds across all $\drivingforce$ values. What does this mean? Far from
equilibrium, the thermodynamic term does not play a role and can be
ignored. Close to equilibrium, in contrast we obtain a simple
approximation for fluxes $$\begin{align}
    \flux < \enzconc \cdot \kcatplus \cdot (1 -   \expe^{- \drivingforce}) < \enzconc \cdot \kcatplus \cdot  \drivingforce
\end{align}$$ and hence for the enzyme demand $$\begin{align}
    \label{PAT:eq:EnzymeDemandApproximation1}
    \enzconc > \frac{\flux}{\kcatplus \cdot (1 -   \expe^{- \drivingforce})} > \frac{\flux}{\kcatplus \cdot  \drivingforce}\,.
\end{align}$$ As $\drivingforce$ goes to zero, the enzyme demand (for a
given desired flux) goes to infinity. We already know the reason from
Chapter : the driving force determines the ratio of forward and reverse
one-way fluxes, $\frac{\flux^{+}}{\flux^{-}}= \expe^{ \drivingforce}$.
If $\drivingforce$ comes close to zero, their relative difference
becomes very small, and in order to obtain a given net flux
$\flux=\flux^{+}-\flux^{-}$, both $\flux^{+}$ and $\flux^{-}$ must grow
enormously, which would require an a large amount of enzyme. This effect
concerns only very small $\drivingforce$ values - for $\drivingforce$
much larger than 1 (or $\deltaG$ much smaller than -RT), it can be
neglected. Therefore, redistributing driving forces between reactions,
to avoid very small forces, can save enzyme costs. The relation between
driving forces, enzyme efficiency enzyme demand is shown in more detail
in Figure [1.4](#PAT:fig:MDFschema){reference-type="ref"
reference="PAT:fig:MDFschema"}.

If small driving forces should be avoided to prevent enzyme costs from
going infinity, how can this happen in practice? The driving forces
themselves depend on metabolite levels, which can vary over several
orders of magnitude. While the true metabolite concentrations are
usually unknown, we hypothesize that selection favors concentration
profiles that prohibit very small driving forces, in order to escape the
ensuing large enzyme demands. Of course, completely avoiding small
driving forces may be impossible, as there is always a trade-off: if a
metabolite concentration decreases, the driving forces of all reactions
producing it will increase, but the driving forces of all reactions
consuming it will decrease simultaneously. So, all else being equal, the
optimal metabolite profile is one that distributes its driving forces as
evenly as possible.

<figure id="PAT:fig:MDFschema" data-latex-placement="t">
<div class="center">
<p><br />
</p>
</div>
<figcaption>Thermodynamic forces, enzyme efficiency, and enzyme demand
in a linear chain of reactions – The plot in the center represent two
possible profiles of the thermodynamic driving forces (blue and red).
The curves describe the cumulative <span
class="math inline">\(\deltaG\)</span> values: while the total <span
class="math inline">\(\deltaG\)</span> is fixed (and determined by
external metabolite concentrations), the shape of the profile can vary.
In the optimal profile (in red), small driving forces are avoided. The
driving forces determine the ratios of forward and backward one-way
fluxes (red arrows), and at a given net flux (black arrows) the enzyme
demands. In the suboptimal blue curve, in contrast, the last three
reactions show lower forces, and therefore relatively high reverse
fluxes (blue arrows); to obtain the same net flux, forward and backward
fluxes have to be strongly increased, which increases the enzyme
demand.</figcaption>
</figure>

### Max-Min driving force method

Previously in Chapter , we discussed adding thermodynamic constraints to
constraint-based models in order to comply with the second law of
thermodynamics. We can extend that approach in order to implement the
idea of avoiding small driving forces. When we talk about the
thermodynamic profile of a metabolic pathway, we usually try to
visualize it by the cumulative Gibbs energy of reaction: we start at 0
and at each step add the $\deltaG$ of the next reaction, which, assuming
the pathway is feasible, is a negative number. The profile therefore has
a shape of a downhill slope. The end point represents the total Gibbs
energy and depends only on the concentrations of the metabolites that
are part of the net reaction. Intermediate metabolites do not affect it,
but they do determine the shape of the profile itself (see Figure
[1.4](#PAT:fig:MDFschema){reference-type="ref"
reference="PAT:fig:MDFschema"}). Specifically, each intermediate
metabolite typically affects the driving force of two reactions -- the
one producing it and the one consuming it -- with opposite signs.
Therefore, changing the concentration of an intermediate can help
increase the driving force of one reaction, but always at the expense of
another reaction. This strong coupling between $\deltaG$ is why it is
not trivial to find the optimal thermodynamic profile of a pathway.

The Max-Min driving force method (MDF) [@NoorBarEven2014] is a method
for predicting metabolite concentrations, based on the principle of
evenly distributed driving forces. All fluxes are fixed and given, and
assumed to be positive. It assumes that each metabolite concentration
must remain in a predefined range, converts each choice of metabolite
concentrations into the corresponding pattern of driving forces, and
determines the *smallest* resulting driving force in the network. If
this smallest driving force is negative, the flux distribution cannot be
realized thermodynamically. Otherwise, the larger this smallest driving
force, the better the overall metabolite profile. Hence, among all
possible metabolite profiles, MDF predicts the one that maximizes the
value of the minimal driving force across the network. Mathematically,
this leads to a linear optimization problem: in the space of logarithmic
metabolite concentrations, a lower bound on all driving forces (denoted
$B$) is maximized
(Eq. [\[PAT:eqn:MDF_problem\]](#PAT:eqn:MDF_problem){reference-type="ref"
reference="PAT:eqn:MDF_problem"}). An illustrative example is shown in
Figure [1.5](#PAT:fig:toyExampleMDF){reference-type="ref"
reference="PAT:fig:toyExampleMDF"}.

$$\begin{align}
    \begin{split}\label{PAT:eqn:MDF_problem}
    \textrm{Maximize}_{\mathbf{x}, B} ~~&~~ B \\
    \textrm{Subject to} ~~&~~ -(\mathbf{\deltaGstd} + RT \cdot \Stoichmattot^\top \mathbf{x}) \geq B \\
    &\ln(\mathbf{C}_\textrm{min}) \leq \mathbf{x} \leq \ln(\mathbf{C}_\textrm{max})
    \end{split}
\end{align}$$

<figure id="PAT:fig:toyExampleMDF" data-latex-placement="t">
<p>(A)<br />
</p>
<p>  </p>
<table>
<tbody>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;">(B) <span>Driving force 1</span></td>
<td style="text-align: left;">(C) <span>Driving force 2</span></td>
<td style="text-align: left;">(D) <span>Driving force 3</span></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"><embed
src=".//images/PAT_MDFContours/example_four_chain_dr1.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_MDFContours/example_four_chain_dr2.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_MDFContours/example_four_chain_dr3.pdf"
style="width:26mm" /></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;">(E) <span>Minimal driving
force</span></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"><embed
src=".//images/PAT_MDFContours/example_four_chain_obd.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
<embed
src=".//images/PAT_MDFContours/example_four_chain_colour_legend_force.pdf"
style="width:8mm" />
<p><br />
</p>
<figcaption>Max-Min Driving force method (MDF): an optimality problem in
metabolite space – (A) Example pathway with given equilibrium constants
and fixed concentrations of the external metabolites <span
class="math inline">\(X\)</span> and <span
class="math inline">\(Y\)</span>. What are the most favorable
concentrations of the internal metabolites <span
class="math inline">\(A\)</span> and <span
class="math inline">\(B\)</span>? Assuming that small driving forces
should be avoided in all reactions, MDF determines the metabolite
profile that optimizes a worst case: it maximizes the worst (that is,
smallest) driving force among all three reactions. (B) Driving force in
reaction 1, as a function of the logarithmic concentrations of <span
class="math inline">\(A\)</span> and <span
class="math inline">\(B\)</span>, called <span class="math inline">\(\ln
a\)</span> and <span class="math inline">\(\ln b\)</span>. Higher
concentrations of <span class="math inline">\(A\)</span> (the reaction
product) lead to smaller driving forces. Above a critical value (where
<span class="math inline">\(X\)</span> and <span
class="math inline">\(A\)</span> are in equilibrium), the driving force
becomes negative, and a forward flux is impossible (gray region). The
concentration of <span class="math inline">\(B\)</span>, which does not
participate in the reaction, does not play a role. (C) Driving force for
reaction 2. Here, it is the ratio <span
class="math inline">\(b/a\)</span> that counts. The lower the ratio
(lower right), the higher the driving force. If the ratio is higher than
the equilibrium constant, the driving force becomes negative (grey
region). (C) Driving force for reaction 3. (E) By overlaying the
contours in (B), (C), and (D) and taking the minimum value, we obtain
the minimal driving force <span class="math inline">\(\drivingforce^{\rm
min}\)</span> among all three reactions. <span
class="math inline">\(\drivingforce^{\rm min}\)</span> is a piecewise
linear function of <span class="math inline">\(\ln a\)</span> and <span
class="math inline">\(\ln b\)</span> within the feasible range, yielding
positive forces in all three reactions. The maximum point of this
function is the optimum metabolite profile predicted by MDF. In the
example shown, the feasible concentration space is entirely defined by
the driving forces themselves, given the external concentrations. In
general, physiological concentration ranges for all metabolites could
further decrease the solution space and shift the optimum point (not
shown).</figcaption>
</figure>

MDF is easy to apply: it is based on a simple Linear Programming problem
and requires only the following input data: (i) the stoichiometric
network; (ii) the flux directions; (iii)) the known equilibrium
constants (or equivalently, the standard reaction Gibbs free energies);
(iv) physiological ranges for metabolite concentrations. Based on these
data alone, metabolite concentrations and driving forces (or $\deltaG$
values) are predicted. An example application can be found in
@HadickeKamp2018, where the potential of CO$_2$ fixation in *E. coli*
via endogenous pathways was analyzed using MDF.

A theoretical insight from MDF is the notion of distributed bottlenecks.
A simple bottleneck would consist of a single reaction whose driving
force cannot be increased because the substrates are at their upper
concentration bounds and the products are at their lower concentration
bounds. Given the fixed equilibrium constant, nothing can be done to
increase the driving force in this reaction. A distributed bottleneck is
more complicated: it consists of a series of reactions that all share
the same low driving force, which, because of all the concentration
constraints in the system, cannot be further increased (e.g. as in
Figure [1.4](#PAT:fig:MDFschema){reference-type="ref"
reference="PAT:fig:MDFschema"}). Even though each single reaction looks
"harmless" because its own driving force could still be increased, this
increase would happen at the expense of other driving forces.

### The role of thermodynamics for metabolic states

In summary, thermodynamics provides important clues both about the
feasibility of pathways fluxes and about their enzyme demand. To use
this knowledge, fluxes need to be considered together with metabolite
concentrations (to obtain the possible driving forces), but no detailed
knowledge of enzyme kinetics is required. Thermodynamics alone yields an
upper bound on fluxes (and hence, a lower bound on enzyme demands) that
holds for any kinetic rate laws. The only required data (except for the
metabolic network itself) are equilibrium constants (or equivalently,
standard Gibbs free energies of reactions $\deltaGstd$), which can be
obtained from the eQuilibrator tool
([equilibrator.weizmann.ac.il](https://equilibrator.weizmann.ac.il))
[@FlamholzNoor2012; @NoorBarEven2012; @BeberGollub2021] as well as
physiological bounds on metabolite concentrations. Given this
information, and given a feasible choice of metabolite concentrations,
we can compute the driving forces of all reactions, and from the
factorized rate law (and assuming positive fluxes by convention) we can
then approximate the reaction rates by
$\flux \le \enzconc \,\kcat\,(1- \expe^{- \drivingforce})$.

We also recall from Chapter that driving forces are not independent
between reactions, but depend on the metabolite concentrations, which
creates trade-offs: in a chain A $\stackrel{R_{1}}{\rightarrow}$ B
$\stackrel{R_{2}}{\rightarrow}$ C, a lower concentration of B will
increase the driving force in $R_{1}$, but decrease the driving force in
$R_{2}$. For high enzyme efficiency (low enzyme demand), all driving
forces should in principle be high, but this is most important for low
$\drivingforce$ values (while for $\drivingforce \gg$ 1 it does not even
matter). Therefore we may conclude that, to save enzyme, a cell should
rearrange its metabolite levels within physiological bounds such that
small $\drivingforce$ are avoided. Implementing this as an optimality
problem, we obtain MDF.

In conclusion, we described (i) a general rule of thumb that poor
thermodynamics makes reactions costly; (ii) simple approximations of
enzyme cost; and (iii) practical methods (MDF) to obtain metabolite
profiles with favorable thermodynamic properties.

## Enzyme cost minimization {#PAT:Sec:Optimizing}

### Enzyme cost minimization {#enzyme-cost-minimization}

The problem of minimizing the total enzyme demand (or cost) for a given
pathway can be solved numerically, thanks to the fact that they are
always convex [@NoorFlamholz2016]. Finding the minimum of the convex
objective (the total enzyme cost) in a convex set (the set of admissible
metabolite profiles, a convex polytope in log-metabolite space) can be
done efficiently. In contrast to general optimality problems, such
problems have a unique local optimum, which can be found by simple
numerical methods. In this section, we demonstrate it with a simple
example, the same three-reaction pathway that you already saw in Section
[1.3](#PAT:Sec:Thermodynamics){reference-type="ref"
reference="PAT:Sec:Thermodynamics"} above.

### Enzyme cost landscape of a metabolic pathway

Given the fluxes, kinetics, and concentration bounds in a metabolic
pathway model, one can predict the enzyme demand by assuming that cells
minimize the enzyme cost in that pathway. In the Enzyme Cost
Minimization method A reaction rate
$\flux = \enzconc \cdot \catrate(\metconcv)$ depends on enzyme level
$\enzconc$ and metabolite concentrations $\metconci$ through the
enzymatic rate law, $\catrate(\metconcv)$. If the metabolite
concentrations were known, we could directly compute enzyme demands
$\enzconc = \flux / \catrate(\metconcv)$ from fluxes, and similarly
calculate the flux-specific enzyme demand $e/v = 1/\catrate(\metconcv)$.
However, metabolite concentrations are usually unknown and vary between
experimental conditions. Therefore, there can be many solutions for
$\enzconc$ and $\metconcv$ realizing one flux distribution. To select
one of them, we employ an optimality principle: we define an enzyme cost
function (for instance, total enzyme mass) and choose the enzyme profile
with the lowest cost while restricting the metabolite levels to
physiological ranges and imposing some thermodynamic constraints. As we
shall see below, the solution is in many cases unique.

Let us demonstrate this procedure with a simple example (Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} (a)). In the pathway
$X \rightleftharpoons A \rightleftharpoons B \rightleftharpoons Y$, the
external metabolite levels \[X\] and \[Y\] are fixed and given, while
the intermediate levels \[A\] and \[B\] need to be found. As rate laws
for each of the three reactions, we use reversible Michaelis-Menten (MM)
kinetics $$\begin{equation}
    \label{PAT:eq:mmratelaw}
    \flux = \enzconc\, \frac{\kcatplus\, \sconc/\kmS - \kcatminus \, \pconc /\kmP}{1+ \sconc/\kmS+\pconc/\kmP}
\end{equation}$$ with enzyme level $\enzconc$, substrate and product
levels $\sconc$ and $\pconc$, turnover rates $\kcatplus$ and
$\kcatminus$, and Michaelis constants $\kmS$ and $\kmP$. In kinetic
modeling, steady-state concentrations would usually be obtained from
given enzyme levels and initial conditions through numerical
integration. Here, instead, we fix a desired pathway flux $\flux$ and
compute the enzyme demand as a function of metabolite concentrations:
$$\begin{equation}
    \label{PAT:eq:mmratelawdemand}
    \enzconc(\sconc,\pconc,\flux) = \flux\, \frac
    {1+ \sconc/\kmS+\pconc/\kmP}
    {\kcatplus\, \sconc/\kmS - \kcatminus \, \pconc /\kmP}.
\end{equation}$$ Figure [1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} shows how the enzyme demand in each
reaction depends on the logarithmic reactant concentrations. To obtain a
positive flux, substrate levels $\sconc$ and product levels $\pconc$
must be restricted: for instance, to allow for a positive flux in
reaction 2, the rate law numerator $\kcatplus\, [A]/\kmS -
\kcatminus \, [B] /\kmP$ must be positive. This implies that $[B]/[A]
< \Keq$ where the reaction's equilibrium constant $\Keq$ is determined
by the Haldane relationship, $\Keq = (\kcatplus / \kcatminus) \cdot
(\kmP / \kmS)$. With all model parameters set to 1, we obtain the
constraint $[B]/[A] < 1$, i.e. $\ln [B]-\ln [A]<0$, putting a straight
boundary on the feasible region (Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} (c)). Close to chemical equilibrium
($[B]/[A] \approx \Keq$), the enzyme demand $\enzconc_2$ approaches
infinity. Beyond that ratio ($[B]/[A] > \Keq$) no positive flux can be
achieved (grey region). Such a threshold exists for each reaction (see
Figure [1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} (b)-(d)). The remaining feasible
metabolite profiles form a triangle in log-concentration space, which we
call *metabolite polytope* ${\mathcal P}$ (Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} (e)), and
Eq. ([\[PAT:eq:mmratelawdemand\]](#PAT:eq:mmratelawdemand){reference-type="ref"
reference="PAT:eq:mmratelawdemand"}) yields the total enzyme demand
$\etot =
\enzconc_1+\enzconc_2+\enzconc_3$, as a function on the metabolite
polytope. The demand increases steeply towards the edges and becomes
minimal in the center. The minimum point marks the optimal metabolite
profile, and via
Eq. ([\[PAT:eq:mmratelawdemand\]](#PAT:eq:mmratelawdemand){reference-type="ref"
reference="PAT:eq:mmratelawdemand"}) we obtain the resulting optimal
enzyme profile.

<figure id="PAT:fig:ECMschema" data-latex-placement="t">
<p>(A)<br />
</p>
<p>  </p>
<table>
<tbody>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;">(B) <span>Enz. demand 1</span></td>
<td style="text-align: left;">(C) <span>Enz. demand 2</span></td>
<td style="text-align: left;">(D) <span>Enz. demand 3</span></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_u1.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_u2.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_u3.pdf"
style="width:26mm" /></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;">     <span>in total</span></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;">     <span
class="math inline">\({\kcat}_{,1}\)</span> <span>value</span></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;">     <span>on <span
class="math inline">\([A]\)</span></span></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_utot.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_utot_altered_kcat.pdf"
style="width:26mm" /></td>
<td style="text-align: left;"><embed
src=".//images/PAT_ECMContours/example_four_chain_utot_constrained.pdf"
style="width:26mm" /></td>
</tr>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
<embed
src=".//images/PAT_ECMContours/example_four_chain_colour_legend.pdf"
style="width:8mm" />
<p><br />
</p>
<figcaption> Enzyme demand in a metabolic pathway – (A) Pathway with
reversible Michaelis-Menten kinetics (equilibrium constants, catalytic
constants, and <span class="math inline">\(K_{\rm M}\)</span> values are
set to values of <span class="math inline">\(1\)</span>, <span
class="math inline">\([A]\)</span> and <span
class="math inline">\([B]\)</span> denote the variable concentrations of
intermediates <span class="math inline">\(A\)</span> and <span
class="math inline">\(B\)</span> in mM). The external metabolite
concentrations <span class="math inline">\([X]\)</span> and <span
class="math inline">\([Y]\)</span> are fixed. Plots (B)-(D) show the
enzyme demand of reactions 1, 2, and 3 at given flux <span
class="math inline">\(\flux=1\)</span> according to Eq. (<a
href="#PAT:eq:mmratelawdemand" data-reference-type="ref"
data-reference="PAT:eq:mmratelawdemand">[PAT:eq:mmratelawdemand]</a>).
Grey regions represent infeasible metabolite profiles. At the edges of
the feasible region (where <span class="math inline">\(A\)</span> and
<span class="math inline">\(B\)</span> are close to chemical
equilibrium), the thermodynamic driving force goes to zero. Since small
forces must be compensated by high enzyme levels, edges of the feasible
region are always dark blue. For example, in reaction 1 (panel (B)),
enzyme demand increases with the level of <span
class="math inline">\(A\)</span> (x-axis) and goes to infinity as the
mass-action ratio <span class="math inline">\([A]/[X]\)</span>
approaches the equilibrium constant (where the driving force vanishes).
(E) Total enzyme demand, obtained by summing all enzyme levels. The
metabolite polytope – the intersection of feasible regions for all
reactions – is a triangle, and enzyme demand is a cup-shaped function on
this triangle. The minimum point defines the optimal metabolite
concentrations and optimal enzyme levels. (F) As the <span
class="math inline">\(k_{\rm cat}\)</span> value of the first reaction
is lowered by a factor of <span class="math inline">\(5\)</span>, states
close to the triangle edge of reaction 1 become more expensive and the
optimum point is shifted away from the edge. (G) The same model with a
physiological upper bound on the concentration <span
class="math inline">\([A]\)</span>. The bound defines a new triangle
edge. Since this edge is not caused by thermodynamics, it can contain an
optimum point, in which driving forces are far from zero and enzyme
costs are kept low. Please note the resemblance to the MDF problem for
the same pathway, shown in Figure <a href="#PAT:fig:toyExampleMDF"
data-reference-type="ref"
data-reference="PAT:fig:toyExampleMDF">1.5</a>.</figcaption>
</figure>

The metabolite polytope and the large enzyme demand at its boundaries
follow directly from thermodynamics. To see this, we consider the
unitless *thermodynamic driving force* $\drivingforce = -\deltaG/RT$
[@BeardQian2007] derived from the reaction Gibbs free energy $\deltaG$.
The thermodynamic force can be written as $\drivingforce
= \ln \frac{\Keq}{[B]/[A]}$, i.e. the driving force is positive whenever
$[B]/[A]$ is smaller than $\Keq$, and it vanishes if $[B]/[A]
= \Keq$. How is this force related to enzyme cost? A reaction's net flux
is given by the difference $\flux=\flux^{+} - \flux^{-}$ of forward and
backward fluxes, and the ratio $\flux^{+}/\flux^{-}$ depends on the
driving force as $\flux^{+}/\flux^{-} =  \expe^{\drivingforce}$. Thus,
only a fraction $v/\flux^{+}
= 1-  \expe^{- \drivingforce}$ of the forward flux acts as a net flux,
while the remaining forward flux is partially canceled by the backward
flux. Close to chemical equilibrium, where the mass-action ratio
$[B]/[A]$ approaches the equilibrium constant $\Keq$, the driving force
goes to zero, the reaction's backward flux increases, and the flux per
enzyme level drops. This is what happens at the triangle edges in Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"}: a reaction approaches chemical
equilibrium, the driving force $\drivingforce$ goes to zero, and large
enzyme amounts are needed for compensation. Exactly on the edge, the
driving force vanishes and no enzyme level, no matter how large, can
support a positive flux. The quantitative cost depends on model
parameters: for example, by lowering a $\kcat$ value, the increase in
enzyme cost at the boundary becomes steeper and the optimum point is
shifted away from the boundary (see Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"} (f)).

### Enzyme cost as a function of metabolite concentrations

The prediction of optimal metabolite and enzyme levels can be extended
to models with general rate laws and complex network structures. In
general, enzyme demand depends not only on driving forces and $\kcat$
values, but also on the kinetic rate law, which includes $\km$ values
and small-molecule regulation. We can conveniently model or approximate
these factors by using factorized rate laws. Let us write this rate laws
here again in a general form to see the different factors at play. As we
learned in Section
[1.2](#PAT:Sec:PathwayEfficiency){reference-type="ref"
reference="PAT:Sec:PathwayEfficiency"}, the rate of a reaction depends
on enzyme level $\enzconc$, forward catalytic constant $\kcatplus$
(i.e. the maximal possible forward rate per unit of enzyme, in
s$^{-1}$), driving force (i.e. the ratio of forward and backward
fluxes), and on kinetic effects such as substrate saturation or
small-molecule regulation. If all active fluxes are positive, reversible
rate laws like the Michaelis-Menten kinetics in
Eq. ([\[PAT:eq:mmratelaw\]](#PAT:eq:mmratelaw){reference-type="ref"
reference="PAT:eq:mmratelaw"}) can be factorized as [@NoorFlamholz2013]:
$$\begin{equation}
    \label{PAT:eq:factorized}
    \flux = \enzconc \cdot \kcatplus \cdot  \etarev \cdot  \etakin \cdot  \etareg.
\end{equation}$$ Negative fluxes, which would complicate our formulae,
can be avoided by orienting the reactions in the direction of fluxes.

Enzyme demand can be quantified as a concentration (e.g. enzyme
molecules per volume) or mass concentration (where enzyme molecules are
weighted by their molecular weights). If rate laws, fluxes, and
metabolite concentrations are known, the enzyme demand of a single
reaction $l$ follows from
Eq. ([\[PAT:eq:factorized\]](#PAT:eq:factorized){reference-type="ref"
reference="PAT:eq:factorized"}) as $$\begin{equation}
    \label{PAT:eq:factorizedU}
    \enzconc_l(\metconcv,\flux_l) = \flux_l \cdot \frac{1}{\kcatplusl} \cdot
    \frac{1}{ \etarev_l( \drivingforce(\metconcv))}
    \cdot \frac{1}{\etakin_l(\metconcv)} \cdot \frac{1}{\etareg_l(\metconcv)}.
\end{equation}$$ To determine the enzyme demand of an entire pathway, we
sum over all reactions: $\enzPW = \sum_l \enzconc_l$. Based on its
enzyme demands $\enzconc_l$, we can associate each metabolic flux with
an enzyme cost $q = \sum_l h_{\enzconc_l}\,\enzconc_l$, describing the
effort of maintaining the enzymes. The burdens $h_{\enzconc_l}$ of
different enzymes represent, e.g. differences in molecular mass,
post-translational modifications, enzyme maintenance, overhead costs for
ribosomes, as well as effects of misfolding and non-specific catalysis.
The enzyme burdens $h_{\enzconc_l}$ can be chosen heuristically, for
instance, depending on enzyme sizes, amino acid composition, and
lifetimes. Setting $h_{\enzconc_l}=m_l$ (protein mass in grams per
mole), $q$ will be in gram protein per gram cell dry weight. Considering
the specific amino acid composition of enzymes, we can also assign
specific costs to the different amino acids. Alternatively, an empirical
cost per protein amount can be established by the level of growth
impairment that an artificial induction of protein would cause
[@DekelAlon2005; @ShachraiZaslaver2010]. Thus, each reaction flux
$\flux_l$ is associated with an enzyme cost $q_{l}$, which can be
written as a function
$q_{l}(\flux_l,\metconcv) \equiv h_{\enzconc_l}\,\enzconc_l(\metconcv, \flux_l)$
of flux and metabolite concentrations. From now on, we refer to
log-scale metabolite concentrations $s_i = \ln \metconci$ to obtain
simple optimality problems below. From the factorized rate law
Eq. ([\[PAT:eq:factorizedU\]](#PAT:eq:factorizedU){reference-type="ref"
reference="PAT:eq:factorizedU"}), we obtain the enzyme cost function
$$\begin{equation}
    \label{PAT:eq:TotalEnzymeDemand}
    q(\sconcv, \fluxv) \equiv  \sum_{l} h_{\enzconc_l}\,\enzconc_l(\flux_l,\sconcv)
    = \sum_{l}
    h_{\enzconc_l}  \cdot \flux_l \cdot \frac{1}{\kcatplusl} \cdot
    \frac{1}{ \etarev_l(\sconcv)}
    \cdot \frac{1}{\eta_l^\mathrm{sat}(\sconcv)}
    \cdot \frac{1}{ \etareg(\sconcv)}
\end{equation}$$ for a given pathway flux $\fluxv$. If the fluxes are
fixed and given, our enzyme cost becomes, at least formally, a function
of the metabolite levels. The cost function is defined on the metabolite
polytope ${\mathcal P}$, a convex polytope in log-concentration space
containing the feasible metabolite profiles. Like the triangle in Figure
[1.6](#PAT:fig:ECMschema){reference-type="ref"
reference="PAT:fig:ECMschema"}, the polytope is defined by physiological
and thermodynamic constraints.

Beyond minimizing the total enzyme cost, one can also use Enzyme Cost
Minimization to analyze the individual enzyme demands. When the
metabolite levels are known, the demand can be directly calculated and
each efficiency factor ($\eta$) in
Eq. ([\[PAT:eq:TotalEnzymeDemand\]](#PAT:eq:TotalEnzymeDemand){reference-type="ref"
reference="PAT:eq:TotalEnzymeDemand"}). By omitting some factors or
replacing them by constant numbers $0<\eta\le 1$, simplified enzyme cost
functions with fewer parameters can be obtained. For example,
$\etarev = 1$ would imply an infinite driving force
$\drivingforce \rightarrow \infty$ and a vanishing backward flux,
$\eta^{\rm sat} = 1$ implies full substrate saturation, and
$\eta^{\rm reg} = 1$ implies full enzyme activation and no enzyme
inhibition (or no small-molecule regulation at all). In these limiting
cases, enzyme activity will not be reduced, and enzyme demand will be
given by the capacity-based estimate $v/\kcatplus$, a lower estimate of
the actual demand. Instead of omitting an efficiency factor, it can also
be set to a constant value between 0 and 1. Such simplifications and the
resulting enzyme cost functions with fewer parameters can be practical
if kinetic constants are unknown.

### General lessons from Enzyme Cost Minimization

Enzyme cost minimization not only provides numerical solutions, but also
some general insights.

1.  **Convexity** Enzyme Cost Minimization shows again the importance of
    the metabolite polytope. The usage of logarithmic metabolite
    concentrations not only leads to a good search space for feasible
    metabolite profiles (as in MDF), but also facilitates optimization
    because enzyme cost is a convex function of the metabolite
    log-concentrations [@LiebermeisterNoor2015]. Convexity makes this
    optimization tractable and scalable -- unlike a direct optimization
    in enzyme space. Convexity holds for a wide range of rate laws and
    for extended versions of the problem, e.g. including bounds on the
    sum of (non-logarithmic) metabolite concentrations or bounds on
    weighted sums of enzyme fractions.\

2.  **Factorized rate laws disentangle individual enzyme cost effects**
    To see how metabolic states are shaped by different physical
    factors, we considered factorized rate laws. The different terms in
    these functions represent specific physical factors and require
    different kinetic and thermodynamic data for their calculation. By
    neglecting some terms, one obtains different approximations of the
    true enzyme cost. By comparing the different scores, we can estimate
    the enzyme cost that cells "pay" for running reactions at small
    driving forces (to save Gibbs free energy) or for keeping enzymes
    beneath substrate-saturation (e.g., to dampen fluctuations in
    metabolite levels ).\

3.  **Relationship to other optimality approaches** Beyond their
    practical advantages, factorized enzyme cost functions also allow us
    to easily compare our method to earlier modeling and optimization
    approaches. These approaches typically focused on only one or two of
    the factors that are taken into account in Enzyme Cost Minimization,
    and many of them can be reformulated as approximations of this
    method
    [@NoorBarEven2014; @HatzimanikatisLi2005; @FinleyBroadbelt2009].\

4.  **Enzyme cost is related to thermodynamics** In FBA, thermodynamic
    constraints and flux costs appear as completely unrelated aspects of
    metabolism (as is explained in Chapter ). Thermodynamics is used to
    restrict flux directions, and to relate them to metabolite bounds,
    while flux costs are used to suppress unnecessary fluxes. In Enzyme
    Cost Minimization, thermodynamics and flux cost appear as two sides
    of the same coin. Like in FBA, flux profiles are thermodynamically
    *feasible* if they lead to a non-empty metabolite polytope, allowing
    for positive forces in all reactions. However, the values of these
    forces also play a role in shaping the enzyme cost function on that
    polytope. Together, metabolite polytope and enzyme cost function (as
    in Figure [1.6](#PAT:fig:ECMschema){reference-type="ref"
    reference="PAT:fig:ECMschema"}) summarize all relevant information
    about flux cost.

Many pathways are regulated, for instance by feedback inhibition of
enzymes via the end product. While this may stabilise the dynamics and
adapt it to current demands, such enzyme regulation comes at a cost,
which we can estimate by following the logic of Enzyme Cost
Minimization. Many enzymes are regulated by small molecules that act as
competitive or allosteric inhibitors [@ReznikChristodoulou2017], an
effective way to implement feedback control, for example to adapt the
flux in biosynthesis pathways to current needs. In order for such a
regulation to work, the enzyme needs to be partially inhibited on
average (because only then, its activity can be increased on demand, by
alleviating the inhibition). Therefore, the enzyme efficiency goes down,
and the cell needs to provide more enzyme to catalyze the same flux than
without the inhibition.

How much will this regulation cost the cell as part of the enzyme
budget? From the perspective of Enzyme Cost Minimization, where we start
from desired fluxes and compute the enzyme demand, this question is easy
to answer: in the inhibited enzyme case, the lower efficiency will be
described by a factor $\etareg \in [0,1]$ (Mathematical Details Box
[\[PAT:box:FactorizedRateLaws\]](#PAT:box:FactorizedRateLaws){reference-type="ref"
reference="PAT:box:FactorizedRateLaws"}). In the same reaction, the
enzyme demand increases by a factor $1/ \etareg$, so the extra cost is
simply $1/ \etareg-1$ times the "baseline" cost of this enzyme (without
inhibition). Specifically, a non-competitive inhibitor, with efficiency
factor $\etareg = \frac{1}{1~+~c/K_{I}}$ yields a cost factor
$1+c/K_{I}$. If the metabolite concentrations are fixed, this
corresponds to an extra enzyme demand
$\Delta \enzconc_l = \frac{\enzconc_l\,c_{i}}{K_{I,li}}$. Similarly, an
enzyme activation with efficiency factor
$\etareg = \frac{c/K_{A}}{1+c/K_{A}}$ in the rate laws yields a cost
factor $\frac{1 + c/K_{A}}{c/K_{A}} = 1 + K_{A}/c$ in the formulae for
enzyme demands. If the metabolite concentrations are fixed, this
corresponds to an extra enzyme demand
$\Delta \enzconc_l = \frac{\enzconc_l\,K_{A,li}}{c_{i}}$ (where $l$ and
$i$ denote the regulated reaction and the regulating metabolite,
respectively). As usually in Enzyme Cost Minimization, an optimal
rearrangement of enzyme and metabolite concentrations must be taken into
account, which will then slightly reduce the overall cost.

The predictions of optimal states by Enzyme Cost Minimization rely on
two main inputs: a metabolic model that relates metabolite
concentrations, enzyme levels, and fluxes, and an optimality principle
based on the assumption that cells realize their production fluxes at a
minimal total enzyme cost. To test whether this optimality principle
holds at all, @NoorFlamholz2016 compared the predictions from Enzyme
Cost Minimization to predictions from the same metabolic model and the
same flux distribution, but with randomly sampled metabolite profiles
(and the corresponding enzyme profiles). In comparison, metabolite
profiles sampled close to the Enzyme Cost Minimization optimum yielded
significantly better enzyme level predictions than metabolite profiles
sampled more broadly. This strongly supports the idea that *E. coli*
metabolism, in the conditions studied, is at least partially optimized
for low enzyme cost, and thus supports cost-optimality as a principle in
living cells.

## Comparison of alternative pathways {#PAT:Sec:Alternatives}

Having clarified our main functional criteria for pathways (substrate
productivity and enzyme productivity) and how they depend on pathway
details (including outer concentrations), we can now compare alternative
pathways by their substrate and enzyme demand per production flux (an
example of "cost per benefit") and see which one scores better.

### A tale of two glycolyses

One of the canonical examples discussed throughout this book is how
cells choose between respiration and fermentation for making their ATP.
However, having a precise kinetic model for respiration is difficult,
since it involves electron transfer and membrane-bound reactions.
Therefore, it is challenging to calculate the enzyme cost of respiration
using models like those discussed in this chapter. @FlamholzNoor2013
analyzed a similar but simpler case by comparing between the EMP and ED
variants of glycolysis, since all the required enzymes are soluble and
expressed in the cytoplasm and/or the periplasm and many of their
kinetic parameters are measured. The common description of glycolysis
ends in pyruvate (e.g., as depicted in Figure
[1.1](#PAT:fig:emp_vs_ed_map){reference-type="ref"
reference="PAT:fig:emp_vs_ed_map"}). This means that the pathway is not
neutral in terms of redox, since the oxidation state of pyruvate is
higher than glucose. In order to simplify the comparison and focus only
on ATP yield (rather than NADH), the EMP and ED pathways were extended
to end in lactate by including lactate dehydrogenase (*ldh*) as an extra
step, making them redox neutral. These could be thought of as the more
relevant versions of the pathways in anaerobic conditions.

Although EMP-based fermentation is usually described in textbooks as
less efficient than respiration, since it produces only 2 moles of ATP
per mole glucose instead of $\approx30$, the ED pathway has an even
lower yield -- 1 mole of ATP. Nevertheless, the ED pathway is quite
common among the bacteria. For example, *Zymomonas mobilis* -- the
bacterium used in fermenting pulque (a.k.a., agave wine
[@RogersSkotnicki1982]) and a promising platform for bio-production
[@BehrendtFrohwitter2022] -- lacks key enzymes from the EMP pathway and
uses the ED pathway exclusively to metabolize sugars. These bacteria
don't seem to be bothered by the low ATP yield and can achieve high
growth rates [@FuhrerFischer2005]. This already suggests to us that the
ED pathway is probably superior to EMP in other aspects, such as the
enzyme demand. Another clue was provided by a study which found that the
ED pathway improves *E. coli* growth during glucose up-shifts and that
the flux through it increases by 130% [@LawNurwono2022] (see Economic
Analogy Box
[\[PAT:eco:dynamic_response\]](#PAT:eco:dynamic_response){reference-type="ref"
reference="PAT:eco:dynamic_response"})

To see if indeed the models provide predictions that are consistent with
the experimental evidence, @FlamholzNoor2013 first used the MDF method
to compare the two pathways. The ED pathway was found to be
substantially more thermodynamically favorable, with a much higher score
than the EMP pathway (8.0 versus 4.8 kJ/mol, see Figure
[1.7](#PAT:fig:emp_vs_ed_mdf){reference-type="ref"
reference="PAT:fig:emp_vs_ed_mdf"}).

<figure id="PAT:fig:emp_vs_ed_mdf" data-latex-placement="t">
<p>(A) (B)<br />
</p>
<figcaption> Comparing two metabolic pathways using the Max-min Driving
Force (MDF) method. The light blue line represents the cumulative Gibbs
free energy along the pathway if all metabolite concentrations were 1
mM. The MDF solution is presented as a gray line, where the bottleneck
reactions are highlighted in red. </figcaption>
</figure>

<figure id="PAT:fig:emp_vs_ed_ecm" data-latex-placement="t">
<p>(A) (B)<br />
</p>
<figcaption> Comparing two metabolic pathways using the Enzyme Cost
Minimization (ECM) method. We used the same kinetic parameters for all
enzymes in both pathways (<span class="math inline">\(\kcatplus\)</span>
= 200 s<span class="math inline">\(^{-1}\)</span>, <span
class="math inline">\(\km\)</span> = 200 <span
class="math inline">\(\upmu\)</span>M, same as in <span class="citation"
data-cites="FlamholzNoor2013"></span>). However, here we used an updated
version of Enzyme Cost Minimization with the factorized rate law,
therefore the results are not identical. A Jupyter notebook for
generating the figure can be found on the <a
href="https://gitlab.com/principlescellphysiology/book-economic-principles-in-cell-biology/-/blob/master/book-manuscript/latex/chapters/PAT/jupyter/plot_figures.ipynb">book
website</a>. </figcaption>
</figure>

Although the EMP pathway is clearly more favorable, we can still argue
that an MDF of 4.8 kJ/mol is good enough, as it means
$\drivingforce > 1.9$ for each one of the pathway reactions. In this
case, $\etarev > 0.85$ (see Figure
[1.3](#PAT:fig:ThermoEfficiency){reference-type="ref"
reference="PAT:fig:ThermoEfficiency"}) and therefore it might be a small
price to pay for double the ATP yield. But, as discussed earlier, the
efficiency of a pathway is affected by other factors besides the
thermodynamics. @FlamholzNoor2013 tried to see whether ED is superior to
EMP also in terms of the enzyme cost using the Enzyme Cost Minimization
method. Indeed, they found that the ED pathway would require
$\approx$`<!-- -->`{=html}5 times less protein compared to EMP for
catalyzing the same flux (see Figure
[1.8](#PAT:fig:emp_vs_ed_ecm){reference-type="ref"
reference="PAT:fig:emp_vs_ed_ecm"}). So, although the ATP yield of the
ED pathways is half that of EMP, one can still generate ATP at a higher
rate using the same amount of protein, according to the model.

The comparison of EMP and ED provided some insight as to a trade-off
that can exists between the yield of a pathway and its cost, or enzyme
burden. However, one can expand the question and ask if there are any
other theoretically possible glycolysis pathways that might be able to
break this trade-off and be more efficient than EMP and ED in both
aspects. @NgWang2019 tried to address this question with an algorithm
they called *optStoic* that generates all biochemically feasible routes
between glucose and pyruvate, with various ATP/glucose yields. They then
ran pathway analysis on all 11,916 options and found that indeed both
EMP and ED are both (nearly) Pareto-optimal. This suggests that
evolution may indeed select for features such as high yield and low
enzyme cost, where one might be more important than the other depending
on the context.

### Metabolic engineering

Besides the quest for understanding the evolution of existing
biochemical pathways, pathway analysis methods like MDF and Enzyme Cost
Minimization have also been used by metabolic engineers in order to rank
and prioritize different alternative designs. For example,
@VolpersClaassens2016 used the MDF algorithm and the Pathway Specific
Activity measure to compare between designs of photo-electro-autotrophic
strains. Similarly, @LoweKremling2021 used the Enzyme Cost Minimization
algorithm to predict the enzyme demand of both natural and synthetic
carbon fixation cycles.

### Predicting the metabolite concentrations

So far, the examples given in this section focused on analyzing and
comparing pathway alternatives in isolation, outside of the context of
actual living organisms. However, we should not forget that the
motivation for optimization goals such as enzyme demand are derived from
physiological and evolutionary principles. Therefore, the optimal
solutions coming from MDF and Enzyme Cost Minimization might be good
predictions for the actual metabolic state that exists in naturally
evolved organisms.

For example, a few years after the *in silico* analysis of the ED
pathway [@FlamholzNoor2013], @JacobsonAdamczyk2019 measured the
intracellular concentrations ED intermediates in *Z. mobilis*, and used
them to calculate the Gibbs energies of the pathway's reactions. Indeed,
they found that they closely fit the predicted values from the MDF
solution. Similarly, measured values of enzyme and metabolite
concentrations in *E. coli* correlate with predicted values from Enzyme
Cost Minimization (when empricial reaction fluxes were obtained from
$^{13}$C-MFA measurements, Figures
[1.9](#PAT:fig:ecoli_model){reference-type="ref"
reference="PAT:fig:ecoli_model"} and
[1.10](#PAT:fig:ccm_ecm_validation){reference-type="ref"
reference="PAT:fig:ccm_ecm_validation"}) [@NoorFlamholz2016]. In a
related paper, @WortelNoor2018 expanded the idea of this method to
explore the entire flux polytope.

These results suggest that indeed the optimization process that occurs
throughout evolution is somewhat similar to the (much simplified) models
presented here. Of course, improving the accuracy of the inputs and
accounting for other effects that impact fitness could improve the
predictions further. On the other hand, it might be naïve to expect
natural systems to be optimal, which would mean that using basic
principles to *precisely* predict phenotypes is an impossible task.

<figure id="PAT:fig:ecoli_model" data-latex-placement="t">
<p><embed src=".//images/PAT_EcoliModel.pdf"
style="width:65.0%" /><br />
</p>
<figcaption> The <em>E. coli</em> model of central metabolism used in
<span class="citation" data-cites="NoorFlamholz2016"></span>. Reaction
names are abbreviated (3 letters) and colored based on the pathway:
(blue) upper glycolysis, (cyan) lower glycolysis, (orange) pentose
phosphate pathway, (red) TCA cycle. </figcaption>
</figure>

<figure id="PAT:fig:ccm_ecm_validation" data-latex-placement="t">

<figcaption> Validation of metabolite and enzyme concentrations,
predicted by Enzyme Cost Minimization, in the central carbon metabolism
of <em>E. coli</em> (Fig  <a href="#PAT:fig:ecoli_model"
data-reference-type="ref" data-reference="PAT:fig:ecoli_model">1.9</a>)
– (A) Comparing predicted and measured metabolic concentrations. The
thin diagonal line marks <span class="math inline">\(x=y\)</span>,
i.e. where the predictions match the measurements. Full blue points are
for all metabolites whose allowed concentration range was set to <span
class="math inline">\(1 \upmu\)</span>M - <span
class="math inline">\(10\)</span> mM. Hollow blue points represent
co-factors whose concentration was fixed in the analysis and therefore
are not actually predicted – these were omitted from the statistics. The
Root Mean Squared Error (RMSE, in log<span
class="math inline">\(_{10}\)</span> scale) was 0.62, the <span
class="math inline">\(r^2\)</span> (Pearson correlation) was 0.50, and
<span class="math inline">\(p\)</span>-value was <span
class="math inline">\(2.2 \times 10^{-4}\)</span>. (B) Comparing
predicted and measured enzyme concentrations. Here, the RMSE was 0.47,
<span class="math inline">\(r^2\)</span> = 0.54, and <span
class="math inline">\(p = 5.3 \times 10^{-6}\)</span>. (C) A pie chart
showing the distribution of the predicted absolute mass-concentrations
for both enzymes (orange) and metabolites (blue) together. Note that
<em>aconitase</em> (catalyzing the reactions acn1 and acn2) has a lower
specific activity than <em>glyceraldehyde-3P dehydrogenase</em>
(catalyzing gap), and therefore occupies a higher fraction of the
mass-concentration even though the required concentration of the latter
enzyme is higher. Labels of enzymes and metabolites that occupy the
smallest fractions of the biomass are omitted due to lack of space. Data
and model predictions taken from <span class="citation"
data-cites="NoorFlamholz2016"></span>. </figcaption>
</figure>

::: Ecoblock
The ED pathway seems to be useful as a quick response to a sudden
increase in abundance of resources (glucose), but less efficient than
EMP when the environment is steady. This is somewhat analogous to
start-up companies, which burn large amounts of venture capital in order
to grow rapidly. However, after reaching a certain scale, the dynamic
nature of start-ups often becomes a burden, where overhead costs pile up
and signal that it is time to join a larger corporation.
:::

## Concluding remarks {#PAT:Sec:PredictingEvolution}

Coming back to our initial question, what have we learned from theory
about the choice between possible pathways? The "choice between
pathways" in a larger network is actually a choice between
(network-wide) flux distributions that use different alternative
pathways. Here we discussed how to score the usefulness of given flux
distributions, which can also be used to score single pathways.

Importantly, flux distributions are scalable (by scaling all enzyme
levels proportionally, and keeping all metabolite levels constant). If
we scale the fluxes, this will scale both the flux benefit (for
instance, the production of a desired product or biomass) and the
required resources (substrates consumed, enzyme budget invested, or
toxic byproducts produced). Because of this scaling property, our
"quality criteria" mostly have the form of ratios between an output flux
(as the benefit) and some (limited) resource (the cost). Such ratios are
called "productivities", where in Chapter - we focused mostly on
substrate productivity (or yield on substrate) and in this chapter on
enzyme productivity (or enzyme-specific rate) as important criteria. Why
these criteria? On the one hand, they are closely related to some big
objectives of the entire cell -- depending on the type of competition it
is facing. On the other hand, they are easy to link to some concrete
criteria about metabolic pathways such as product yield, pathway length,
$\kcat$ values, thermodynamic forces, etc.

::: Ecoblock
In the models described in this chapter, we generally assume that our
system (for example, a metabolic pathway in a cell) is spatially and
temporally homogeneous, and that it shows stable stationary states. This
is clearly a simplification: in reality, cells are inhomogeneous, with
compartments, with enzymes unequally distributed across the cell, and
with enzymes forming complexes or dedicated compartments like the
glycosome (an organelle in some organisms that contains the glycolytic
enzymes), which changes (average) enzyme kinetics. Cells are also
dynamic on various time scales (chemical noise, metabolic dynamics,
protein expression dynamics), which also may change (average) enzyme
kinetics. If we ignore this in our models -- assuming a timeless steady
state -- this will not only cause approximation errors in our metabolic
model, but much more importantly, we ignore the fact that the cell can
exploit spatial inhomogeneity (e.g. compartments or channeling) and
non-steady states (e.g. metabolic oscillations, or adaptation to
fluctuations in the environment) to further improve its fitness (as
compared to a steady-state, constant enzyme model).

Interestingly, classical economic theory makes similar assumptions --
e.g. about markets in equilibrium-- which ignore the spatio-temporal,
dynamic side of real economic systems, which -- as in the case of
metabolic models -- is likely to lead to wrong results.
:::

Since yield on substrate depends only on the shape of the flux
distribution, it can be studied by methods like FBA (see chapters and ).
In this chapter, we focused on the more difficult case, enzyme
productivity, where thermodynamics, enzyme kinetics, and the arrangement
of metabolite and enzyme concentrations come into play. The factorized
law in
Eq. ([\[PAT:eqn:factorized_multi\]](#PAT:eqn:factorized_multi){reference-type="ref"
reference="PAT:eqn:factorized_multi"}) shows us how the enzyme demand of
a flux distribution can be computed if metabolite concentrations are
known, and how the demand depends on forward $\kcat$, the thermodynamic
force, and enzyme saturation. The only difficulty is that the
thermodynamic forces and metabolite concentrations are usually not
known. Here we considered some best-case scenarios, assuming that the
cell will realize the concentration arrangements that optimize pathway
performance. When considering thermodynamics alone (and making some
further simplifications), this led to the MDF method. For the full
problem, the solution is provided by Enzyme Cost Minimization. This
method is directly related to the different pathway criteria we
discussed initially (including pathway length, thermodynamic forces, and
$\kcat$ values) and thus shows how these different factors determine
enzyme demand. As a numerical method, it is relatively easy to use
because it is a convex optimization problem. But if little data is
available, simpler methods such as MDF, with their lower demand for
parameters, may be useful tools to predict pathway usage.

In order to predict optimal metabolic states, we started in the previous
chapter with models that optimize the fluxes in an entire network.
Howeve, to keep the models linear, kinetics and concentrations were
largely ignored. In FBA with molecular crowding, a connection between
fluxes and enzyme levels was made via empirical parameters, the apparent
catalytic rates or \"enzyme efficiencies\". We now saw that these
parameters are not at all constant parameters, but emerge from kinetics
and given concentration profiles, and we also saw how optimal
concentration profiles can be computed for a given flux distribution.
This means: we now know how to predict optimal fluxes from known enzyme
efficiencies, and we know how to predict optimal concentrations (and
therefore enzyme efficiencies) from known fluxes. In the next chapter we
will put these two things together, in order to predict all variables in
the system -- fluxes, metabolite concentrations, enzyme efficiencies,
and enzyme levels -- from a single principle of maximal overall enzyme
efficiency.

## Recommended readings {#recommended-readings .unnumbered}

##### A search for efficient pathways, based on different criteria:

Arren Bar-Even, Elad Noor, Nathan E. Lewis, and Ron Milo. Design and
analysis of synthetic carbon fixation pathways. Proceedings of the
National Academy of Sciences, 107(19):8889--8894, 2010. doi:
[10.1073/pnas.0907176107](https://doi.org/10.1073/pnas.0907176107).

##### The max-min driving force method:

Elad Noor, Arren Bar-Even, Avi Flamholz, Ed Reznik, Wolfram
Liebermeister, and Ron Milo. Pathway thermodynamics highlights kinetic
obstacles in central metabolism. PLoS Comput. Biol., 10(2):e1003483,
2014. doi:
[10.1371/journal.pcbi.1003483](https://doi.org/10.1371/journal.pcbi.1003483).

##### Enzyme cost minimization: {#enzyme-cost-minimization-1}

Elad Noor, Avi Flamholz, Arren Bar-Even, Dan Davidi, Ron Milo, and
Wolfram Liebermeister. The protein cost of metabolic fluxes: Prediction
from enzymatic rate laws and cost minimization. PLoS Comput. Biol.,
12(11):e1005167, 2016. doi:
[10.1371/journal.pcbi.1005167](https://doi.org/10.1371/journal.pcbi.1005167).

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
[]{#PAT:Exerc:estimate label="PAT:Exerc:estimate"} Estimate pathway
efficiencies (i.e. product production rates per total enzyme
concentration) from simple back-of the envelope calculations and
plausible numbers (refer to the BioNumbers database for realistic
values). (a) From pathway length (assuming reasonable apparent $\kcat$
values); (b) from given apparent $\kapp$ values (or given $\kcat$ values
and $\Delta_r G$). (c) Convert the results into growth rates (assuming
realistic estimates of the total protein density; the proteome fraction
of metabolic enzymes; the biomass production rate etc). Assume plausible
numbers in all cases.
:::

::: exercise
[]{#PAT:Exerc:compute label="PAT:Exerc:compute"}

Compute the reduction of pathway efficiency in a linear chain when
decreasing the external substrate concentration (no constraints on
metabolite levels)
:::

::: exercise
[]{#PAT:Exerc:derive label="PAT:Exerc:derive"} Derive the optimal ATP
yield in a glycolysis model with a linear flux-force relationship
:::

::: exercise
[]{#PAT:Exerc:MDF label="PAT:Exerc:MDF"} Implement the MDF method in a
programming language of your choice.
:::

::: exercise
[]{#PAT:Exerc:MDFandECM label="PAT:Exerc:MDFandECM"} The optimality
principle of MDF (avoiding small thermodynamic driving forces) can be
justified by assuming that low driving forces would entail high enzyme
demands. Do you expect that MDF solutions are also Enzyme Cost
Minimization solutions (or vice versa)? Otherwise, can you think of an
approximation of the Enzyme Cost Minimization problem, such that MDF
provides the correct solution? Show how the Enzyme Cost Minimization
objective could be approximated step by step, and illustrate this with
an example.
:::

::: exercise
[]{#PAT:Exerc:CycleChemicalReactions
label="PAT:Exerc:CycleChemicalReactions"} Assume a cycle of chemical
reactions $A \leftrightarrow B \leftrightarrow C \leftrightarrow A$
without co-factors or external inputs/outputs. (a) Show that there is no
stationary, thermodynamically feasible flux distribution except for the
(trivial) vanishing flux. (b) Explain why, if there were a flux, this
would be a perpetuum mobile.
:::

::: exercise
[]{#PAT:Exerc:OptimalEnzymeLevels label="PAT:Exerc:OptimalEnzymeLevels"}
Consider a chain of two reactions
$S \leftrightarrow X \leftrightarrow P$ with enzymes $\enzconc_1$ and
$\enzconc_2$,
$\flux_{1} = \enzconc_1 (k_{+1} S - k_{-1} X), \flux_{2} = \enzconc_2(k_{+2} X - k_{-2} P)$.
Compute the steady state flux given $\enzconc_1, \enzconc_2$. Let
$\enzconc_1+\enzconc_2 = \enzPW$ be fixed. Determine
$\enzconc_1, \enzconc_2$ such that the flux is maximal. Use Lagrange
multipliers. Hint: Assume forward flux where
$P/S< (k_{+1} k_{+2})/(k_{-1} k_{-2})= q_{1} q_{2}$.
:::

::: exercise
[]{#PAT:Exerc:FluxMinLinPath label="PAT:Exerc:FluxMinLinPath"} Prove
that the function: $$\begin{equation}
        f(\enzconcv) = \frac{1}{\sum_i (A_i \enzconci)^{-1}}
    
\end{equation}$$ for a fixed $\vec{A}$ and under the constraint
$\sum_i \enzconci = \etot$, is at its maximum when: $$\begin{equation*}
        \enzconci = \etot \cdot \frac{A_i^{-1/2}}{\sum_i A_i^{-1/2}}
    
\end{equation*}$$
:::

::: exercise
[]{#PAT:Exerc:HaldaneRateLaw label="PAT:Exerc:HaldaneRateLaw"}

Haldane described an enzyme-catalyzed reaction by three steps, each
following a mass-action rate law: $$\begin{equation}
        {\rm S} + {\rm E} \ce{<=>[k_{1}][k_{2}]} {\rm ES} \ce{<=>[k_{3}][k_{4}]} {\rm EP} \ce{<=>[k_{5}][k_{6}]} {\rm P} + {\rm E}\,.
    
\end{equation}$$

The ODE system describing the change in time of each species is:
$$\begin{align}
    \begin{split}
        \frac{d [ES]}{dt} &= [E]\cdot [S]\cdot k_1 + [EP]\cdot k_4 - [ES]\cdot (k_2 + k_3) \\
        \frac{d [EP]}{dt} &= [E]\cdot [P]\cdot k_6 + [ES]\cdot k_3 - [EP]\cdot (k_4 + k_5) \\
        \frac{d [E]}{dt} &= -[E]\cdot[S]\cdot k_1 + [ES]\cdot k_2 + [EP]\cdot k_5 - [E]\cdot[P]\cdot k_6
    \end{split}
    
\end{align}$$

Prove that at quasy-steady-state (where the total enzyme concentration
is fixed, and the concentration of each species doesn't change over
time), the rate in which $[S]$ is converted to $[P]$ is governed by the
following rate law: $$\begin{equation}
\label{eq:haldane}
            v = [E_0] \frac{\kcatplus [S]/\kmS - \kcatminus [P]/\kmP}{1 + [S]/\kmS + [P]/\kmP}
    
\end{equation}$$ where: $$\begin{equation*}
        \kmS = \frac{k_2 k_4 + k_2 k_5 + k_3 k_5}{k_1(k_3 + k_4 + k_5)} ;~
        \kmP = \frac{k_2 k_4 + k_2 k_5 + k_3 k_5}{k_6(k_2 + k_3 + k_4)} ;~
        \kcatplus = \frac{k_3 k_5}{k_3 + k_4 + k_5} ;~
        \kcatminus = \frac{k_2 k_4}{k_2 + k_3 + k_4}
    
\end{equation*}$$
:::

::: exercise
[]{#PAT:Exerc:FacRateLaw label="PAT:Exerc:FacRateLaw"}

Use the Haldane relationship: $$\begin{equation}
        \frac{\kcatplus}{\kcatminus} \frac{\kmP}{\kmS} = \frac{k_1 k_3 k_5}{k_2 k_4 k_6} = \Keq
    
\end{equation}$$ and the definition of Gibbs free energy:
$$\begin{align}
        \begin{split}
        \deltaGstd &= - R \cdot T \cdot \ln{\Keq}\\
        \deltaG &= \deltaGstd + R \cdot T \cdot \ln{\left([P]/[S]\right)}
        \end{split}
    
\end{align}$$ to prove that
Eq. ([\[eq:haldane\]](#eq:haldane){reference-type="ref"
reference="eq:haldane"}) is equivalent to the following factorized rate
law: $$\begin{equation}
      v = [E_0] \kcatplus \cdot \left(1 -   \expe^{\deltaG/RT} \right) \cdot \frac{[S]/\kmS}{1 + [S]/\kmS + [P]/\kmP}.
      \label{eq:factorized}
    
\end{equation}$$
:::

[^1]: In general, reaction stoichiometries can be arbitrarily scaled.
    For example, instead of a reaction 2 A $\rightarrow$ B, we may write
    A $\rightarrow \frac{1}{2}$ B for convenience, which will only lead
    to a scaling factor in the reaction rate. However, this holds only
    if reaction stoichiometries are used to describe mass-balance. In
    cases like
    Eq. ([\[PAT:eqn:factorized_multi\]](#PAT:eqn:factorized_multi){reference-type="ref"
    reference="PAT:eqn:factorized_multi"}), where stoichiometries appear
    in kinetic rate laws or in thermodynamic balances, we do not have
    this choice. In these cases, the stoichiometries must reflect the
    molecularities, that is, the actual number of reactant molecules
    involved in the enzymatic reaction.
