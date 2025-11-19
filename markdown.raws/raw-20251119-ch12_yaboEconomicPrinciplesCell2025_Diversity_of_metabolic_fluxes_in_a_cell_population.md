# Diversity of metabolic fluxes in a cell population {#VAR}

::: chapterhighlights
Even in clonal populations, cells appear to be strongly heterogeneous in
terms of, e.g., protein levels, RNA levels, sizes at birth or division,
interdivision times and elongation rates. Part of this variability is
likely due to the inherent stochasticity of gene expression at the level
of single cells. It is however known that heterogeneous populations may
possess an evolutionary advantage, for instance in variable environments
or under stress. Despite appearing to be at odds with the idea of
optimality presented in the previous chapters, metabolic diversity can
be described and modeled within the constraint-based framework
introduced in the previous chapters. Specifically, a statistical
representation of heterogeneous populations can be obtained by defining
suitable probability distributions on the flux polytope. This chapter
addresses

- the different sources of variation that affect microbial metabolism
  along with the mechanisms that may favor higher variability,

- the methods devised to represent heterogeneous microbial populations
  within the framework of constraint-based models, and

- how these approaches connect to the optimality scenario presented in
  the previous chapters.
:::

## Introduction

The theory of cellular metabolism developed up to this point through
constrained-based models (CBMs) relies crucially on some type of
optimality assumption: among all viable flux states encoded in the flux
polytope by mass-balance, thermodynamic and regulatory constraints,
cells strive for those that maximize a physiologically motivated
objective function. For *E. coli* cells growing on carbon-limited
substrates, for instance, it is reasonable to take such a function to be
the growth yield. At the very least, these optimal states provide
reference points to gauge cellular behavior. In this respect, having a
good grasp of what makes a configuration of fluxes through the network
'optimal' with respect to a certain objective is rather important from a
theoretical viewpoint. On the other hand, it is not easy to prove
directly in an experiment that a certain function is *actually* being
optimized (in any physical system, let alone in a microbe or a microbial
population). An optimality assumption can usually be corroborated *a
posteriori*, e.g. by comparing optimality predictions to experimentally
measured fluxes or growth rates
[@segre2002analysis; @mori2016constrained], or indirectly, e.g. by
showing that, in a given growth medium, certain metabolic enzymes are
expressed at just the level ensuring maximal growth
[@bruggeman2020searching]. By looking at the behavior of individual
cells in a population, however, one cannot help but notice a salient
feature: their diversity. Individual cells are macroscopically
heterogeneous in terms of parameters like interdivision times,
elongation rates, sizes at birth or division, etc. This suggests that a
corresponding diversity is present at the level of intracellular
processes like cell cycle, gene expression and, of course, metabolism.
Quantitative experiments probing populations at single-cell resolution
(see Experimental Methods Box
[\[VAR:box:hdghd\]](#VAR:box:hdghd){reference-type="ref"
reference="VAR:box:hdghd"}) can nowadays characterize such a diversity
in some detail. Among the remarkable outcomes of these studies is that,
when analyzed through a lens that accounts for diversity, bacterial
growth displays signatures of universality
[@iyer2014scaling; @taheri2015cell; @kennard2016individuality],
suggesting the existence of general, system- and condition-independent
control mechanisms (e.g. of cell division and growth) that do not change
with specifics like strain, quality of medium, etc. Identifying these
mechanisms yields robust insight (and predictive capacity) into the
physiology of microbial systems (see also Chapter ).

::: Expblock
At the very minimum, quantitative experimental characterization of
cell-to-cell diversity in microbial populations requires (i) the
possibility of achieving steady-state cell growth in controlled
environments, and (ii) the possibility of identifying individual cells
within a population. The two setups that are most important for the
present chapter (and most widely used in general for the study of
cell-to-cell heterogeneity in microbial systems) are the following.

- High-resolution optical microscopy of bacteria growing on agarose
  pads. Optical microscopy is the first and still most used technique to
  address cellular individuality [@spudich1976non]. Besides giving
  direct information about the macroscopic growth dynamics of individual
  cells [@kiviet2014stochasticity; @kennard2016individuality], it can be
  used in conjunction with gene expression reporters like fluorescent
  proteins to quantify diversity in gene expression levels
  [@locke2009using] and dynamics [@young2012measuring]. Optical means
  usually allow to reliably follow the expression of a relatively small
  number of genes. In addition, however, they can also provide
  information about many other aspects of bacterial physiology, like
  motility, chemotaxis or the spatial self-organization of colonies.

- Microfluidic 'lab-on-a-chip' devices. In essence, these techniques
  allow to confine single cells or small lineages thereof in controlled
  environments for long-term data acquisition
  [@bennett2009microfluidic]. A well-known example is the 'mother
  machine' [@wang2010robust]. In a mother machine cells grow in narrow
  (ca. 1 $\upmu$m) microfluidic dead-end channels such that (a) all
  cells in the same channel are daughters of a mother cell stuck at the
  closed side of the channel; (b) a main feeding channel carries away
  cells that grow out of the length of dead-end channels (which suffice
  to contain a few cells, usually 5 to 10); and (c) nutrient in-flow and
  waste out-flow from the feeding channel ensure a constant medium in
  all dead-end channels via diffusion. This setup effectively keeps the
  population size fixed. Growing bacteria can then be imaged and
  analyzed by standard means like time-lapse microscopy to obtain the
  statistics of quantities like the interdivision time or the size at
  birth at stationarity [@taheri2015cell].

The setup of mother machines has the advantage that cells can be
followed for many more generations than on agarose pads, since the
latter tend to become overcrowded after a limited number of rounds of
divisions. On the other hand, agarose pads offer a more natural
environment for cell division. In addition to these, a host of other
techniques are being increasingly refined and used to probe single-cell
properties and behavior in bacterial populations, including single-cell
metabolomics by mass spectrometry [@shrestha2020single], nanoscale
secondary ion mass spectrometry (nanoSIMS) [@musat2016tracking], and
single-cell transcriptomics [@homberger2022ushering].
:::

It is not hard to guess why a bunch of identical cells sharing the same
medium would, say, elongate at different rates. For one, gene expression
has a stochastic component, from e.g. the random diffusion of
transcription factors to targets to the thermal noise driving the on/off
dynamics of transcription events. We also know that the cell cycle can
be highly variable [@walker2016generation]. And other 'natural' sources
of variance can be found in the dynamics of expression in genetic
circuits, aging, asymmetric partitioning of cellular resources at
division, inter-cellular interactions, and epigenetic modifications
[@ackermann2015functional]. In other terms, a degree of variability
across a population is to be expected. The question, however, is, how
can variability be reconciled with the optimality picture? And related
to this: can we explain cell-to-cell differences in terms of some other,
perhaps more involved, optimality criterion? Are there cases in which
variability is optimized? Can we describe quantitatively a microbial
population in ways that account for inter-cellular diversity? Note that
cell-to-cell variability is inherently a population-level concept.
Addressing it therefore requires a framework that is capable of clearly
distinguishing single-cell properties from population-level ones.

It is definitely possible to explain cell-to-cell variability within an
optimality framework (see Chapter ). For example, one could say that, in
appropriate conditions, all microbes in a population are optimal, but
the optima are slightly different for different cells. As a matter of
fact, optimal states in CBMs need not be isolated points belonging to
the flux polytope. There can in fact be infinitely many flux vectors
that maximize an objective function (this happens, for instance, when an
objective function attains its maxima on one of the edges or faces of
the polytope, see Figure
[1.1](#VAR:fig:FluxPolytope){reference-type="ref"
reference="VAR:fig:FluxPolytope"}).

<figure id="VAR:fig:FluxPolytope" data-latex-placement="t!">
<p><embed src="./images/VAR_FluxPolytope.pdf"
style="width:85.0%" /><br />
</p>
<figcaption>Single optimum versus multiple optima in the flux polytope –
(A) A two-dimensional flux polytope (shaded area) with non-negative
fluxes and the defining constraints shown as dashed lines. (B) The
linear objective function represented by the blue line has a unique
maximum (red dot). (C) The linear objective function, represented by the
blue line parallel to one of the constraints, has a continuous set of
maxima points which coincides with the segment shown in
red.</figcaption>
</figure>

This implies that identical cells subject to the same constraints and
sharing the same objective may end up having different metabolic
profiles despite carrying the same value for the objective function. In
this scenario, diversity is induced by a very special feature of the
objective function and, unless some other ingredient is brought into the
game to lift the degeneracy, all optimal states would be equally likely
for cells. If having an objective function of this type seems unlikely
in a high-dimensional setup such as metabolism, one may imagine a
scenario in which all cells optimize the same objective but with
slightly different constraints (i.e. in a slightly different polytope,
e.g. due to small variations in regulatory constraints, energy demands,
or nutrient uptakes). In this case, each cell would solve its own
optimization problem, ending up having, along with a different metabolic
profile, a slightly different value of the objective function. Metabolic
diversity is therefore induced by variability in the constraints. But it
is also possible that, if cells are subject to fluctuating exogenous
constraints (e.g. variable nutrient levels), they would prefer to
maximize their, say, growth rate *averaged over conditions*, especially
if fluctuations occur on faster timescales than those over which
metabolic reactions equilibrate. In such a case, the average growth rate
would be maximum (given the external variability), but other than that
every cell could carry a different growth rate and a different metabolic
profile. In this respect, one can say that diversity is now being
optimally adapted to external conditions, or one may even think that
different cells have different objective functions. This scenario,
possibly unrealistic for growing microbial populations but not for other
cell types (think for instance of the mixture of neurons with high
energy demands and glia with low energy demands in the brain), would
also lead to heterogeneous flux profiles and objectives. And so on.

It is clear from these examples that, in order to represent
heterogeneity within CBMs, one must, first and foremost, clarify the
origin of heterogeneity as much as possible. Next, it is necessary to
shift from the language of individual flux vectors belonging to the flux
polytope to that of *ensembles* of flux vectors or, more reasonably for
large populations, of *probability densities* defined on the flux
polytope. This transition is less trivial and more momentous than it
sounds and, together with the causes of variability, is the core subject
of the present chapter. We shall begin by giving a more precise
characterization of the different types and sources of diversity that
can be considered when modeling metabolic networks. Next, we shall
introduce probability densities on the flux polytope and briefly discuss
a few simple examples. We shall then address the general problem of
using probability densities to represent heterogeneity and uncertainty,
most notably that seen in empirical data. Finally, we will show how
these ideas can be used to generalize the notion of optimality to
heterogeneous populations.

## Sources of variability and uncertainty in metabolism

Metabolic heterogeneity is widespread among clonal populations of
prokaryotic and eukaryotic cells. Populations of *Escherichia coli*
display diverse cell-to-cell conversion yields of glucose into final
products, such as fatty acids and tyrosine [@xiao2016exploiting]; not
surprisingly, the intracellular concentration of co-factors, including
ATP, also vary significantly between cells [@yaginuma2014diversity].
*Saccharomyces cerevisiae* metabolic states have been observed to change
over time for each cell. For instance, a single budding yeast does
uptake oxygen before duplicating its genetic material, but it changes to
an anaerobic metabolism once DNA duplication starts in order to prevent
mutations related to free radicals [@kuang2014high]. Animal cells within
a single tissue also show heterogeneous metabolisms. Non-small cell lung
cancer display a remarkable diversity of preferred carbon sources.
Within the tumor, some cells consume glucose and produce lactate,
whereas others divert their metabolism to consume lactate as a carbon
source [@hensley2016metabolic].

The root cause of this metabolic heterogeneity is manifold, including
uneven distribution of nutrients in the environment, asymmetric cell
partitioning at division, and noise in gene expression
[@elowitz2002stochastic; @raj2008nature]. These effects are stochastic,
and prevent the determination of a cell metabolic state in advance. This
type of uncertainty is rooted in the nature of metabolism itself. We
refer to it as *objective uncertainty*.

There is however another type of uncertainty at play, one that comes
from our models of metabolism. In any metabolic network reconstruction,
there can be missing reactions [@krumholz2015sequence], errors or lack
of knowledge about the directionality of certain reactions under *in
vivo* conditions [@noor2018removing], and errors in the experimental
estimates of certain parameters --such as exchange fluxes, or the
weights of the biomass reaction [@dinh2022quantifying]. Even when using
a *bona fide* metabolic network conditioned by precisely measured
parameters, optimality principles can lead to a reduction of the viable
polytope as opposed to the identification of a single 'optimal' state
[@smallbone2009flux] (see Chapter ). This is exemplified in the network
of Fig. [1.2](#VAR:fig:MinMetabolicNetwork){reference-type="ref"
reference="VAR:fig:MinMetabolicNetwork"}.A, where the maximization of
$v_4$ only reduces the viable polytope to a subspace defined by the line
shown in Fig. [1.2](#VAR:fig:MinMetabolicNetwork){reference-type="ref"
reference="VAR:fig:MinMetabolicNetwork"}.B. Uncertainties that stem from
modeling uncertainties can be categorized as *subjective*, as they arise
solely from an observer's imperfect knowledge.

As we will see in the following, although objective and subjective
uncertainties have different sources, both can be modeled using
probability theory.

![Minimal metabolic network with multiple optima -- (A) Toy network
where the top metabolite is imported by reaction $v_1$ and processed by
reactions $v_2$ and $v_3$, which convert it into the bottom metabolite
that is then excreted via $v_4$. When fixing $v_1=10$, the maximization
of $v_4$ --a proxy of biomass growth rate-- under mass balance results
in $v_4=10$. There are however infinitely many flux vectors (defined by
the condition $v_2+v_3=10$) that are coherent with this solution,
including those indicated by red blue and green flux values. (B) The
subspace of optimal solutions forms a line (dark purple) in the space of
feasible flux vectors (Problem
[\[VAR:ex1\]](#VAR:ex1){reference-type="ref" reference="VAR:ex1"} ). The
orange-shaded triangle represents the flux polytope for
$0\leq v_1\leq 10$.](./images/VAR_MinMetabolicNetwork.pdf){#VAR:fig:MinMetabolicNetwork
width="55%"}

## Probability densities over the flux polytope

In what follows, we shall denote the convex flux polytope by
$\fluxpolytope$ and a generic flux configuration in $\fluxpolytope$ by
$\fluxv = \{\fluxi\}_{i=1}^N$. A probability density $p$ defined on
$\fluxpolytope$ is any non-negative function such that
$$\begin{equation}
\label{norm}
\int_{\fluxpolytope}p(\fluxv) d\flux_1\cdots d\flux_N\equiv\int_{\fluxpolytope}p(\fluxv)d\fluxv = 1~~.
\end{equation}$$ Notice that the integral over $\fluxpolytope$
implicitly encodes two types of constraints: mass-balance equations
(i.e. $\mathbf{Sv=0}$) and ranges of variability of the form
$v_{i,\min}\leq \fluxi\leq v_{i,\max}$ (see Chapter ). The quantity
$\int_{\fluxpolytope}d\fluxv$ represents therefore the *a priori* volume
of $\fluxpolytope$ (which, understandably, is far from simple to
calculate for high-dimensional polytopes like those corresponding to
genome-scale metabolic network reconstructions
[@braunstein2017analytic]). As usual, $p(\fluxv)$ can be interpreted as
the relative likelihood of flux configuration $\fluxv$: if we imagine
that a cell is assigned a flux configuration by "randomly sampling it
from $\fluxpolytope$" using the rule described by $p$, then
$p(\fluxv)d\fluxv$ represents the probability that the cell's flux
configuration will lie in a small volume $d\fluxv$ around $\fluxv$. It
is clear then that probability densities on $\fluxpolytope$ provide a
mathematically convenient way of describing the metabolic state of large
populations (or ensembles) of cells at a given time, provided one can
assume that cells have the same metabolic network and are subject to the
same constraints, so that $\fluxpolytope$ is the same for all of them.
For the population of cells described by $p$, the probability density
clearly contains all the statistics of metabolic fluxes, from mean
values to variances to correlations. For instance, by integrating $p$
over all fluxes except the $i$-th, one obtains the marginal probability
density of flux $\fluxi$, i.e. $$\begin{equation}
\int_{\fluxpolytope}p(\fluxv)d\fluxv_{\setminus i}=p_i(\fluxi)~~,
\end{equation}$$ where the subscript $\setminus i$ corresponds to
'except for the flux of index $i$' (so
$d\fluxv_{\setminus i} = d\flux_1\cdots d\flux_{i-1}d\flux_{i+1}\cdots d\flux_N$).
And from $p_i$ we can immediately retrieve the statistical features of
flux $\fluxi$ (e.g. mean value, variance, etc).

Let us make a few simple examples.

- If we assume that all cells in the population maximize the same
  objective function, and that there is no degeneracy in the optimal
  state, then $$\begin{equation}
  \label{dirac}
      p(\fluxv)=\delta(\fluxv-\fluxv^\star)~~, 
         
  \end{equation}$$ where $\fluxv^\star$ denotes the (unique)
  objective-maximizing flux vector and $\delta(x)$ denotes Dirac's
  $\delta$-distribution.

  ::: MathDetailblock
  For our purposes, the defining property of the $\delta$-distribution
  in one dimension is the following: if a variable $x$ is
  $\delta$-distributed around the finite value $x^\star$, then, for any
  continuous function $f$, $$\begin{equation}
      \int_{-\infty}^{+\infty}f(x)\delta(x-x^\star)dx=f(x^\star)~~.
  \end{equation}$$ This means that, intuitively, $\delta(x-x^\star)=0$
  everywhere on the real axis except at $x^\star$, where its value is
  $+\infty$. Such a function only makes sense within an integral. In
  this respect, ([\[dirac\]](#dirac){reference-type="ref"
  reference="dirac"}) should be seen as an abuse of notation, albeit a
  convenient one. There are however several ways to represent the
  $\delta$-distribution that comply with the above requirement. For
  example, one can define $$\begin{multline}
      \int_{-\infty}^{+\infty}f(x)\delta(x-x^\star)dx:=\lim_{\sigma\to 0}\int_{-\infty}^{+\infty}f(x)\frac{1}{\sqrt{2\pi\sigma^2}}\, e^{-\frac{(x-x^\star)^2}{2\sigma^2}}dx\\=\lim_{\sigma\to 0}\int_{-\infty}^{+\infty}f(x^\star+\sigma y)\frac{1}{\sqrt{2\pi}}\, \expe^{-\frac{y^2}{2}}dy=f(x^\star)~~.
  \end{multline}$$ The generalization to $n>1$ dimensions is obtained by
  straightforwardly assuming
  $\delta(\mathbf{x-x^\star})=\prod_{i=1}^n\delta(x_i-x^\star_i)$, so
  that $$\begin{equation}
  \label{uyadf}
  \int_{\mathbb{R}^n}f(\mathbf{x})\delta(\mathbf{x-x^\star})d\mathbf{x}=f(\mathbf{x^\star})~~.
  \end{equation}$$ Because the $\delta$-distribution effectively has
  non-zero probability mass only at a single point, it is reasonable to
  expect ([\[uyadf\]](#uyadf){reference-type="ref" reference="uyadf"})
  to hold also if the integral is carried out over a compact domain $D$,
  provided $\mathbf{x^\star}$ belongs to $D$. This is indeed the case,
  although the proof requires some work. For a quick guide to the many
  other interesting and useful properties of the $\delta$-distribution
  that are beyond our current scopes, see [@DeltaFunction].
  :::

- If we can make no assumption on the cells' metabolic activity other
  than it has to be compatible with the constraints encoded by
  $\fluxpolytope$, then any flux vector $\fluxv\in\fluxpolytope$ is
  equally likely to occur in a population. This means that $p$ is
  constant on $\fluxpolytope$. Specifically, its value must be equal to
  the inverse of the volume of $\fluxpolytope$: $$\begin{equation}
  \label{unif}
  p(\fluxv)=\left(\int_{\fluxpolytope}d\fluxv'\right)^{-1}~~~~~~ (\fluxv\in\fluxpolytope)~~.
  \end{equation}$$ For any given flux polytope, this distribution can be
  sampled at least in principle using the methods described in Chapter .

- Imagine having a dataset derived from a $^{13}$C labeling experiment
  (mass spectrometry) that gives the mean value $\overline{v}_i$ of
  *every* flux in the network (the average being over the population of
  cells used in the experiment), together with an experimental error
  $\sigma_i$ (which likely conflates different sources of uncertainty of
  which we may know very little, if anything at all), such that the
  experimental population-level estimate of $\fluxi$ is
  $\overline{v}_i\pm\sigma_i$. Let us assume that we know enough about
  the experiment to be able to define a flux polytope for the cell type
  ($\fluxpolytope$), and that all empirically measured averages and
  errors are in $\fluxpolytope$. Then, if we want to describe the
  population by a probability density in $\fluxpolytope$ that is uniform
  over the domain defined by experimental estimates, we can set
  $$\begin{equation}
  \label{probex}
  p(\fluxv)=\prod_{i=1}^N\frac{\theta(\overline{\fluxi} + \sigma_i - \fluxi)\theta(\fluxi - \overline{\fluxi} + \sigma_i)}{2\sigma_i}~~~~~~ (\fluxv\in\fluxpolytope)~~,
  \end{equation}$$ where $\theta(x)$ denotes the Heaviside (step)
  function defined as (Problem
  [\[VAR:ex2\]](#VAR:ex2){reference-type="ref" reference="VAR:ex2"})
  $$\begin{equation}
          \theta(x)=
          \begin{cases}
          1&\text{for $x>0$}\\
          0&\text{for $x<0$}
  \end{cases}~~.
      
  \end{equation}$$

- (Boltzmann distribution) Let $f(\fluxv)$ denote a generic function of
  the flux vector, such as $f(\fluxv) = \sum_{i=1}^N c_i \fluxi$, with
  $c_i$ prescribed constants. The Boltzmann distribution is defined as
  $$\begin{equation}
  \label{boltz}
  p(\fluxv)=\frac{1}{Z(\beta)}\,\expe^{\beta f(\fluxv)}~~~~~~ (\fluxv\in\fluxpolytope)~~,
  \end{equation}$$ where $\beta$ is a constant and $Z$ is a factor
  ensuring normalization (i.e. ([\[norm\]](#norm){reference-type="ref"
  reference="norm"})), namely
  $Z(\beta) = \int_{\fluxpolytope} \expe^{\beta f(\fluxv)}d\fluxv$. The
  behavior of $p$ is simple to grasp in three limits.

  1.  For $\beta\to 0$, ([\[boltz\]](#boltz){reference-type="ref"
      reference="boltz"}) reduces to
      ([\[unif\]](#unif){reference-type="ref" reference="unif"}): in
      other words, $p$ becomes uniform over $\fluxpolytope$ (and
      therefore insensitive to $f$).

  2.  For $\beta\to+\infty$, $p$ effectively concentrates on the flux
      vector $\fluxv^\star$ that maximizes $f$ (which for simplicity we
      assume to be unique). To see this at a heuristic level, it
      suffices to notice that, for any $\fluxv\neq\fluxv^\star$, the
      ratio $$\begin{equation}
      \frac{p(\fluxv^\star)}{p(\fluxv)}=\expe^{\beta[f(\fluxv^\star)-f(\fluxv)]}
      \end{equation}$$ increases exponentially as $\beta$ increases.
      Because densities are normalized, when this ratio becomes large,
      $p(\fluxv)$ must become very small. Hence, when integrated over
      $\fluxpolytope$, the larger is $\beta$, the closer to
      $\fluxv^\star$ must flux vectors be in order to give a significant
      contribution to the integral. For $\beta\to+\infty$, the only
      relevant contribution comes from $\fluxv^\star$, so that,
      effectively, $p(\fluxv)\simeq\delta(\fluxv-\fluxv^\star)$. This
      conclusion can be reached more precisely using Laplace's method
      (a.k.a. saddle-point approximation) to evaluate integrals of the
      form $\int_{\mathbb{R}^n}\expe^{\beta g(\mathbf{x})}d\mathbf{x}$
      in the limit $\beta\to\infty$ for fixed $n$ (see
      e.g. [@mackay2003information], Ch. 27).

  3.  By a similar reasoning, for $\beta\to -\infty$ the only relevant
      contribution to integrals involving $p$ comes from the (unique, by
      assumption) flux vector $\mathbf{v_\star}$ that *minimizes* $f$,
      so that, effectively,
      $p(\fluxv)\simeq\delta(\fluxv-\mathbf{v_\star})$.

  <figure id="VAR:fig:Boltzmann" data-latex-placement="t!">
  <p><embed src="./images/VAR_Boltzmann.pdf" style="width:50.0%" /><br />
  </p>
  <figcaption>Boltzmann distribution on the flux polytope – The Boltzmann
  distribution, Eqn (<a href="#boltz" data-reference-type="ref"
  data-reference="boltz">[boltz]</a>), morphs from a uniform probability
  density to a <span class="math inline">\(\delta\)</span>-distribution
  concentrated on the flux vector that maximizes the function <span
  class="math inline">\(f\)</span> as <span
  class="math inline">\(\beta\)</span> varies from 0 to <span
  class="math inline">\(+\infty\)</span>.</figcaption>
  </figure>

  When $\beta$ varies, things depend strongly on the form of $f$ and can
  become rather complicated when $f$ is non-linear, especially when
  terms that involve the product of two or more fluxes ('high-order
  interactions') are present. However, in the simple case in which $f$
  is linear (as outlined above), then the probability density gradually
  morphs from a uniform distribution over $\fluxpolytope$ to a
  $\delta$-distribution around the maximum of $f$ as $\beta$ increases
  from $0$ to $+\infty$ as shown in
  Fig. [1.3](#VAR:fig:Boltzmann){reference-type="ref"
  reference="VAR:fig:Boltzmann"} (and likewise when $\beta$ decreases
  from $0$ to $-\infty$). In this respect, the parameter $\beta$ can be
  seen simply as a 'degree of optimization': the closer a population is
  to optimizing $f$, the higher the value of $\beta$. For reasons that
  will become clear in the next section, the Boltzmann distribution
  plays an especially important role in this chapter (Problem
  [\[VAR:ex3\]](#VAR:ex3){reference-type="ref" reference="VAR:ex3"}).

- In Constrained Allocation FBA [@mori2016constrained] (see Chapter ),
  one considers an ensemble of growth-rate maximization problems
  constructed by sampling (from a prescribed probability density) a
  family of random variables representing the proteome fraction to be
  invested in each metabolic enzyme per unit flux of the corresponding
  reaction. The idea in CAFBA is that different sets of parameters
  effectively correspond to different cells, reflecting the cell-to-cell
  variability in e.g. transcription levels and protein abundances. The
  population-level behavior is then obtained by averaging over different
  choices of these parameters (i.e. over a population of heterogeneous
  cells). An alternative interpretation is however possible, namely that
  different parameters reflect the different environmental conditions
  that a species can encounter over its life process history. By
  averaging over parameters one obtains a growth strategy that levels
  out this environmental variability. Such a strategy may be the one
  that cells prefer to implement e.g. when environmental fluctuations
  are fast (faster than regulatory timescales). In either case, in
  CAFBA, randomness in a family of parameters related to the
  optimization problem induces randomness in the solutions, and
  therefore a probability density over the feasible space. This
  probability is unfortunately hard to write down explicitly in the case
  of CAFBA due to the complexity of the optimization problem. Its
  marginal distributions are however easy to calculate numerically. Two
  of them, specifically for the single-cell growth rate and acetate
  excretion fluxes, are shown in Fig. 2 in [@mori2016constrained].

We could provide more examples but the key message of this section
should already be visible: probability densities on the flux polytope
are useful (a) when one wants to explicitly represent how uncertainties,
experimental knowledge (with errors), or variability in parameters
impact our knowledge of what part of the flux space $\fluxpolytope$ is
occupied by the metabolic states that occur in a true microbial
population; and (b) when one is interested in representing an *optimal*
(in some sense) population in a way that explicitly accounts for
heterogeneity. If one has data (with errors), a probability density can
provide a representation of the data, as in
([\[probex\]](#probex){reference-type="ref" reference="probex"}). It can
likewise describe the solution to a population-level optimization
problem, and therefore a purely theoretical prediction, as in
([\[dirac\]](#dirac){reference-type="ref" reference="dirac"}). Or the
solution to an optimization problem with uncertainty, i.e., partial
knowledge or variability in some of the parameters, in which case it
represents an 'informed' theoretical prediction (as in the CAFBA
example, where the 'information' injected into the problem comes from
the probability density from which parameters are sampled). Or it can
simply be a tool to interpolate between extreme cases when we are unsure
about how well a certain function is being optimized (as in
([\[boltz\]](#boltz){reference-type="ref" reference="boltz"})). Notice
how, in our examples, different motivations activate different
theoretical routes, all of which lead to working with probability
densities that have *a priori* different origins and meanings even
though they can be formally the same.

The two broad motivations for working with probability densities on
$\fluxpolytope$ outlined above \[i.e. (a) representing uncertainty and
(b) representing optimal heterogeneous populations\], pose fundamentally
different modeling challenges. In the first case, the key question is
one of model selection: given some empirical knowledge, what is the
probability density on $\fluxpolytope$ that best represents our residual
uncertainty? For instance: how good of a choice for $p$ is
([\[probex\]](#probex){reference-type="ref" reference="probex"}) given
the data we had? Are there criteria that can guide our choice of a
probability density? We will briefly consider these issues in the
upcoming Sec. [\[four\]](#four){reference-type="ref" reference="four"}.
When attempting to model optimal heterogeneous populations at the
theoretical level, instead, one basically has to generalize the problem
tackled by CBMs like FBA to the case in which an optimal probability
density is searched for instead of an optimal flux configuration. We
will see how this can be done in Sec.
[\[five\]](#five){reference-type="ref" reference="five"}.

## Representing heterogeneity and uncertainty[]{#four label="four"}

### Maximum Likelihood, Maximum a Posteriori and Bayesian inference

We have seen that probability densities on $\fluxpolytope$ can
represent, under certain assumptions, populations of microbes whose
metabolism can be described by the same flux polytope, and that
different probability densities can be surmised to model the
distribution of $\fluxv \in \fluxpolytope$ when some external
information (e.g. experimental data) is available. Here, we will address
the following question: how can one choose the $p$ that best represents
our knowledge about the metabolic state of a population in presence of
these external data?

To summarize the huge and highly involved set of problems behind the
above (very general) question [@mackay2003information] in a way that is
useful for the purposes of this chapter, we can start by assuming we
have *a priori* chosen a form of $p$ that depends on certain free
parameters and ask how to tailor parameters so that $p$ 'optimally'
matches the empirical evidence. To be concrete, let us denote by
$\boldsymbol{\psi}$ the vector of parameters of $p$, and by
$\mathbf{W} =  \{\mathbf{w}^1,\mathbf{w}^2,...,\mathbf{w}^R\}$ a set of
$R$ experimental samples of $\fluxv$. Each measurement, $\mathbf{w}$, is
a vector of metabolic fluxes that ideally should include all the
reactions of a metabolic network. In practice, a vector $\mathbf{w}$
typically spans only a subset of all the reactions of the metabolic
network, e.g. those that are amenable to $^{13}$C labeling (TCA,
glycolysis, and pentose phosphate pathways) or that correspond to
exchange fluxes that can be reliably measured (glucose and oxygen
consumption, or lactate and ethanol, to name a few). According to Bayes'
rule (we assume all variables to be continuous), the quantities

- $p(\boldsymbol{\psi}|\mathbf{W})$: the conditional probability density
  of the parameters given the observations (a.k.a. the *posterior*);

- $p(\mathbf{W}|\boldsymbol{\psi})$: the conditional probability density
  of the observations given the parameters (a.k.a. the *likelihood*);

- $p(\boldsymbol{\psi})$: the prior probability density of parameters
  (a.k.a. the *prior*);

- $p(\mathbf{W})$: the (marginal) probability density of observations
  (a.k.a. the *evidence*)

are related by the formula $$\begin{equation}
 \label{bayes}
p(\boldsymbol{\psi}|\mathbf{W})=\frac{p(\mathbf{W}|\boldsymbol{\psi})p(\boldsymbol{\psi})}{p(\mathbf{W})}~~.
\end{equation}$$

Ideally, what one would like to know in order to 'optimally' set the
parameters of $p$ is how likely a parameter set is given the data,
i.e. the full posterior $p(\boldsymbol{\psi}|\mathbf{W})$, as it allows
to quantify our uncertainty on the model itself. One may however also
consider different (less ambitious) ways to choose parameters. The three
best known methods are the following:

- Maximum Likelihood (ML) inference aims at finding the parameter vector
  that maximizes the likelihood: $$\begin{equation}
  \boldsymbol{\psi}_{\mathrm{ML}}=\text{arg }\max_{\boldsymbol{\psi}}p(\mathbf{W}|\boldsymbol{\psi})~~.
  \end{equation}$$ In standard cases, this produces a single 'optimal'
  vector $\boldsymbol{\psi}$ (hence it is called a 'point estimator'),
  resulting in a $p$ that models -in a context-specific manner- the
  metabolic heterogeneity within the cellular population.

- Maximum a Posteriori (MAP) inference aims instead at finding the
  parameter vector that maximizes the posterior: $$\begin{equation}
   \label{map}
  \boldsymbol{\psi}_{\mathrm{MAP}}=\text{arg }\max_{\boldsymbol{\psi}}p(\boldsymbol{\psi}|\mathbf{W})\equiv\text{arg }\max_{\boldsymbol{\psi}}p(\mathbf{W}|\boldsymbol{\psi})p(\boldsymbol{\psi})~~,
  \end{equation}$$ where the last equality follows from the fact that
  $p(\mathbf{W})$ does not depend on $\boldsymbol{\psi}$. As for ML, the
  MAP estimator is a point estimator.

- Bayesian inference aims finally at computing the full posterior
  distribution $p(\boldsymbol{\psi}|\mathbf{W})$. It is therefore a
  'distribution estimator' rather than a point estimator.

Problem [\[VAR:ex4\]](#VAR:ex4){reference-type="ref"
reference="VAR:ex4"} should clarify the way in which point estimators
differ from (and are less informative than) distribution estimators in
practice.

::: MathDetailblock
Maximum Likelihood (ML) is the most commonly used point estimation
method. As said above, the estimated parameters,
$\hat{\boldsymbol{\psi}}$, are computed as the argument that maximizes
the likelihood of the observed data, i.e. $$\begin{equation}
\hat{\boldsymbol{\psi}} = \
%\arg\!\max_{\boldsymbol{\psi}} L(\mathbf{W} | \boldsymbol{\psi}|) =\
\arg~\!\max_{\boldsymbol{\psi}} p(\mathbf{W}|\boldsymbol{\psi}) =\
\arg~\!\max_{\boldsymbol{\psi}} \prod_{i=1}^R p(\mathbf{w}^{(i)}|\boldsymbol{\psi})=\arg~\!\max_{\boldsymbol{\psi}} \sum_{i=1}^R \log [p(\mathbf{w}^{(i)}|\boldsymbol{\psi})] ~~,\label{mle}
\end{equation}$$ where in the last step we used the fact that, as far as
the solution is concerned, maximizing $p(\mathbf{W}|\boldsymbol{\psi})$
is equivalent to maximizing its logarithm. ML takes a familiar form if
one follows, for instance, Theorell *et al.* [@theorell2017certain] in
modeling data according to a multivariate normal distribution:
$$\begin{equation}
\mathbf{w} \sim N(\mathbf{w}|\boldsymbol{\psi}) = \frac{1}{\sqrt{(2\pi)^N|\Sigma|}} {\left(-\frac{1}{2}(\bar{\fluxv}-\mathbf{w})^T \Sigma^{-1} (\bar{\fluxv}-\mathbf{w})\right)}
\end{equation}$$ The parameters encompass the mean values,
$\bar{\fluxv}$, and the covariance matrix, $\boldsymbol{\Sigma}$. That
is, $\boldsymbol{\psi} = [\bar{\fluxv},\boldsymbol{\Sigma}]$.
Accordingly, $$\begin{equation}
p(\mathbf{w}^{(i)}|\boldsymbol{\psi}) = N(\mathbf{w}^{(i)}|\boldsymbol{\psi}) = \frac{1}{\sqrt{(2\pi)^N|\Sigma|}} \expe^{\left(-\frac{1}{2}(\bar{\fluxv}-\mathbf{w}^{(i)})^T \Sigma^{-1} (\bar{\fluxv}-\mathbf{w}^{(i)})\right)}~~,
\end{equation}$$ and $$\begin{equation}
\hat{\boldsymbol{\psi}} = %&= \
%\arg~\!\max_{\boldsymbol{\psi}} \sum_{i=1}^R \log [p(\mathbf{w}^{(i)}|\boldsymbol{\psi})] \\
%&=
\arg~\!\max_{\bar{\fluxv},\boldsymbol{\Sigma}} \sum_{i=1}^R \left[ -\frac{1}{2}(\bar{\fluxv}-\mathbf{w}^{(i)})^T \Sigma^{-1} (\bar{\fluxv}-\mathbf{w}^{(i)}) - \log \left( \sqrt{(2\pi)^N|\Sigma|} \right) \right]
\label{VAR:log-mle}~~,
\end{equation}$$ which leads to the well-known weighted least squares
estimators of mean values ($\hat{\bar{\fluxv}}$) and variances
($\hat{\boldsymbol{\Sigma}}$). With $\hat{\bar{\fluxv}}$ and
$\bar{\boldsymbol{\Sigma}}$, the frequency of any vector $\mathbf{w}$
can be computed from
$N(\mathbf{w}|\hat{\bar{\fluxv}},\hat{\boldsymbol{\Sigma}})$. Standard
techniques, such as confidence intervals, can be applied to assess the
precision of $\hat{\boldsymbol{\psi}}$. Generally speaking, the larger
the number of samples, $R$, the smaller the uncertainty in
$\hat{\boldsymbol{\psi}}$.
:::

::: MathDetailblock
In metabolic network modeling $\fluxv$ is usually a vector of fluxes.
Unfortunately, the number of samples is usually very small
[@zhang2015cecafdb], which may lead to $\hat{\boldsymbol{\psi}}$
over-fitted to the sample set. One way to overcome limited sample sizes
is to regularize the estimation procedure by incorporating *prior*
information on $\boldsymbol{\psi}$ via the MAP estimation method
([\[map\]](#map){reference-type="ref" reference="map"}). The evidence
$p(\boldsymbol{\psi})$ in MAP can be used to encode the distribution of
$\fluxv$ values observed in previous experiments or formulated as a
plausible non-informative probability distribution. For example,
Heinonen *et al.* [@heinonen2019bayesian] formulated
$p(\boldsymbol{\psi})$ as a multivariate normal distribution with mean
values equal to zero, and variances for each flux adjusted to prevent
fluxes extending beyond their lower and upper bounds defined in
$\fluxpolytope$. MAP estimation can be considered as an ML estimation
whose objective function has been augmented by the prior distribution of
$p(\boldsymbol{\psi})$. In this sense, MAP estimation is a 'regularized'
ML estimation, which helps prevent overfitting.

MAP estimation however does not exploit the capacity of Bayes' theorem
to explore the full set of values that the parameters can achieve. By
producing a distribution estimation of the parameters, Bayesian
inference allows quantifying the parameters' variability. Compared to
point estimation methods, though, Bayesian inference is computationally
expensive as it requires to asses how different values of
$p(\boldsymbol{\psi})$ affect $p(\mathbf{W}|\boldsymbol{\psi})$.
Fortunately, some families of $p$ are susceptible to methods such as
Gibbs sampling or Markov Chain Monte Carlo that offer an efficient way
to compute the posterior numerically [@murphy2018machine]. This is the
case, for instance, for the truncated multivariate normal distributions
that Heinonen *et al.* [@heinonen2019bayesian] used for the likelihood
and prior functions appearing in
([\[bayes\]](#bayes){reference-type="ref" reference="bayes"}). The
posterior can then be used to derive statistical features of quantities
that depend on $\boldsymbol{\psi}$, e.g. metabolic fluxes.

In practice, most parameters underlying the mechanisms that govern
cellular metabolism -e.g., enzymes' allosteric regulation or the local
conditions within cells' organelles- remain unknown. Various hypotheses
can be advanced to close this knowledge gap. Alas, it is not uncommon to
have conflicting scenarios. For instance, to explain overflow metabolism
in *S. cerevisiae* and *E. coli*
[@Wolfe2005; @Postma1989; @Warburg1956], numerous plausible explanations
have been pushed forward, including ATP savings for the production of
non-oxidative enzymes (which by being smaller, compared to their
oxidative counterparts, require less ATP in their synthesis)
[@Molenaar2009; @Basan2015], limited uptake rates capacity
[@Zhuang2017], and an upper limit on the dissipation of Gibbs energy
[@Niebel2019]. (See [@de2020common] for an excellent review of
optimization-based explanations.) Because each mechanism can be encoded
through a different prior, it is clear that the choice of the prior is a
delicate matter in Bayesian inference. Generally speaking, the choice of
the prior becomes less and less problematic the more data we have,
i.e. the better sampling we have of the state space of the system.
However, if data is scant, the prior will leave an important imprint on
the resulting posterior. In these cases, a careful selection of the
prior is paramount. Among the methods most commonly employed are (a) the
construction of empirical priors (namely priors that encode previous
knowledge about parameters), (b) the use of so-called "non-informative
priors" (i.e. priors that reflect 'vague knowledge' about parameters,
like the fact that a certain parameter is non-negative)
[@yang1996catalog], and (c) the selection of priors based on the Maximum
Entropy principle (see below)
[@rivas2020metabolic; @gonzalez2023phenotype].
:::

### MaxEnt inference

According to the principle of Maximum Entropy (MaxEnt)
[@jaynes1957information], among all probability densities that are
consistent with given prior knowledge or data, the one having the
largest value of the entropy $$\begin{equation}
\label{entropy}
    H[p]=-\int_{\fluxpolytope}p(\fluxv)\ln p(\fluxv)d\fluxv
\end{equation}$$ is the one that best represents our knowledge about the
system. A classical intuitive justification of the MaxEnt principle is
most easily given for discrete variables [@de2018introduction].

Consider $N$ cells, each of which can be found in any of $K$ states
(what precisely defines a state is immaterial for this reasoning). Let
an assignment $\mathbf{n}=\{n(i)\}$ be given, such that $n(i)$ denotes
the number of cells in state $i$ (with $\sum_{i=1}^K n(i)=N$). Because
we can always exchange the states of two cells without changing
$\mathbf{n}$, there are multiple 'microscopic' ways to realize an
assignment $\mathbf{n}$. Combinatorics tells us that the number of
different microscopic realizations of an assignment $\mathbf{n}$ is
given by $$\begin{equation}
    \mathcal{N}(\mathbf{n})=\frac{N!}{\prod_{i=1}^K n(i)!}~~.
\end{equation}$$ If all $n(i)$'s are large enough, we can use Stirling's
approximation ($n!\simeq (n/e)^n$) to see that $$\begin{equation}
    \mathcal{N}(\mathbf{n})\simeq \expe^{NH(\mathbf{n})}~~~~~,~~~~~ H(\mathbf{n})=-\sum_{i=1}^K\frac{n(i)}{N}\ln\frac{n(i)}{N}\equiv -\sum_{i=1}^K p(i)\ln p(i)\equiv H(\mathbf{p})~~,
\end{equation}$$ where $p(i)$ denotes the fraction of cells in state $i$
(or, equivalently for us, the probability to find a cell in state $i$).
$H$ is the *entropy* of the assignment $\mathbf{n}$, and is in essence a
measure of the microscopic degeneracy that underlies a macroscopic
arrangement. The distribution $\mathbf{p}=\{p(i)\}$ carrying the largest
entropy subject to certain constraints is therefore the one having the
largest underlying microscopic degeneracy given those constraints. So,
if one were to randomly pick a microscopic state given those
constraints, the most likely macroscopic state would be the maximum
entropy distribution. In other terms, the MaxEnt distribution is the
least biased distribution compatible with the constraints, as any other
distribution satisfying the same constraints would correspond to a
smaller underlying degeneracy, thereby neglecting some feasible
(i.e. constraint-satisfying) microscopic configurations. In this
respect, a MaxEnt distribution requires the least information besides
prior knowledge (i.e. constraints). (A more detailed justification for
using the MaxEnt principle as an inference tool is given e.g. in
[@de2018introduction].) If for instance cells are assigned to states in
a completely random way, the MaxEnt distribution is the solution of
$$\begin{equation}
\label{gdssdgf}
\max_{\mathbf{p}} -\sum_{i=1}^K p(i)\ln p(i)~~~\text{subject to}~~~\sum_{i=1}^K p(i)=1~~,
\end{equation}$$ which can be found via the method of Lagrange
multipliers (Problem [\[VAR:ex5\]](#VAR:ex5){reference-type="ref"
reference="VAR:ex5"}). If other constraints are imposed, though, the
MaxEnt distribution will clearly change (Problem
[\[VAR:ex6\]](#VAR:ex6){reference-type="ref" reference="VAR:ex6"}). For
our purposes, the continuous case with entropy given by
([\[entropy\]](#entropy){reference-type="ref" reference="entropy"}) can
be seen as a straightforward generalization of the discrete one.

::: Ecoblock
Most of economic theory relies on the assumption that markets are
capable of allocating resources optimally, i.e. so that the utilities of
each of the participating agents is maximized (an assumption can can be
seen as the analog of each cell in a population maximizing its growth
rate). In order to achieve optimal states (called 'equilibria' in
economics), agents endowed with *a priori* different preferences,
resources and goals identify the actions that maximize their utilities
(e.g. transactions, trade, or production) and carry them out. This
process however can become more and more demanding as the number of
agents that take part in the market gets larger and larger, because (in
short) the set of viable transactions for each agent can become
exceedingly large. How can one describe the equilibria that arise from
these situations?

A possible approach, used at least since [@foley1994statistical], is
based on the Maximum Entropy principle. The idea, in short, is the
following. Once every agent has somehow chosen their preferred actions
(i.e. once a system-wide 'configuration of individual actions' has been
selected), the market as a whole presents a set of transactions to be
carried out that aggregate the choices of individual agents. When looked
at the aggregate level, though, each set of transactions can correspond
to more than one configuration of individual actions. (This can happen,
for instance, because agents have a degree overlap in their
characteristics which makes them indistinguishable from an economic
perspective.) If one assumes that agents choose their actions at random
from their set of viable transactions, then some sets of transactions
are bound to be more likely than others, simply because they can be
realized in more 'microscopic' ways (for instance, by interchanging
agents of the same type). It is then reasonable to think that the
likelihood of any particular set of transactions will be larger, the
larger the number of microscopic ways in which it can be realized.
Taking entropy as a measure of multiplicity, the most likely set of
transactions, then, is the one that maximizes the entropy.

A model of market where the above program is worked out in detail is
found in [@foley1994statistical]. The 'statistical equilibrium' theory
that follows from the use of the Maximum Entropy principle generalizes
the standard competitive equilibrium discussed in microeconomics by
providing a description of optimality in large markets with
heterogeneous participants. This line of work has also inspired further
developments that explicitly included agents' heterogeneity into the
theory of competitive equilibria
[@de2004statistical; @de2007typical; @bardoscia2017statistical]. To the
best of our knowledge, a similar approach has not yet been used to model
heterogeneous microbial systems.
:::

To get some grasp of the scenario that the MaxEnt rule provides within
CBMs, let us work out one especially noteworthy case, namely the MaxEnt
probability density of flux configurations with a given mean value of a
generic function $f$ of the fluxes. This probability density is the
solution of $$\begin{equation}
\max_{p(\fluxv)} 
-\int_{\fluxpolytope}p(\fluxv)\ln p(\fluxv)d\fluxv~~~~~\text{subject to}~~~\int_{\fluxpolytope}p(\fluxv)d\fluxv=1~~~\text{and}\int_{\fluxpolytope}f(\fluxv)p(\fluxv)d\fluxv=\overline{f}~~.
\end{equation}$$ To find it, we construct the functional
$$\begin{equation}
 \label{Lagrangian}
\mathcal{L}[p] = H[p] + \alpha \left[\int_{\fluxpolytope} p(\fluxv)d\fluxv - 1\right] + \beta \left[\int_{\fluxpolytope}f(\fluxv)p(\fluxv)d\fluxv - \overline{f}\right]~~,
\end{equation}$$ where $\alpha$ and $\beta$ are Lagrange multipliers for
the normalization and the mean-value-of-$f$ constraints, respectively.
Variation of $\mathcal{L}$ with respect to $p$ yields the maximum
condition $$\begin{equation}
-1 - \ln p(\fluxv) + \alpha + \beta f(\fluxv) = 0~~. \label{dLagrangian1}  
\end{equation}$$ Solving for $p$ results in $$\begin{equation}
 \label{entropy_p1}
p(\fluxv) = \frac{\expe^{\beta f(\fluxv)}}{ \expe^{1-\alpha}} ~~.
\end{equation}$$ The normalization condition however determines the
value of $\alpha$, as one must have $$\begin{equation}
\int_{\fluxpolytope} \expe^{\beta f(\fluxv)}d\fluxv = \expe^{1-\alpha}\equiv Z(\beta)~~.\label{betaTerm}
\end{equation}$$ One is then left with $$\begin{equation}
 \label{entropy_p2}
p(\fluxv) = \frac{1}{Z(\beta)}\,\expe^{\beta f(\fluxv)}~~~~~~ (\fluxv\in\fluxpolytope)~~.
\end{equation}$$ The value of $\beta$ must be determined from the
constraint on the mean value, namely from $$\begin{equation}
\frac{1}{Z(\beta)}\int_{\fluxpolytope} f(\fluxv) \expe^{\beta f(\fluxv)}d\fluxv=\overline{f}~~.
\end{equation}$$ Notice that the result is nothing but Boltzmann's
distribution ([\[boltz\]](#boltz){reference-type="ref"
reference="boltz"}). We have therefore found that
([\[boltz\]](#boltz){reference-type="ref" reference="boltz"}) is the
MaxEnt distribution for a given mean value of the function $f$. This
means that if we have a dataset returning the empirical mean value of an
observable $f$ over a population of cells, our knowledge is best
represented by assuming that $p(\fluxv)$ is of the form
([\[boltz\]](#boltz){reference-type="ref" reference="boltz"}), with
$\beta$ ensuring the matching of empirical and theoretical means.

This suggests a possible way to represent single-cell growth-rate
distributions [@de2016growth], such as the *E. coli* populations growing
in rich media studied e.g. in
[@taheri2015cell; @kennard2016individuality] (see Figure
[1.4](#VAR:fig:MaxEnt){reference-type="ref"
reference="VAR:fig:MaxEnt"}).

<figure id="VAR:fig:MaxEnt" data-latex-placement="t!">
<p><embed src="./images/VAR_MaxEnt.pdf" style="width:75.0%" /><br />
</p>
<figcaption>MaxEnt modeling of single-cell growth rate distributions –
Empirical distributions (blue points, left) are reproduced by a MaxEnt
assumption where the mean growth rate is constrained (right), leading to
a Boltzmann distribution over the flux polytope (Eq. <a href="#boltzl"
data-reference-type="eqref"
data-reference="boltzl">[boltzl]</a>).</figcaption>
</figure>

Let us assume that all cells in the population can be described by the
same flux polytope $\fluxpolytope$ and let $\lambda(\fluxv)$ denote the
growth rate associated to flux configuration $\fluxv$. We can ask the
following question: what is the $p(\fluxv)$ on $\fluxpolytope$ that best
represents our knowledge that the mean growth rate of cells is
$\overline{\lambda}$ (empirical)? The answer is $$\begin{gather}
\label{boltzl}
p(\fluxv)=\frac{1}{Z(\beta)}\, \expe^{\beta \lambda(\fluxv)}~~~~~~ (\fluxv\in\fluxpolytope)~~,
\end{gather}$$ where
$Z(\beta)=\int_\fluxpolytope \expe^{\beta \lambda(\fluxv)}d\fluxv$, and
where $\beta$ is set so that the empirical mean growth rate
($\overline{\lambda}$) matches the theoretical mean, i.e.
$$\begin{gather}
\frac{1}{Z(\beta)}\int_{\fluxpolytope}\lambda(\fluxv) \expe^{\beta \lambda(\fluxv)}\,d\fluxv=\overline{\lambda}~~.
\end{gather}$$ We can therefore solve the above equation (numerically)
and analyze the resulting distribution. One sees from
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}) that
$\beta$ has a 'natural' unit given by $\lambda_{\max}^{-1}$, the inverse
maximum growth rate achievable in $\fluxpolytope$ (which is easily
computed by LP). In the populations analyzed in [@de2016growth], the
value of $\beta$ that ensures the matching condition ranges from
$190/\lambda_{\max}$ to $300/\lambda_{\max}$, suggesting that indeed the
degree of optimization of $\lambda$ is significant. The most remarkable
result, however is that the marginal distribution of the growth rate
computed from ([\[boltzl\]](#boltzl){reference-type="ref"
reference="boltzl"}), namely $$\begin{gather}
\label{poflam}
p(\lambda)=\int_\fluxpolytope\delta(\lambda-\lambda(\fluxv))p(\fluxv)d\fluxv~~,
\end{gather}$$ matches the overall empirical growth-rate distributions.
In other words, if one adjusts the parameter of
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}) so that
the theoretical mean growth rate and the experimental one coincide, then
([\[poflam\]](#poflam){reference-type="ref" reference="poflam"})
reproduces the entire empirical growth-rate distribution. This
observation confirms the empirical evidence that the variance of
single-cell growth-rate distributions is a function of the mean, such
that, if growth rates are re-scaled by the mean, distributions roughly
collapse on 'universal curves'
[@taheri2015cell; @kennard2016individuality]. In addition, the analysis
of [@de2018statistical] has shown that predictions for individual fluxes
obtained from ([\[boltzl\]](#boltzl){reference-type="ref"
reference="boltzl"}) (i.e. mean values plus standard deviations) provide
a better fit to experimentally measured fluxes than growth-rate
maximizing fluxes obtained from FBA. This is especially important as it
suggests that, despite the relatively high degree of optimization, the
cell-to-cell variability underlied by
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}) is
biologically relevant.

In the following section we will use this observation as a springboard
for the analysis of optimal heterogeneous populations.

## Representing optimal populations[]{#five label="five"}

Let us start from a rather abstract question. Suppose that an organism
is actually maximizing a certain function $F$, unknown to us, which
depends on metabolic fluxes $\fluxv$ as well as on a set of other
variables $\mathbf{w}$ that are not part of metabolism:
$F\equiv F(\fluxv,\mathbf{w})$. We shall denote by
$\fluxv^\star,\mathbf{w}^\star)$ the (supposedly unique) configuration
of variables where $F$ attains its maximum. Let's furthermore say that
we have a guess for what the organism's objective function might be, and
that this guess is only a function of metabolic fluxes, which we denote
by $f\equiv f(\fluxv)$. If we trust our guess, and if $f$ is maximized
by the (supposedly unique) flux vector $\widehat{\fluxv}$, our
prediction for the fluxes would be $\widehat{\fluxv}$. Question: what is
the probability that $\widehat{\fluxv}$ is the true optimum, i.e. that
$\widehat{\fluxv}=\fluxv^\star$? Note that
$f(\fluxv^\star)\equiv f^\star<\widehat{f}\equiv f(\widehat{\fluxv})$
(i.e. at the 'true' optimum the value of $f$ is bound to be smaller than
the maximum value of $f$).

The answer goes like this: according to the MaxEnt principle, the
probability density $p(\fluxv)$ for any flux configuration $\fluxv$ to
be the true state of the system (i.e. the true optimum) should be
undetermined other than by our knowledge that the real optimum has some
value of $f$ below $\widehat{f}$. What is the correct constraint to
enforce (besides normalization) if we are to look for such a
$p(\fluxv)$? We could impose that allowed configurations strictly have
some fixed value of $f<\widehat{f}$. This choice would lead to a uniform
density over all states with a given value of $f$. In this way, though,
we are imposing that states with a different value of $f$ are strictly
inaccessible, which is not part of our knowledge. However, if we impose
that only the mean value of $f$ is constrained, MaxEnt will return a
probability density with the exact same mean value as the uniform
density just described (by construction) but a much larger entropy, just
because --intuitively-- it will assign a non-zero probability to all
states. Hence, as long as we have no other information, the best
prediction we can make for $p(\fluxv)$ is given by the probability
density that maximizes the entropy $H[p]$ subject to the constraint
$\langle f\rangle\equiv \int_\fluxpolytope p(\fluxv)f(\fluxv)d\fluxv=f^\star$,
i.e. by the solution of $$\begin{equation}
\max_p ~-\int_\fluxpolytope p(\fluxv)\ln p(\fluxv) d\fluxv~~~\text{subject to}~~ \int_\fluxpolytope p(\fluxv)d\fluxv=1 ~~\text{and}~~\int_\fluxpolytope p(\fluxv)f(\fluxv)d\fluxv=f^\star~~.
\end{equation}$$ We now know the result to be given by
([\[boltz\]](#boltz){reference-type="ref" reference="boltz"}), i.e.
$$\begin{gather}
\label{boltz2}
p(\fluxv)=\frac{1}{Z(\beta)}\, \expe^{\beta f(\fluxv)}~~~~~~ (\fluxv\in\fluxpolytope)~~,
\end{gather}$$ where $\beta$ is the Lagrange multiplier enforcing the
constraint $\langle f\rangle=f^\star$. What this means in practice is
this: if one is modeling a microbe's metabolism and is unsure about the
objective function but has a guess ($f$), information theory suggests
that the best one can do is to assume that metabolic flux configurations
are selected according to ([\[boltz2\]](#boltz2){reference-type="ref"
reference="boltz2"}). Ideally, the value of $\beta$ for which one
obtains the best agreement between predictions based on sampling
([\[boltz2\]](#boltz2){reference-type="ref" reference="boltz2"}) and
experiments is the 'degree' to which the system optimizes $f$. If $f$ is
the true objective function, then the agreement between theory and
experiments will get better and better as $\beta$ increases. It is
important to keep in mind that (i) while we have assumed that the
organism is actually maximizing something, we didn't really use the fact
that $F$ is maximized at $(\fluxv^\star,\mathbf{w}^\star$) (only that
the true state of the system has some value of $f$ below $\widehat{f}$);
(ii) this is a totally ideal situation (for instance, experimental data
have errors, so whether comparisons between theory and experiments are
informative doesn't only depend on the theory but also on the quality of
the data).

The fact that ([\[boltz2\]](#boltz2){reference-type="ref"
reference="boltz2"}) is 'optimal' in a rather fundamental sense (*a
priori* different from the sense in which $f$-maximizing populations are
optimal) encourages to view distributions described by
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}) through
a different lens. When we maximize the entropy at fixed mean growth
rate, in practice, we are looking for the 'broadest' probability density
(i.e. the most variable population) on $\fluxpolytope$ that is
compatible with the given mean. In other terms, we are saying that,
given a mean growth rate, the optimal population is the one that has the
largest possible variability. To quantify variability in a more readily
understandable way, it is convenient to transform it into a measure of
the amount of information encoded in $p$. One can reason as follows: if
no prior information is available about the population, uncertainty is
maximal and all flux vectors in $\fluxpolytope$ must be considered to be
equally likely. This means that, for such a population, the probability
density over $\fluxpolytope$ is uniform (see
([\[unif\]](#unif){reference-type="ref" reference="unif"})). We shall
denote the entropy of the uniform distribution over $\fluxpolytope$ by
$H(0)$. When we inject information into the problem (e.g. the fact that
the population has a certain mean growth rate), then the probability
density is no longer uniform but given, say, by
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}). The
uncertainty is therefore reduced by $H(0)-H(\beta)$, where $H(\beta)$ is
the entropy of ([\[boltzl\]](#boltzl){reference-type="ref"
reference="boltzl"}). (Clearly, $H(0)$ is just the entropy of
([\[boltzl\]](#boltzl){reference-type="ref" reference="boltzl"}) for
$\beta=0$.) The quantity $$\begin{equation}
\label{infoc}
I=\frac{H(0)-H(\beta)}{\ln 2}
\end{equation}$$ denotes the amount of information (in bits, hence the
factor $\ln 2$) injected by a non-zero value of $\beta$. Re-formulating
our population-level optimization, we can say that, for any fixed mean
growth rate $\langle\lambda\rangle$, the optimal population is the one
carrying the smallest value of $I$. A short calculation (Problem
[\[VAR:ex7\]](#VAR:ex7){reference-type="ref" reference="VAR:ex7"}) shows
that $\langle\lambda\rangle$ and $I$ are related by $$\begin{equation}
\label{VAR:iufefhkjgs}
\beta\langle\lambda\rangle=I\ln 2+\int_0^\beta\langle\lambda\rangle d\beta'~~,
\end{equation}$$ where it should be noted that $\langle\lambda\rangle$
is an increasing function of $\beta$ (as $\beta$ increases, the density
gets more and more concentrated around the growth-rate maximizing flux
vector, thereby leading to an increase of $\langle\lambda\rangle$).

<figure id="VAR:fig:Fitness" data-latex-placement="t!">
<p><embed src="./images/VAR_Fitness.pdf" style="width:50.0%" /><br />
</p>
<figcaption>Fitness-information bound (general form) – The orange line
encodes the maximum mean growth rate achievable for any given value of
the information content <span class="math inline">\(I\)</span> (Eq. <a
href="#infoc" data-reference-type="eqref"
data-reference="infoc">[infoc]</a>) of a metabolic flux distribution (or
the minimum value of <span class="math inline">\(I\)</span> required to
achieve any given mean growth rate).</figcaption>
</figure>

The curve $\langle\lambda\rangle$ versus $I$ described by
([\[VAR:iufefhkjgs\]](#VAR:iufefhkjgs){reference-type="ref"
reference="VAR:iufefhkjgs"}) can therefore be computed numerically for
any metabolic network reconstruction (as the only ingredients required
are encoded in the flux polytope $\fluxpolytope$) [@de2016growth]. The
resulting line (see Figure [1.5](#VAR:fig:Fitness){reference-type="ref"
reference="VAR:fig:Fitness"}) separates the $(\langle\lambda\rangle,I)$
plane in a viable (achievable) region and a forbidden region where the
mean growth rates are too large for the amount of information encoded in
the population. This 'phase diagram' yields, first and foremost, a
general prediction linking the mean growth rate (fitness) of a microbial
population to its metabolic heterogeneity: all populations must have
fitness-heterogeneity values in the viable region. Recent work relying
on an advanced statistical inference framework has shown that actual
microbial populations indeed lie in the viable part of the plane
[@muntoni2022relationship]. In addition, it provides a quantitative
definition of an optimal population that accounts for variability:
optimal populations have fitness-heterogeneity pairs that lie on the
boundary between the viable and the forbidden region. In this respect,
results from
[@de2016growth; @de2018statistical; @muntoni2022relationship] can be
summarized by saying that heterogeneous, faster-growing *E. coli*
populations (mean growth rate larger than roughly 1/h, richer growth
media) are very close to optimality, while slower-growing ones tend to
have mean growth rates and information contents that get more and more
sub-optimal the less rich is the growth medium. (Of course, this notion
of optimality refers to the growth rate and information content as the
key parameters to evaluate a population's performance. It may well be,
and this is an issue definitely worth exploring, that slower-growing
population are optimal with respect to some other parameter(s).) At any
rate, the above definition of optimality coincides with the standard one
(growth-rate maximization) for $\beta\to +\infty$, in which case
variability goes strictly speaking to zero as all cells collapse on the
same flux configuration. And we now understand how it generalizes it: by
stressing the way in which heterogeneous populations can be optimal
despite growing at sub-maximal rates.

For later convenience, note that, because the entropy is a convex
functional, the solution to the MaxEnt problem is the same as the
solution to $$\begin{equation}
\label{optii}
\max_p ~ \int_\fluxpolytope p(\fluxv)\lambda(\fluxv)d\fluxv
~~~\text{subject to}~~ \int_\fluxpolytope p(\fluxv)d\fluxv=1 ~~\text{and}~~-\int_\fluxpolytope p(\fluxv)\ln p(\fluxv) d\fluxv=H^\star~~.
\end{equation}$$ The above problem has perhaps a more direct
interpretation: the optimal population is the one that has the largest
mean growth rate at fixed variability (entropy) or, equivalently, at
fixed information content.

Before moving on, we notice that, in the above setting, optimality of
heterogeneous populations has a rather simple mechanistic interpretation
in terms of how populations 'occupy' the flux polytope. If one considers
the uniform distribution on $\fluxpolytope$,
Eq. [\[unif\]](#unif){reference-type="eqref" reference="unif"}, and
calculates the marginal distribution for the growth rate
(i.e. [\[poflam\]](#poflam){reference-type="eqref" reference="poflam"}),
one finds that the growth-rate landscape in which populations grow is
extremely skewed towards slow growth rates: the overwhelming majority of
metabolic flux configurations corresponds to slow-growing cells,
i.e. with growth rates roughly two orders of magnitude below
$\lambda_{\max}$. This implies that, whatever flux vector we are in, a
small random change to it is overwhelmingly more likely to decrease our
growth rate than increase it. In this respect, slow states have an
'entropic' advantage over fast states. On the other hand, by definition,
fast-growing flux configurations replicate faster than slow-growing
ones, and therefore have a replicative advantage. It is therefore
tempting to interpret the probability density
[\[boltzl\]](#boltzl){reference-type="eqref" reference="boltzl"} as
resulting from the balance between these two tendencies. One can for
instance imagine that a microbial population grows and evolves in time
in $\fluxpolytope$ due to (i) replication events, and (ii) small random
changes of the flux vector (due e.g. to gene expression noise). Ref.
[@de2016growth] has indeed shown that such a population evolves toward a
distribution very close to ([\[boltzl\]](#boltzl){reference-type="ref"
reference="boltzl"}), where the role of $\beta$ is played by the inverse
rate of diffusion of the population in $\fluxpolytope$, that is, by the
inverse of the rate at which small random changes occur: fast rate
implies small $\beta$, and vice versa. (As the mathematical analysis of
this scenario requires the toolbox of non-linear Fokker-Planck
equations, it is beyond the scopes of this chapter.)

The above theory can be extended in various directions. We shall limit
ourselves to one example here, namely that of optimal populations in
fluctuating environments [@muntoni2022optimal]. The basic assumption we
make is that the growth rate $\lambda$ is a function of both the flux
vector $\fluxv$ and of a single (for simplicity) exogenous variable
$s\geq 0$ representing the stress level to which the population is
subject: $\lambda\equiv\lambda(\fluxv,s)$. We furthermore assume that
$s$ is a random variable with probability density $P(s)$. For any value
of $s$, $\lambda$ will be maximized by a certain flux vector
$\fluxv^\star\equiv\fluxv^\star(s)$. If fluctuations of $s$ are
sufficiently slow, then cells may be able to perfectly adapt their
metabolic response to every value of $s$ they encounter. But this is
unlikely to be possible in rapidly fluctuating environments. In the
latter case, it is instead reasonable to assume that cells will try to
maximize their average growth rate, where the average is taken over the
distribution of $s$. The relevant quantity is now the probability
density to observe a certain flux configuration $\fluxv$ given that the
state of the environment is $s$ ($p(\fluxv|s)$), while the objective
function (to be maximized over $p(\fluxv|s)$) is just $$\begin{equation}
    \langle\lambda\rangle=\int ds\,P(s)\int_\fluxpolytope p(\fluxv|s)\lambda(\fluxv,s)d\fluxv~~.
\end{equation}$$ We should now specify the constraints. One is simple
and concerns normalization: $\int_\fluxpolytope p(\fluxv|s)d\fluxv$
should be equal to one for all $s$. To introduce the second one, we note
that, because one expects $\fluxv$ to encode information about the
environment, it is convenient to constrain the mutual information of
$\fluxv$ and $s$, i.e. $$\begin{equation}
    I(\fluxv;s)=\int ds\,P(s)\int_\fluxpolytope p(|s)\log_2 \frac{p(\fluxv,s)}{p(\fluxv)P(s)} d\fluxv~~,
\end{equation}$$ where $p(\fluxv,s)=P(s)p(\fluxv|s)$ is the joint
distribution of $\fluxv$ and $s$, whereas
$p(\fluxv)=\int ds P(s) p(\fluxv|s)$. Clearly, $I=0$ if $p(\fluxv,s)$
factorizes over $\fluxv$ and $s$ and it gets larger and larger as
$\fluxv$ and $s$ become more and more correlated. Putting these pieces
together, we can write the cell's optimization problem as
$$\begin{multline}
\label{jkhgjhvhrbjkh}
\max_{p(\fluxv|s )} ~ \int ds\,P(s)\int_\fluxpolytope p(\fluxv|s)\lambda(\fluxv,s)d\fluxv
~~~\text{subject to}~~ \int_\fluxpolytope p(\fluxv|s)d\fluxv=1~~(\forall s)\\ ~~\text{and}~~\int ds\,P(s)\int_\fluxpolytope p(\fluxv|s)\log_2 \frac{p(\fluxv|s)}{p(\fluxv)} d\fluxv=I^\star~~.
\end{multline}$$ A comparison with
([\[optii\]](#optii){reference-type="ref" reference="optii"}) should
clarify how the above generalizes the previously discussed optimization
framework. Again using the method of Lagrange multipliers one finds that
the optimal probability density is now given by (Problem
[\[VAR:ex8\]](#VAR:ex8){reference-type="ref" reference="VAR:ex8"})
$$\begin{eqnarray}
\label{pags}
p(\fluxv|s)=\frac{p(\fluxv)}{Z(s,\beta)}\,\, \expe^{\beta \lambda(\fluxv,s)}~~,
\end{eqnarray}$$ where $$\begin{eqnarray}
Z(s,\beta)=\int_\fluxpolytope d\fluxv\, p(\fluxv) \,\expe^{\beta \lambda(\fluxv,s)} \label{pags2}~~,%\equiv \qavg{\expe^{\beta \mu(q,s)}}~~.
\end{eqnarray}$$ while $\beta$ is a Lagrange multiplier.

The meaning of ([\[pags\]](#pags){reference-type="ref"
reference="pags"}) is straightforward: when $\beta\to 0$, the metabolic
flux configuration $\fluxv$ becomes independent of $s$, implying $I=0$.
As $\beta$ increases, $\fluxv$ and $s$ get more and more correlated,
while $p^\star(\fluxv|s)$ tends to get more and more sharply peaked
around $\fluxv^\star(s)$. In the limit $\beta\to+\infty$ cells respond
to each value of $s$ by selecting the exact flux configuration that
maximizes $\lambda$. To achieve this, maximal $I$ is required. A
detailed study of the optimal probability density emerging in this case
within a highly coarse-grained model of metabolism has been carried out
in [@muntoni2022optimal], showing how complex metabolic strategies
(including the coexistence of slow-growing, persistent states with
fast-growing ones) arise as optimal responses to a fluctuating
environment.

## Concluding remarks

Metabolic variability in cell populations has, as we have discussed,
multiple origins, both rooted in unavoidable stochastic effects and
(possibly) in the fact that, in certain cases, being heterogeneous can
be optimal for a microbial population. Models can account for
variability by representing (sufficiently large) populations via
probability densities defined on the flux polytope. Two main (different)
goals can be achieved. First, one can look for the probability density
that yields the best (in a precise sense) description of a set of
empirical data. Methods like Maximum Likelihood and Maximum Entropy
provide different, albeit related, approaches to this task. Second, one
can formulate optimization problems for populations, whose general
solution is a probability density rather than a single flux
configuration. Solutions to these problems can highlight how fitness and
variability are related in optimal populations, providing useful
theoretical benchmarks for real microbial systems. While possibly more
demanding from a mathematical viewpoint (and certainly more demanding
from a computational viewpoint), these approaches expand the scope of
CBMs, including in terms of predictive power. In addition, they can
refine the notion of optimality and provide insights into the
fundamental principles that govern the organization of metabolism across
populations. The question of whether variability confers an advantage to
microbial populations is however very general, and goes beyond the
metabolic level of CBMs on which we focused here. A broader discussion
of these aspects is presented in Chapter .

## Recommended readings {#recommended-readings .unnumbered}

- Gardiner, C. (2009) *Stochastic Methods: A Handbook for the Natural
  and Social Sciences*. Springer Series in Synergetics (Springer,
  Berlin)

- Jaynes, E. T. (1957) Information theory and statistical mechanics.
  Physical Review, 106:620

- MacKay, D. J. (2003) *Information theory, inference and learning
  algorithms* (Cambridge University Press)

- De Martino, A., & De Martino, D. (2018) An introduction to the maximum
  entropy approach and its application to inference problems in biology.
  Heliyon, 4:e00596

- Scharfenaker, E., & Yang, J. (2020). Maximum entropy economics. The
  European Physical Journal Special Topics, 229:1577-1590

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
Use the model in
Fig. [1.2](#VAR:fig:MinMetabolicNetwork){reference-type="ref"
reference="VAR:fig:MinMetabolicNetwork"} to study different objective
functions, specifically combinations of fluxes. Can you find other cases
in which the optimum is not unique?[]{#VAR:ex1 label="VAR:ex1"}
:::

::: exercise
[]{#VAR:ex2 label="VAR:ex2"} Show that, for a real variable $x$, a
continuous function $f$ and upon integration over $\mathbb{R}$,
$\frac{d}{dx}\theta(x)=\delta(x)$. Hint: Use the fact that
$\frac{d}{dx}[\theta(x)f(x)]=\theta'(x)f(x)+\theta(x)f'(x)$.
:::

::: exercise
[]{#VAR:ex3 label="VAR:ex3"}

Using the sampling methods introduced in Chapter . and a linear
objective function of your choice, write a program that will sample a
toy two-dimensional flux polytope according to
([\[boltz\]](#boltz){reference-type="ref" reference="boltz"}), and check
the outcome for a few values of $\beta$. Then try changing the shape of
the polytope in different ways by changing the constraints. What
features of the polytope can make sampling harder and/or less accurate
(i.e. require a larger number of samples)? Can you work out a
modification of the sampling algorithms that alleviates these problems?
:::

::: exercise
[]{#VAR:ex4 label="VAR:ex4"} Consider a Bernoulli random variable with
parameter $\psi$, i.e. such that the probability of having $k$ successes
in $n$ trials given $\psi$ is $$\begin{equation}
p(k|\psi)={n\choose k}\psi^k(1-\psi)^{n-k}~~,
\end{equation}$$ and assume that the prior for $\psi$ is a
$\beta$-distribution with parameters $a$ and $b$, i.e.
$$\begin{equation}
p(\psi)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}\,\psi^{a-1}(1-\psi)^{b-1}~~.
\end{equation}$$ Calculate the full posterior $p(\psi|k)$ and the MAP
estimator for $\psi$ as a function of $k$, $n$, $a$ and $b$. Then assume
$a=b=2$ and compare the following situations: (i) a Bernoulli process
that returned 2 successes in 3 trials; (ii) a Bernoulli process that
returned 20 successes in 33 trials. Show that the MAP estimator for
$\psi$ is 60% for both (i) and (ii) (so the two processes are
indistinguishable to MAP), while the posterior is different. Knowing the
posterior, which process would you pick if you were asked to point to
the one that is more likely to have $\psi=0.6$?
:::

::: exercise
[]{#VAR:ex5 label="VAR:ex5"} Show that the solution of the maximization
problem ([\[gdssdgf\]](#gdssdgf){reference-type="ref"
reference="gdssdgf"}) is the uniform distribution $p(i)=1/K$ for all
$i$.
:::

::: exercise
[]{#VAR:ex6 label="VAR:ex6"} Assume that a certain real variable $x$
takes values $x(i)$ in the $K$ states (one can for instance think of
$x(i)$ as the growth rate of cells in state $i$). Show that the MaxEnt
distributions for constraints imposed on (i) normalization of the
distribution, (ii) normalization and mean value of $x$, (iii)
normalization, mean value of $x$ and second moment of $x$, and (iv)
normalization and mean of the logarithm of $x$, are, respectively,
uniform, exponential, Gaussian, and power-law.
:::

::: exercise
[]{#VAR:ex7 label="VAR:ex7"} Retrieve formula
([\[VAR:iufefhkjgs\]](#VAR:iufefhkjgs){reference-type="ref"
reference="VAR:iufefhkjgs"}).
:::

::: exercise
[]{#VAR:ex8 label="VAR:ex8"} Retrieve formula
([\[pags\]](#pags){reference-type="ref" reference="pags"}) (hard).
:::
