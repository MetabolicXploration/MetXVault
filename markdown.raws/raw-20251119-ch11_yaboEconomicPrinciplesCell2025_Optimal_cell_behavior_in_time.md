# Optimal cell behavior in time {#TIM}

::: chapterhighlights
- Microorganisms live in continually changing environments, which
  require them to develop adaptation strategies.

- These strategies have been profitably studied under the assumption
  that microorganisms have evolved to optimize one or several aspects of
  their adaptive response.

- The mathematical formalization of this assumption leads to dynamic
  optimization problems that can be solved by means of techniques from
  optimal control theory.

- The chapter discusses three example problems: dynamic optimization of
  enzyme expression in metabolic pathways, dynamic optimization of
  coarse-grained models of cellular growth, and dynamic flux balance
  analysis.

- The results obtained for these problems illustrate the interest of
  studying adaptation strategies from the perspective of dynamic
  optimization, and the strengths and weaknesses of this approach.
:::

## Introduction {#TIM:Sec:Introduction}

The study of microorganisms in the laboratory has often focused on the
creation of stable conditions enabling balanced, reproducible growth of
the population. Such conditions are almost never found in nature.
Microorganisms live in continually changing environments in which
nutrients are only intermittently available and in which the cells are
submitted to a variety of other temporally varying stresses (acidity,
temperature, drought, \...). In order to survive in these conditions,
microorganisms have developed a range of molecular mechanisms to detect
changes in the environment, or signals announcing such changes, and to
adapt their functioning accordingly.

A well-studied example of the dynamic response of bacteria to changes in
their environment is the phenomenon of diauxic growth, discovered by
Jacques Monod ([@Monod49] (see also Chapter ). When *Escherichia coli*
is grown in a medium containing a mixture of two carbon sources, *e.g.*,
glucose and lactose, the cells generally first deplete the carbon source
supporting the highest growth rate (glucose) before starting to
assimilate the other carbon source (lactose). A variety of mechanisms
are involved in this switch from a preferred to a secondary carbon
source, including the release of the repression of enzymes necessary for
lactose utilization, the release of the inhibition of lactose
transporters, and the global regulation of a large number of other genes
[@Goerke08; @Kremling15].

In many situations, the precise functioning of the molecular mechanisms
regulating the adaptation of microbial physiology to changes in the
environment is not or only qualitatively understood. This precludes
their inclusion in quantitative models that accurately predict the
dynamic response of the cell in a variety of conditions. The lack of
mechanistic, quantitative information can be bypassed by making
appropriate assumptions about the regulatory systems, in particular that
the latter have evolved under the selection pressure of the environment
to optimize the response to external perturbations. More precisely, it
is assumed that microorganisms have developed mechanisms that allocate
limiting resources (proteins, fluxes, \...) to cellular processes so as
to maximize or minimize some objective function, or combination of
objective functions, over the time-interval of environment changes.

The use of an optimality assumption to make up for missing or incomplete
information was already exploited with success in Chapter of this book.
The difference with those approaches is that here we are interested in
cases where the optimality criterion is defined over an interval of time
rather than at steady state, and thus we need to consider dynamic
instead of static optimization. Moreover, some methods take into account
that cells may vary the allocation of limiting resources to cellular
processes over the time interval in which the environmental changes
occur, instead of only considering a constant response in a stable
environment. This generalization of the problem enormously increases its
complexity. It may also lead to nontrivial dynamical effects that are
not found in the case of static optimization, such as the accumulation
of resource buffers to anticipate future changes in the environment
[@Reimers17].

The classical argument motivating the optimality assumption in the case
of microorganisms is that mutants of genes coding for enzymes in central
metabolism often have a lower growth rate than the wild-type strain,
where growth rate is interpreted as indicating fitness [@Heinrich91].
This argument, however, derives from observations of balanced growth in
a stable environment. Is there any evidence that, in the case of
changing environments, microorganisms have evolved to perform dynamic
optimization? Some circumstantial evidence is provided by the observed
capacity of microorganisms to anticipate changes in their environment.
For example, when moving along the digestive tract, *E. coli* cells are
exposed first to lactose and then to maltose, thus requiring the ability
to switch from growth on lactose to growth on maltose (reminiscent of
diauxic growth in the laboratory) [@Savageau98]. Interestingly, reporter
gene studies found that the enzymes required for maltose assimilation
are expressed at a much higher level in the presence than in the absence
of lactose, in otherwise identical conditions [@Mitchell09]. This
suggests a specific effect of the presence of lactose on the expression
of maltose enzymes, preparing the cells for the expected future
availability of maltose. This and other examples of anticipatory
behavior are not conclusive in themselves, but they suggest that dynamic
optimization is a plausible working hypothesis that may be useful in
practice.

The aim of this chapter is to show how microbial physiology can be
studied by means of dynamic optimization, by combining a specific
objective function, or combination of objective functions, with models
of different scope and granularity, while taking into account a number
of biophysical and biochemical constraints. We first provide a general
definition of dynamic optimization problems in the mathematical
framework of optimal control. We then instantiate this general
definition for three types of biological problems, each giving rise to a
specific class of models. In particular, we discuss (i) dynamic
optimization of enzyme expression in metabolic pathways, (ii) dynamic
optimization of resource allocation in coarse-grained models of cellular
growth, and (iii) dynamic flux balance analysis (dFBA) of metabolic
networks. Across the different examples, the scope of the models varies
from metabolic pathways (i) to metabolic networks (iii) to the entire
cell (ii). The increase in scope is sometimes traded against a lower
granularity of the description of cellular process (ii). Some of the
models provide a kinetic description of the rates of the individual
reactions (i and ii), whereas other models only provide constraints on
the reaction rates (iii). In every case, different objective functions
are tried, for example the minimization of the time to produce a given
compound or the maximization of the amount of biomass produced.

For each of the biological problems and corresponding models considered,
we give the precise definition of the modeling formalism and the
optimization problem, a small example as an illustration, a discussion
of the solution of the problem, and a brief description of more
realistic applications and the insights they have given into the
functioning of cellular networks. The chapter does not give a detailed
explanation of the mathematical methods that are used for solving
different classes of optimal control problems, because this would
require knowledge of specialized mathematical concepts with which the
average reader of the book may not be familiar. Moreover, these methods
have been the subject of dedicated textbooks
[@gerdts2011optimal; @kirk2004optimal]. Rather, we focus on the
definition of the dynamic optimization problems and the interpretation
of the solutions returned by available numerical solvers of optimal
control problems.

## Mathematical form of dynamic optimization problems {#TIM:Sec:Formalization}

The models of cellular processes considered in this chapter have the
form of systems of ordinary differential equations (ODEs) (Chapter ).
Dynamic optimization problems for such systems take the form of
so-called optimal control problems, which have their roots in physics
and engineering [@gerdts2011optimal; @kirk2004optimal].

Let $\mathbf{x}(t)$ be the (time-varying) state of the dynamical system,
typically concentrations of (intracellular or extracellular) metabolites
or proteins, and let $\mathbf{f}(\cdot)$ describe the (linear or
nonlinear) dynamics of the state. $\mathbf{u}(t)$ denotes the
(time-varying) control variables, *e.g.*, fluxes allocated to specific
reactions or protein fractions allocated to specific enzymes. The
time-points $0$ and $T>0$ indicate the bounds of the interval over which
the behavior of the system is optimized, with respect to an objective
function $J$. The behavior of the system, given the control exerted by
$\mathbf{u}(t)$, is subject to constraints
$\mathbf{c}_\mathbf{1}(\cdot)$ and $\mathbf{c}_\mathbf{2}(\cdot)$ on the
admissible control inputs at specific time-points $t$ or over the entire
time-interval $[t_0, t_e]$, respectively. The constraints express
physical limitations, such as the intracellular density of molecular
constituents (Chapter ), or biochemical limitations, such as the maximum
protein synthesis rate. Combining the above elements, we obtain the
following definition of dynamic optimization problems:

$$\begin{equation}
\max_{u\in U}\, J(\mathbf{x}(t), \mathbf{u}(t), 0, T), \label{eq_TIM:U}
\end{equation}$$ such that $$\begin{align}
\dfrac{d\mathbf{x}}{dt} & = \mathbf{f}(\mathbf{x}(t),\mathbf{u}(t)), \ \  \mathbf{x}(0) = \mathbf{x}_\mathbf{0}, %\label{eq_TIM:f} 
\nonumber \\
0 & \geq \mathbf{c}_\mathbf{1}(\mathbf{x}(t),\mathbf{u}(t)), 
%\label{eq_TIM:c1} 
\nonumber \\
0 & \geq \mathbf{c}_\mathbf{2}(\mathbf{x}(0),\mathbf{x}(T)). \label{eq_TIM:c2}
\end{align}$$ In summary, the problem consists in finding controls that,
given the dynamics of the system, maximize the objective function and
satisfy the constraints [@Tsiantis18].

The above definition makes no specific assumptions about the dynamics of
the system under consideration. Given that we deal with biochemical
reaction systems, the dynamics can be refined to

$$\begin{equation}
\dfrac{d\mathbf{x}}{dt} = \mathbf{N}\, \mathbf{v}(\mathbf{x}(t),\mathbf{u}(t)) - \mu(t)\, \mathbf{x}(t), \ \  \mathbf{x}(0) = \mathbf{x}_\mathbf{0}, \label{eq_TIM:Nv} \\
\end{equation}$$ where $\mathbf{N}$ represents the stoichiometry matrix
and $\mu$ is the (time-varying) growth rate. The principles of
describing the structure of biochemical reactions systems by means of a
stoichiometry matrix were described in Chapter above.

The problem definition assumes that there is only a single objective
function to be optimized. This may not be appropriate, since
microorganisms seem to optimize several criteria in parallel, for
example growth rate and survival under stress [@Schuetz12]. In many
situations, it is therefore more appropriate to generalize the above
problem to the case where $\mathbf{J}(\ldots)$ represents a vector of
$n$ objective functions $\mathbf{J} = [J_1, \ldots, J_n]$. Thus
generalized, the problem does not usually have a single solution, but
rather an infinite set of solutions located on a so-called Pareto
surface [@Miettinen98]. Solutions on the Pareto surface have the
property that every alternative solution improving the performance with
respect to some objective necessarily degrades the performance with
respect to at least one of the other objectives. In the problems
developed in the sections below, we principally consider optimality in
the case of a single, possibly composite objective.

Many methods for solving optimal control problems
([\[eq_TIM:U\]](#eq_TIM:U){reference-type="ref"
reference="eq_TIM:U"})-([\[eq_TIM:c2\]](#eq_TIM:c2){reference-type="ref"
reference="eq_TIM:c2"}) exist. While some optimal control problems can
be solved analytically, most of the problems considered in the examples
below require numerical approximations to be solved. All examples
developed in the sections below have been solved by means of freely
available solvers.

## Dynamic optimization of enzyme expression in metabolic pathways {#TIM:Sec:Dynamic-pathway}

A number of experimental works suggest that metabolic regulation encodes
temporal patterns in enzyme expression that may be beneficial for cell
physiology [@zaslaver_etal04; @Chechik2008]. Since the timing of gene
expression can directly control resource expenditure, several authors
have attempted to rationalize such patterns as solutions of optimal
control problems defined as in
([\[eq_TIM:U\]](#eq_TIM:U){reference-type="ref"
reference="eq_TIM:U"})-([\[eq_TIM:c2\]](#eq_TIM:c2){reference-type="ref"
reference="eq_TIM:c2"}). The general idea is to optimize the temporal
evolution of enzyme concentrations using objective functions that are
representative of cellular goals. This provides a rationale to
reverse-engineer optimality principles that underlie the expression
patterns observed in experiments. In this section, we briefly describe
results obtained for unbranched metabolic pathways, the basic building
blocks of the metabolic networks of the cell.

Dynamic optimization of enzymatic concentrations was first considered by
Klipp and co-workers [@klheho02]. The problem under study was the
minimal-time activation of an unbranched network from an "off" state,
where only the precursor is present, to a state where all substrate has
been converted into product. To this end, the authors considered an
unbranched pathway with $n$ enzymes and $(n+1)$ metabolites:
$$\begin{align}
    \begin{split}
    \ddt{x_0}     &= -k_1e_1x_0,\\
    \ddt{x_i}   &= k_i e_i x_{i-1}  - k_{i+1}e_{i+1}x_{i},\\
    \ddt{x_n}     &= k_n e_n x_{n-1},
    \end{split}\label{eq_TIM:modelKlipp}
\end{align}$$ with a given initial condition $x_0(0)\neq0$ and
$x_i(0)=0$ for $i=1,2,\ldots,n$, and where all enzymatic reactions are
assumed to follow mass-action kinetics with rate constant $k_i$. To
model the "off" state prior to pathway activation, the initial
conditions can be set to $x_0(0)=s$, where $s$ is the concentration of
precursor at $t=0$, and $x_i(0)=e_i(0)=0$ for all $i=1,\,\ldots n$. The
goal was to determine a vector of optimal enzyme concentrations
$\mathbf{e}(t)$ that solve the following problem: $$\begin{align}
    \mathbf{e^\star}(t) &= \arg \min_{\mathbf{e}\in U} \frac{1}{s}\int_0^\infty \left(s-x_n(t)\right)\dt, \label{eq_TIM:optproblemKlipp}
\end{align}$$ subject to the dynamic model in
[\[eq_TIM:modelKlipp\]](#eq_TIM:modelKlipp){reference-type="eqref"
reference="eq_TIM:modelKlipp"} and constraint set $U$ as in
[\[eq_TIM:U\]](#eq_TIM:U){reference-type="eqref" reference="eq_TIM:U"}
defined by a limited overall enzyme abundance over the optimization
horizon: $$\begin{align}
    \sum_{i=1}^{n} e_i(t) = e_{\mathrm{tot}},\label{eq_TIM:constraintKlipp}
\end{align}$$ where $e_{\text{tot}}$ is a constant amount of total
enzyme concentration. The objective function in
[\[eq_TIM:optproblemKlipp\]](#eq_TIM:optproblemKlipp){reference-type="eqref"
reference="eq_TIM:optproblemKlipp"} is called the *transition time* of
the pathway and quantifies the time needed to convert all precursor into
product. Note that the optimization problem
([\[eq_TIM:modelKlipp\]](#eq_TIM:modelKlipp){reference-type="ref"
reference="eq_TIM:modelKlipp"})-([\[eq_TIM:constraintKlipp\]](#eq_TIM:constraintKlipp){reference-type="ref"
reference="eq_TIM:constraintKlipp"}) falls within the general class of
problems defined by ([\[eq_TIM:U\]](#eq_TIM:U){reference-type="ref"
reference="eq_TIM:U"})-([\[eq_TIM:c2\]](#eq_TIM:c2){reference-type="ref"
reference="eq_TIM:c2"}).

Numerical solutions of the optimization problem reveal that the enzyme
profiles have a temporal sequence that matches the order in which the
enzymes appear in the pathway. Crucially, such pattern resembles the
"just-in-time" strategies widely studies in operations research
[@cheng1996just], whereby costly resources are deployed only when needed
in a production line. In the context of cellular metabolism, such a
strategy implies that minimal time activation tends to express
biosynthetic enzymes only when their substrates have been built up to
sufficiently high concentrations, and thus avoid wasteful protein
expression.

The first experimental demonstration of the just-in-time principle was
presented by Zaslaver and colleagues [@zaslaver_etal04]. This work
employed luminescent and fluorescent reporters to measure the temporal
adaptation of *Escherichia coli* upon withdrawal of amino acids from the
growth media. Clear just-in-time patterns of enzyme expression were
found in the serine, methionine and arginine biosynthetic pathways. To
better understand such patterns, the authors studied a model for an
unbranched pathway with three enzymatic steps and Michaelis-Menten
kinetics: $$\begin{align}
    \ddt{x_i}   &= k_{\text{cat},i}\, e_i\, \frac{x_{i-1}}{x_{i-1} + K_{\mathrm{M},i}} - k_{\text{cat},i+1}\, e_{i+1} \, \frac{x_{i}}{x_{i} + K_{\mathrm{M},i}} - \mu \, x_i,\quad i= 1,\ldots ,3,
\end{align}$$ with given initial conditions $x_1(0)\neq0$,
$x_2(0)=x_3(0)=0$, and where $(k_{\text{cat},i},\,K_{\text{M},i})$ are
the enzyme turnover rate and Michaelis-Menten constants of each enzyme,
respectively. The precursor concentration $x_0$ is assumed to be
constant. The model also includes a dilution term that accounts for
dilution by cell growth at rate $\mu$. In contrast to previous works,
this model also includes an explicit description of enzyme expression:
$$\begin{align}
    \ddt{e_i}   &= \frac{\beta_i}{1 + r/\kappa_i} - \mu \, e_i,\quad i= 1,\ldots ,3,\label{eq_TIM:modelEZaslaver}
\end{align}$$ where the first term is a lumped model of enzyme
expression controlled by a time-varying (active) repressor concentration
$r(t)$, with maximal expression rate $\beta_i$, and $\kappa_i$ being the
concentration of (active) repressor required for half-maximal
expression. Moreover, since bacterial amino acid pathways are often
subject to end-product feedback, the model assumed that the repressor
gets activated by the pathway product: $$\begin{align}
    r(t)                &= r_{\mathrm{T}}(t)\frac{x_3(t)}{K_{\mathrm{r}}+x_3(t)},
\end{align}$$ where $r_{\mathrm{T}}(t)$ denotes the total (active and
inactive) repressor concentration. The model also included negative
autoregulation of the repressor itself: $$\begin{align}
    \ddt{r_{\mathrm{T}}} &= \frac{\beta_0}{1 + r/\kappa_0} - \mu \, r_{\mathrm{T}},
\end{align}$$ where $\beta_0$ and $\kappa_0$ define the strength of
autoregulation similarly as in the lumped model for enzyme expression in
[\[eq_TIM:modelEZaslaver\]](#eq_TIM:modelEZaslaver){reference-type="eqref"
reference="eq_TIM:modelEZaslaver"}.

The authors constructed an optimization problem so as to study the
relation between optimality, and the strength of the regulatory
parameters $\mathbf{k}=(k_1,k_2,k_3)$ and
$\boldsymbol\beta=(\beta_1,\beta_2,\beta_3)$. To this end, they defined
the optimization problem $$\begin{align}
   \min_{\mathbf{k},\boldsymbol\beta} a \cdot \sum_{i=1}^3 \underbrace{\int_0^T \frac{\beta_0}{1+r(t)/\kappa_0}\dt}_{\text{total amount of repressor}} + \underbrace{\int_0^T\left| F-F_{\mathrm{goal}} \right|\dt}_{\text{deviation from steady state}}, \label{eq_TIM:objectiveZaslaver}
\end{align}$$ where $a$ is a scalar weight accounting for the protein
costs, $T$ is the optimization horizon, and $F$ is the rate of product
synthesis: $$\begin{align}
    F &= k_{\text{cat},3}\, e_3\, \frac{x_2}{x_2 + K_{\mathrm{M},3}}.
\end{align}$$ In problem
[\[eq_TIM:objectiveZaslaver\]](#eq_TIM:objectiveZaslaver){reference-type="eqref"
reference="eq_TIM:objectiveZaslaver"}, the constant $F_{\text{goal}}$ is
a prescribed production flux that the pathway should achieve at steady
state. Minimization of the objective in
[\[eq_TIM:objectiveZaslaver\]](#eq_TIM:objectiveZaslaver){reference-type="eqref"
reference="eq_TIM:objectiveZaslaver"} accounts for the activation of the
pathway from an "off" state until it reaches a prescribed flux
$F_{\text{goal}}$. This formulation differs from the previous example
[@klheho02] in two important ways. First, it accounts for cellular
resources in the objective function itself. The first term of the
objective quantifies the total amount of repressor produced through the
optimization horizon, and thus relates to the amount of cellular
resources required to activate the pathway. Second, the decision
variables are the regulatory parameters, not the temporal profiles of
the molecular species. Therefore, strictly speaking, this is not an
optimal control problem but rather a static optimization problem subject
to dynamic constraints encapsulated by the pathway ODE model. Through
numerical solutions for different values of the protein cost weight $a$
and optimization horizon $T$, the authors determined conditions under
which the optimal solutions showed two features of the just-in-time
property, namely: $$\begin{align}
    \tau_1<\tau_2<\tau_3,\quad \max_t e_1 > \max_t e_2 > \max_t e_3,
\end{align}$$ where $\tau_i$ is the response time, i.e. the time to
reach 50% of maximal concentration, and $\max_t e_i$ is the peak
concentration of each enzyme. This theoretical model was designed to
mimic the architecture of gene regulation in such pathways, whereby the
end product commonly represses the expression of upstream enzymes, and
thus gave both experimental and computational evidence that just-in-time
patterns may be the result of optimality principles underlying the
regulation of metabolic pathways.

Further experimental evidence of temporal patterns in enzyme expression
have been found in other pathways [@ou_etal08] and organisms
[@Chechik2008], and number of subsequent works have explored their
optimality in more detail; we refer the reader to the review in
[@Ewald2017] for a detailed discusson on such approaches. Oyarzún and
colleagues [@oyarzun_etal09], in particular, gave the first mathematical
proof that just-in-time dynamics are a general property in models of
unbranched metabolic pathways. Using a cost-benefit objective function
that balances the speed of response against the cost of expressing
pathway enzymes, they showed that the just-in-time patterns emerge in
pathways of arbitrary length and with minimal assumptions on the enzyme
kinetics. Specifically, they considered a general model for an
unbranched pathway with $n+1$ reactions: $$\begin{align}
    \ddt{x_i} &= g_{i-1}(x_{i-1}) \, e_{i-1} - g_i(x_i) \, e_i, \quad i=1,\ldots, n,\label{eq_TIM:modelOyarzun}
\end{align}$$ with initial conditions $x_i(0)=0$ for $i=1,2,\ldots n$,
and the precursor $x_0$ assumed to be at a constant concentration. The
functions $g_i$ represent a general kinetic turnover rate satisfying the
following conditions: $$\begin{align}
\begin{split}
    g_i(0) &= 0,\\
\frac{\partial g_i(x_i)}{\partial x_i} &>0.    
\end{split}\label{eq_TIM:conditionsOyarzun}
\end{align}$$ The above assumptions are generally satisfied by most
enzyme kinetic functions, as catalytic rates are typically a monotonic
function of the substrate concentration. In particular, the assumptions
in
[\[eq_TIM:conditionsOyarzun\]](#eq_TIM:conditionsOyarzun){reference-type="eqref"
reference="eq_TIM:conditionsOyarzun"} are met by common kinetics such as
mass-action, Michaelis-Menten and Hill equations. The optimization
problem considered in [@oyarzun_etal09] corresponds to a free final-time
optimal control problem: $$\begin{align}
    \mathbf{e^\star}(t) &= \arg \min_{\mathbf{e}\in U} \int_0^T \left(1 + \boldsymbol\alpha' \, \mathbf{e}(t)\right)\dt,\label{eq_TIM:objectiveOyarzun}
\end{align}$$ where $\mathbf{e}(t)$ is the vector of enzyme
concentration, $\boldsymbol\alpha$ is an $(n+1)-$dimensional vector of
tuneable weights, $T$ is a free optimization horizon, and $U$ is a
constraint set as in [\[eq_TIM:U\]](#eq_TIM:U){reference-type="eqref"
reference="eq_TIM:U"}. The first term in the objective function
[\[eq_TIM:objectiveOyarzun\]](#eq_TIM:objectiveOyarzun){reference-type="eqref"
reference="eq_TIM:objectiveOyarzun"} accounts for the total time taken
to activate the pathway from the "off" state up to a steady state flux,
while the second term weighs the cost of pathway activation. To account
for limited availability of cellular resources, the authors also
included a temporal constraint on the enzyme concentrations:
$$\begin{align}
    \sum_{i=0}^{n} e_i(t) \leq e_{\text{tot}},
\end{align}$$ which is a relaxation of the constraint originally
employed by Klipp *et al* in
[\[eq_TIM:constraintKlipp\]](#eq_TIM:constraintKlipp){reference-type="eqref"
reference="eq_TIM:constraintKlipp"}, as well as a terminal constraint of
the form: $$\begin{align}
    e_i(t) &= \frac{F_\text{goal}}{g_i(x_i(T))},\quad \text{for}\,\, t\geq T,
\end{align}$$ where $F_\text{goal}$ is a (constant) target pathway flux,
similar as in
[\[eq_TIM:objectiveZaslaver\]](#eq_TIM:objectiveZaslaver){reference-type="eqref"
reference="eq_TIM:objectiveZaslaver"}. The terminal constraint ensures
that the pathway reaches a steady state at the final time $T$. Using
Pontryagin's Minimum Principle [@kirk2004optimal], the authors showed
that the optimal enzyme concentrations follow a bang-bang temporal
profile that matches the order in the which they act on the pathway.
This result was shown to be independent of the weight $\alpha$, the
number of enzymatic steps, and valid for a wide range of enzyme kinetics
satisfying the assumptions in
[\[eq_TIM:conditionsOyarzun\]](#eq_TIM:conditionsOyarzun){reference-type="eqref"
reference="eq_TIM:conditionsOyarzun"}, thus extending the original
finding in [@klheho02] to a larger class of pathways.
Figure [1.1](#fig_TIM:enzymemodel){reference-type="ref"
reference="fig_TIM:enzymemodel"} shows a numerical example of the
optimal activation pattern obtained for an unbranched metabolic pathway
of length three (see also
Exercise [\[TIM:Exerc:enzopt\]](#TIM:Exerc:enzopt){reference-type="ref"
reference="TIM:Exerc:enzopt"}).

In this section we have reviewed some optimal control approaches for the
optimization of unbranched metabolic pathways. While differing in their
formulations and solution strategies, these approaches provide
substantial computational evidence that some temporal patterns observed
in metabolic dynamics can be understood as the solution of an optimal
control problem. In the next section we focus on approaches that go
beyond individual pathways and include additional components and
processes of the cellular machinery.

<figure id="fig_TIM:enzymemodel" data-latex-placement="t!">
<p>(A) <span class="math display">\[\begin{align}
\scalemath{1.2}{
      { \boldsymbol x_0 } \, \longrightarrow \, { \boldsymbol x_1 }
\,  \longrightarrow \, { \boldsymbol x_2 } \,  \longrightarrow \, {
\boldsymbol x_3 }} \nonumber
  
\end{align}\]</span> (B)</p>
<div class="center">
<img src=".//images/im_diego" style="width:90.0%" />
</div>
<figcaption>Example of optimal enzyme expression in an unbranched
metabolic pathway – (A) A simple scheme of the metabolic pathway. (B)
Time evolution of the optimal enzyme expression <span
class="math inline">\(u_i\)</span> and metabolite concentration <span
class="math inline">\(x_i\)</span>. For the simulations, the functions
<span class="math inline">\(g_i\)</span> are Michaelis-Menten with
constants <span class="math inline">\(k = (1,2,4,3)\)</span> s<span
class="math inline">\(^{-1}\)</span>, <span class="math inline">\(K =
1\)</span> mM, <span class="math inline">\(V = 0.2\)</span> mM s<span
class="math inline">\(^{-1}\)</span> and <span class="math inline">\(x_0
= 5\)</span> mM. Enzymatic weights are set to <span
class="math inline">\(\alpha_i = 1\)</span> mM<span
class="math inline">\(^{-1}\)</span> s and maximum enzyme availability
<span class="math inline">\(E_{\rm tot} = 1\)</span> mM. Resulting
activation times are <span class="math inline">\(t_0 = 1.59\)</span> s,
<span class="math inline">\(t_1 = 2.2\)</span> s and <span
class="math inline">\(t_f = 2.55\)</span> s.</figcaption>
</figure>

## Dynamic optimization of resource allocation in coarse-grained models of cellular growth {#TIM:Sec:kinetic-ram-dynamic}

In the previous section, we considered models that were essentially
limited to metabolic pathways. The optimization problems were formulated
in terms of the allocation of enzymes to the different reactions in the
pathway. In this section, we generalize the perspective by increasing
the scope of the models from metabolism to protein synthesis and growth.
The optimization problems concern the allocation of resources to the
synthesis of enzymes catalyzing different metabolic reactions, but also
to the synthesis of ribosomes in charge of the production of proteins.
Growth is explicitly defined in terms of the increase of protein mass,
and leads to growth dilution of all cellular components. The models are
very similar to those considered in Chapter , but the optimization
problems are dynamic rather than static. That is, instead of searching
an allocation of cellular resources to the synthesis of different
classes of proteins that is optimal at steady state, during balanced
growth, we are interested in finding a time-varying resource allocation
strategy optimizing an objective defined over an interval of time,
*e.g.*, during a transition between two states of balanced growth.

We consider the class of models with dynamics given by
Eq. ([\[eq_TIM:Nv\]](#eq_TIM:Nv){reference-type="ref"
reference="eq_TIM:Nv"}), where the input $\mathbf{u}$ is interpreted as
the (time-varying) resource allocation strategy. Among the cellular
components $\mathbf{x}$, we distinguish between metabolites and
proteins, with concentrations $\mathbf{c}$ and $\mathbf{p}$,
respectively. Accordingly, the concentration vector can be written as
$\mathbf{x} = [\mathbf{c}, \mathbf{p}]'$. We also distinguish between
enzymatic reactions and protein synthesis reactions. While the former
have metabolites as substrates and products, the latter convert
metabolites (amino acids) into proteins. An enzymatic reaction $i$ has
the following reaction rate function:

$$\begin{equation}
v_i(t) = k_i\, p_j(t) \, h_i(c),
\end{equation}$$ where $k_i$ is a catalytic constant, $p_j$ the
concentration of protein $j$, and $h_i$ a function describing enzyme
saturation. Enzyme saturation is determined by the substrates, products,
and activators/inhibitors of the reaction. Typical rate functions $v_i$
follow mass-action kinetics or (ir)reversible Michaelis-Menten kinetics.
The synthesis of protein $i$ is associated with the reaction-rate
function

$$\begin{equation}
v_i(t) = u_i(t)\, v_R(t),
\label{eq_TIM:vi_R}
\end{equation}$$ where $v_R$ is the total protein synthesis rate defined
by $$\begin{equation}
v_R(t) = k_R\, p_R(t) \, h_R(c(t)),
\end{equation}$$ with $k_R$ the maximum protein synthesis rate, $p_R$
the concentration of ribosomes, and $h_R$ a function describing the
saturation of ribosomes by their substrate, that is, amino acids (or
more precisely, tRNAs charged with amino acids). The function $u_i$ in
Eq. ([\[eq_TIM:vi_R\]](#eq_TIM:vi_R){reference-type="ref"
reference="eq_TIM:vi_R"}) is a time-varying resource allocation
function, describing the fraction of the total protein synthesis rate
allocated to the synthesis of protein $i$. The fractions are
non-negative and sum to 1, that is, for every time $t$,

$$\begin{equation}
\sum_i \, u_i(t) = 1, \ \ \textrm{and} \ \ u_i(t) \geq 0, \ \textrm{for all} \ i.
\label{eq_TIM:props_u}
\end{equation}$$

In most models, the biomass of a growing cell population is equated with
the mass of proteins, the most abundant cellular component (Chapter ).
Under the further assumption that the biomass density is constant, it
follows that the total protein concentration $p_{tot}$ must be constant,
where

$$\begin{equation}
p_{tot} = \sum_i\, p_i(t),
\end{equation}$$ with the index $i$ running over all proteins. Moreover,
the growth rate reduces to the relative (or specific) increase of the
protein mass, which leads to

$$\begin{equation}
\mu (t) = \dfrac{v_R(t)}{p_{tot}} = \dfrac{k_R\, p_R(t) \, h_R(c(t))}{p_{tot}}.
\label{eq_TIM:mu_growth}
\end{equation}$$ The above model couples metabolism, protein synthesis,
and growth in a single formalism, in the spirit of the small resource
allocation models discussed in Chapter .

Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"} gives an example of a resource
allocation model, describing a simple self-replicatory microbial system
[@Giordano16; @Yabo22] (see Chapter  for related models). The model
divides the proteome into three categories: ribosomes, enzymes, and
housekeeping proteins, with concentrations $p_Q$, $p_R$, and $p_M$,
respectively. In addition to the three categories of protein, we add a
metabolite representing the precursors for protein synthesis, with
concentration $c$. The precursors are produced from nutrients in the
environment at a rate $v_M$, a macroreaction catalyzed by the enzymes.
Protein synthesis occurs at a rate $v_R$, catalyzed by the ribosomes.
The resource allocation functions $u_Q$, $u_R$, and $u_M$ determine the
fraction of the protein synthesis rate assigned to each of the three
protein categories, where $u_Q$ is assumed to be a constant,
growth-rate-independent fraction. The rate equations for the metabolic
and protein synthesis reactions follow irreversible Michaelis-Menten
kinetics, where the substrate concentration in the medium is assumed
saturating.

<figure id="fig_TIM:resallmodel" data-latex-placement="t!">
<div class="center">
<div class="minipage">
<img src=".//images/figure_TIM_resalloc" />
</div>
<div class="minipage">
<p><span class="math display">\[\begin{equation*}
\scalemath{1}{\setstretch{1.2}
  \begin{aligned}
      &amp;{\textbf{Dynamical system}} \\
      &amp;\dot c = v_M - \mu \, c \\
      &amp;\dot p_Q = u_Q \, v_R - \mu \, p_Q \\
      &amp;\dot p_R = u_R \, v_R - \mu \, p_R \\
      &amp;\dot p_M = u_M \, v_R - \mu \, p_M \\
  \noalign{\bigskip} %\hline
  \noalign{\bigskip}
  &amp;{\textbf{Synthesis rates}} \\
      &amp;v_M = k_M \, p_M \\
      &amp;v_R = k_R \, p_R \, \frac{c}{c + K_R} \\
      &amp;\mu = \frac{v_R}{P_Q + P_R + P_M} \\
      &amp;u_Q + u_R + u_M = 1 \\
  \noalign{\bigskip} %\hline
  \noalign{\bigskip}
  &amp;{\textbf{Objective function}} \\
      &amp;J(u) = \int_{0}^{T} \mu(t) \, \mathrm{d}t \\
  \noalign{\bigskip} %\hline
  \noalign{\bigskip}
  &amp;{\textbf{Optimal control}} \\
      &amp;u_{\rm opt} = \arg \max_{u \in \mathcal{U}} J(u)
  \end{aligned}}
\end{equation*}\]</span></p>
</div>
</div>
<figcaption>Example of optimal resource allocation strategy in a
coarse-grained model of microbial growth – (A) Representation of simple
self-replicator model of microbial growth. (B) Model and optimization
problem for the self-replicator shown in panel A, as discussed in the
text. (C) Optimal dynamic resource allocation strategy, in terms of the
fraction of resources attributed to ribosome synthesis (<span
class="math inline">\(u_R\)</span>). (D) Time-varying protein mass
fractions corresponding to the optimal solution shown in panel C. The
parameter values used for the simulation are <span
class="math inline">\(k_M = 0.5\)</span>, <span
class="math inline">\(k_R = 1\)</span>, <span class="math inline">\(K_R
= 0.5\)</span> and <span class="math inline">\(u_Q = 0.6\)</span>. <span
id="fig_TIM:resallmodel" data-label="fig_TIM:resallmodel"></span>
</figcaption>
</figure>

The resource allocation functions in the model are not explicitly
specified by regulatory mechanisms, but assumed to follow a dynamic
pattern optimizing an objective criterion. In many cases, the objective
criterion is based on the hypothesis that microorganisms have evolved to
maximize the accumulation of biomass. While this hypothesis can be
criticized on theoretical and empirical reasons, it is a reasonable
choice in well-mixed environments and provides an interesting baseline
in other environments. In the model framework considered here, this
gives rise to the following objective function:

$$\begin{equation}
\max_{u\in U}\, J(x(t), u(t), 0, T) =  \int_{0}^{T} \, k_R\, p_R(t) \, h_R(c(t))\, dt, 
\label{eq_TIM:U_growth}
\end{equation}$$ where like in the general case of
Eq. ([\[eq_TIM:U\]](#eq_TIM:U){reference-type="ref"
reference="eq_TIM:U"}), $U$ denotes the set of admissible profiles for
the resource allocation functions $u$. Note that maximization of biomass
over the time-interval $[0, T]$ amounts to taking the integral of the
instantaneous growth rate over that time-interval, defined by
Eq. ([\[eq_TIM:mu_growth\]](#eq_TIM:mu_growth){reference-type="ref"
reference="eq_TIM:mu_growth"}). This objective does not generally reduce
to growth rate maximization, that is, maximization of the instantaneous
growth rate at every time-point of this interval. In particular, there
may be situations where a lower-than-optimal growth rate over some
sub-interval of $[0, T]$ may prepare for a higher growth rate after a
sudden change in conditions, and thus turn out to be beneficial for the
total accumulation of biomass over $[0, T]$. The dynamic perspective on
microbial growth in this chapter thus entails a generalization of the
objective criterion in comparison with previous chapters, where balanced
growth of microorganisms at steady state was considered.

The question can be asked, for the microbial self-replicator in
Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"}, how the cells redistribute their
resources over the different protein categories after a change in
environment, in particular a shift of the cells from a poor to a rich
carbon source. In the case of *E. coli*, for example, such as shift
might involve a change from minimal medium with acetate to minimal
medium with glucose. Given that *E. coli* grows faster on glucose than
on acetate, and that a higher growth rate requires an increased
proportion of resources to be allocated to ribosomes according to the
growth law (Chapter ), one expects $u_R$ to increase after the shift.
Since $u_Q$ is assumed constant, and the resource allocation functions
must sum to 1 at every time-point, this overall increase of $u_R$ must
be balanced by a decrease of $u_M$. These expectations concern resource
allocation before the shift (balanced growth on acetate) and a long time
after the shift (balanced growth on glucose), but the growth law
provides no information on the pattern of adaptation immediately after
the shift.

In order to investigate the optimal adaptation pattern of $u_R$
immediately after the growth transition, we solve the dynamic
optimization problem specified in
Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"}. For the simple example considered
here, the optimal solution can be characterized analytically
[@vandenBerg02; @Giordano16; @Yabo22]. This is not possible for more
complicated examples, however, which require the optimal solution to be
constructed numerically.
Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"}C-D show a typical solution for
parameter values estimated from experimental data [@Yabo22]. Starting
from a low value of $u_R$ during balanced growth on acetate, the optimal
resource allocation scheme consists of a sequence of switches between
$u_R=1$ (maximal ribosome synthesis) and $u_R=0$ (no ribosome
synthesis), until an intermediate value of $u_R$ for balanced growth on
glucose is attained. The value of $u_R$ during balanced growth on
glucose is higher than that for balanced growth on acetate, as expected
from the growth law.

The sequence of on-off switches followed by the intermediate
steady-state value is called a bang-bang-singular solution in optimal
control theory [@Giordano16; @Yabo22]. The solution reflects a dynamic
trade-off between the two different functions contributing to growth:
metabolism and protein synthesis. When, due to growth dilution, the
ribosome concentration falls to a level that is limiting for maximal
protein synthesis, the synthesis of ribosomal proteins is switched on
($u_R=1$), leading to an increase of the ribosome concentration.
Switching on the synthesis of ribosomal proteins causes the synthesis of
metabolic enzymes to be switched off. When, due to growth dilution, the
concentration of metabolic enzymes next falls to a level that the
precursors produced by the latter become limiting, the synthesis of
metabolic enzymes is switched on ($u_R=0$) to replenish the precursor
pool, and so on (see
Exercise [\[TIM:Exerc:resalloc\]](#TIM:Exerc:resalloc){reference-type="ref"
reference="TIM:Exerc:resalloc"}).

Optimal solutions with a similar bang-bang pattern were already
encountered in the previous section. They also occur in a model with a
more detailed description of different precursor (amino acid) synthesis
pathways under the objective under the minimal time of adaptation after
a shift from a medium supplemented with amino acid to a medium lacking
amino acids [@Pavlov13]. In a different type of problem, the development
of intestinal crypts, the minimal time to mature crypts was found to
depend on the on-off control of the proliferation of stem and non-stem
cells [@Itzkovitz12]. There is no convincing experimental evidence that
the adaptation of ribosomal synthesis after a nutrient upshift from a
poor to a carbon source follows a bang-bang singular pattern. The
interpretation of proteomics data after a nutrient upshift in *E. coli*
shows that the simple upregulation of ribosomal resource allocation to
the steady-state value for growth on the rich nutrient captures the
ribosomal protein expression data well [@Erickson17].

This example serves to emphasize that, while the optimality assumption
may lead to thought-provoking predictions, these need to be confronted
with experimental data. In case the optimal solutions do not agree with
the data, several revisions of the problem could be considered. While
growth optimization was chosen as the objective criterion in the example
of Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"}, there is evidence that during balanced
growth, microorganisms find a trade-off between maximizing growth rate
in a given environment and minimizing necessary adjustments to other
environments [@Schuetz12]. The problem could therefore be generalized to
a multi-criteria optimization problem. An example is the analysis of a
model similar to that considered here under the objectives of biomass
maximization and minimal adaptation time after a nutrient shift
[@Koebis22]. The formulation of the optimization problem in
Figure [1.2](#fig_TIM:resallmodel){reference-type="ref"
reference="fig_TIM:resallmodel"} does not put any constraints on valid
optimal resource allocation strategies, except that the individual
functions $u_i$ components need to sum to 1
(Eq. ([\[eq_TIM:props_u\]](#eq_TIM:props_u){reference-type="ref"
reference="eq_TIM:props_u"})). Bearing in mind that the regulatory
mechanisms underlying a resource allocation come with a cost, and need
to respect certain physical constraints, the predicted resource
allocation strategy may not be feasible. When such constraints are taken
into account, the optimal solution may no longer be bang-bang singular,
but resemble the observed adaptation pattern [@Cinquemani19; @Yabo22].

In summary, the dynamical optimization approach for studying microbial
growth presented here provides a way to test the consequences of
hypothesized objective functions in combination with simple resource
allocation models. The predictions can be confronted with experimental
data, but may also inform the redesign of microbial strains for
metabolic engineering purposes
(Box [\[TIM:Box:optimizationBiotech\]](#TIM:Box:optimizationBiotech){reference-type="ref"
reference="TIM:Box:optimizationBiotech"}).

::: Generalblock
As explained in
Section [1.2](#TIM:Sec:Formalization){reference-type="ref"
reference="TIM:Sec:Formalization"}, time-dependent optimization problems
are defined by an objective function, expressing the criterion that
microorganisms presumably optimize. In the case of microorganisms
growing in natural conditions, the choice of a particular objective
function is difficult to make and several functions may qualify. For
example, microorganisms could be assumed to maximize their biomass over
a given interval of time or minimize the time to adapt to their new
environment after a change in growth conditions. The choice may be
somewhat arbitrary and in many cases it makes sense to consider a
multi-criteria optimization problem. Even more fundamentally, the idea
that microorganisms have evolved to the point that they optimize one or
several objective functions, is controversial.

In bioengineering applications, however, the formulation of an objective
function is less problematic. In this context, the objective function is
not assumed to have evolved through natural selection, but is rather
stipulated by the metabolic engineer in an *a-priori* manner, in
agreement with a practical objective. Possible objective functions are
the maximal amount of fermentation product that can be obtained from a
given amount of substrate (maximal yield) or the minimal time to produce
a given amount of fermentation product (maximal productivity). The use
of optimal control methods for process design in bioengineering is
well-known [@Banga05]. Most of these methods, however, treat microbial
growth as a black box and do not provide much detail about the
underlying cellular processes, contrary to the formalisms discussed in
this chapter. Opening up the black box of microbial growth allows the
use of control variables that go beyond standard process parameters of
the bioreactor and represent directed perturbations of specific cellular
processes.

One example is the use of coarse-grained models of microbial growth for
the design of optimal operating conditions for the so-called growth
switch [@Yegorov19]. The growth switch is a synthetic regulatory circuit
allowing growth of *E. coli* to be arrested in order to passively
reorient the resources thus becoming available towards the production of
a metabolite of interest [@Izard15]. The maximal production of this
metabolite from a given amount of substrate, within a given interval of
time, was formulated as an optimal control problem. Its solution showed
that the optimal solution consists of two phases: a first phase of
maximal biomass production followed by a second phase of maximal product
synthesis [@Yegorov19]. The conclusion that this two-phase procedure is
optimal corresponds well with established practice in biotechnology
[@Venayak15]. Very similar conclusions were attained in related work by
Jeanne *et al.* [@jeanne2018].
:::

## Dynamic flux balance analysis (dFBA) of metabolic networks {#TIM:Sec:dynamic-FBA}

Dynamic Flux Balance Analysis (dFBA) is an extension of Flux Balance
Analysis (FBA) as described in Chapter , that can simulate the
interactions between the metabolism of an organism and its dynamic
environment. In contrast to the constant, steady-state flux solutions
that are generated by classical FBA, dFBA yields flux solutions that may
dynamically depend on concentrations of extracellular metabolites, such
as sugars or other carbon sources, dissolved oxygen, or secreted waste
metabolites. Applying these fluxes to the concentration balance of
extracellular metabolites also permits to capture dynamic changes in
these concentrations due to the metabolic activity of the cells, and
track the resulting overall biomass growth. It is noted that a basic
assumption of dFBA is that organisms rapidly reach intracellular steady
state in response to extracellular perturbations, and on the long run no
metabolite can accumulate or deplete.

In general, a dFBA model comprises three main parts as demonstrated in
Figure [1.3](#fig_TIM:dFBA){reference-type="ref"
reference="fig_TIM:dFBA"}: the dynamic equations, in the form of
differential equations, for biomass and extracellular metabolites,
constraints on the fluxes as in the FBA model, and an optimization
objective that determines how to choose the optimal fluxes.

We first consider the dynamic equations used for dFBA.

The biomass dynamics are given by $$\begin{equation}
  \label{eq_TIM:biomass-dynamics}
  \dot X = \mu X,
\end{equation}$$ where $X$ denotes the biomass concentration, typically
measured as dry mass in $\mathrm{g} \ \mathrm{L}^{-1}$, and $\mu$
denotes the growth rate, typically measured in $\mathrm{h}^{-1}$. In
principle, this equation follows the equations for balanced growth.
However, instead of using simple models, like a Monod equation for the
growth rate, the growth rate is taken from the value of the biomass
reaction in an FBA model (check in Chapter !).

Denoting the concentrations of the extracellular metabolites that are
modelled dynamically as the vector $c$, the dynamics for these
metabolites can be formulated as the differential equation
$$\begin{equation}
  \label{eq_TIM:concentration-dynamics}
  \dot c = S_{exch} v X.
\end{equation}$$ Here, $v$ is the flux vector for the complete metabolic
network, including uptake and production reactions for exchange
metabolites, and $S_{exch}$ is the stoichiometric matrix that links
these reaction fluxes to the metabolite concentrations which are
balanced dynamically. Multiplication with the biomass $X$ is necessary,
since the flux values in the FBA model are determined relative to
biomass, whereas the concentrations $c$ of the dynamic metabolites are
relative to the system volume. The equations are not yet closed, because
the fluxes $v$ (including the growth rate $\mu$ as one element of the
flux vector) still need to be determined by optimization.

As constraints, two types of constraints are used in dFBA models. A flux
balance constraint as in steady-state FBA models is applied to the
concentrations of all metabolites that are not dynamically balanced
in [\[eq_TIM:concentration-dynamics\]](#eq_TIM:concentration-dynamics){reference-type="eqref"
reference="eq_TIM:concentration-dynamics"}, *e.g.*, intracellular
metabolites. This steady state constraint is given by $$\begin{equation}
  \label{eq_TIM:DFBA-steady-state-constraint}
  S_{int} v = 0,
\end{equation}$$ where $S_{int}$ is the stoichiometric matrix that links
reaction fluxes in the vector $v$ to the steady-state metabolites.
Further, upper and lower bounds need to be put on the individual
reaction fluxes. In contrast to classical FBA, where these bounds are
constant, in dFBA flux bounds can depend on concentrations of
metabolites in the vector $c$. This is mostly applied to uptake
reactions for nutrients, and often as Michelis-Menten kinetics. For
example, if $c_i$ is the concentration of a sugar substrate, and $v_i$
is the uptake reaction for this substrate (conventionally negative in
FBA models), bounds of the form $$\begin{equation}
  \label{eq:DFBA-example-flux-bounds}
  - \frac{V_{i,max} c_i}{K_M + c_i} \leq v_i \leq 0
\end{equation}$$ would be used, where $V_{i,max}$ and $K_M$ are the
common parameters of the Michealis-Menten kinetics (Chapter ).

<figure id="fig_TIM:dFBA" data-latex-placement="t!">

<figcaption>Schematic representation of dFBA – As in FBA, the
intracellular environment in dFBA is represented by a linear programming
(LP) optimization problem that describes the metabolism of the
microorganism based on its genome-scale metabolic model (GSMM). FBA
assumes that all intracellular metabolite concentrations remain constant
while the cells optimally distribute their metabolic fluxes to maximize
their growth rate and hence, an LP can calculate the growth rate, as
well as the intracellular and exchange fluxes of the GSMM. The
calculated growth rate and exchange fluxes can be used to update the
extracellular environment. The extracellular environment in dFBA is
represented by ordinary differential equations (ODEs) that describe the
mass balance equations for biomass and metabolites found outside of the
cell. Moreover, the intracellular GSMM and the extracellular mass
balance equations can be linked through kinetic rules for substrate
uptake, like the Michaelis-Menten equations, that can raise
concentration-dependent constraints for exchange fluxes and predict
growth rate dependencies on substrate concentrations.</figcaption>
</figure>

In recent years, dFBA is increasingly applied for the simulation of
dynamic biological systems, especially due to the promising use of
genome-scale metabolic models (GSMMs) for interpreting cell physiology
and evolution, as well as for guiding metabolic engineering and
bioprocess design and optimization
[@varmaMetabolicFluxBalancing1994; @priceGenomescaleMicrobialSilico2003; @obrienUsingGenomescaleModels2015].
The dFBA applications based on GSMMs include the bacteria *Escherichia
coli* [@anesiadisDynamicMetabolicEngineering2008] and *Lactococcus
lactis* [@oddoneDynamicGenomescaleFlux2009], as well as the yeast
*Saccharomyces cerevisiae*
[@hjerstedGenomescaleAnalysisSaccharomyces2007; @hjerstedSteadystateDynamicFlux2009; @jouhtenDynamicFluxBalance2012; @hohenschuhDynamicFluxBalance2015].
However, the majority of dFBA applications use small-scale metabolic
models, most of which include less than 100 reactions. Such applications
include models of bacteria, like *Escherichia coli*
[@varmaStoichiometricFluxBalance1994; @mahadevanDynamicFluxBalance2002; @meadowsApplicationDynamicFlux2010; @konigDynamicFluxBalance2018]
and *Corynebacterium glutamicum* [@plochMultiscaleDynamicModeling2019],
models of yeast [@sainzModelingYeastMetabolism2003], but also plant and
animal models, such as a model of the core metabolism of *Arabidopsis
thaliana* [@schroederIntroducingOptimizationExplicit2020].

It is noted that most of the dFBA applications for microorganisms
simulate microbial fermentations under batch or fed-batch conditions.
Since dFBA can be used for the analysis, control and optimization of
biochemical processes, many dFBA applications focus on either dynamic
metabolic engineering or optimal control of bioreactors, or both
simultaneously. Dynamic metabolic engineering studies can predict the
effect of strain gene insertion and deletion on the dynamic behavior and
productivity of a bioprocess
[@hjerstedGenomescaleAnalysisSaccharomyces2007; @anesiadisDynamicMetabolicEngineering2008; @hjerstedSteadystateDynamicFlux2009],
while optimal control of batch or fed-batch operation of bioreactors is
important for the production of desired chemicals
[@hjerstedGenomescaleAnalysisSaccharomyces2007]. Finally, dFBA has also
been expanded for the study of microbial communities, where each
microorganism is represented by a linear program (LP) that is solved
independently
[@hensonDynamicFluxBalance2014; @zhuangGenomescaleDynamicModeling2011; @gomezDFBAlabFastReliable2014].
Co-culture simulations with dFBA can predict possible consortia
compositions, as well as metabolic engineering approaches to improve the
productivity of the consortia, but they are out of the scope of this
chapter.

Coming to the mathematical formulation of dFBA models, dFBA is an
optimization problem coupled with a system of ordinary differential
equations, that can be solved with the help of various mathematical and
numerical techniques. Even though dFBA was first introduced in 1994
[@varmaStoichiometricFluxBalance1994], it was not formalized until 2002
[@mahadevanDynamicFluxBalance2002]. The existing formalized solution
approaches that are going to be discussed here involve the static
optimization approach (SOA), the dynamic optimization approach (DOA),
and the direct approach (DA). More recently, reformulation approaches
and surrogate models for the optimization problem have also been
proposed in order to ease the computational complexity of dFBA
simulations. This complexity arises from several characteristics of
dFBA. More specifically, the solution of dFBA problems faces challenges
in terms of:

1.  problem size and scalability: As the size of the metabolic network
    increases, the computational cost increases. For this reason,
    simulations that involve large genome-scale metabolic models or
    multispecies microbial communities are limited.

2.  stiffness: The stiff behavior of dFBA has been observed in many
    cases, such as the simulation of the diauxic growth in *E. coli*
    [@mahadevanDynamicFluxBalance2002].

3.  nonlinearity: The presence of nonlinear constraints or objective
    functions can significantly increase the computational cost.

4.  feasibility: The intracellular optimization problem can become
    infeasible and lead to failure of the integration of the
    extracellular ODEs.

5.  differentiability: The optimal value of the intracellular
    optimization problem may not be continuously differentiable, which
    poses an obstacle when dFBA is used for optimal control or parameter
    estimation.

6.  non-unique solutions: The solution of the intracellular optimization
    problem is usually not unique which can make fluxes unrealistically
    "jump" between different optimal solutions.

##### Static Optimization Approach (SOA)

divides the total time horizon of the dFBA simulation into several
smaller time intervals. The optimization problem is solved to obtain the
flux distribution at the beginning of each time interval, and then the
ODEs are integrated over the time interval with this fixed flux
distribution. The dynamics calculated from this time step are used to
constrain the optimization problem solved at the beginning of the next
time interval, and the process is repeated until the end of the
simulation time is reached. SOA can be implemented easily with the use
of an Euler scheme for integrating the system and a suitable existing LP
solver for solving the FBA at each time step. SOA is also implemented in
the constraint-based reconstruction and analysis (COBRA) toolbox for
MATLAB [@heirendtCreationAnalysisBiochemical2019] which can perform dFBA
simulations. Since its implementation is relatively simple, SOA has been
widely used in studies for the diauxic
[@mahadevanDynamicFluxBalance2002; @konigDynamicFluxBalance2018],
aerobic and fermentative
[@varmaStoichiometricFluxBalance1994; @anesiadisDynamicMetabolicEngineering2008]
growth of *E. coli*, for *S. cerevisiae* fermentations
[@sainzModelingYeastMetabolism2003; @jouhtenDynamicFluxBalance2012; @hohenschuhDynamicFluxBalance2015],
as well as for the metabolism underlying plant growth
[@schroederIntroducingOptimizationExplicit2020]. Many of these
applications include larger-scale or genome-scale metabolic networks,
due to the scalability of SOA. However, the main drawback is that SOA is
inefficient and can become computationally expensive because it has to
solve the optimization problem at each time step. This can be
challenging for most dFBA problems which are stiff and require small
time steps to ensure accuracy, convergence, and stability of the
solution.

##### Dynamic Optimization Approach (DOA)

follows closely the general dynamic optimization framework described in
Section [1.2](#TIM:Sec:Formalization){reference-type="ref"
reference="TIM:Sec:Formalization"}: an objective function that depends
on the dynamic states of the system over the complete time horizon of
interest is formulated, and the dynamics
 [\[eq_TIM:biomass-dynamics\]](#eq_TIM:biomass-dynamics){reference-type="eqref"
reference="eq_TIM:biomass-dynamics"}--[\[eq_TIM:concentration-dynamics\]](#eq_TIM:concentration-dynamics){reference-type="eqref"
reference="eq_TIM:concentration-dynamics"} and algebraic constraints
 [\[eq_TIM:DFBA-steady-state-constraint\]](#eq_TIM:DFBA-steady-state-constraint){reference-type="eqref"
reference="eq_TIM:DFBA-steady-state-constraint"}--[\[eq:DFBA-example-flux-bounds\]](#eq:DFBA-example-flux-bounds){reference-type="eqref"
reference="eq:DFBA-example-flux-bounds"} are added as optimization
constraints. In other words, DOA discretizes the total time horizon of
the dFBA simulation, and then transforms the dynamic optimization
problem into a non-linear programming (NLP) problem, which is solved
once by simultaneously optimizing over the entire time of the
simulation. In this way, DOA obtains the time profiles of fluxes and
metabolite concentrations in the system, and allows the formulation of a
dynamic objective function, which could provide useful information about
the design of genetically modified metabolic networks or the
maximization of bioprocess productivity. Because of this characteristic,
DOA is often used in dynamic metabolic engineering, parameter estimation
and optimal control applications. For example, DOA has been used for
simulating the diauxic growth of *E. coli*
[@mahadevanDynamicFluxBalance2002; @waldherrDynamicOptimizationMetabolic2015].
On the downside, even though the optimization problem does not need to
be repeatedly solved like in SOA, the single NLP of DOA can become
easily intractable, as its dimension increases with the fineness of time
discretization. Additionally, DOA has been mainly limited to small-scale
metabolic networks, since it cannot be easily applied to genome-scale
metabolic networks due to the large number of variables and constraints
that are introduced in the NLP as the size of the network increases.

##### Direct Approach (DA)

has been formulated more recently than SOA and DOA, and directly
includes the LP solver for the FBA in the right-hand side evaluator
function of the ODEs. In this way, it can take advantage of existing ODE
integrators with adaptive step size and error control that can reduce
the number of integration steps and provide better solution accuracy
compared to SOA. DA has been implemented in the ORCA toolbox
[@maoORCACOBRAToolbox2014], which complements the constraint-based
reconstruction and analysis (COBRA) toolbox for MATLAB
[@heirendtCreationAnalysisBiochemical2019]. Furthermore, DA has been
used for studying the (an)aerobic growth of wild-type and engineered *E.
coli* strains [@meadowsApplicationDynamicFlux2010], the aerobic growth
of *Corynebacterium glutamicum* on glucose and xylose in biorefinery
simulations [@plochMultiscaleDynamicModeling2019], as well as the
aerobic and anaerobic growth of wild type and engineered *S. cerevisiae*
strains
[@hjerstedGenomescaleAnalysisSaccharomyces2007; @hjerstedSteadystateDynamicFlux2009; @jouhtenDynamicFluxBalance2012].
Some of these applications involve dynamic metabolic engineering for
product maximization, and many of them include genome-scale metabolic
networks, since DA is relatively easily scalable like SOA.

However, DA requires the LP to be resolved at least once, every time the
right-hand side of the ODEs is evaluated [@bradie2006friendly]. This can
make DA computationally demanding, especially for larger metabolic
networks. Another major challenge is that when evaluating the right-hand
side of the ODEs close to the boundary of feasibility, the LP can become
infeasible and make the dFBA simulation fail. The LP can become
infeasible either because it is really infeasible and the simulation
should be terminated, or because the ODE integrator becomes unable to
evaluate the right-hand side of the ODEs and the simulation is
discontinued, or erroneous death phase messages are being displayed. The
latter can happen as dFBA simulations involve discrete events that
correspond to switches in the active set of the LP solution. More
specifically, different bases for the optimal solution of the LP can
emerge at each time step. Moreover, at the points of change of the
active set, the dFBA model is not differentiable, since the optimal
value of the LP as a function of the right-hand side of the constraints
is not continuously differentiable. This is a problem because the first
and second derivatives of the model must be computed when dFBA is used
for optimal control or parameter estimation applications. Finally,
another drawback emerges due to the primal multiplicity of the LP. As it
is well-known, FBA is formulated as an underdetermined problem and
therefore, the LP does not have a unique solution
[@mahadevanEffectsAlternateOptimal2003]. Non-unique optimal reaction
fluxes can lead different ODE integrators to different results.

::: MathDetailblock
In order to address some of the computational challenges of dFBA,
Höffner, Harwood, and Barton proposed a simulator for dFBA, which was
initially coded in FORTRAN [@hoffnerReliableSimulatorDynamic2013], but
gained popularity when implemented in MATLAB with the name Dynamic Flux
Balance Analysis laboratory (DFBAlab) [@gomezDFBAlabFastReliable2014],
and more recently in Python [@tourignyDfbaSoftwareEfficient2020]. It is
noted that the DFBAlab is compatible with the COBRA toolbox
[@heirendtCreationAnalysisBiochemical2019]. Based on this dFBA
simulator, it is not necessary to resolve the LP each time the
right-hand side of the ODEs is evaluated and consequently, the solution
process becomes faster. This is possible because the FBA solution at an
initial time can be used to compute future optimal solutions by
detecting changes in the active set or by computing the optimal basis of
the FBA solution [@brunnerMinimizingNumberOptimizations2020].
Unfortunately, such formulations need to continuously monitor the active
set of the LP, which increases with the size of the metabolic network,
or need to choose a basis for the optimal solution that is most likely
to remain optimal as the simulation proceeds
[@brunnerMinimizingNumberOptimizations2020]. The latter is challenging
since the optimal basis can be non-unique even for a unique optimal
solution. Nevertheless, DFBAlab manages to reduce the number of times
that the LP is resolved, and also avoids obtaining infeasible LPs and
numerical failure by using the LP feasibility problem and the
Karush-Kuhn-Tucker (KKT) optimality conditions of the FBA problem (see
below). In addition, the differentiability problem could be solved with
the help of non-smooth analysis which provides optimality conditions in
terms of sub-gradients or generalized gradients, for convex and
non-convex functions respectively. Furthermore, to tackle the issue of
primal multiplicity of the FBA problem, DFBAlab performs lexicographic
optimization .
:::

::: MathDetailblock
Lexicographic or hierarchical optimization involves the solution of a
series of LPs with auxiliary objectives ranked in priority order. The
use of auxiliary objectives reduces the feasible space and leads to a
unique optimal solution, while the auxiliary objectives can have
specific biological meanings and can be selected based on prior
knowledge about the organism [@Schuetz12]. Some of the most-used
auxiliary objectives are based on the assumption that evolution leads to
the exclusion of inefficient pathways so that cells can biosynthesize
the smaller possible number of enzymes. Examples of such auxiliary
objectives include the minimization of enzyme cost
[@noorProteinCostMetabolic2016], the minimization of the total reaction
flux [@holzhutterPrincipleFluxMinimization2004], and the minimization of
the number of active reactions [@murabitoCapturingEssenceMetabolic2009].
However, it has been shown that such objectives may not be suitable for
some engineered cells. In general, it is not trivial to find a series of
auxiliary objectives that are consistent with experimental data, assure
uniqueness and preserve continuity of the optimal solution. In some
cases, even when all auxiliary objectives have been used, hierarchical
optimization cannot ensure the uniqueness of the dFBA solution. Apart
from the use of auxiliary objectives, auxiliary rules or auxiliary
parameters have also been proposed to address the primal multiplicity of
FBA. For example, geometric methods have been proposed to identify a
unique distribution of reaction fluxes for FBA
[@smallboneFluxBalanceAnalysis2009], even though there is no biological
evidence to justify such methods.
:::

<figure id="fig_TIM:dfba-example">
<p><embed src="./images/dfba-example.pdf" /><br />
</p>
<figcaption>Example result of a dFBA simulation for the <em>E. coli</em>
core model <span class="citation"
data-cites="orthReconstructionUseMicrobial2010"></span> performed with
DFBAlab – (A) Illustration of dynamic metabolites and relevant exchange
fluxes. Extracellular metabolites use mass concentration (<span
class="math inline">\(\mathrm{g}\ \mathrm{L}^{-1}\)</span>), exchange
fluxes are in molar amount per dry biomass and time (<span
class="math inline">\(\mathrm{mmol}\ \mathrm{gDW}^{-1}\
\mathrm{h}^{-1}\)</span>). (B) Concentration-dependent constraints
applied to the exchange fluxes during the dFBA simulation. (C)
Differential equation model for biomass concentration <span
class="math inline">\(X\)</span> and metabolite mass concentrations.
Growth rate <span class="math inline">\(\mu\)</span> and exchange fluxes
<span class="math inline">\(v_\ast\)</span> (in red) are optimal values
from the underlying FBA model. <span
class="math inline">\(m_{\species{O}_2}\)</span>, <span
class="math inline">\(m_{\species{G}}\)</span>, <span
class="math inline">\(m_{\species{E}}\)</span>, <span
class="math inline">\(m_{\species{A}}\)</span> are molar masses of <span
class="math inline">\(\species{O}_2\)</span>, glucose, ethanol, and
acetate, respectively. <span class="math inline">\(k_L a = 8.5\
\mathrm{h}^{-1}\)</span> is the volumetric mass transfer coefficient for
oxygen. (D) Simulation results for concentrations of biomass and
metabolites. We can observe four growth phases: aerobic growth on
glucose with production of acetate, anaerobic growth on glucose with
production of ethanol and acetate, aerobic growth on acetate, and a
stationary phase. (E) Simulation result for oxygen concentration in the
liquid medium. Oxygen is depleted in the second growth phase due to mass
transfer limitations, but replenishes at the start of the third phase.
(F) Penalty function time course. Increases of the penalty function
indicate periods where the underlying FBA model is infeasible. Here,
this occurs when the ATP maintenance constraint cannot be satisfied due
to a lack of substrates, and happens in this simulation during a brief
period where the switch from glucose to acetate as a substrate takes
place, since oxygen needs to be replenished first, and in the stationary
phase. </figcaption>
</figure>

## Concluding remarks

One approach for understanding the response of microorganisms to changes
in their environment is to assume that this response has been optimized
by evolution. That is, the regulatory mechanisms controlling the
response optimize an objective, or a trade-off between competing
objectives, subject to a variety of physical and biochemical
constraints. This approach gives rise to dynamic optimization problems
([\[eq_TIM:U\]](#eq_TIM:U){reference-type="ref"
reference="eq_TIM:U"})-([\[eq_TIM:c2\]](#eq_TIM:c2){reference-type="ref"
reference="eq_TIM:c2"}) that can be solved by techniques from optimal
control theory. Three examples of such problems were considered in this
chapter: dynamic optimization of enzyme expression in metabolic
pathways, dynamic optimization of coarse-grained models of cellular
growth, and dynamic flux balance analysis. This does not exhaust the
range of possible problems that can be considered. One example is the
combination of the resource allocation perspective with dynamic flux
balance analysis [@waldherrDynamicOptimizationMetabolic2015].

Some of the predictions obtained by means of dynamic optimization seem
to be supported by available experimental data, such as the
time-ordering of enzyme expression in a linear pathway. Other
predictions cannot currently be tested or may not be consistent with the
available experimental data, such as the dynamical ribosomal protein
synthesis pattern. The contradiction between a predicted optimal
response and the observations is interesting, because it indicates that
some of the assumptions underlying the problem need to be revised. The
model may not account for all relevant processes taking place in the
cell, important constraints may have been ignored, or the objective may
not capture the actual processes taking place.

The solution of a dynamic optimization problem may be different from the
concatenation of the solutions of repeated static optimization problems
defined over short, consecutive time intervals making up the time
horizon. For instance, the optimal pattern of resource allocation over a
time horizon may involve the accumulation of a reserve of unused
resources that, while being wasteful in the short run, is beneficial
when the whole time interval of interest is considered. One example was
given in the introduction of this chapter, concerning the expression of
maltose enzymes in the presence of lactose [@Mitchell09]. Another
example is the accumulation of glycogen in cyanobacteria during
daylight, providing the energetic resources for maintenance metabolism
in the night time [@Reimers17].

The analysis of the growth of microorganisms using dynamic optimization
critically depends on the choice of an appropriate objective function.
In the examples discussed above, optimization was performed with respect
to a single objective, *e.g.*, the maximal accumulation of biomass over
a time interval or the minimal time to deplete a given amount of
substrate. It is plausible, however, that microorganisms have evolved
under the necessity to satisfy several objectives simultaneously. This
can be taken into account by formulating a weighted sum of the different
objective functions, such as the simultaneous minimization of throughput
time and investment in enzymes in
Eq. ([\[eq_TIM:objectiveOyarzun\]](#eq_TIM:objectiveOyarzun){reference-type="ref"
reference="eq_TIM:objectiveOyarzun"}). Another approach is to generalize
the optimization problem to a multi-objective optimization problem, with
sets of Pareto optimal solutions, each providing a trade-off between
mutually conflicting objectives. One example of such a multi-objective
optimization problem is given by a generalization of the dynamic
optimization of enzyme expression in metabolic pathways in
Section [1.3](#TIM:Sec:Dynamic-pathway){reference-type="ref"
reference="TIM:Sec:Dynamic-pathway"}, with the double objective of
minimizing the time to consume a given amount of substrate and
minimizing the concentration of (possibly toxic) intermediate
metabolites [@deHijas14].

Instead of making *a-priori* assumptions about the objectives presumably
optimized by microorganisms, one could try to infer the latter from the
experimental data. This inverse optimization approach leverages the
large amounts of time-course data on the dynamic response of
microorganisms to environmental perturbations that have accumulated in
the past decade. Inverse optimization requires the solution of complex
inverse optimal control problems that have been little explored until
now [@Tsiantis18].

## Recommended readings {#recommended-readings .unnumbered}

**General references introducing the problem of dynamic optimization in
biology:**

- Sutherland, The best solution, *Nature*, 2005 [@Sutherland2005].
  Influential statement of the use of optimization as an explanatory and
  predictive principle in biology.

- Banga, Optimization in computational systems biology, *BMC Systems
  Biology*, 2008 [@Banga08]. General review of optimization approaches
  in systems biology.

- Heinrich, Schuster, and Holzhütter, Mathematical analysis of enzymic
  reaction systems using optimization principles, *European Journal of
  Biochemistry*, 1991 [@Heinrich91]. Classical review on the use of
  dynamic optimization in the analysis of biochemical systems.

- Ewald, Bartl, and Kaleta. Deciphering the regulation of metabolism
  with dynamic optimization: an overview of recent advances.
  *Biochemical Society Transactions*, 2017 [@Ewald2017]. Recent review
  on the use of dynamic optimization in the analysis of metabolism.

**Methodological foundations of dynamic optimization and optimal
control:**

- Gerdts, *Optimal Control of ODEs and DAEs*, De Gruyter, 2011
  [@gerdts2011optimal]. Introduction to optimal control theory.

- Kirk, *Optimal Control Theory: An Introduction*, Courier Corporation,
  2004 [@kirk2004optimal].

**Dynamic optimization of enzyme expression in metabolic pathways:**

- Klipp, Heinrich, and Holzhütter. Prediction of temporal gene
  expression: metabolic optimization by re-distribution of enzyme
  activities. *European Journal of Biochemistry*, 2002 [@klheho02].
  Classical paper on dynamic optimization of enzyme expression in
  unbranched pathways.

- Oyarzún, Ingalls, Middleton, and Kalamatianos. Sequential activation
  of metabolic pathways: a dynamic optimization approach. *Bulletin of
  Mathematical Biology*, 2009 [@oyarzun_etal09]. Recent example
  revisiting the problem of dynamic optimization of enzyme expression.

**Dynamic optimization of resource allocation in coarse-grained models
of cellular growth:**

- Pavlov and Ehrenberg. Optimal control of gene expression for fast
  proteome adaptation to environmental change. *Proceedings of the
  National Academy of Sciences USA*, 2013 [@Pavlov13]. Example of the
  use of optimal control to understand temporal adaptation of gene
  expression in response to a change in the environment.

- Giordano, Mairet, Gouzé, Geiselmann, and de Jong. Dynamical allocation
  of cellular resources as an optimal control problem: Novel insights
  into microbial growth strategies. *PLoS Computational Biology*, 2016
  [@Giordano16]. Example of dynamic optimization applied to a
  coarse-grained model of microbial growth, including a review of
  related work.

**Dynamic flux balance analysis of metabolic networks:**

- Mahadevan, Edwards, and Doyle. Dynamic flux balance analysis of
  diauxic growth in *Escherichia coli*, *Biophysical Journal*, 2002
  [@mahadevanDynamicFluxBalance2002]. Classical paper proposing two
  different approaches for dynamic flux balance analysis, with an
  example of diauxic growth in *E. coli*.

- Hjersted and Henson. Steady-state and dynamic flux balance analysis of
  ethanol production by *Saccharomyces cerevisiae*, *IET Systems
  Biology*, 2009 [@hjerstedSteadystateDynamicFlux2009]. Comparison of
  steady-state and dynamic flux balance analysis of variably-sized
  metabolic models for screening metabolic engineering strategies
  affecting ethanol production by *Saccharomyces cerevisiae*.

- Köbis, Bockmayr and Steuer. Time-optimal adaptation in metabolic
  network models, *Frontiers in Molecular Biosciences*, 2022
  [@kobis2022]. Overview of various approaches to dynamic optimization
  focused on time optimality.

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
[]{#TIM:Exerc:enzopt label="TIM:Exerc:enzopt"} The solutions of some of
the optimization problems in
section [1.3](#TIM:Sec:Dynamic-pathway){reference-type="ref"
reference="TIM:Sec:Dynamic-pathway"} exhibit abrupt switches in enzyme
concentrations (\"bang-bang behavior\"), which in reality are not
possible.

1.  What would be possible adjustments of the models to make the
    predictions more realistic? (Hint: consider explicit modeling of
    enzyme synthesis and enzyme degradation or dilution by growth.)

2.  What predicted behavior would you expect for these modified models?

3.  In these extended models, which possibilities would the cell have to
    speed up the adaptation of enzyme concentrations? Under what
    circumstances could this provide an actual advantage?
:::

::: exercise
[]{#TIM:Exerc:resalloc label="TIM:Exerc:resalloc"} The resource
allocation model in
Section [1.4](#TIM:Sec:kinetic-ram-dynamic){reference-type="ref"
reference="TIM:Sec:kinetic-ram-dynamic"} defines biomass as being
composed of proteins only, neglecting notably the (small) contribution
of metabolites. This has the disadvantage of putting no constraints on
metabolite concentrations, which is not realistic from a biological
point of view.

1.  What would be a possible adjustment of the model to integrate
    metabolites into the biomass composition, under the assumption that
    the total biomass density remains constant? (Hint: consider the
    definition of growth rate in
    Eq. ([\[eq_TIM:mu_growth\]](#eq_TIM:mu_growth){reference-type="ref"
    reference="eq_TIM:mu_growth"}).)

2.  How would the objective function for this model
    (Eq. ([\[eq_TIM:U_growth\]](#eq_TIM:U_growth){reference-type="ref"
    reference="eq_TIM:U_growth"})) need to be adapted accordingly?

3.  How would you expect the resulting constraint on metabolite
    concentrations to affect the predicted behavior of the microbial
    self-replicator?
:::
