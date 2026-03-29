# Optimization of metabolic states {#OME}

::: chapterhighlights
- Optimal metabolic states in this chapter refer to enzyme-efficient
  states, which are metabolic states that realize a given objective flux
  at a minimal enzyme cost.

- In models without further flux constraints, flux distributions of
  enzyme-efficient states are Elementary Flux Modes (EFMs).

- Elementary Flux Modes can be used to find enzyme-efficient states in
  networks that would be too large to optimize metabolic states \"by
  brute force\".

- Biomass per enzyme efficiency can be converted to cell growth rate by
  simple approximate formulae.

- The Elementary Flux Mode that is realized in an enzyme-efficient state
  depends on the external conditions.

- As growth conditions change, either the flux profile changes
  continuously (together with metabolite and enzyme concentrations), or
  fluxes change discontinuously, implying jumps also in metabolite and
  enzyme concentrations.
:::

## Introduction {#OME:Sec:Introduction}

In a simple economic picture of cells, we assume that cells adjust their
metabolic state in each environment to obtain a maximal fitness
advantage. This may be impossible in reality, but it remains an
interesting question what this best metabolic state would look like,
according to our knowledge of cells. So what is the best metabolic state
overall (comprising metabolic fluxes, metabolite concentrations and
enzyme levels)? What pathways should a cell use, which enzymes should be
induced or repressed, and how should this change in a new environment?
To answer these questions, we need to remember that all metabolic
variables (fluxes, metabolite levels, enzyme levels, and enzyme
efficiencies) depend on each other. Physically, fluxes depend on
metabolite concentrations through kinetics and enzyme regulation
(e.g. competitive inhibition) and metabolites are produced and consumed
by the fluxes until a steady state is reached. Hence, if we think in
terms of cellular economics (treating enzymes as control variables),
then all metabolic variables must be optimized together.

In the previous chapters we saw some ways to predict optimal metabolic
fluxes, metabolite concentrations and enzyme levels separately: in Flux
Balance Analysis (FBA, Chapter ), we optimized fluxes by maximizing an
objective function (typically biomass) while in Enzyme Cost Minimization
[@FlamholzNoor2013; @NoorFlamholz2016] (Chapter ) metabolite
concentrations were optimized by minimizing cost (or, equivalently,
maximizing the enzyme efficiencies). Each of these methods is based on a
strong assumption: FBA requires measured flux ranges and/or apparent
catalytic rates and assumes enzyme saturation effects can be neglected,
while enzyme cost minimization requires a given flux distribution. But
what if we don't know any of the variables in advance? How can we
predict all of them from first principles?

Before thinking about this, let us briefly step back: what do we
actually mean by an "optimal state"? What quantity should be maximized
in metabolism? There could be very different aims (e.g. production in
biotechnology, versus number of offspring and survival in a wild-type
cell). However, in both cases an important aim is cell growth -- or at
least, avoiding strong growth deficits. Below we will see that cell
growth depends, to a good approximation, on biomass/enzyme efficiency,
that is, biomass production per total enzyme invested. Hence, whenever
fast growth is important, cells should maximize this efficiency.

In conclusion, we will consider the following optimality problem:
maximize biomass/enzyme efficiency, defined as the production flux per
invested enzyme with respect to all metabolic variables (metabolites,
enzymes and fluxes) and under all constraints (steady state, enzyme
kinetics, etc.). Solutions to this problem are considered optimal
states.

## Enzyme-efficient metabolic states use elementary flux modes {#OME:Sec:efm_cost_optimal}

The optimization problem in this chapter is to reach maximal objective
flux with minimal enzyme investment. The biological interpretation is
that this would lead to the highest growth rate, because it optimizes
the ratio between gains (fluxes) and costs (enzymes). When we solve this
optimization problem with mathematical tools, it is convenient to either
find the minimal enzyme investment for a certain flux, or the maximum
flux for a fixed enzyme investment. Although one could think of
different biological explanations for those two ways to state the
optimization problem, mathematically they are equivalent. For the
outline of the proof that optimal states are elementary flux modes, it
is convenient to fix the objective flux to an arbitrary value (we
choose 1) and then minimize the enzyme investment. This leads to the
following optimization problem over the fluxes ($\fluxv$), enzymes
levels ($\enzconcv$) and internal metabolite concentrations
($\metconcv$): $$\begin{align}
    &\underset{\fluxv,\enzconcv,\metconcv}{\text{minimize}} &&\sum_{i = 1}^r h_i ~\enzconci \label{OME:eq:optimization_problem}\\
    &\text{subject to:} &&\Stoichmat \cdot \fluxv = \mathbf{0} &&&\text{steady state} \nonumber\\
    & &&\forall i: \fluxi = \enzconci~ \catrate_i(\metconcv) &&&\text{enzyme kinetics} \nonumber\\
    & &&\enzconcv,\metconcv \geq 0 &&&\text{positive concentrations} \nonumber\\
    & &&\flux_r = 1 &&&\text{fixed objective flux} \nonumber \\
    & &&\metconcv \leq \metconcv_{\mathrm{max}} &&&\text{metabolite bounds} \nonumber
\end{align}$$

where $h_i$ are the weights, $\Stoichmat$ is the stoichiometry matrix,
$i$ is the index of the reactions (ranging from 1 to $r$), with the last
reaction (with index $r$) representing the objective. This optimization
problem states that by adjusting the fluxes ($\fluxv$), metabolite
concentrations ($\metconcv$) and enzyme concentrations ($\enzconcv$),
the total cost (sum of costs -- $h_i \enzconci$ -- for every reaction)
is minimized, while keeping the objective flux constant (any arbitrary
constant can be chosen, here we chose 1). The weights ($h_i$) can be
thought of as the size or production costs of the enzymes (measured, for
example, in molecular weight or gene length) We require certain
constraints: (i) the metabolic network needs to be in steady state to
avoid built-up of intermediates, (ii) enzyme kinetics -- the flux of
each reaction ($\fluxi$) has to be equal to the enzyme concentration
($\enzconci$) times a metabolite dependent (e.g., saturation) term
($\catrate_i(\metconcv)$), (iii) all enzyme and metabolite
concentrations have to be positive, (iv) the objective flux is equal to
1, and (v) the metabolite concentrations are within their given bounds.
The latter constraint is optional and is mostly necessary when dealing
with irreversible kinetics. Reversible kinetics usually lead to bounded
metabolite levels because very high concentrations of products inhibit
the reaction that forms the products.

In this section, we will explain why the optimal state is reached at an
Elementary Flux Mode (EFM). One important starting point is that, as we
have seen before in Chapter , convex optimization problems with only
positivity or equality constraints (no other inequalities) lead to an
optimal solution at an extreme point of the feasible solution space, and
those extreme points are Elementary Flux Modes. However, the
optimization problem
[\[OME:eq:optimization_problem\]](#OME:eq:optimization_problem){reference-type="eqref"
reference="OME:eq:optimization_problem"} is not convex, mainly due to
the hyperbolic dependence of reaction rates on the concentrations of
metabolites ($\catrate_i(\metconcv)$ is usually not linear in the
internal metabolite concentrations).

There are several ways to prove that the solution of this optimization
problem is an EFM, of which some are outlined in the papers by
@WortelPeters2014 and @MuellerRegensburger2014. Here we will outline a
proof by contradiction: assuming a solution to the optimization problem
that is not an EFM and showing that this leads to a contradiction.

::: theorem
The flux distribution that maximizes an objective flux over the total
enzyme cost in a metabolic network without additional constraints is an
Elementary Flux Mode.
:::

::: proof
*Proof.* Assume we have some optimal state where the flux distribution
is not an EFM. Any optimal solution is associated with a set of fluxes,
enzyme concentrations and metabolite concentrations. Now we set the
metabolite concentrations to the concentrations of the assumed optimal
state. Then all metabolite-dependent terms ($\catrate_i(\metconcv)$)
become constants, and we return to a convex problem. As explained in
Chapter and Figure [1.1](#OME:fig:Proof){reference-type="ref"
reference="OME:fig:Proof"}, the optimum of this problem (now in terms of
enzyme concentrations and fluxes) is a flux distribution that is an EFM.
But this contradicts our initial assumption that the optimal state from
which we took the set of metabolite concentrations was not an EFM. The
proof by contradiction shows that the optimal state must be an EFM. ◻
:::

<figure id="OME:fig:Proof" data-latex-placement="t!">
<div class="center">
<embed src=".//images/OME_Proof.pdf" style="width:80.0%" />
</div>
<figcaption>Translation from flux to enzyme space retains EFMs as
extreme rays – The top left panel shows the feasible flux space with the
steady state constraints, all fluxes positive (using splitting of
fluxes, as explained in the text, if necessary) and a fixed objective
flux. The extreme points here are points where one flux becomes 0 and
are elementary flux modes (see Chapter ). Here we show that when we have
assumed metabolite concentrations, such as when we keep them at an
optimal solution, we get a linear transformation and the extreme rays
are maintained. Different metabolite levels, for example solutions to
different environmental conditions, can lead to different
transformations and therefore different optima (minimal total enzyme),
but those are always located at an EFM.</figcaption>
</figure>

## Enzyme-efficient states in an example network

To illustrate the proof, we study a simple network representing growth
on glucose and pyruvate that we have seen previously in Chapter (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}). We use $\metG$ and $\metP$ for
glucose and pyruvate in the equations, we use the subscript
$\mathrm{ex}$ when a metabolite is extracellular and square brackets to
denote a concentration. For the use in this chapter, we add enzyme
kinetics to this network. We will use the factorized rate law as in
Chapter , but then generalized for $n_s$ substrates and $n_p$ products
(also compare Eq. () in Chapter ):

$$\begin{eqnarray}
\flux = \enzconc \cdot \kcatplus \cdot \frac{\prod^{j=1}_{n_s} s_j/\kmSn{j}}{1 + \prod^{k=1}_{n_p} p_k/\kmPn{k} + \prod^{j=1}_{n_s} s_j/\kmSn{j}}\cdot \left(1 - \expe^{\deltaG / RT}\right) \label{OME:eq:rate_equation}
\end{eqnarray}$$

:::: Generalblock
The detailed kinetic equations for the example model (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}) using the factorized rate law (see
Equation
[\[OME:eq:rate_equation\]](#OME:eq:rate_equation){reference-type="eqref"
reference="OME:eq:rate_equation"} and Chapters and ) are:

::: tiny
$$\begin{align}
\begin{split}
    \flux_0 &= \enzconc_0 \cdot \kcatplusn{0} \cdot \frac{ \concgex/\kc{\Gex}}{1 + \concg/\kc{\mathrm{G}} + \concgex/\kc{\Gex}}\cdot \left(1 - \expe^{\deltaG_0/RT}\right) \\
    \flux_1 &= \enzconc_1 \cdot \kcatplusn{1} \cdot \frac{ (\concg/\kc{\mathrm{G}})(\concadp/\kc{\adp})}{1 + (\concp/\kc{\mathrm{P}})(\concp/\kc{\mathrm{P}})(\concatp/\kc{\atp}) + (\concg/\kc{\mathrm{G}})(\concadp/\kc{\adp})}\cdot \left(1 - \expe^{\deltaG_1/RT}\right) \\
    \flux_2 &= \enzconc_2 \cdot \kcatplusn{2} \cdot \frac{ \concp/\kc{\mathrm{P}}}{1 + \concpex/\kc{\Pex} + \concp/\kc{p}}\cdot \left(1 - \expe^{\deltaG_2/RT}\right) \\
    \flux_3 &= \enzconc_3 \cdot \kcatplusn{3} \cdot \frac{ (\concp/\kc{\mathrm{P}})(\concadp/\kc{\adp})(\coxy/\kc{\oxy})}{1 + (\cco/\kc{\co})(\concatp/\kc{\atp}) + (\concp/\kc{\mathrm{P}})(\concadp/\kc{\adp})(\coxy/\kc{\oxy})}\cdot \left(1 - \expe^{\deltaG_3/RT}\right) \\
    \flux_4 &= \enzconc_4 \cdot \kcatplusn{4} \cdot \frac{ \concpex/\kc{\Pex}}{1 + \concpex/\kc{\Pex} + \concp/\kc{\mathrm{P}}}\cdot \left(1 - \expe^{\deltaG_4/RT}\right) \\
    \flux_{\rm BM} &= \eBM \cdot \kcatplusn{\mathrm{BM}} \cdot \frac{ (\concp/\kc{\mathrm{P}})(\concatp/\kc{\atp})}{1 + (\concbm/\kc{\mathrm{BM}})(\concadp/\kc{\adp}) + (\concp/\kc{\mathrm{P}})(\atp/\kc{\atp})}\cdot \left(1 - \expe^{\deltaG_5/RT}\right)
\end{split}
\end{align}$$
:::

Note that $\metP$ is a product twice in $\flux_1$, as $\flux_1$ produces
2$\metP$. Note that $\flux_2$ and $\flux_4$ are the same reaction, but
defined in the opposite direction. The standard set of parameters we
used for the toy model is all $\kcatplusn{i} = 10$ $s^{-1}$ except
$\kcatplusn{3} = 0.1$ $s^{-1}$, all $\deltaGstd_i/RT = -440$ and all
$\km = 1$ mM. For the external metabolites $\concpex = 1$ mM,
$\concgex = 0.05$ mM, $\coxy = 0.1$ mM, $\concbm = 1$ mM and $\cco = 10$
mM unless mentioned otherwise.
::::

See Box
[\[OME:Physicsblock:example_model_kinetics\]](#OME:Physicsblock:example_model_kinetics){reference-type="ref"
reference="OME:Physicsblock:example_model_kinetics"} for all detailed
rate laws of the example network. We can simplify this equation by
combining the forward catalytic constant, the thermodynamic efficiency
factor, the saturation efficiency factor, and the regulation efficiency
factor (if that exists) in a function $\catrate(\metconcv)$, which only
depends on the metabolites, and not on the enzyme concentrations. We
will below write $\catrate$ for $\catrate(\metconcv)$.
$$\begin{eqnarray}
\fluxi = \enzconci \cdot \catrate_i \label{OME:eq:enz_convert}
\end{eqnarray}$$

Now we take $\fluxbm = 1$ and optimize all fluxes, enzyme concentrations
and metabolite concentrations to minimize the enzyme costs
($\etot = \sum_i \enzconci$), while satisfying the constraints posed in
Equations
[\[OME:eq:optimization_problem\]](#OME:eq:optimization_problem){reference-type="eqref"
reference="OME:eq:optimization_problem"}, for different levels of
external glucose and standard levels of the other external metabolites.
We see that for different concentrations of external glucose, lead to
different optimal fluxes, enzyme levels and metabolite levels (Table
[1.1](#OME:Table:optimization_example_network){reference-type="ref"
reference="OME:Table:optimization_example_network"}).

:::: center
::: {#OME:Table:optimization_example_network}
   $\concgex$   $\etot$   $\flux_0$   $\flux_1$   $\flux_2$   $\flux_3$   $\flux_4$   $\fluxbm$   $\enzconc_0$   $\enzconc_1$   $\enzconc_2$   $\enzconc_3$   $\enzconc_4$   $\eBM$   $\concg$   $\concp$   $\concatp$   $\concadp$
  ------------ --------- ----------- ----------- ----------- ----------- ----------- ----------- -------------- -------------- -------------- -------------- -------------- -------- ---------- ---------- ------------ ------------
     $0.01$     $156.2$      $5$         $5$         $0$         $9$         $0$         $1$         $54.4$         $4.4$           $0$           $94.4$          $0$        $2.9$     $0.08$    $15.14$      $0.05$      $20.09$
     $0.1$      $91.3$      $50$        $50$        $99$         $0$         $0$         $1$         $61.3$         $11.3$         $14.2$          $0$            $0$        $4.4$     $0.13$     $4.55$      $0.11$      $20.09$
      $1$       $36.2$      $50$        $50$        $99$         $0$         $0$         $1$         $13.0$         $8.0$          $12.5$          $0$            $0$        $2.7$     $0.60$     $7.65$      $0.11$      $20.09$

  : Outcomes of the optimization of the example network with standard
  kinetics, parameter values and external concentrations (see Box
  [\[OME:Physicsblock:example_model_kinetics\]](#OME:Physicsblock:example_model_kinetics){reference-type="ref"
  reference="OME:Physicsblock:example_model_kinetics"}) for varying
  levels of $\concgex$.
:::
::::

The table shows that the total enzyme needed for a biomass flux of one
decreases with increasing glucose levels, as we expect. In addition, the
optimal level of internal glucose increases with increasing external
glucose. This is because a higher external glucose allows for a higher
internal glucose while still maintaining a steady glucose influx, and a
higher internal glucose allows fewer enzymes to drive further
metabolism. Moreover, the fluxes of the solutions follow an EFM (see
Figure [1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}b).

We can now reformulate the problem for only the flux and enzyme levels
while keeping the metabolite levels as they are in the table. With the
metabolite levels in the first row of the table, we can linearly relate
the enzyme and flux levels (with the factors $\catrate_i$ that have
become constants now we have set the internal metabolite
concentrations), and thus the extreme rays of the enzyme and flux space
will be equal and EFMs, as pointed out above (see also Chapter and
Figure [1.1](#OME:fig:Proof){reference-type="ref"
reference="OME:fig:Proof"}). Optimization in this space will lead to the
optimal flux distributions following an EFM (see Box
[\[OME:Physicsblock:example_model_analysis\]](#OME:Physicsblock:example_model_analysis){reference-type="ref"
reference="OME:Physicsblock:example_model_analysis"} for the detailed
calculations). As fixing part of the optimal solution should lead to the
same optimal solution, this required the flux distribution of the
optimization over all variables to follow an EFM, as was indeed the
case.

We point out two important aspects, using the network (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}) as an example. First, it is
convenient to split reversible reactions such that fluxes are always
positive. In this case, that means that the reversible reaction from
$\metP$ to $\Pex$ is split into the forward reaction $\flux_2$ and the
reverse reaction $\flux_4$, both of which can have only positive flux.
This splitting makes sure that EFMs are the extreme rays of the flux
space (see Chapter ). This splitting is purely a mathematical
convenience; we still assume this to be one reaction in the biological
sense, and therefore the kinetic equations of both the forward and the
backward reactions will be exactly the same. Depending on in which
direction the flux goes, either one of the reactions will be positive
and the other zero. Any solution with both reactions positive is
infeasible, but minimizing enzyme levels will never lead to such a
solution; therefore we do not need to set additional constrains to avoid
this. Second, the feasibility of EFMs can depend on external
concentrations. In this network, the biomass reaction ($\fluxbm$) is the
objective flux and there are three EFMs leading to the production of
biomass: EFM1 consisting of $\flux_0$, $\flux_1$, $\flux_2$ and
$\fluxbm$, EFM2 consisting of $\flux_0$, $\flux_1$, $\flux_3$ and
$\fluxbm$ and EFM3 consisting of $\flux_4$, $\flux_3$ and $\fluxbm$.
However, if $\Pex$ is absent in the environment, the uptake flux
$\flux_4$ will always be 0 and therefore EFM3 will not be feasible.

::: Generalblock
We minimize the enzyme investment for $\fluxbm=1$ with $\concpex = 0$
(and therefore $\flux_4=0$ and EFM3 is not feasible) for the network in
Figure [1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"} (the optimization problem in
Equation
[\[OME:eq:optimization_problem\]](#OME:eq:optimization_problem){reference-type="eqref"
reference="OME:eq:optimization_problem"}). Assuming all $h_i = 1$, the
objective function
$\sum_{i = 1}^r h_i ~\enzconci = \enzconc_0 + \enzconc_1 + \enzconc_2 + \enzconc_3 + \eBM$.
The constraints $\fluxbm = 1$ and $\enzconcv, \metconcv \geq 0$ in
Eq. [\[OME:eq:optimization_problem\]](#OME:eq:optimization_problem){reference-type="eqref"
reference="OME:eq:optimization_problem"} are straightforward. The steady
state of all internal metabolites (G, P, ADP and ATP) leads to the
following equalities (the steady states of ADP and ATP lead to the same
equality):

$$\begin{equation}
    \begin{aligned} 
        \text{Steady state } \mathrm{ATP}  &\Longrightarrow 100~ \fluxbm = 2~ \flux_1 + 10~ \flux_3 \nonumber \\
        \text{Steady state } \mathrm{P} &\Longrightarrow 2~ \flux_1 + \flux_4 = \flux_2 + \flux_3 + \fluxbm \nonumber \\
        \text{Steady state } \mathrm{G} &\Longrightarrow \flux_0 = \flux_1
    \end{aligned}
\end{equation}$$

Substituting $\flux_{BM} = 1$ and $\flux_4=0$ and solving this set of
linear equations, we can write all fluxes as functions of $\flux_2$:
$\flux_0 = \flux_1 = 5 + \frac{5}{11} \flux_2$ and
$\flux_3 = 9 - \frac{1}{11} \flux_2$ (there is only one independent flux
in this system). This means we can draw the feasible flux space on the
$\flux_2$ line and we can express the objective function in terms of
$\flux_2$:

$$\begin{equation}
    \begin{aligned} 
        \sum_{i = 1}^r h_i \enzconci &= \enzconc_0 + \enzconc_1 + \enzconc_2 + \enzconc_3 + \eBM \\
        &= \flux_0/\catrate_0 + \flux_1/\catrate_1 + \flux_2/\catrate_2 + \flux_3/\catrate_3 + \fluxbm/\catrate_{\mathrm{BM}} \\
        &= (5 + 5/11 \flux_2)/\catrate_0 + (5 + 5/11 \flux_2)/\catrate_1 + \flux_2/\catrate_2 + (9 - 1/11 \flux_2)/\catrate_3 + 1/\catrate_{\mathrm{BM}} \\
        &= \underbrace{(5/\catrate_0 + 5/\catrate_1 + 9/\catrate_3 + 1/\catrate_{\mathrm{BM}})}_{\alpha} + \underbrace{\left(5/(11 \catrate_0) + 5/(11 \catrate_1) + 1/\catrate_2 - 1/(11 \catrate_3)\right)}_{\beta} \flux_2 \\
        &= \alpha + \beta \flux_2
    \end{aligned}
\end{equation}$$

The kinetic functions ($\catrate_i$) depend on several parameters
(external metabolite levels $\concgex$, $\oxy$, $\cco$ and $\concpex$,
catalytic constants, Michaelis constants and Gibbs free energies) and
the variables $\concg$, $\concp$, $\concatp$ and $\concadp$. That means
that once we have a set of internal metabolite concentrations
$\metconcv$, the enzyme levels in the objective function can be written
as a constant times the flux: $e_i = \fluxi/\catrate_i$, with
$\catrate_i$ a constant. For a set of parameters, $\alpha$ and $\beta$
are positive or negative depending on the choice of $\metconcv$. It is
clear that when we minimize this objective function by adjusting
$\flux_2$, we will always have an optimum at $\flux_2 = 0$ (when $\beta$
is positive) or $\flux_2 = 99$ (when $\beta$ is negative).
$\flux_2 = 99$ is the maximum of $\flux_2$ because then
$\flux_3 = 9 - \frac{1}{11} \flux_2 = 0$, and higher values of $\flux_2$
would lead to negative values for $\flux_3$.

In conclusion, the optimum cannot be at a value of $0 < \flux_2 < 99$.
If there would be an optimum with $0 < \flux_2 < 99$, we can determine
$\metconcv$ and calculate whether $\beta>0$ to find a lower objective
value at $\flux_2 = 0$ or $\flux_2 = 99$, contradicting that we started
with an optimum. Only if $\beta =0$ there is a range of optima, but this
requires very precise parameter values. $\flux_2 = 0$ and $\flux_2 = 99$
correspond to EFMs of this network
(Figure [1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}).
:::

<figure id="OME:fig:DiscreteSwitch" data-latex-placement="t!">
<div class="center">
<p>(A) (B)<br />
<embed src=".//images/OME_MetabolicNetwork.pdf" /><br />
(C) (D)<br />
</p>
</div>
<figcaption>States of maximal efficiency in an example model – (A)
Example network from Chapter with added stoichiometry. (B) Three
elementary flux modes of this network. (C) Calculated enzyme investment
needed for a biomass flux of 1. At a very low concentration of
extracellular glucose (<span class="math inline">\(\concgex\)</span>),
EFM3 has the lowest cost. But as we move along the x-axis, at around
<span class="math inline">\(\concgex=0.02\)</span> there is a switch to
EFM1 and later, at around <span
class="math inline">\(\concgex=0.07\)</span>, EFM2 becomes the one with
the lowest cost. (D) Specific fluxes (flux divided by total enzyme)
associated with the optimal EFM for different levels of <span
class="math inline">\(\Gex\)</span>. Note that <span
class="math inline">\(v_1\)</span> is not shown as it is always equal to
<span class="math inline">\(v_0\)</span>. The rates show a discontinuity
when there is a switch from one optimal EFM to another.</figcaption>
</figure>

## Calculation of optimal states

We can now use the result that states of maximal enzyme efficiency are
reached at an elementary flux mode to calculate optimal states in a
metabolic network using the following steps:

1.  Enumerate the elementary flux modes that include the objective flux

2.  Calculate the minimal enzyme for each EFM scaled to an objective
    flux of 1

3.  Compare the EFMs and select the one with minimal enzyme demands

Step 1 is possible for relatively large networks, although usually not
for genome scale metabolic networks. Step 2 is a convex optimization
problem as we have seen in Chapter and Step 3 is straightforward. These
three steps together are called Enzyme Flux Cost Minimization, because
it is similar to Enzyme Cost Minimization, but while that is focused on
fixed fluxes, Enzyme Flux Cost Minimization simultaneously finds the
optimal fluxes, enzyme and metabolite levels. In this section we will
show the method on the example network of Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}.

First, we describe the network with the stoichiometric matrix
($\Stoichmat$) and the concentration vector ($\metconcv$):

$$\begin{equation}
    \Stoichmat = \begin{pmatrix} 1 & -1 & 0 & 0 & 0 & 0 \\ 0 & 2 & -1 & -1 & 1 & -1 \\ 0 & 2 & 0 & 10 & 0 & -100 \\ 0 & -2 & 0 & -10 & 0 & 100 \end{pmatrix}, \qquad
    \metconcv \equiv \begin{pmatrix} \concg \\ \concp \\ \concatp \\ \concadp \end{pmatrix}
\end{equation}$$

And with the stoichiometric matrix we can describe the steady state
constraints:

$$\begin{align}
\begin{split}
    \frac{\mathrm{d}}{\mathrm{d}t} \metconcv &= \Stoichmat~ \fluxv = \begin{pmatrix} 1 & -1 & 0 & 0 & 0 & 0 \\ 0 & 2 & -1 & -1 & 1 & -1 \\ 0 & 2 & 0 & 10 & 0 & -100 \\ 0 & -2 & 0 & -10 & 0 & 100 \end{pmatrix} \begin{pmatrix} \flux_0 \\ \flux_1 \\ \flux_2 \\ \flux_3 \\ \flux_4 \\ \fluxbm \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \\ 0\end{pmatrix}
\end{split}
\end{align}$$

Now we find the EFMs (for example with EFMtool [@TerzerStelling2008]).
It can easily be checked that the following EFMs (denoted by vectors
$\EFMf^{(i)}$) are in the nullspace of the stoichiometric matrix:

$$\begin{equation}
    \EFMf^{(1)} =\begin{pmatrix} 5 \\ 5 \\ 0 \\ 9 \\ 0 \\ 1 \end{pmatrix}, \quad
    \EFMf^{(2)} = \begin{pmatrix} 50 \\ 50 \\ 99 \\ 0 \\ 0 \\ 1 \end{pmatrix},\quad
    \EFMf^{(3)} = \begin{pmatrix} 0 \\ 0 \\ 0 \\ 10 \\ 11 \\ 1 \end{pmatrix} \\
\end{equation}$$

The next step is to perform the convex optimization over the metabolite
levels for each one of the three EFMs. Therefore, we express the enzyme
levels as a ratio of the flux and the function $f(\metconcv)$, using
Equation
[\[OME:eq:enz_convert\]](#OME:eq:enz_convert){reference-type="ref"
reference="OME:eq:enz_convert"}. Summing over all enzymes, we get a
function for the total enzyme cost (level) as a function of fluxes,
metabolite concentrations and parameters: $$\begin{equation}
\label{OME:eq:total_enz_cost}
    \etot = \sum_i \enzconci = \sum_i \frac{\fluxi}{\catrate_i(\metconcv)}\,. 
\end{equation}$$ We use the standard parameters (Box
[\[OME:Physicsblock:example_model_kinetics\]](#OME:Physicsblock:example_model_kinetics){reference-type="ref"
reference="OME:Physicsblock:example_model_kinetics"}) and replace
$\fluxi$ by the values given by each EFM. We are then left with a convex
optimization over the metabolite levels, an Enzyme Cost Minimization
problem as in Chapter . For $\concgex = 0.05$ we obtain a total enzyme
of 111.1 for EFM1, of 146.3 for EFM2 and 136.5 for EFM3. That means that
for these conditions we will conclude that EFM1 is optimal. From the
optimization we obtain the metabolite concentrations: $\concg = 0.08$,
$\concp = 3.93$, $\concatp = 0.11$ and $\concadp = 20.09$ (that the
internal glucose concentration is higher than the external is because we
described the transport with regular enzyme kinetics instead of
transporter enzyme kinetics, which would have been more realistic). We
can next use the rate equations to calculate the enzyme levels from the
fluxes and metabolite levels, using the values for the parameters and
external concentrations.

We can repeat this procedure for different levels of external
concentrations and see that the optimal EFM can change depending on the
external concentration (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}c). When the optimum shifts to using
a different EFM, there is a discontinuity in the fluxes at the external
metabolite concentration (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}d). Many cells show shifts in
metabolic strategies depending on the external conditions and Enzyme
Flux Cost Minimization is one way of explaining those shifts.

Above, Enzyme Cost Flux Minimization was used to find the metabolic
state with the maximum enzyme efficiency. Although in our calculation we
obtain the enzyme concentrations last, it is by enzyme concentrations
that cells actually control metabolism. If cells produce enzymes at the
concentrations we calculated and reach a steady state, this state will
realize the fluxes and metabolite levels that lead to our optimal state.

<figure id="OME:fig:BiomassToGrowth" data-latex-placement="t">
<p>(A) (B)<br />
</p>
<figcaption>Translation of enzyme-specific biomass rate to growth rate –
(A) Both from experimental data and a cell-optimization point of view,
the ribosomal fraction of the proteome increases with the growth rate,
while the metabolic fraction decreases. (B) This leads to a hyperbolic
dependency of the growth rate on the biomass production rate per amount
of enzymes.</figcaption>
</figure>

## Translating enzyme efficiency into cell growth rate {#OME:Sec:biomass_rate_to_growth}

In the section above, we learned how to optimize metabolic states for a
maximal overall enzyme efficiency. Why is this quantity relevant? One
reason is that overall enzyme efficiency, according to some simple
reasoning, determines the cell's growth rate. If microbes compete by
growing fast, their fitness is largely determined by their momentary
growth rate in their respective environment. In such environments, the
biomass/enzyme efficiency will be under selection, which makes it one of
the important objective functions in this book. If higher enzyme
efficiency means higher growth rate, and if we have a conversion formula
for this, we can plot the "growth rate" of the different EFMs instead of
"overall enzyme efficiency".

Enzyme-efficient metabolic states allow us to compute specific biomass
production rates, i.e. the rate of biomass production per metabolic
enzyme invested. If biomass consisted only of enzymes, the ratio
\"enzyme production rate per total enzyme demand\" would give us
directly the growth rate. However, biomass does not only consist of
metabolic enzymes, but includes ribosomal enzymes, RNA, DNA, lipids, and
other compounds. Therefore we need a formula for converting
biomass/enzyme efficiency into cellular growth rate.

<figure id="OME:fig:GrowthRatesSwitch" data-latex-placement="t">

<figcaption>Optimal growth rates of the two EFMs for different levels of
the external metabolite <span class="math inline">\(\Gex\)</span>,
computed using Equation <a href="#OME:eq:mainMethodsMuNonlinear"
data-reference-type="eqref"
data-reference="OME:eq:mainMethodsMuNonlinear">[OME:eq:mainMethodsMuNonlinear]</a>
from the enzyme demands (at a unit biomass production rate) shown in
Figure <a href="#OME:fig:DiscreteSwitch" data-reference-type="ref"
data-reference="OME:fig:DiscreteSwitch">1.2</a> (C). </figcaption>
</figure>

Mathematically, a cell's growth rate is given by
$\growth = \fluxbm/\metconcbm$, where $\fluxbm$ is the biomass
production rate (biomass produced per cell volume and time) and
$\metconcbm$ is the biomass amount per cell volume. If a cell contained
nothing but metabolic enzymes (more precisely, the enzymes described in
our model), the biomass/enzyme efficiency $\muEnz =  \fluxbm/\enzCost$
would directly describe the cellular growth rate. Since that is not the
case, we need to convert $\enzCost$ to $\metconcbm$. The metabolic
protein fraction decreases with the growth rate, leading to a hyperbolic
dependency of the growth rate on the biomass production rate (Figure
[1.3](#OME:fig:BiomassToGrowth){reference-type="ref"
reference="OME:fig:BiomassToGrowth"}). We may use the empirical
approximation
$\enzCost / \metconcbm = \catrate_{\rm prot}(a - b~\growth)$, where
$\catrate_{\rm prot} = 0.5$ is the fraction of protein mass within the
cell dry mass and the parameters $a = 0.27$ and $b = 0.2\,\mathrm{h}$
were fitted to describe the metabolic enzyme fraction in proteomics
data, assuming a linear dependence on growth rate [@ScottGunderson2010].
This yields the conversion formula (see also [@WortelNoor2018]):
$$\begin{eqnarray}
\label{OME:eq:mainMethodsMuNonlinear}
\growth = \frac{a~\catrate_{\rm prot}~\fluxbm}{\enzCost + b~\catrate_{\rm prot}~\fluxbm}\,.
\end{eqnarray}$$ This formula has been used to convert the minimal
enzyme cost per biomass flux for different external concentrations in
the toy model (Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}c) to the maximal growth for each EFM
(Figure [1.4](#OME:fig:GrowthRatesSwitch){reference-type="ref"
reference="OME:fig:GrowthRatesSwitch"}).

<figure id="OME:fig:EcoliCarlsonNetwork" data-latex-placement="t">
<div class="center">
<embed src=".//images/OME_EcoliCarlsonNetworkLumped.pdf"
style="width:70.0%" />
</div>
<figcaption>Model of central metabolism in <em>E. coli</em> bacteria.
(A) The metabolic network of the <em>E. coli</em> model used by <span
class="citation" data-cites="WortelNoor2018"></span>. Note that only for
the purpose of visualization, the network shown here has been condensed
by lumping consecutive reactions that are fully coupled (e.g., the
reactions between DHAP and PEP are now represented by a single arrow).
Furthermore, some groups of metabolites have been merged to a single
node: H6P – representing the hexose phosphates G6P, F6P, and FBP; T3P –
representing the triose phosphates G3P and DHAP; P5P – representing the
pentose phosphates R5P, X5P, and Ru5P. The metabolites that are direct
substrates of the biomass reaction are marked in bold. (B) A Venn
diagram showing statistics of biomass-producing EFMs in the model and
their reliance on oxygen.</figcaption>
</figure>

## Application to central metabolism in *E. coli* bacteria

In the previous sections, we saw that finding enzyme-efficient metabolic
states can be done by iterating through all possible EFMs and performing
the enzyme cost minimization on each one. We demonstrated it on a toy
model comprising only 3 EFMs. In @WortelNoor2018, this method was scaled
up and applied to a more realistic model covering the central metabolic
network, as shown in Figure
[1.5](#OME:fig:EcoliCarlsonNetwork){reference-type="ref"
reference="OME:fig:EcoliCarlsonNetwork"}A. For this larger network,
there are 1566 biomass-generating EFMs. Each reaction is assigned to a
single enzyme along with its molecular weight, $\kcatplus$, $\km$, and
$\deltaGstd$, and follows the generalized factorized rate law as in
Equation ([\[OME:eq:rate_equation\]](#OME:eq:rate_equation){reference-type="ref"
reference="OME:eq:rate_equation"}). These parameters are listed in
Appendix section
[\[OME:Appendix:sec:CentralMetabolismModel\]](#OME:Appendix:sec:CentralMetabolismModel){reference-type="ref"
reference="OME:Appendix:sec:CentralMetabolismModel"}, and the full
procedure for obtaining them is described in @WortelNoor2018, along with
other model parameters.

<figure id="OME:fig:EcoliCarlsonNetworkSelectEFMs"
data-latex-placement="t!">
<div class="center">
<embed src=".//images/OME_EcoliCarlsonNetworkEFMs.pdf"
style="width:75.0%" />
</div>
<figcaption>The four flux modes chosen for drawing the Monod curves in
Figure <a href="#OME:fig:MonodCurveEFMs" data-reference-type="ref"
data-reference="OME:fig:MonodCurveEFMs">1.7</a>: (A) <em>max-gr</em> –
the EFM with the highest growth rate under the standard conditions
chosen in the study, (B) <em>aero-ace</em> – an EFM which mixes between
respiration and acetate fermentation, (C) <em>ana-lac</em> – an EFM that
does not require oxygen (i.e. anaerobic) and uses lactate fermentation,
and (D) <em>exp</em> – which is not an elementary flux mode, but rather
one based on the measured flux distribution for <em>E. coli</em> growing
on minimal media and glucose. The active reactions are highlighted in
color (with the flux direction indicated by the arrowhead). The
magnitude of each flux is not shown here but can be found in the
Supplementary section of <span class="citation"
data-cites="WortelNoor2018"></span>. The biomass reaction is not shown
here due to space limitations, but is always active.</figcaption>
</figure>

First, @WortelNoor2018 wanted to study the effect of environmental
conditions on the growth rate of *E. coli*, and see whether the model
would be able to recapitulate empirical phenomena. The external glucose
concentration was set to 100 mM and oxygen levels were varied between 1
$\upmu$ and 10 mM. They selected 4 flux modes as representatives (the
EFMs *max-gr*, *ana-lac*, and *aero-ace*, and *exp*, which is based on
experimentally measured fluxes; the flux distributions are shown in
Figure
[1.6](#OME:fig:EcoliCarlsonNetworkSelectEFMs){reference-type="ref"
reference="OME:fig:EcoliCarlsonNetworkSelectEFMs"}), and calculated
their predicted growth rates in each condition, using Equation
([\[OME:eq:mainMethodsMuNonlinear\]](#OME:eq:mainMethodsMuNonlinear){reference-type="ref"
reference="OME:eq:mainMethodsMuNonlinear"}). The results are shown in
Figure [1.7](#OME:fig:MonodCurveEFMs){reference-type="ref"
reference="OME:fig:MonodCurveEFMs"}. When focusing on a single flux
mode, one can see that as the oxgyen level increases so does the growth
rate. The increase saturates at some point, which depends on the flux
modes and on the kinetic parameters in the model. Indeed, it has long
been known that growth rate dependence on a limiting substrate
concentration has this specific shape -- a relationship generally called
the *Monod curve*.

In this specific example, it is interesting to see the Monod curves of
the different EFMs, and try to understand the differences. First, the
EFM called *ana-lac* (red curve), is a flat line. This makes sense
because cells that use this EFM do not utilize the oxidative
phosphorylation system and therefore do not require oxygen at all for
growth. *max-gr*, on the other hand, is very sensitive to the level of
oxygen mainly because of the high flux going through oxidative
phosphorylation. It is also the EFM with the highest growth rate in
standard oxygen levels (0.21 mM), even when taking all the other
$\sim$`<!-- -->`{=html}1500 EFMs into account (not shown here).

<figure id="OME:fig:MonodCurveEFMs" data-latex-placement="t!">
<div class="center">

</div>
<figcaption>Monod curves (cell growth rate as a function of oxygen
level) computed using the model shown in Figure <a
href="#OME:fig:EcoliCarlsonNetwork" data-reference-type="ref"
data-reference="OME:fig:EcoliCarlsonNetwork">1.5</a> – Each curve was
computed using one of the EFMs and the associated (oxygen-dependent)
enzyme demands. The ana-lac strategy (anaerobic growth with lactate
secretion) does not use oxygen, therefore it curve is flat.</figcaption>
</figure>

Instead of screening only external oxygen levels, we can also screen
several model parameters and compute \"winning EFMs\", their enzyme
demands, and the resulting growth rates for our parameter combination.
By screening glucose and oxygen concentrations, we obtain the Monod
landscape shown in Figure
[1.8](#OME:fit:MonodSurfaceWinningEFM){reference-type="ref"
reference="OME:fit:MonodSurfaceWinningEFM"} (A). Just like in
Figure [1.7](#OME:fig:MonodCurveEFMs){reference-type="ref"
reference="OME:fig:MonodCurveEFMs"}, there are distinct parameter
regions in which optimal growth is reached by specific EFMs. While the
*max-gr* EFM remains best when glucose and oxygen levels are high, at
low oxygen levels we see a large number of different EFMs, one of them
*ana-lac* (see the EFM phase diagram in Figure
[1.8](#OME:fit:MonodSurfaceWinningEFM){reference-type="ref"
reference="OME:fit:MonodSurfaceWinningEFM"} (B)). More results for this
model (fluxes plotted in the EFM phase diagram and in flux space, as
well as ideal and real enzyme costs for all EFMs), are shown in Appendix
Section
[\[OME:sec:DetailsMonodLandscape\]](#OME:sec:DetailsMonodLandscape){reference-type="ref"
reference="OME:sec:DetailsMonodLandscape"}.

## Concluding remarks

In this chapter we considered the metabolic network of a cell - and
enzyme levels, metabolite concentrations, and fluxes as the state
variables - and studied its maximally efficient states. Finding such
states can be difficult because fluxes, metabolite concentrations, and
enzyme levels are tightly coupled: metabolite concentrations determine
enzyme efficiencies, enzyme efficiencies determine optimal enzyme
levels, and enzyme levels determine fluxes and metabolite
concentrations, which in turn determine enzyme efficiencies. To find an
optimal state, all variables need to be optimized at the same time,
which is a non-linear optimality problem with (possibly) many local
optima. In small toy models, solutions can be found numerically, but for
large detailed models, the computational effort becomes enormous.
Instead of simplifying the problem (as in the previous chapters) we here
used the insight that (in models without extra flux bounds) the optimal
solutions must be EFMs.

<figure id="OME:fit:MonodSurfaceWinningEFM" data-latex-placement="t">
<div class="center">
<table style="width:50%;">
<colgroup>
<col style="width: 50%" />
<col />
</colgroup>
<tbody>
<tr>
<td style="text-align: left;">(A)</td>
<td style="text-align: left;">(B)</td>
</tr>
<tr>
<td style="text-align: left;"><embed
src=".//images/OME_monod_surface.pdf" style="width:90.0%" /></td>
<td style="text-align: left;"><embed
src=".//images/OME_winning_heatmap.pdf" style="width:45.0%" /></td>
</tr>
</tbody>
</table>
</div>
<figcaption>Monod landscape – (A) Similar to the 1-dimensional Monod
curve (Figure <a href="#OME:fig:MonodCurveEFMs"
data-reference-type="ref"
data-reference="OME:fig:MonodCurveEFMs">1.7</a>), the graphics shows the
cell growth rate as a function of external glucose and oxygen
concentrations, predicted from the <em>E. coli</em> model in Figure <a
href="#OME:fig:EcoliCarlsonNetwork" data-reference-type="ref"
data-reference="OME:fig:EcoliCarlsonNetwork">1.5</a>. The growth rate of
the “winning” EFM – i.e. the one with the highest growth rate under the
glucose and oxygen levels matching the <span
class="math inline">\(x\)</span> and <span
class="math inline">\(y\)</span> values – determines the height of each
point. Each color represents the region in which a certain EFM is the
“winning” one. (B) EFM phase diagram. The same plot as in (A), seen from
above. The “winning EFMs” form a sort of phase diagram. At the boundary
between every two regions, the two EFMs lead to the same growth rate
(similar to the intersections between curves in Figure <a
href="#OME:fig:MonodCurveEFMs" data-reference-type="ref"
data-reference="OME:fig:MonodCurveEFMs">1.7</a>). The EFMs from Figure
<a href="#OME:fig:EcoliCarlsonNetworkSelectEFMs"
data-reference-type="ref"
data-reference="OME:fig:EcoliCarlsonNetworkSelectEFMs">1.6</a> are
marked by their names. Note that the colors in this figure do not match
the previous colors marking these select EFMs. </figcaption>
</figure>

## Recommended readings {#recommended-readings .unnumbered}

- M.T. Wortel, H. Peters, J. Hulshof, B. Teusink, and F.J. Bruggeman.
  Metabolic states with maximal specific rate carry flux through an
  elementary flux mode. FEBS Journal, 281(6):1547--1555, 2014.

- S. Müller, G. Regensburger, and R. Steuer. Enzyme allocation problems
  in kinetic metabolic networks: Optimal solutions are elementary flux
  modes. Journal of Theoretical Biology, 347:182--190, 2014.

- M.T. Wortel, E. Noor, M. Ferris, F.J. Bruggeman, and W. Liebermeister.
  Metabolic enzyme cost explains variable trade-offs between microbial
  growth rate and yield. PLoS Computational Biology, 14 (2):e1006010,
  2018

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
[]{#OME:Exerc:ex1 label="OME:Exerc:ex1"}

Consider the model in Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"}. What would be the qualitative
effect of a change in oxygen concentration on the enzyme cost of the
three EFMs and on the choice of the optimal strategy?
:::

::: exercise
[]{#OME:Exerc:ex2 label="OME:Exerc:ex2"}

Consider the model in Figure
[1.2](#OME:fig:DiscreteSwitch){reference-type="ref"
reference="OME:fig:DiscreteSwitch"} under standard conditions (Box
[\[OME:Physicsblock:example_model_kinetics\]](#OME:Physicsblock:example_model_kinetics){reference-type="ref"
reference="OME:Physicsblock:example_model_kinetics"} and $\concgex = 1$,
such that EFM2 is optimal, and EFM1 second best (remember that the
higher the enzyme cost, the less optimal the EFM). What might happen
when we gradually increase the concentration $\concpex$? What is the
qualitative effect on the enzyme cost of the three EFMs?
:::

:::: exercise
[]{#OME:Exerc:exMaxGrowthRate label="OME:Exerc:exMaxGrowthRate"}

Consider the following small toy network:

::: center
![image](.//images/OME_branched_pathway.pdf){width="25%"}
:::

We want to optimize the specific pathway flux for the production of
$\metP$ (which is $\flux_3/\etot$, where we assume all enzymes to have
equal costs: i.e. $\etot = \enzconc_1 + \enzconc_2 + \enzconc_3$) at
steady state. We assume mass-action kinetics, meaning the rate is the
enzyme concentration times the forward rate constant times the substrate
minus the backward rate constant times the product:
$\flux = \enzconc (\krate^+ s - \krate^- p)$. Unless mentioned
otherwise, we use the values $s_2 = 10$, $\krate_1^+ = 2$,
$\krate_1^- = 1$, $\krate_2^+ = 3$, $\krate_2^- = 1$, $\krate_3^+ = 1$,
$\krate_3^- = 0.1$, $p = 0$ (concentrations are denoted by lower case
letters).

1.  Write out the rate equations for all three rates in terms of the
    parameters and the concentrations.

2.  Give an expression of the total enzyme concentration in terms of
    fluxes and the metabolite concentrations $s_1$ and $x$.

3.  Find the concentration of X for which the specific flux
    $\flux_3/\etot$ is maximal for $\enzconc_1 = 0$ and $s_2 = 10$, and
    also give the corresponding value of $\flux_3$. HINT: Is is easiest
    to set $\etot = 1$ and maximize $\flux_3$, replacing $\enzconc_3$
    using the equation for the total enzyme cost and the steady state
    assumption.

4.  Find the concentration of X for which the specific flux
    $\flux_3/e_T$ is maximal for $\enzconc_2 = 0$ and $s_1 = 10$, and
    also give the corresponding value of $\flux_3/\etot$.

5.  Find the concentration of X for which the enzyme cost is minimal for
    $\enzconc_1 = \enzconc_2$ and $s_1 = s_2 = 10$, and also give the
    corresponding value of $\flux_3/\etot$.

6.  What was the best distribution of enzymes from the three options
    above for $s_1=10$?

7.  Find the concentration of X for which the enzyme cost is minimal for
    $\enzconc_1 = 0$ and $s_1 = 50$, and also give the corresponding
    value of $\flux_3/\etot$.

8.  Find the concentration of X for which the enzyme cost is minimal for
    $\enzconc_2 = 0$ and $s_1 = 50$, and also give the corresponding
    value of $\flux_3/\etot$.

9.  Find the concentration of X for which the enzyme cost is minimal for
    $\enzconc_1 = \enzconc_2$ and $s_1 = 50$, and also give the
    corresponding value of $\flux_3/\etot$.

10. What was the best distribution of enzymes from the three options
    above for $s_1=50$?

11. Interpret the results from this problem in light of the proof shown
    in this chapter about the optimal specific flux being attained at an
    EFM.
::::
