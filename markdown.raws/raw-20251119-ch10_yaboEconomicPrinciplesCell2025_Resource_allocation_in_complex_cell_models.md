# Resource allocation in complex cell models {#LAR}

::: chapterhighlights
- Whole-cell resource allocation models on a genomic scale combine a
  detailed, FBA-like description of metabolism with a model of
  macromolecule synthesis, formulated as linear constraint-based
  problems.

- Resource allocation models of cells can be built based on three basic
  constraints: stationary fluxes (balancing production and consumption
  fluxes, uptake and excretion fluxes, as well as compound dilution by
  cell growth); catalytic constraints relating fluxes to the amounts of
  catalyzing enzymes (or other machines); and density constraints,
  limiting molecule amounts in cell compartments, or molecule
  concentrations.

- Large resource allocation models build on the same principles, and
  have been implemented as different variations (RBA models, ME-models,
  and pc-models).

- These constraints narrow down the solution space predicted by FBA
  towards more physiological solutions
:::

## Detailed resource allocation models of cells {#LAR:Sec:Introduction}

In the previous chapters, we have saw two principal approaches to
modeling production processes in cells. To keep the number of variables
low, but with intention of well-parametrizing the model, one can
construct small, coarse-grained models of growing cells (Chapter ). On
the contrary, Flux Balance Analysis (FBA) models can accommodate a very
large number of variables (Chapter ), making them an excellent choice to
model metabolic networks at genome-scale.

Small, coarse-grained models are very suitable for investigating base
principles of life. Likely the best example to illustrate this is the
work of Douwe Molenaar and co. [@MolenaarVanBerlo2009], where a
self-replicator model was used to proposed that the low-yield, or
substrate-inefficient (\"wasteful\") metabolic strategies are adopted as
a consequence of these pathways being more efficient in terms of protein
use, compared to the high-yield pathways. In other terms, the growth
output of the \"wasteful\" strategy per unit protein is higher than the
\"efficient\" one. Thus we now believe that fermentation of glucose,
often called under an umbrella term \"overflow metabolism\", will take
place in many organisms if the substrate in their environments is
abundant enough.

However, the chemistry of life is extremely diverse, and even such a
familiar concept as fermentation can become complicated. Take three
representatives of the tree of life: a bacterium *Escherichia coli*,
budding yeast *Saccharomyces cerevisiae*, and mammalian, say, human
cells. All three exhibit overflow metabolism - even when enough oxygen
is available in the environment - yet the underlying biochemistry tells
us that *E. coli* ferments glucose into acetic acid, *S. cerevisiae* -
into ethanol, and human cells - into lactate. Bringing more contrasts on
the table, there might be extreme differences in a single taxon already:
some yeasts, for instance, will never produce ethanol when oxygen is
present; some of them have lost the ability to do respiration at all
over the course of evolution. This might sound like playing a trivia
game, but in many cases, meaningful modeling of complex biological
systems requires both taking and making biochemical insight. Therefore,
when we aim not only to uncover the underlying principles, but also to
learn biochemistry, more detailed models such as FBA model have an upper
hand.

Yet we already know from previous chapters that the predictions of
canonical FBA models are limited to substrate-efficient metabolic
states. Continuing with the example of the overflow metabolism, FBA
models would predict *E. coli* or *S. cerevisiae* to respire on minimal
medium with glucose as the main carbon source -- regardless of the
maximal flux of glucose into the cell. Thus the prediction of
substrate-inefficient metabolism using FBA over the years used to rely
on introducing additional, mainly empirical (e.g. maximal oxygen
uptake), constraints onto the system [@deGrootLischke2020]. Moreover, we
can impose only linear constraints in FBA models, and this greatly
reduces our options.

Overall, we often seek to take the advantageous points of both \"schools
of modeling\", however, this is where we need to start doing
compromises. In an ideal world, the self-replicator models from Chapter
would be much more detailed, and would be extended with explicit
kinetics and thermodynamic constraints to obtain a detailed cell model.
However, the number of variables would increase tremendously, and
non-linear optimization is very inefficient already past even small
systems. On the contrary, we could try to advance on existing FBA-type
models by introducing the concepts of protein economy (Chapter ) at
genome-scale, as well as self-replication. Following our best
understanding, these, again, would constitute non-linear relationships
(e.g. enzyme kinetics), yet large-scale non-linear programming is not a
viable option either. Thus simplifications are necessary to keep
linearity (and convexity) to solve optimization problems for large-scale
models.

So can we make large-scale models tractable? If we linearize **all**
formulae, then instead of a biconvex or convex/concave problem, we
obtain a linear problem (a bit like FBA); more precisely, a system of
linear equalities and inequalities that define a set of feasible states.
This set is a polytope, and linear optimality problems on this set can
be solved easily. More specifically, to model metabolism in a growing
cell, we need to consider dilution of metabolites in the growing cell
volume, or simply - the growth rate of the cell.

### Replacing enzyme kinetics by linear catalytic constraints

To obtain large, detailed cell model that we can actually solve, all
relationships between models variables have to be linearized. This
concerns, most importantly, all catalyzed processes: we assume a linear
dependence between a catalyzed flux and its catalyst (enzyme or machine)
concentration, but ignore the dependence on the concentrations of
substrates, products, cofactors, or additional regulators. What does
this mean in practice? As we know from Chapter , typical enzymatic rate
laws have the form $\flux = \enzconc ~ k(\mathbf{\metconc})$: the rate
$\flux$ is proportional to enzyme level $\enzconc$ and enzyme efficiency
$k$, which is given by a kinetic rate law $k(\mathbf{\metconc})$, a
nonlinear function of the metabolite concentrations. Depending on the
context, $k$ is also called apparent $\kcat$. The kinetic rate laws
$k(\metconc)$ have typical shapes, as described in Chapter .

To linearize the expression for $\flux$, while keeping the dependence on
$\enzconc$, we need to replace the ratio $k=\flux/\enzconc$ by a fixed
number, and so $k$ becomes a model parameter. If the metabolite
concentrations were known (experimentally, or from kinetic models under
optimality assumptions, see Chapter ), the value of $k$ could be
computed. Otherwise, it can also be determined experimentally, by
measuring $\flux$ and $\enzconc$ and setting $k=\flux/\enzconc$
[@DavidiNoor2016], which is feasible for a limited number of enzymes,
however. Obviously, in reality, neither $\mathbf{\metconc}$ nor $k$ will
be fixed and given, but for our linearized model, we need to assume
this. This holds both for metabolic reactions (with enzymes as
catalysts) and for macromolecular reactions (with molecular machines as
catalysts).

Under this assumption, we can replace all kinetic constraints by two
linear constraints on the enzyme. If we consider coefficients $k$ and
$k^{'}$ to approximate enzyme kinetics in the forward and backward
direction, respectively, the flux the enzyme $\enzconc$ catalyzes should
satisfy $-\enzconc ~ k^{'} \leq \flux \leq \enzconc ~ k$. We set
$k^{'} = 0$ for irreversible reactions, and, for simplicity reasons, we
usually assume $k = k^{'}$ for reversible reactions, unless kinetic
measurements are available that suggest otherwise. This relationship can
be formulated as enzyme capacity constraints in order to replace the
kinetic rate laws in the FBA model. By writing down such constraints for
each enzyme in the model, we can couple the metabolic fluxes with the
demand for enzymes, needed to operate these fluxes.

By linearizing all formulae as described above, it is possible to build
very large models, describing resource allocation on genome scale. What
we commonly refer to as \"resource allocation models\" therefore
formalize the mathematical relationships defining the interactions and
allocation of resources between the cellular processes to describe
optimal resource allocation using constraint-based models. All these
relationships take the form of linear, growth-rate dependent equalities
and inequalities, and, when linearized, form a convex feasibility
problem
[@GoelzerFromion2009; @GoelzerFromion2011a; @GoelzerFromion2011b].

### Overview of existing FBA extensions

By itself, the idea of constraining metabolic models to represent
limited metabolic capacity of cells is not new. There are two ways to
approach this budgeting problem. The first possibility is \"protein
budgeting\", where a fixed amount of protein needs to be partitioned in
the optimal manner (e.g. to maximize growth). The second, alternative
method is \"resource budgeting\", where models include both the protein
budgeting and the descriptions of demands for protein synthesis.
However, \"protein budgeting\" problems assume that investments in
protein production follow the budget, and not vice versa.

Some enzyme-constrained variants of FBA account for empirical
constraints on the total concentration of metabolic enzymes (FBA with
molecular crowding, or FBAwMC [@VazquezBeg2008]), or on proteome sectors
(Constrained-Allocation FBA, or CAFBA [@MoriHwa2016]). While these types
of models can predict metabolic states more reliably, the empirical
constraints come as model assumptions and thus cannot be understood by
the models themselves. In these models, the primary assumption is that
the cell phenotype is obtained by genetic regulations, and the main goal
and utility of genetic regulation can be interpreted as ways of saving
resources. Thus in many cases when we predict cell phenotype maximizing
growth, we find predictions in good agreement with the experimental
observations. Therefore, resource allocation models extend and embed the
ideas of proteome partitioning beyond frameworks like CAFBA and GECKO
[@SanchezZhang2017], or representing metabolic capacity limitations
beyond FBAwMC.

Currently, there are three main implementations of large-scale resource
allocation models: Resource Balance Analysis (RBA)
[@GoelzerFromion2011], Models of Metabolism and Macromolecular
Expression (ME-models) [@OBrienLerman2013] and proteome-constrained
models (pc-models) [@ElsemmanRodriguez2021]. All these implementations
are formalized as LP feasibility problems at a fixed growth rate, where
the growth rate can then be maximized in an additional optimization
loop. Originally, ME-models were considered as an extension of M-models,
by including predictions for mRNA, protein, and ribosome levels.
Importantly, they do not consider density constraints that, for
instance, RBA does. Therefore, limitations on the capacity of exchange
fluxes (as in FBA) are necessary to obtain a solution.

### Why maximize the growth rate? {#sec:linearization}

Under the assumption of the balanced growth, the copy number of each
cell component is doubled between two consecutive cell divisions. If
metabolites are described by their concentration, we can think of cell
growth as dilution by which the concentrations of all compounds would go
down if their amounts remain the same. For a given compounds, dilution
by growth can be effectively modeled of every metabolite by a
\"consuming reaction\", with a flux given by
$\flux_{\rm dil} = \mu~\metconc$, the compound concentration multiplied
by the growth rate. By adding these hypothetical dilution reactions to
the metabolic network, we obtain a new stationarity condition
$\Stoichmat~\flux = \growth~\mathbf{\metconc}$ that connects the vectors
of fluxes and compound concentrations, and in which the growth rate
$\growth$ appears as a parameter. For each choice of the parameter
$\growth$, we can ask whether a feasible steady growth state -- i.e. a
feasible combination of $\mathbf{\flux}$ and $\mathbf{\metconc}$ exists.
Furthermore, the feasible combinations
$(\growth,\mathbf{\flux},\mathbf{\metconc})$ form a convex set, with
possible solutions $(\mathbf{\flux}, \mathbf{\metconc})$ for low values
of $\mu$ and no solutions above a critical value $\growth_{\rm max}$,
the maximal possible growth rate for our model. Finding this critical
value as well as the corresponding optimal fluxes $\mathbf{\flux}$ and
compound concentrations $\mathbf{\metconc}$ is relatively easy, and can
be done by bisection: solving a series of Linear Programming problems
(checking for potential solutions $(\mathbf{\flux}, \mathbf{\metconc})$
for different values of $\growth$).

## The basic constraints in resource allocation models {#LAR:Sec:constraints}

As mentioned above, fine-grained resource allocation models build on
genome-scale metabolic models (GEMs) to encompass all the reactions that
can be employed in a metabolic network. The technical advance, when
constructing such models, is to impose sets of additional constraints
onto GEMs to couple the metabolic fluxes with investment into metabolic
pathways (production of enzymes). To the date, different implementations
of this concept were proposed to predict optimal resource allocation in
different microorganisms [@deBeckerTotis2022].

Although the precise formulations vary, resource allocation models build
on three principal types of constraints (Figure
[1.1](#LAR:fig:RBASchemeBiological){reference-type="ref"
reference="LAR:fig:RBASchemeBiological"}):

- Mass-conservation constraints

- Flux coupling constraints

- Compartment capacity, or protein density, constraints

The general description of these constraints in fact is the same as for
small, coarse-grained self-replicator models, only the number of
individual constraints increases. Moreover, every of the constraints
described can be split into a number of constraints, considering only a
subset of fluxes in the model (e.g., fluxes taking place in a certain
cell compartment).

Alongside these three major types of constraints, there is another set
of constraints, which we may call \"environment\" constraints - these
correspond to, e.g. the composition of growth medium, biomass
composition at at given growth rate $\growth$, etc. They are implemented
by setting target values for amounts and/or fluxes defining a viable
cell in a given (or several) environmental conditions, but they are not
structural constraints. These constraints usually are added *ad hoc* and
do not need to bear any functional meaning *per se*. We will now expand
on the three types of constraints used in resource allocation models;
note that the description is not exhaustive and peculiarities may vary
among different formulations.

<figure id="LAR:fig:RBASchemeBiological" data-latex-placement="t!">
<p>(A)<br />
</p>
<embed src=".//images/LAR_RBASchemeBiological_a.pdf"
style="width:90.0%" />
<p> <br />
(B)<br />
</p>
<embed src=".//images/LAR_RBASchemeBiological_b.pdf"
style="width:70.0%" />
<figcaption>Overview of biological components and mathematical
constraints in large-scale resource allocation models – A Resource
Balance Analysis (RBA) model is shown as an example. (A) Typically, an
RBA model describes metabolisms and macromolecule production in a
growing cell (yellow blocks). Precursors from metabolism are needed to
produce macromolecules, and some macromolecules serve as enzymes to
catalyze metabolic reactions. In addition, macromolecules are diluted
and are localized in cell compartments. (B) Sets of mathematical
constraints. The variables and processes described by an RBA model must
satisfy a number of constraints, include mass-balance constraints
(between production, degradation, and dilution of compounds); capacity
constraints (relating process velocities to the concentrations of
catalysts); density constraints (on the total amount of compounds in a
cell compartment); and possibly empirical physiological constraints on
any types of "target variables", to ensure realistic
models.</figcaption>
</figure>

### Steady-state and mass-conservation constraints

*Mass-conservation* constraints define the metabolic network
(stoichiometry and relation between fluxes). The initial building blocks
of these extended models are GEMs, and thus the metabolic network
stoichiometry is already there; what remains to be defined are the
protein turnover processes. We consider four types of protein turnover
reactions in fine-grained resource allocation models: protein synthesis,
folding, degradation and dilution-by-growth. So, for every protein
present in such a model, we add these four reactions: two of them,
translation and degradation, include the stoichiometry of amino acids
needed for its translation and released during degradation based on the
protein sequence. The reactions which represent either protein folding
modeled as the conversion of the \"unfolded\" protein species into the
\"folded\" ones, and the dilution-by-growth is modeled as a sink for the
\"folded\" protein species (\"folded\" $\rightarrow \emptyset$).

### Catalytic constraints

Next, the flux *coupling* constraints couple the metabolic fluxes with
protein usage: usually, the usage scales with the catalytic turnover
value $\kcat$ of the enzyme. In this step we have to collect the kinetic
information (in most cases, $\kcat$ values), which are used as model
parameters. We establish the coupling between fluxes and protein
synthesis by setting $\flux = \kcat ~ \enzconc ~ \eta$, where $\enzconc$
is the enzyme concentration and $0 < \eta \le 1$ is an efficiency term
summarizing the effects of reaction thermodynamics, enzyme saturation,
and possibly small-molecule regulation. The value for $\eta$ can be
either assumed or fitted from experimental data, and when $\eta = 1$,
the enzyme is considered to operate at its maximal rate. Coupling
constraints are introduced to couple both (i) the metabolic reactions
with enzyme usage (as described above) and (ii) protein turnover
reactions with the respective macromolecular machinery (e.g. sum demand
of ribosomes for protein translation,
$\flux_{\rm translation} = [\mbox{Ribosome}] \times k_{\rm cat, ribosome}$).
The sheer number of the kinetic parameters needed for formulating the
coupling constraints in the fine-grained models requires the modeler to
consider different assumptions and simplifications when building and
parameterizing these models, as briefly discussed below.

The number of processes described in a fine-grained manner directly
translates to the number of reactions and metabolites in the model. For
instance, transcription is modelled explicitly in the ME-models
[@OBrienLerman2013]. The modeler's decision is key here: under
assumption that transcription and translation form a linear pathway with
fixed scaling factors (i.e. there is a fixed ratio of peptides
translated per mRNA transcribed), the flux through mRNA translation
reaction can be computed post-optimization based on the flux through the
protein translation reaction. Explicit modelling of transcription would
require describing processes of mRNA transcription, processing, export
from nucleus, and then cytosolic degradation after the mRNA is
translated -- for each of the transcripts, with precise stoichiometry
and a new set of coupling constraints.

The next issue is kinetic parametrization of these fine-grained models.
We currently can use only very simplified kinetics in the models (flux
coupling $\flux = \kcat ~ \enzconc ~ \eta$), and simplify such factors
as enzyme saturation and thermodynamic driving force into a single value
of factor $\eta$. Two approaches are used to deal with this, as a large
fraction of parameters are not even available. First,
condition-dependent kinetic parameters (\"apparent catalytic
constants\", $\kapp$) are fitted from experimental (mostly quantitative
proteomics) data (setting $k_{\rm eff} = \kcat ~ \alpha$, where
$0 < \alpha \le 1$) with a value $\alpha$ chosen to match predicted
enzyme abundance and experimental measurements. Otherwise, for the
enzymes with measured $\kcat$ values, we can assume that enzymes work at
their maximal rate, i.e. the saturation function $\eta = 1$. Then the
model computes the *minimal* protein requirement to sustain the flux
through the metabolic reactions. The comparison of *minimal predicted*
vs. *observed* protein abundance can represent the \"apparent
saturation\", or \"overcapacity\" of enzymes. For instance, it is common
in yeast *S. cerevisiae* that the flux and not protein expression varies
across conditions, and the relationship between predicted and measured
expression can suggest the nature of the observed protein expression
[@GrigaitisTeusink2022].

### Protein density constraints

The final layer of information in our resource allocation models is a
set of *protein density* constraints in each cell. These constraints put
an upper limit on the amounts machines driving the cellular processes,
e.g. a maximal protein capacity of a compartment. These constraints are
formulated as weighted sums of protein abundance, usually with weights
proportional to the proteins' molecular weight. Usually, the density
constraints are expressed in terms of (usually maximal) *mass*, *area*,
and *volume* of the compartment (e.g. \"what is the maximal mass the
mitochondrial proteins can take up in $gDW$ of cells?\"). Based on the
biological interpretation of the constraints, we formulate the weighing
multipliers to represent either of the metrics (mass/area/volume) that
every protein occupies.

The capacity constraints can be both *equality* and *inequality*
constraints: more frequent are the latter (usually defining the \"upper
limit\" of, e.g. amount of protein targeted to mitochondria). However,
some cell properties should be described through equality constraints:
one of these is the protein density of biomass, defining the \"target\"
protein translation per gram dry cell biomass.

::: Generalblock
Here we would like to include a relevant note for interpretation of the
output of the fine-grained resource allocation models. Both the
classical FBA and these extensions do not consider \"metabolite
concentration\" as a concept: optimization variables are all *fluxes*.
Frameworks discussed in this chapter model protein synthesis from amino
acids and energy equivalents explicitly, with a typical flux dimension
of $mmol\ gDW^{-1}\ h^{-1}$ (as for any other fluxes). To compute the
amount of protein that has to be produced in the steady-state growth, we
should consider the flux balance for the protein $\enzconc$:
$\flux_{\rm synthesis,\enzconc} = \flux_{\rm degradation,\enzconc} + \flux_{\rm dilution,\enzconc}$,
or, rewritten with the respective parameters,
$\flux_{\rm synthesis,\enzconc} = (\flux_{\rm deg,\enzconc} + \growth)  ~ \enzconc$.
Here, $k_{\rm deg,e}$ is the degradation rate for the protein
$\enzconc$, and $\growth$ is the specific growth (= dilution-by-growth)
rate. The $[\enzconc]$ in the rewritten equation holds dimension of
mmol gDW$^{-1}$, which is protein *abundance*, rather than
*concentration*.

The predicted amount of protein in cells can be compared to experimental
measurements in two ways. First option is to convert abundance to
concentration using the relationship between the cell volume and dry
weight (e.g. $V_{gDW} = 1.7\ mL\ gDW^{-1}$ in *Saccharomyces
cerevisiae*, [@CanelasRas2011]). Alternatively, proteome mass fractions
are a popular unit in label-free mass spectrometry-based protein
quantification, a popular method in quantitative microbiology.
Respectively, predicted proteome mass fractions can be inferred by
converting protein abundance in $mmol$ to $g$, and scaling to the
protein content in dry cell biomass. Here, it is important to consider
the conversion factors (protein content in dry biomass). *E. coli*
maintains rather constant protein content in dry weight across growth
rates (ca. 0.55 $(g\ \mbox{protein})\ gDW^{-1}$)
[@MartinezMartin1981; @ZimmermanTrach1991]. On the contrary, the protein
content is known to vary in *S. cerevisiae* as a function of growth rate
[@CanelasRas2011].
:::

### Interpreting the consequences of the additional constraints

We have briefly discussed what types of additional constraints need to
be implemented to extend FBA models to account for cellular resource
allocation, and now let us recap on what these sets of rules mean in
biological terms. The constraints described above shall couple the
metabolic fluxes with the production of enzymes that operate these
functions, so the model has to produce amino acids and generate ATP in
order to use them for protein translation. Moreover, the enzyme demand
will be coupled with the production of the macromolecular machines
required to produce, fold, and degrade these enzymes (ribosomes,
chaperones, and proteases, respectively), requiring the same building
blocks (see Chapter ). These constraints therefore formalize a
self-replicating molecular system in balanced growth subject to
different structural constraints:

1.  The metabolic network has to produce all metabolic precursors
    necessary for biomass production and mass conservation must hold for
    all intracellular molecule species - i.e. intracellular metabolites
    and molecular machines.

2.  The capacity of each type of molecular machine must be sufficient to
    ensure its function, i.e. to catalyze chemical conversions at a
    sufficient rate;

3.  The intracellular density of compartments and the occupancy of
    membranes must not exceed the defined limits.

As highlighted before, the biological interpretation of the additional
constraints discussed above is rather universal for different
implementations of resource allocation models, with minor deviations in
terminology and/or formulation. To illustrate how resource allocation
models are built from conventional GEMs, and how the respective models
are formalized in mathematical terms, in the following we will consider
one of the popular formulations of resource allocation models in more
depth.

## Resource Balance Analysis: model construction and simulation

Resource Balance Analysis (RBA) is a flexible and generic modeling
framework that describes the functioning of an organism using linear
equality and inequality constraints, as described in general terms in
Section [1.2](#LAR:Sec:constraints){reference-type="ref"
reference="LAR:Sec:constraints"}. As a consequence, an RBA model
includes all known metabolic reactions coupled to relevant cell
processes with major protein investments (production of biomass
precursors; including, but not limited to protein translation, protein
folding, protein transmembrane transport, and protein degradation).
Where applicable, circumstantial information can be included into the
model to establish the dependency of enzyme activity on metal ions,
vitamins, and/or cofactors. Which metabolic reactions and cell processes
are regarded as relevant may vary between organisms and is a modeler's
choice.

### Building a draft RBA model

The software package `RBApy` [@BulovicFischer2019] contains all the
routines needed to build and simulate RBA models. In order to build a
new RBA model, it takes as an input a genome-scale metabolic network in
SBML format [@HuckaFinney2003], together with additional information to
formulate all the constraints described above. Different types of
biological data are needed to build an RBA model for a given type of
cell:

- Amino acid sequences for metabolic enzymes and macromolecular machines
  (e.g. ribosomes and chaperones),

- If applicable, stoichiometry of known cofactors (e.g. metal ions),

- Efficiencies of metabolic enzymes,

- Molecular weights and localization of proteins (for density
  constraints),

- Any empirical constraints on concentrations or fluxes (\"targets\",
  see previous section).

The software first extends the input GEM with a description of protein
production and dilution in the cell. To do so, it extracts information
from the input files on (i) protein sequences and cofactors, (ii) the
subunit stoichiometry of protein complexes, and (iii) protein
localization (using information from public databases such as UniProt).
Using this information, reactions corresponding to protein synthesis,
folding, degradation, and dilution by growth are added automatically.
Finally, the software maps enzymes to the reactions they catalyze and to
the proteins they consist of. The output of the routine is a draft
(uncalibrated) RBA model.

### Mathematical description of a RBA problem {#LAR:sec:RBA_formulation}

##### Notation.

Below $A^T$ refers to the transpose of the matrix $A$.
$\Rsetp^n \eqbydef \big\{x \in \Rset^n\, | x_i > 0   \text{ for all } i \in \{1,\cdots,n\}\big\}$,
$\Rsetp \eqbydef \Rsetp^1$,
$\Rsetep^n \eqbydef \left\{x \in \Rset^n\, |\, x_i \geq 0  \text{ for all } i \in \{1,\cdots,n\} \right\}$
and $\Rsetep  \eqbydef \Rsetep^1$.\
In a standard RBA model, we consider balanced growth (see Chapter ),
that is, the average state of a cell in a cell bacterial population
growing exponentially at the specific (constant) growth rate
$\mu\geq 0$, i.e. the amount of produced biomass per biomass per cell
per unit of time. Our simulated average cell is composed of different
molecule species:

1.  $n_y$ types of molecular machines, which can be subdivided further
    into $n_e$ enzymes and transporters involved in the metabolic
    network $\mathbb{ E} \eqbydef ({ \rm E}_1, \ldots, { \rm E}_{n_e})$
    at the concentrations ${\bf e} \eqbydef (e_1, \ldots, e_{n_e})^T$
    and metabolic fluxes ${\bf v} \eqbydef ( v_1, \ldots, v_{n_e})^T$;
    and $n_{m}$ macromolecular machines
    $\mathbb{ M} \eqbydef ({\rm M}_1, \ldots, {\rm M}_{n_m})$ involved
    in non-metabolic cellular processes, such as the translation
    apparatus, at the concentrations
    ${\bf m} \eqbydef (m_1, \ldots, m_{n_m})^T$;

2.  $n_p$ proteins
    $\mathbb{P} \eqbydef \{{\rm P}_{1}, \ldots, {\rm P}_{n_p}\}$
    belonging to unspecified cellular processes.
    ${\bf p} \eqbydef  (p_{1},\ldots ,p_{n_p})^T$ denotes the set of
    concentrations of $\mathbb{P}$;

3.  $n_s$ intracellular and mass-balanced metabolites
    $\mathbb{S} \eqbydef ({\rm S}_1, \ldots, {\rm S}_{n_s})$. Within the
    set $\mathbb{S}$, we distinguish a subset
    $\mathbb{B} \eqbydef ({\rm B}_1, \ldots, {\rm B}_{n_b})$ of abundant
    metabolites which have fixed growth-independent concentrations
    ${\bf \bar{b}} \eqbydef (\bar{b}_1, \ldots, \bar{b}_{n_b})^T$ (and
    usually coincide with biomass macro-components such as DNA, cell
    wall or plasmic membrane). We also consider a set of extracellular
    metabolites
    $\mathbb{S_{\rm ext}} \eqbydef ({\rm S}_{\rm ext,1}, \ldots, {\rm S}_{\rm ext,n_{\rm ext}})$
    of concentrations
    ${\bf s}_{\rm ext} \eqbydef  (s_{\rm ext,1},\ldots, s_{\rm ext,n_{\rm ext}})^T$
    that are not mass-balanced.

Finally, let us introduce the vector
${\bf y}^T \eqbydef ({\bf e}^T,{\bf m}^T)$ of concentrations of
molecular machines of size $n_y$. Typical units of concentrations
${\bf e}$, ${\bf m}$ and ${\bf p}$ are in millimoles per gram of cell
dry weight, and fluxes ${\bf v}$ in millimoles per gram of cell dry
weight per unit of time.

For a given cell growth rate $\mu\geq 0$, the RBA optimization problem
(named ${\mathcal P}_{\rm rba}(\mu)$) can be formalized mathematically
as follows. For a fixed vector of concentrations ${\bf p} \in \Rsetp^{N
n_p}$ and the given growth rate $\mu\geq 0$, $$\begin{array}{ll}
 \mbox{find possible cell states}  &   \quad  {\bf y} \in \Rsetep^{n_y},    {\bf v} \in \Rset^{n_e},  \\[0pt]
\mbox{subject to } \\
(C_{1}) &  - \rmb{\Omega} \rmb{v}  + \mu( \rmb{C}^{\rm{S}}_{\rm{Y}} \, {\bf y}  +  \rmb{C}^{\rm{S}}_{\rm{B}} \, {\bf \bar{b}} + \rmb{C}^{\rm{S}}_{\rm{P}}  \, {\bf p}) =  0   \\ [6pt]
(C_{2a})  &   \mu (\rmb{C}^{\rm{M}}_{\rm{Y}}  \, {\bf y} + \rmb{C}^{\rm{M}}_{\rm{P}} \, {\bf p}) - \rmb{K}_{\rm{T}} \, {\bf y}  \leq  0  \\[6pt]
(C_{2b})  &    -\rmb{K}^{\rm{'}}_{\rm{E}}  \, {\bf y} \leq \rmb{v}    \leq \rmb{K}_{\rm{E}} \, {\bf y}  \\[6pt]
(C_{3}) &   \rmb{C}^{\rm{D}}_{\rm{Y}} \, {\bf y} +  \rmb{C}^{\rm{D}}_{\rm{P}}  \, {\bf p} - \rmb{\bar{d}} \leq 0 
\end{array}$$

where all the inequalities are defined component-wise and:

- $\rmb{\Omega}$ is the stoichiometry matrix of the metabolic network of
  size $n_s \times n_e$, where $\rm{\Omega}_{ij}$ corresponds to the
  stoichiometry of metabolite $\rm{S}_i$ in the $j$-th enzymatic
  reaction;

- $\rmb{C}^{\rm{S}}_{\rm{Y}}$ (resp. $\rmb{C}^{\rm{S}}_{\rm{P}}$) is an
  $n_s  ~  n_y$ (resp. $n_s  ~  n_p$) matrix where each coefficient
  $\rm{C}^{\rm{S}}_{\rm{Y}_{ij}}$ corresponds to the number of
  metabolite $\rm{ S}_i$ consumed (or produced) for the synthesis of one
  machine $\rm{Y}_j$ (resp. $\rm{ P}_{j}$);
  $\rm{C}^{\rm{S}}_{\rm{Y}_{ij}}$ is then positive, negative or null if
  $\rm{ S}_i$ is produced, consumed or not involved in the the synthesis
  of one machine $\rm{Y}_j$ (resp. $\rm{ P}_{j}$);

- $\rmb{C}^{\rm{S}}_{\rm{B}}$ is an $n_s \times n_b$ matrix in which
  each coefficient $\rm{C}^{\rm{S}}_{\rm{B}_{ij}}$ corresponds to a
  metabolite $\rm{S}_i$ consumed (or produced) for the synthesis of one
  $\rm{B}_j$;

- $\rmb{K}_{\rm{T}}$ ($\rmb{K}_{\rm{E}}$ and $\rmb{K}^{'}_{\rm{E}}$,
  respectively) are matrices of size $n_m \times n_y$ ($n_e \times n_y$,
  respectively) in which each coefficient $\rm{k}_{\rm{T}_i}$
  ($\rm{k}_{\rm{E}_i}$ and $\rm{k}^{'}_{\rm{E}_i}$, respectively) is
  positive and corresponds to the efficiency of molecular machine
  $\rm{M}_i$ , i.e. the rate of the process per amount of the catalyzing
  molecular machine, (the efficiency of the enzyme $\rm{E}_i$ in forward
  and backward sense, respectively);

- $\rmb{C}^{{\rm{M}}}_{\rm{Y}}$ (resp. $\rmb{C}^{{\rm{M}}}_{\rm{P}}$) is
  an $n_m \times n_y$ (resp. $n_m \times n_p$) matrix in which each
  coefficient $\rm{C}^{\rm{M}}_{{\rm{Y}}_{ij}}$ typically corresponds to
  the length in amino acids of the machine $\rm{Y}_j$
  (resp. $\rm{ P}_{j}$). In some cases (for instance for the constraints
  on protein chaperoning), the length in amino acids can be multiplied
  by a coefficient, such as the fraction of the whole proteome that
  necessitates chaperoning;

- $\rmb{\bar{d}}$ is a vector of size $n_c$, where $n_c$ is the number
  of compartments (compartment membrane and/or compartment interior for
  which density constraints are considered. $\rm{\bar{d}}^i$ is the
  density of molecular entities within the volume or surface area.
  Densities are typically expressed as a number of amino-acid residues
  by volume or surface area.

- $\rmb{C}^{\rm{D}}_{\rm{Y}}$ (resp. $\rmb{C}^{\rm{D}}_{\rm{P}}$) is an
  $n_c \times N_y$ (resp. $n_c \times n_p$) matrix in which each
  coefficient $\rm{C}^{\rm{D}}_{{\rm{Y}}_{ij}}$ corresponds to the
  density of one machine $\rm{Y}_j$ (resp. $\rm{ P}_{j}$) in the
  compartment $i$. By construction, we have one unique localization per
  machine.

For given growth rate and medium composition, all equalities and
inequalities in our RBA problem ${\mathcal P}_{\rm rba}(\mu)$ is linear
in the decision variables $({\bf y},{\bf v})$ and is proven to be convex
[@GoelzerFromion2009; @GoelzerFromion2011b]. At given $\mu$,
${\mathcal P}_{\rm rba}(\mu)$ is a feasibility optimization problem,
where constraints ($C_1$-$C_3$) define the feasibility domain. The
feasibility domain can be empty or non-empty. If there exists a solution
$({\bf y},{\bf v})$ to ${\mathcal P}_{\rm rba}(\mu)$ -i.e. the
feasibility domain is non-empty-, then there exists a feasible resource
distribution compatible with the given growth rate. In other words, the
cell can grow at this growth rate value. By construction, the
feasibility domain of ${\mathcal P}_{\rm rba}(\mu)$ corresponds to the
set of all possible phenotypes of the cell at a growth rate $\mu\geq 0$.

We conclude this with some remarks:

1.  In practice, the vector $\rmb{\bar{b}}$ contains non-zero values
    only for the concentrations of macro-components such as DNA, cell
    wall, and lipid membranes, and for a few set of metabolites. These
    values are usually extracted from the biomass formation reaction
    used in FBA models (see Chapter ).

2.  To model reversible enzymes, we introduced two diagonal matrices
    containing the enzyme efficiencies, i.e. $\rmb{K}_{\rm{E}}$ and
    $\rmb{K}^{'}_{\rm{E}}$, describing the capacity constraints of
    enzymes in both directions. If an enzyme $\rm{E}_i$ is considered
    irreversible, $\rm{k}'_{\rm{E}_i}$ is set to $0$.

3.  In [@GoelzerFromion2011a; @GoelzerMuntel2015], an RBA model was
    built for *Bacillus subtilis*. It integrates two macromolecular
    processes in constraint $C_{2a}$, the translation and chaperoning of
    proteins, and two density constraints, the limitation of the
    cytosolic density and of the membrane occupancy. An RBA model can be
    refined by integrating for instance other cellular processes and
    molecular machines, such as the transcription machinery, the protein
    secretion apparatus (see [@GoelzerMuntel2015; @BulovicFischer2019]),
    or molecule turnover [@GoelzerFromion2019], as well as other types
    of constraints.

### Simulation and analysis of RBA models {#LAR:sec:RBA_howTo}

##### How to incorporate the medium composition.

We represent the medium composition in two aspects, namely (i)
qualitatively, by allowing exchange of the medium metabolites in the
model ($UB_{Exchange, n} > 0$). Note that some metabolites, although not
explicitly represented by the growth media, should also adhere to this
rule (e.g. oxygen, water, and protons). The (ii) quantitative
composition of the growth medium is determined by extracellular
concentrations, which, in turn, dictate the efficiencies of metabolic
transporters via Michaelis-Menten-like rate laws (as nonlinear $k(c)$
functions; see section [1.1.3](#sec:linearization){reference-type="ref"
reference="sec:linearization"}). For an extracellular nutrient
${\rm S}_{\rm ext,i}$ with concentration $\metconc_{\rm ext,i} \geq 0$,
the efficiency of the corresponding metabolic transporter(s) is given by
$\rm{k_E}(\metconc_{\rm ext,i}) = \frac{\rm{\kcat \metconc_{\rm ext,i}}}{\km + \metconc_{\rm ext,i}}$,
with parameters $\kcat$ and $\km$ for the turnover number and the
affinity of the transporter, respectively.

##### Obtaining the RBA solution for a given parameter set.

For an RBA problem with given parameters, there exists a maximal growth
rate $\growth^* \geq 0$, such that for any $\growth$,
${\mathcal P}_{\rm rba}(\growth)$ is feasible if and only if
$\growth \leq \growth^*$ [@GoelzerFromion2009; @GoelzerFromion2011b].
For a given medium composition, the maximal growth rate $\growth^*$ can
computed by using a bisection algorithm, in which a series of LP
problems are solved to narrow down the exact growth rate at which the
problem becomes infeasible. A real-life example would be simulating
growth in glucose-limited chemostat cultures under different dilution
rates $D$. With increasing $D$, the glucose availability increases, and
a set of $n$ different glucose uptake rates $q_{Glc}$ ($q_{Glc,1}$,
$q_{Glc,2}$, $\dots$, $_q{Glc,n}$) can be subjected to an RBA model to
obtain a set of optimal metabolic states ($\growth^{*}_{1}$,
$\growth^{*}_{2}$, $\dots$, $\growth^{*}_{n}$).

Together with the maximal feasible growth rate one obtains the optimal
cell configuration maximizing growth
$(\growth^*, {\bf y}^*, {\bf \flux}^*)$. The principle of optimal
performance, in this case, that a cell phenotype should maximize growth
rate, in fact, coincides with the principle of parsimonious resource
allocation between cellular processes.

##### Exploration of the feasibility domain.

Although RBA models inherently reduce the solution space due to
principle of parsimonious resource allocation, the solutions obtained
might still contain considerable flux variability. In the same vein as
Flux Variability Analysis ([@MahadevanSchilling2003], see Chapter ), the
feasibility domain can be explored at optimal ($\growth^*$) or
sub-optimal ($\growth \leq \growth^*$) growth rates. For one decision
variable $y_i$ (resp. $\flux_i$), two LP problems are solved, where
($i$) constraints $C_1$, $C_2$ and $C_3$ remain unchanged; ($ii$) the
decision variable $y_i$ (resp. $v_i$) is maximized (LP 1) and minimized
(LP 2). This operation is repeated for each decision variable to obtain
*in fine* the feasibility domain of all decision variables.

It was proven that the feasibility domain becomes smaller with
increasing growth rate [@GoelzerFromion2009; @GoelzerFromion2011b], so
it might be worthwhile to probe the solution space at slow-growth
regimes. In practice, at the optimum, the cell configuration
$(\growth^*, {\bf y}^*, {\bf \flux}^*)$ is often unique. Indeed,
non-unique solutions will exist if two alternative metabolic pathways
have exactly the same cost in resources. Since all enzymes have
different amino acid sequences, use different cofactors, are differently
localization, etc, this is highly unlikely. A caricatural example of a
model with non-unique solutions would be one in which an enzyme pool is
arbitrarily split into two, and the two new \"enzyme species\" are given
different names, although they are physically exactly the same.

### Calibration of model parameters

An RBA model may contain a high number of model parameters. First, the
global parameters to be estimated are related to cell composition: (i)
the concentrations of bulk biomass components ${\bf \bar{b}}$, which is
usually deduced from the biomass reaction of the genome-scale metabolic
network of the organism. Using quantitative proteomics data
[@BleinZivy2016], one can infer (ii) the protein densities in different
compartments ($\rmb{\bar{d}}$), and (iii) the abundance of housekeeping
(unspecified) proteins (${\bf p}$).

The next set of parameters we need to collect concerns the efficiencies
of molecular machines ($\rmb{K}_{\rm E}$,
$\rmb{K}^{'}_{\rm E}$,$\rmb{K}_{\rm T}$). As we learned in Chapters and
, the rate of an enzymatic reaction $\flux$ depends on the enzyme
efficiency or \"apparent catalytic rate\", given by
$\flux = \enzconc \kapp$, with
$\kapp = \catrate(\cv) = \kcat^{+} \cdot \eta^{\rm rev}(\cv) \cdot \eta^{\rm sat}(\cv) < \kcat^+$.
The $\kapp$ values are always below the $\kcat$ value, but may vary from
state to state depending on metabolite concentrations. Since internal
metabolite concentrations ${\bf \metconc}$ are unknown and difficult to
measure at genome-scale, we cannot estimate $\kapp$ from the explicit
kinetic law $\catrate(\cv)$. We need to obtain these $\kapp$ parameters
empirically, for example by measuring the flux $\flux$ and the protein
abundance $\enzconc$ in one condition and taking their ratio.

Hence, for a given environmental condition, efficiency parameters can be
estimated using quantitative proteomics in combination with fluxomics
[@GoelzerMuntel2015] or FBA to estimate the flux distribution
[@BulovicFischer2019]. To account for variable enzyme efficiencies, one
may make the simplifying assumption that enzyme efficiencies depend
mostly on growth rate. By estimating the enzyme efficiencies at
different growth rates and interpolating between them, one obtains
empirical relationships between efficiency and the growth rate
[@GoelzerMuntel2015] to be used in ${\mathcal P}_{\rm rba}(\growth)$.
For instance, several estimates of enzymatic efficiencies obtained in
contrasting growth conditions will provide a relationship
$\rmb{K}_{\rm E}(\mu)$ instead of a constant $\rmb{K}_{\rm E}$ value.

### Enzyme efficiencies: use of -omics data-informed $\kapp$ *vs.* naïve $\kcat$ values

The three most popular formalisms of fine-grained resource allocation
models, RBA [@GoelzerFromion2011], ME-models [@OBrienLerman2013], and
pc-models [@ElsemmanRodriguez2021], are variations on the same theme,
implementing the four major constraints discussed in Section
[1.2](#LAR:Sec:constraints){reference-type="ref"
reference="LAR:Sec:constraints"}. Thus most of the ideas, concepts, and
constraints are equivalent (or at least highly similar) in their
biological interpretation. Most of the differences arise from the
approach taken towards parametrization of these models, and
consequently, interpretation of model output. Here we will discuss an
example where implementations differ significantly.

In resource allocation models, two types of constraints define the
proteome capacity at given growth rate $\mu$, the protein density vector
${\bf \bar{b}}$, and the fraction of housekeeping proteins $\bf{p}$ in
the proteome. The remaining proteome space is to be distributed among
the proteins that are explicitly defined in the model. The RBA formalism
requires to formulate the function $k_{\rm app}(\mu)$ (or
$\rmb{K}_{\rm E}(\mu)$ in the RBA problem, Section
[1.3.2](#LAR:sec:RBA_formulation){reference-type="ref"
reference="LAR:sec:RBA_formulation"}) for every protein in the model
using -omics data (see Section
[1.3.3](#LAR:sec:RBA_howTo){reference-type="ref"
reference="LAR:sec:RBA_howTo"}), and the fraction of the
\"housekeeping\" proteins in the proteome is determined from data for
each simulation.

Conversely, the formulation of pc-models [@ElsemmanRodriguez2021] allows
more flexibility to the \"unspecified\" protein $UP$, represented by a
single artificial protein of average size and amino acid composition.
Instead of setting a fixed amount allocated to $\bf{p}$ which changes
across conditions, one can determine the *minimal* fraction of this
protein in proteome $UP_{min}$, and formulate the demand to produce $UP$
as an inequality constraint $UP \ge UP_{min}$. Interestingly, in
*Saccharomyces cerevisiae*, the proteome mass fraction occupied by
non-metabolic proteins is relatively constant under different
glucose-limited conditions, as determined by quantitative proteomics
data (see [@ElsemmanRodriguez2021], Fig. S1 for a plot).

This inequality constraint can be interpreted as the upper limit of
available protein space, i.e., under fixed protein density
${\bf y}+{\bf p} = \mbox{const}.$, the proteome not occupied by
${\bf y} \eqbydef {\bf e}+{\bf m}$ is allocated to $\bf{p}$. Since now
the model can distribute the proteome among explicitly-defined $vs.$
unspecified protein freely, the procedure of fitting $\kapp$ values is
no longer a prerequisite. Using $\kcat$ values, collected from
literature/databases/own experimental measurements, rather than apparent
$\kapp$ values, has consequences both for predictions and the data use:
first, the model prediction on the protein use is the \"demand\" of the
enzyme and is strictly coupled to the flux through the enzyme
(equivalent to the ECM1 layer of enzyme costs in the *Enzyme Cost
Minimization* method, Chapter ). Second, the condition-dependent
quantitative proteomics data can be used as validation dataset for model
predictions instead [@YangYurkovich2016], as the predicted protein
abundance is not dependent on these datasets.

Using less data for parameter fitting and redirecting these data-rich
datasets towards validation of model prediction strengthens the argument
for using resource allocation models for learning new biology, and
already has real-life examples. For instance, the discrepancies in
predicted vs. observed levels of glycolytic enzymes at glucose-scarce
conditions in [@ElsemmanRodriguez2021] inspired the same team to revisit
the question whether the high levels of glycolytic enzymes represent the
optimal expression given very low thermodynamic driving force and
undersaturation of glycolytic enzymes. Comparing predictions of *Enzyme
Cost Minimization* models with the results of the pc-model and
experimental data, [@GrigaitisTeusink2022] proposed that *S. cerevisiae*
expresses genuine excess of glycolytic enzymes in glucose-limited
conditions, meant to amply consume any glucose as soon as it appears in
the environment.

## Biomass composition as a constraint or as a prediction {#LAR:sec:compo_biomass}

Cell models describe, among other things, what a cell is composed of
(see Chapter ). In FBA, specifically, "biomass" refers to the
proportions of different molecule classes (e.g. lipids, protein, DNA,
RNA, cofactors) in 1 gram dry weight of cells, and biomass composition
needs to be defined prior to optimization. Since, at least for FBA
models of microbes, biomass production usually is the optimization
objective, the literature frequently refers to the mathematical
description of cell composition as \"biomass objective function\" (BOF).
In most cases, it is assumed that the proportions of biomass
constituents are fixed, only the total production (flux through BOF)
changes.

For the predictions of FBA models to be reliable, a realistic BOF is a
must (see Chapter ). Therefore, there is a sustained effort to
experimentally determine biomass composition, even for *E. coli*
[@SimensenSchulz2022]; for more details on the usual experimental
measurement methods, see the box in Chapter . In case supporting data
are available, the cell composition in the BOF may be described in a
more fine-grained manner for individual molecule types (e.g., individual
lipids, proteins, mRNA species, etc), or even in terms of atomic
composition (which in turn gives clues about the amounts of molecule
classes). So, overall, biomass composition acts as a global, and one of
the most stringent, constraint on the predicted solution space in
FBA-based models.

However, cell composition may greatly vary not only between
(micro-)organisms, or different cell types within the same organism, but
also for the same organism/cell type across different conditions. The
budding yeast *S. cerevisiae*, for instance, exhibits rather linear
relationships between the proportions of bulk biomass constituents as a
function of growth rate in glucose-limited cultures [@LangeHeijnen2001].
This variable composition often poses a challenge for models: just like
the uptake rates, the varying biomass composition reflects complex
global rearrangements of resources (for instance, different ribosome
content at different growth rates [@MetzlRazKafri2017] leads to changes
in RNA-to-protein ratio in the cells), and choices between metabolic
strategies (e.g. depletion of storage carbohydrates in
glucose-fermenting *S. cerevisiae* [@CanelasRas2011]).

A main advance of resource allocation models, compared to conventional
FBA models, is that only a part of the biomass composition is given as
input information just like in FBA ($\bf \bar{b}$ in RBA). The proteome
composition, on the contrary, becomes a genuine prediction of the
optimization procedure. Unlike small self-replicator models (see the
models in Chapter ), this prediction is very detailed, as the the
predicted proteome composition is represented by the sum of individual
protein abundances. Moreover, if proteins require trace elements or
cofactors (e.g. iron in iron-containing proteins) for function, the
demand and contribution to the overall biomass of these metabolites will
also be predicted by the model (as it will vary with the expression
level of those proteins).

In theory, the abundance of biomass constituents other than proteome
could be formulated in the way they become predictions of the resource
allocation models, rather than hardcoded inputs. Following the idea
implemented in the small, coarse-grained models of
[@MolenaarVanBerlo2009], one could set relationships between, e.g.,
protein density in the cells and production of lipids (in
[@MolenaarVanBerlo2009], the biological interpretation was to maintain
the surface area-to-volume ratio constant). Currently this is not widely
accepted as a standard practice, and, as we can see from the example
above, requires comprehensive experimental evidence, which, by itself,
could be interpreted still as \"input to the model\".

## Concluding remarks

In this chapter we considered whole-cell resource allocation models that
couple metabolic networks with a description of the macromolecular
machinery that is required to operate them. Compared to FBA models,
these models contain a large number of additional reactions,
metabolites, constraints, and model parameters, and, overall, offer a
fine-grained representation of cellular economy. Many of the kinetic
parameters cannot be accurately measured for individual enzymes, and/or
are condition-dependent. The quantitative nature of the predictions of
resource allocation models (and the most cellular decisions/phenotype
shifts), however, is largely due to global constraints: for instance,
when the protein density $g\ gDW^{-1}$ in a compartment reaches its
upper limit (=that compartment is fully packed with protein), the cells
switch from fully-respiratory to respiro-fermentative growth (see
[@OBrienLerman2013] for *E. coli*, or [@ElsemmanRodriguez2021] for
*S. cerevisiae*). Unlike the kinetic parameters in single reactions,
which are rather uncertain, these \"global\", cell-wide constraints are
based on more trustworthy evidence.

Thus these models still retain a reasonable compromise concerning
numerical tractability and model complexity, and can accurately predict
complex adaptations, which cannot be captured by GEMs in an autonomous
way, i.e. without the addition of empirical constraints on fluxes. A
successful use case of using resource allocation models is dissecting
iron economy, using RBA models: some proteins require iron for their
function, and the cell growth can become iron-limited in some
conditions. The RBA model was used to predict cell behavior under iron
starvation, and the predictions suggested couple of scenarios, (i) the
cell may *increase* the import of iron, but also (ii) *avoid* using
proteins that contain iron (and the pathways in which they operate)
[@GoelzerMuntel2015; @TournierGoelzer2017].

As with the biomass composition, another aspect of resource allocation
models (and FBA-based models in general) with some duality in its
interpretation is the objective function. Although its validity has been
always debated since conception, maximization of instantaneous growth
rate as the optimization objective has shown incredible success in
predicting microbial physiology. The current approach we apply for
resource allocation models still remains the FBA-based assumption that
the desired cell phenotypes are the ones maximizing instantaneous growth
rate $\growth$. This time, however, the $\growth$ is also a model
variable, so we have to apply bisection to obtain *the* optimal solution
for each parameter set we use in resource allocation models.

It is becoming more and more evident that many cell phenotypes (and
microbial species!), which we try to predict, do not actually maximize
instantaneous growth rate. For instance, most experimental research on
microbial physiology has been focused on carbon-limited (C-limited)
cultures, especially the yeast work in Delft, the Netherlands (see
[@LangeHeijnen2001; @CanelasRas2011] for examples). It seems that the
principle of growth rate maximization works very well in C-limited case,
and the success of resource allocation models to quantitatively capture
these phenotypes
[@OBrienLerman2013; @GoelzerMuntel2015; @ElsemmanRodriguez2021] affirms
this assumption. But is C-limitation descriptive of natural
environments? Let us continue the argument with yeasts as an example.

Yeasts in the wild, for instance, are often subjected to feast-famine
cycles in terms of carbon availability, and one could argue that in the
famine phase of the cycle, these yeasts should act as if they were
glucose-limited. Yet the current opinion in the yeast ecology seems to
see feast-famine cycles as a continuous, although reduced, supply of
carbon, and steer towards embracing a higher role of nitrogen (N)
limitation in natural environments instead. Currently, our understanding
of N-limited growth is not very comprehensive, and N-limitation is also
a case where the instantaneous growth rate maximization breaks down: the
pc-models of *S. cerevisiae* cannot quantitatively capture the cell
behavior under N-limited conditions.

So the selection of a suitable optimization objective can be a choice
followed by huge success, but also, the optimal solution might end up
contradicting the existing knowledge. How can we try to mitigate that?
One huge advance of resource allocation models is that at any condition,
the available solution space is greatly reduced, compared to
conventional FBA. We can argue that we have introduced a whole new set,
a whole new type of constraints into the model by accepting assumptions
stemming from the metabolism-molecular machinery coupling. In theory, we
should be able to reason further regarding any additional (even
empirical/*ad hoc*) constraints and/or additional optimization
objectives which would bring our model predictions closer to observed
biology. Just remember: fitting models is not a sin; but
nontransparent/reckless fitting is! After all, modeling is an art, and
there is no one cookbook that represents the ground truth: we should be
free to explore the secrets of biology, as unrealistic as our
assumptions are at times.

A final remark on modeling being an art. In this book, we have explored
several types of cell models of different size, detail, and assumptions
behind. This whole hierarchy and diversity of different implementations
and formalisms might seem overcomplicated and unnecessary, but it is a
mere reflection that \"one size does *not* fit all\". Hence, and we
invite (future) modelers to be creative, mix, match, and tailor
different models (and modeling types) to cover more and more biological
knowledge. The compromise between fine-grained but linear modeling
vs. complex kinetics that materialized into resource allocation models
is an inspiring example of how one can push bounds of different methods
to create mathematical representation of our mental pictures of cells.

## Recommended readings {#recommended-readings .unnumbered}

##### RBA website

Website [rba.inrae.fr](rba.inrae.fr){.uri} for further details on RBA.
Under [*Tools*](https://rba.inrae.fr/tools.html), you can find example
models and Jupyter notebooks for running them.

##### Review article on large-scale resource allocation models

K. de Becker *et al.* [\"Using resource constraints derived from genomic
and proteomic data in metabolic network
models\"](https://doi.org/10.1016/j.coisb.2021.100400) *Curr Opin Syst
Biol* 2022, 29:100400

## Problems {#problems .unnumbered}

::: exercise
The available cell space for proteins depends on the assumed space
occupied by small metabolites.

1.  What if the metabolite content of the cell has been underestimated?
    Assume that the amount of small metabolites in cells is currently
    underestimated. What problems in model predictions would arise from
    the fact? In what way would predictions (by FBA or other methods) be
    distorted?

2.  In what way would a cell, in reality, profit from a lower small
    metabolite content? Can we assume that the ratio between small
    metabolites and proteins is optimized? Describe possible aspects of
    this compromise! For inspiration, see [@TepperNoor2013].
:::
