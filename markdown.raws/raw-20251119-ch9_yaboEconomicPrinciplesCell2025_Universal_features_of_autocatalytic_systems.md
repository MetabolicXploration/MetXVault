# Universal features of autocatalytic systems {#AUT}

::: chapterhighlights
- A stoichiometric theory of autocatalysis is outlined, which is based
  on the notion of productivity (either economical or chemical). The
  framework is applied to the von Neumann universal constructor model as
  an example. New methods of identifying autocatalytic subnetworks in
  complex chemical networks follow from this approach.

- The expanding economic model of the von Neumann model is a linear
  model of a circular and productive economy also based on
  stoichiometric considerations. As shown in [@GagraniBlanco2024], a
  notion of growth factor introduced in this model has valuable
  applications for the characterization of autocatalytic chemical
  reaction networks.

- A special case of the von Neumann model is the Leontief model, from
  which the Leontief production function can be derived. This approach
  is useful in modeling certain features of cell metabolism, such as
  cell growth laws and inhibition of bacterial growth by various types
  of antibiotics.
:::

## Stoichiometric versus dynamical autocatalysis {#AUT:section:Structural}

### Stoichiometric autocatalysis

According to IUPAC, "an autocatalytic reaction is a chemical reaction in
which a product (or a reaction intermediate) also functions as a
catalyst. In such a reaction, the observed rate of reaction is often
found to increase with time from its initial value". While this
definition provides a sound kinetic characterization of autocatalysis,
it is not easy to use it to identify autocatalysis in situations in
which kinetics is poorly known. Such situations arise frequently when
trying to analyze complex chemical mixtures, such as astrophysical
samples analyzed by researchers studying the origin of life research, or
man-made prebiotic systems such as complex interacting RNA networks, in
which most of the species and reactions are unknown.

On the theory side, the concept of autocatalytic sets was introduced by
S. Kauffman in 1971, and played an important role in his early
investigations of the Origin of order in living systems. In 2004, W.
Hordijk and M. Steel expanded this original work by introducing the
concept of reflexively autocatalytic food-generated networks (RAFs),
namely self-sustaining networks that collectively catalyze all their
reactions using only compounds from the food sets [@XavierHordijk2020].
This formalism is based on the assumption that any compound (or a
fraction of them) involved in randomly picked reactions has a certain
probability to be catalytic [@JainKrishna2001]. Although very nice
results follow from this assumption, such as the existence of a phase
transition controlled by the connectivity of the network, this
assumption is a bit problematic, because a given species can act as a
catalyst or not depending on the presence of other molecules and
depending on the reactions it is part of. In other words, the
probability for a reaction to be catalytic is context dependent and
strongly constrained by the topology of the network itself. To address
both issues, namely the lack of available data on the kinetics and the
shortcomings of the RAF formalism, a better starting point is to define
autocatalysis from stoichiometry rather than from kinetics. While
alternate definitions of autocatalysis are possible
[@AndersenFlamm2021], we now detail the definition of
[@BlokhuisLacoste2020], which encompasses autocatalytic sets and RAFs as
particular cases.

Given a complete chemical network, autocatalysis is defined at the level
of a subnetwork of stoichiometric matrix $\Stoichmat$, i.e. for a subset
of species and reactions of the full network. Species which are not part
of the autocatalytic subnetwork can still play an important role, for
instance, food species or building blocks. The autocatalysis of this
subnetwork requires two essential properties: *autonomy* (i) and
*productivity* (ii). The *autonomy* condition is there to exclude direct
injection or loss of species from the environment within the set of
autocatalysts. More precisely, this condition requires that each species
is produced by at least one reaction (each row of the stoichiometric
matrix has at least one positive entry) and each reaction must at least
consume one species (each column has at least one negative entry). This
notion of autonomy is a close analog of the notion of circular economy
in the economic context, provided that species are replaced by goods,
and reactions are replaced by industry sectors of an economy.
*Productivity* (ii) means the absence of mass-like conservation laws and
is related to the notion of a productive economy. More precisely, this
condition requires the existence of a non-zero reaction vector $\fluxv$,
such that $$\begin{equation}
\label{AUT:eq:def_autocat}
\Delta \mathbf{n} = \Stoichmat \cdot \fluxv > 0,
\end{equation}$$ element-wise. The existence of the flux vector $\fluxv$
guarantees that there is a set of species and reactions such that all
species of the set are produced by the autocatalytic subnetwork. The
proof that this property is equivalent to the absence of mass-like
conservation law is the content of Gordan's theorem of linear algebra,
which is explained in the box
[\[AUT:box:Gordan\]](#AUT:box:Gordan){reference-type="ref"
reference="AUT:box:Gordan"}.

::: MathDetailblock
Gordan's theorem is the following result of linear algebra which takes
the form of an alternative: $$\begin{equation}
\label{AUT:eq:Gordan_1}
    \exists \fluxv \quad \rm{s.t.} \quad \Stoichmat \cdot \fluxv > 0, 
\end{equation}$$ or $$\begin{equation}
\label{AUT:eq:Gordan_2}
   \exists \boldsymbol{\rho}>0 \quad \rm{s.t.} \quad \Stoichmat^\top \cdot \boldsymbol{\rho} =0. 
\end{equation}$$ The first side of the alternative in
[\[AUT:eq:Gordan_1\]](#AUT:eq:Gordan_1){reference-type="ref"
reference="AUT:eq:Gordan_1"} corresponds to the stoichiometric
definition of autocatalysis, the second side of the alternative in
[\[AUT:eq:Gordan_2\]](#AUT:eq:Gordan_2){reference-type="ref"
reference="AUT:eq:Gordan_2"} corresponds to the existence of a so called
mass-like mass conservation law, i.e. a conservation law with only
strictly positive entries, in which case no autocatalysis is present.
Note that when autocatalysis is present, only mass-like conservation are
forbidden but not general conservation laws in which the entries of
$\rho$ are positive and negative. An example of an autocatalytic network
with non-mass like conservation law is given in
[@KamimuraSughiyama2024], which also provides a nice geometric
interpretation of conservation laws as manifolds. Note also that a
stronger condition for autocatalysis is the absence of any conservation
law, which mathematically means $\ker \Stoichmat^\top = 0$.
:::

A third more technical condition introduced in
Ref. [@BlokhuisLacoste2020] is that $\Stoichmat$ should be
*non-ambiguous* (iii) which means that a species can not be both a
reactant and a product of the same reaction. This condition (iii) is
less essential but is convenient as it ensures that catalytic steps can
be distinguished at the level of stoichiometric matrix. Indeed,
otherwise the stoichiometric matrix would be ambiguous in the sense that
it would not be possible to separate the contribution of the consumption
of reactants from the production of products. In practice it is always
possible to transform an ambiguous reaction into a non-ambiguous one
provided intermediates in the reaction are added. Another way to get
around the issue of ambiguity without having to transform the network,
is to define the chemical network from the start by two stoichiometric
matrices instead of one as we will do in section
[1.2](#AUT:section:Von Neumann){reference-type="ref"
reference="AUT:section:Von Neumann"}.

Remarkably, this mathematical definition is enough to guarantee the
existence of a small number of minimal autocatalytic motifs called
autocatalytic cores. The minimality of these cores means that they
cannot contain smaller cores in them. In [@BlokhuisLacoste2020], it was
found that with the above assumptions, only five minimal motifs could
exist, which are represented in
Fig. [1.1](#AUT:fig:motifs){reference-type="ref"
reference="AUT:fig:motifs"}. It also follows from that construction that
an orientation of the reactions in a core must exist such that $\fluxv$
has only non-negative components [@KoscKuperberg2024].

<figure id="AUT:fig:motifs" data-latex-placement="t!">
<table>
<tbody>
<tr>
<td style="text-align: left;"></td>
<td style="text-align: left;">Type I</td>
<td style="text-align: left;">Type II</td>
<td style="text-align: left;">Type III</td>
<td style="text-align: left;">Type IV</td>
<td style="text-align: left;">Type V</td>
</tr>
</tbody>
</table>
<div class="center">
<p><embed src=".//images/AUT_motifs.pdf" style="width:85.0%" /><br />
</p>
</div>
<figcaption>Five minimal autocatalytic motifs (figure taken from <span
class="citation" data-cites="BlokhuisLacoste2020"></span>). Yellow
circles represent species, black lines connecting them represent
reactions and the orange squares indicate the locations where further
reactions could be added while preserving the motif type.</figcaption>
</figure>

As a simple illustration of this framework, let us consider the
universal constructor which von Neumann introduced in 1940
[@vonNeumann1966]. This is an idealized machine $U$, that would be able
to construct any object including itself when given some set of
instructions $I$. von Neumann identified a potential recursion issue
related to the self-replication of the machine together with its
instructions and he also understood that for such a machine to evolve
without compromising its replication, an additional player in addition
to $U$ and $I$ was needed. This additional player would be a universal
copy machine $X$ that would copy the instructions without translating
them [@SuckjoonFangwei2018]. With this remarkable insight, von Neumann
foresaw the essential mechanism of the DNA based
translation-transcription machinery that we know today. We can summarize
the reactions in which the universal constructor $U$, the universal copy
machine $X$ and the instructions $I$ are involved by the following
simple chemical network : $$\begin{gather}
\label{AUT:eq:non-explicit}
     \ce{X  + I  ->2I +X }, \hspace{1em}  \nonumber \\
    \ce{U + I  ->2U + I}, \hspace{1em}   \\
    \ce{U + I  -> U + I + X}. \nonumber
\end{gather}$$ When written in this way, the sub-network of these three
reactions with the set $\{ U, I, X \}$ contains several catalytic steps,
so that neither conditions (i) nor (iii) are satisfied. To solve the
issue, let us introduce food species $F_1$, $F_2$ and $F_3$,
intermediate species $XIF_1$, $UIF_2$ and $UIF_3$ and their
corresponding reactions so that the network is no longer explicitly
catalytic : $$\begin{gather}
\label{AUT:eq:non-explicit}
     \ce{F_1 + X  + I  ->XIF_1}, \, \, \, \, \, \, \ce{XIF_1 -> 2I + X}, \hspace{1em} \nonumber  \\
    \ce{F_2 + U + I  ->UIF_2}, \, \, \, \, \, \, \ce{UIF_2 -> 2U + I}, \hspace{1em}  \\
    \ce{F_3 + U + I  -> UIF_3}, \, \, \, \, \, \, \ce{UIF_3 -> U + I + X}. \nonumber
\end{gather}$$ Now the subnetwork of species $\{ U, I, X \}$ satisfies
the conditions (i) (*autonomy*) and (iii) (*non-ambiguity*), and also
condition (ii) (*productivity*) because the reaction vector that
corresponds to summing all the reactions produces all the species of the
set, according to the overall reaction
$\ce{X + 2U + 3I -> 2X + 3U + 4I}$. Therefore this network is
autocatalytic from the point of view of stoichiometry. Note also that
all reactions have been assumed to be irreversible here, which is
allowed within the framework of [@BlokhuisLacoste2020], since
thermodynamic compatibility is not considered.

A significant benefit of the stoichiometric definition of autocatalysis
outlined above is that linear programming algorithms, which are a
classic tool of analysis of optimization problems, can be used to search
effectively for autocatalytic subnetworks within large chemical networks
[@PengLinderoth2022; @GagraniBlanco2024; @KoscKuperberg2024]. In
carrying out this program, the authors of [@GagraniBlanco2024] found
that the number of autocatalytic subnetworks typically grow
exponentially with system size. In practice, a much smaller number of
subnetworks is expected to be relevant dynamically in large networks, an
issue which we address now.

### Dynamical autocatalysis {#AUT:section:Dynamics}

Historically, autocatalysis as studied in classic chemistry has been
related to a certain type of kinetic pattern. To distinguish this
classic definition from the previous based on stoichiometry, we will
call this form of autocatalysis, dynamical autocatalysis. In this view,
dynamical autocatalysis is defined as a chemical process in which one of
the products catalyzes its own formation according to $$\begin{equation}
    \label{AUT:eq:autocat_def}
    \frac{\intd x_i}{\intd t}= k({\bf X}) \cdot x_i^n + f({\bf X}), \, \, \rm{for \, \, k>0, n>0, |k| \gg |f|, }
\end{equation}$$ where $\bf X$ is the vector of all the concentrations
$x_i$, the term $k({\bf X}) \cdot x_i^n$ describes the contribution from
autocatalysis while the function $f$ describes the contribution coming
from the rest of the chemical system [@PlassonBrandenburg2011]. It
follows from this definition that diverse forms of autocatalysis are
possible depending on $k({\bf X})$ and $n$, and that these forms could
remain concealed if $f({\bf X})$ is too large. It also follows from this
definition that when $k({\bf X})$ is constant, autocatalysis can
generate exponential growth for $n=1$, but also over-exponential $n>1$
or sub-exponential $n<1$ evolution. In practice, the exponential growth
regime is anyway limited to an intermediate time window either because
the reaction eventually runs out of substrates (at long times) or due to
product inhibition, which can trigger sub-exponential behavior. Further,
$k$ and $n$ are not independent factors since they arise from shared
physical factors (availability and diffusion of ligands, size and
flexibility of the molecules\...) resulting in a trade-off between these
two parameters that is relevant for designing catalysts or autocatalysts
from bottom up [@SakrefRivoire2024].

From the definition in
Eq. ([\[AUT:eq:autocat_def\]](#AUT:eq:autocat_def){reference-type="ref"
reference="AUT:eq:autocat_def"}), it follows that dynamical
autocatalysis has the potential to destabilize a dynamical state, which
would otherwise have remained stable. Recently, the connection between
the topology of the autocatalytic reaction network and its dynamical
stability has been explored in two separate works that address different
sides of that issue. In the first one, it was proven that for fully
connected dilute systems with no degradation, the stoichiometric
definition of autocatalysis leads to dynamical autocatalysis,
characterized by a strictly positive Lyapunov exponent
[@UnterbergerNghe2022]. In the second one, for a certain class of
parameter-rich kinetics, it was shown that the stoichiometric definition
of autocatalysis implies a choice of reaction rates for which an
unstable fixed point necessarily exists [@VassenaStadler2024]. In a
nutshell, the first work provides explicit results regarding the
relation between stoichiometric and dynamical aspects of autocatalysis
but the results are limited to the diluted regime, while the second work
does not have this limitation, but is only a proof of existence: it does
not provide an explicit method to obtain the reaction rate stated in the
result.

Several recent studies have explored growing systems from the point of
view of non-equilibrium thermodynamics [@SrinivasGopal2024]. In
particular, in [@KamimuraSughiyama2024], Kamimura et al. have built a
comprehensive chemical thermodynamic theory of open systems which are
also self-replicating. This approach clarifies the thermodynamic
conditions under which growth is possible in a system in which the
volume is also growing [@KamimuraSughiyama2024]. To include this change
of volume, these researchers developed an extension of traditional
chemical thermodynamics theory. The growth of the volume is an important
feature of autocatalysis, which manifests itself in certain experiments
such as that of [@LuBlokhuis2024]. In this work, small-molecule
autocatalytic reactions occur in compartments made of water in oil
droplets. Small molecules, which act as fuel in these reactions, can
diffuse between compartments while the large molecules which are
produced inside the compartments cannot diffuse across compartments.
This work provides a stunning demonstration that autocatalysis can drive
compartment growth, competition and reproduction.

The question of how to connect stoichiometric, kinetic and thermodynamic
features of autocatalysis is an ongoing active area of research which is
pursued by several groups theoretically
[@KoscKuperberg2024; @DesponsDecker2024; @KamimuraSughiyama2024; @Armand2024].
For instance, in [@DesponsDecker2024], a framework has been proposed to
derive structural and thermodynamic bounds for autocatalytic chemical
networks assuming mass-action law kinetics. The term structural means
that these bounds depend on the topology of the network but not on the
value of the rate constants. Another important structural property of
biochemical networks is for instance robust perfect adaptation (RPA).
This property means that there exist some subnetworks, with specific
topological features, whose parameters are irrelevant to the
steady-state properties of the rest of the network [@HironoGupta2025].

In [@KoscKuperberg2024], the authors proved there always exists a
well-defined CRN corresponding to an autocatalytic core, where by
well-defined, we mean that there exists a list of chemical species with
finite concentrations and a list of reversible chemical reactions
obeying mass action law kinetics that realize this network dynamically.
Within these assumptions, they also showed that thermodynamic
constraints prevent certain associations of autocatalytic cores, which
suggests that only a restricted number of cores is relevant for the
dynamics of a given autocatalytic network.

## von Neumann's model of an expanding economy {#AUT:section:Von Neumann}

Besides his theory of the universal constructor mentioned above, J. von
Neumann made another essential contribution to our topic by proposing in
1945 a model for an expanding economy. The model assumes the economy to
be circular, which means that products (or goods) are produced from
other goods and from building blocks using a number of processes with a
certain intensity $v_j$ [@Neumann1945]. There are $n$ goods and $m$
processes with $n<m$, which are characterized by constant ratios of
inputs to outputs. The model is formulated in terms of an output matrix
$B$ and an input matrix $A$. Since the total amount of good produced
must match the internal and external demand, described by the positive
vector $\vec{d}$, we have the equation

$$\begin{equation}
\mathbf{B} \cdot \fluxv = \mathbf{A} \cdot \fluxv + \vec{d}.
\end{equation}$$

This economic model can be directly mapped onto a chemical reaction
network, if goods are interpreted as chemical species, the vector
$\fluxv$ represent chemical fluxes [@BlancoGonzalez2024] and $d$ could
represent a dilution or degradation. To formalize this analogy, it is
convenient to split the stoichiometric matrix $\Stoichmat$ into the part
that concerns the production of products denoted $\Stoichmat^+$ and the
part that concerns the consumption of goods or species $\Stoichmat^-$,
so that we can use $\mathbf{B}=\Stoichmat^+, \mathbf{A}=\Stoichmat^-$
and $\Stoichmat=\Stoichmat^+ - \Stoichmat^-$. We say that an economy is
productive when there exists a non-negative vector $\fluxv$ such that
$\mathbf{B} \cdot \fluxv > \mathbf{A} \cdot \fluxv$. This condition maps
exactly to the notion of productivity introduced in
Eq. ([\[AUT:eq:def_autocat\]](#AUT:eq:def_autocat){reference-type="ref"
reference="AUT:eq:def_autocat"}) for stoichiometric autocatalysis, while
the condition of circular economy maps to the notion of autonomy
introduced at the same time.

Obviously, we must require the positivity of the vectors $\fluxv$ and
the condition $\sum_i v_i >0$. Another condition is that the economic
system is irreducible, which means that it cannot be decomposed into
isolated independent sub-parts (a sub-part being here a subset of goods
which does not require goods from outside the subset to produce all the
goods of the subset). To show the existence and unicity of the dynamic
equilibrium for such economies, J. von Neumann introduced the function
$$\begin{equation}
\label{AUT:eq:VN_1}
    \alpha(\fluxv)= \min_i \frac{\sum_j N_{ij}^+ \flux_j}{\sum_j N_{ij}^- \flux_j}, 
\end{equation}$$ where the minimum is taken over all goods $i$, and he
proved that the function $\alpha$ is uniquely defined from the vector
$\fluxv$, which is itself part of the solution. The quantity
$$\begin{equation}
\label{AUT:eq:MGF}
    \alpha=\max_{\fluxv} \alpha(\fluxv),
\end{equation}$$ represent a growth factor of the economic system and
the value of the vector $\fluxv$ at the maximum describes the set of
goods that defines a dynamic economic equilibrium.

In [@BlancoGonzalez2024], Blanco et al. applied this framework to the
study of autocatalytic reaction networks. They underlined the importance
of $\alpha$ for chemical reaction networks, which they call the maximum
growth factor (MGF). Note that this maximum growth factor is different
from the dynamical growth rate of species within the network. The MGF
does not have dimensions of a growth rate, instead it is a dimensionless
factor, which can be evaluated based only stoichiometry. Blanco et al.
proved that this MGF is strictly larger than one, if the network is
autocatalytic [@BlancoGonzalez2024]. Conversely, if an autonomous
network (where autonomy is now defined at the level of $\Stoichmat^-$
and $\Stoichmat^+$) has an MGF strictly larger than one, then it is
autocatalytic. As an illustration, the autocatalytic nature of the
network of
Eq. ([\[AUT:eq:non-explicit\]](#AUT:eq:non-explicit){reference-type="ref"
reference="AUT:eq:non-explicit"}) can be assessed without the need of
introducing intermediates, because one can show that its MGF is strictly
larger than one and that it is autonomous.

Blanco et al. also developed efficient algorithms to identify the
strongest, maximal and minimal autocatalytic subnetworks, and used them
to study the formose and E. coli reaction networks. The formose network
is an important prebiotic network, which is known to be autocatalytic.
Their results are markedly different for the two networks as shown in
Fig. [1.2](#AUT:fig:praful_figures){reference-type="ref"
reference="AUT:fig:praful_figures"}. From an analysis of MGF of
subnetworks, they found that in the formose network, a single subnetwork
dominates all the others but is fragile with respect to perturbations.
In contrast, the *E. coli* network is built from interlinked cores,
which together forms a robust structure.

<figure id="AUT:fig:praful_figures" data-latex-placement="t!">
<p>(A)     Formose network (B)     <em>E. coli</em> network</p>
<div class="center">
<p><embed src=".//images/AUT_formose_network.pdf" style="width:42.0%" />
<embed src=".//images/AUT_ecoli_network.pdf"
style="width:47.0%" /><br />
<embed src=".//images/AUT_flow_colorbar.pdf"
style="width:50.0%" /><br />
Flow intensity</p>
</div>
<figcaption>Autonomous subnetworks with highest value of MGF are shown
for the formose network (A) and for the <em>E. coli</em> metabolism (B).
The intensity of fluxes in each subnetwork is shown with the color
scale. The figure is reproduced from <span class="citation"
data-cites="GagraniBlanco2024"></span> with permission from the
authors.</figcaption>
</figure>

::: Ecoblock
In economics, production functions relate the quantities of outputs to
that of inputs in a system. There are various production functions
commonly used in economics, one of the most well-known is the
Cobb-Douglas production function
[@CobbDouglas1928; @GrilichesMairesse1999], which can be written in a
general way:

$$\begin{equation}
    y = c \prod_i x_i^{\alpha_i},
\end{equation}$$

where $x_i$ are production factors (which could be labor, capital or
other factors), $y$ is an amount of product and $c, \alpha_i$ are
positive coefficients. Mathematically, this law bears similarities with
the mass action law in chemistry, where the rate of production of a
species is related to the product of the concentrations of the reactants
to the power of their associated stoichiometric coefficient. A more
general production function is the constant elasticity of substitution
(CES) production function [@KlumpMcAdam2012]. This function accounts for
the fact that one product may be substituted with another one and can be
written in the form: $$\begin{equation}
    y = c \left(\sum_i \alpha_i x_i^{\rho}\right)^{\frac{1}{\rho}}.
\end{equation}$$

Here, $\rho$ is the coefficient of substitution and $\alpha_i$ is the
weight of the production factor $i$ in the total production
($\sum_i \alpha_i = 1$). Instead of $\rho$, one often uses the
elasticity of substitution $\sigma$ which is such that
$\rho = \frac{\sigma - 1}{\sigma}$.

Here it is assumed that the elasticity of substitution is the same for
all pairs of production factors. Note that $\sigma$ could also be
defined as an elasticity coefficient that compares the change in the
ratio of inputs to changes in the ratio of marginal products. Indeed,
the marginal product with respect to factor $j$ is
$y_j = \partial y / \partial x_j = c \rho \alpha_j x_j^{\rho - 1}\left(\sum_i \alpha_i x_i^{\rho}\right)^{\frac{1-\rho}{\rho}}$
and represents the sensitivity of the product to the amount of
production factor $j$. Therefore,
$y_j/y_k = \alpha_j x_j^{\rho-1}/\alpha_k x_k^{\rho-1}$, and we recover
that :

$$\begin{align}
    \sigma = \frac{\partial \ln(x_j/x_k)}{\partial \ln(y_k/y_j)}.
\end{align}$$

Therefore, $\sigma$ measures precisely how the ratio of two production
factors is modified when the ratio of two corresponding marginal
products is modified. Now, three famous cases can be considered
[@KlumpMcAdam2012]:

- $\sigma \to \infty$ : In this case, any modification in the ratio of
  marginal products would require an infinite modification in the ratio
  of production factors. This means that the ratio of marginal products
  remains constant whatever the modification in the ratio of production
  factor. This is the so called *perfect factor substitution* limit.
  Indeed, the CES production function becomes linear ($\rho = 1$),
  $y = c\sum_i \alpha_i x_i$, and any production factor can be
  substituted by another (even if $\exists i, \, x_i = 0$, it can be
  replaced by any other $x_j$).

- $\sigma = 1$ : In this case, a modification in the ratio of marginal
  products translates to the same modification in the ratio of
  production factors. If we want the dependency of the production in
  production factor $j$, we need to double the amount of production
  factor $j$. This limit corresponds to $\rho\to 0$, in which case we
  recover the *Cobb-Douglas* production function
  $y=c \prod_i x_i^{\alpha_i}$. This means that the level of
  substitution of a any production factor is null (if one of the
  $x_i = 0$, then $y=0$). Interestingly, for all values of
  $\sigma \in [0,1]$, there is no possible substitution between
  production factors.

- $\sigma = 0$ : This case is particularly interesting, it means that
  the ratios of the production factors $x_j/x_k$ are fixed whatever the
  ratios $y_j/y_k$. In this limit we recover the so called *Leontief
  function with fixed factor proportions*. There is still no
  substitution between the products (if one $x_i = 0$, then $y=0$), but
  this also means that forming one unit of product always requires the
  production factors in the same proportions. This corresponds to
  $\rho \to -\infty$, which gives $y = c\min(x_i)$. Interestingly, this
  is a way to get rid of the coefficients $\alpha_i$ which represent the
  share of each production factor in the total production. This boils
  down to saying that production is limited by the scarcest resource.
:::

### Leontief's production function {#AUT:subsection:Leontief}

Wassily W. Leontief won the Nobel prize in economics for his work on
input-output relations in economic systems, which he started in 1936
[@Leontief1936]. He later developed this mathematical tool to study the
American economy, and in particular the interdependency between
industries.

The Leontief model is the special case of the von Neumann model, in
which each productive activity has a single output (no joint products)
whereas there may be many activities producing the same output and each
good is produced by at least one industry. As in the von Neumann model,
it is also assumed in the Leontief model that goods are produced with
fixed ratios of production factors. This assumption leads to the
Leontief production function discussed in the box
[\[AUT:box:production_functions\]](#AUT:box:production_functions){reference-type="ref"
reference="AUT:box:production_functions"}.

We can think of this production function as the outcome of a supply
chain where production factors have to be assembled in fixed proportions
in order to form a product. For instance, in order to build one bike,
you need two wheels, one saddle, two pedals, etc. Those ratios are
fixed, or equivalently the elasticity of substitution is $\sigma = 0$ as
discussed in the box
[\[AUT:box:production_functions\]](#AUT:box:production_functions){reference-type="ref"
reference="AUT:box:production_functions"}. If you want to form a product
$P$, for which you need to assemble $n_1$ units of $R_1$, $n_2$ units of
$R_2$, \... up to $n_N$ units of $R_N$, the production rate will be
limited by the smaller value of $R_j/n_j$, that is the number of sets of
resource $j$ required to produce $P$. If the minimum time to produce one
unit of $P$ is $\tau_P$, and the minimum time to use resource $R_j$ in
order to produce one $P$ is $\tau_i$, we can write

$$\begin{equation}
    \frac{\intd P}{\intd t} = \frac{1}{\tau_P}\min \left(\frac{\tau_P}{\tau_1}\frac{R_1}{n_1}, \frac{\tau_P}{\tau_2}\frac{R_2}{n_2}, ..., \frac{\tau_P}{\tau_N}\frac{R_N}{n_N} \right).
\end{equation}$$

Indeed, $\tau_P/\tau_j n_j$ is the number of products which can be
simultaneously produced from one resource $j$. This result holds true if
resources are fully allocated to the production of $P$, but if several
products $P_i$ need to be produced in parallel, one resource may be used
by different production chains simultaneously, meaning that a fraction
$\alpha_{i,j}$ of total available resources $R_j$ must be used for the
specific product $P_i$, so that :

$$\begin{equation}
    \frac{\intd P_i}{\intd t} = \frac{1}{\tau_P}\min \left( \alpha_{i,1}\frac{\tau_P}{\tau_1}\frac{R_1}{n_1}, \alpha_{i,2}\frac{\tau_P}{\tau_2}\frac{R_2}{n_2}, ..., \alpha_{i,N}\frac{\tau_P}{\tau_N}\frac{R_N}{n_N} \right).
\end{equation}$$

Then the prefactor before $R_i$ represents the maximal number of copies
of the product that you can produce simultaneously from one unit of
resource $i$. The fact that resources may not be substituted with other
resources has important consequences for cell metabolism
[@RoyGoberman2021].

In the problem [\[ex:Leontief\]](#ex:Leontief){reference-type="ref"
reference="ex:Leontief"}, we study a single resource - single product
industry or workstation and we show that a Leontief production function
emerges from mass-action law kinetics when a certain time scale
separation holds. This example is important because it illustrates that
the Leontief production function not only involves fluxes associated to
reactions or industries but can typically also include stocks associated
to goods or metabolites, which are only available in finite amounts.

Further applications of this formalism to describe for instance the
ability of a metabolic network to switch from one behavior to another
one (as in the crabtree or Warburg effects in biology and in the Giffen
behavior in economics) is studied in [@YamagishiHatakeyama2021] and in a
coming chapter to be written.

### Liebig's law {#AUT:section:liebig}

Interestingly, the idea that the production rate could be limited by the
scarcest resource is present in the field of agronomy under the name of
*Liebig's law of minimum*
[@BloomChapin1985; @VanDerPloegBohm1999; @TangRiley2021; @Echavarria2023].
It was initially used to describe plant growth, which requires various
resources, and where it is observed that varying the amount of fully
available resources did not modify the final production. This suggests
that only scarce resources will limit production and translates to the
principle that when a population is growing using various resources, the
scarcest will set the growth rate, and the others will be consumed
accordingly. This law can be used to model the growth of an organism in
an environment where resources are constrained. The link between mass
action laws and Liebig's law of minimum has been studied
[@TangRiley2021]. The interest of this method is to obtain equations
that are easier to solve on domains where one resource is scarcest. One
main difference between the Leontief production function and Liebig's
law of the minimum is that for the latter, the minimum is not necessary
taken between the numbers of each production factor, but between the
yields of those production factors (which can be non-linear functions)
[@MustafinKantarbayeva2018]. In particular, this means that the rate of
production is set by the minimum of the yields of each production factor
:

$$\begin{equation}
    \frac{\intd Y}{\intd t} = \frac{1}{\tau}
    \min\left(\{f_i(x_i)\} \right),
\end{equation}$$

where $f_i$ are functions of the production factors $x_i$. To model the
requirements of plants in nutrients, yields given by Michaelis-Menten
kinetics can be used [@TangRiley2021]. Instead of directly comparing the
numbers of each production factors, it consists in comparing the yields.
However, the idea that one resource will be limiting remains the same.

### Application to metabolism {#AUT:section:metabolism}

The law of minimum was used to build simplified models of metabolism as
an ensemble of coupled autocatalytic cycles [@RoyGoberman2021].
Metabolism is seen as a supply chain, where production factors must
first be produced and then assembled in fixed proportions to form a
product. We call $P$ the number of proteins of one type, produced by
translating mRNA (of number $m$) with ribosomes (of number $R$) and
substrates (of number $S$). Using the Leontief production function, we
can write (following the method of [@RoyGoberman2021]) :

$$\begin{equation}
    \left.\frac{\intd P}{\intd t}\right|_{\text{prod}} = \frac{1}{\tau_P} \min\left(\alpha_P R,~\alpha_P S,~\frac{\tau_P}{\tau_e s_R}m,~\ldots\right)
\end{equation}$$

Ribosomes and substrates have to be used simultaneously to produce
different types of proteins, $\alpha_P$ is the fraction of the total
population of ribosomes (and substrates) used to produce the particular
protein $P$. The minimum time to produce one $P$ is $\tau_P$, the
minimum time to elongate the polymer by one amino acid is $\tau_e$, and
$s_R$ is the size of the domain on the mRNA that has to be dedicated to
the production of one polymer $P$ at a given time. As explained in
[@RoyGoberman2021], $\tau_P/\tau_e s_R$ is then the maximum number of
ribosomes that can translate simultaneously one mRNA, and thus the
maximum number of copies of $P$ you can produce simultaneously from one
unit of mRNA. This is indeed what was predicted from Leontief's model
for input-output systems: the prefactor before every amount of resources
is the maximum number of copies of the protein you can produce
simultaneously from this specific resource. This term is that of
production of the protein, now the protein could be consumed to form a
product, or degraded.

To use ribosomes, you first need to form ribosomes by assembling
proteins and ribosomal RNA. Similarly, to use mRNA you must first
polymerize RNA. This suggests that a minimal autocatalytic network that
begins to capture the structure of the transcription-translation
machinery is made of two coupled autocatalytic cycles associated
respectively to RNA and ribosomes. These two cycles will then be
described by coupled equations with production terms described by
Leontief's production function [@RoyGoberman2021].

From such an framework [@RoyGoberman2021], one can derive the various
growth laws that characterize the cell metabolism, which have been
discussed in detail in various chapters of this book. Let us mention
briefly two recent works that follow this line of research : In the
first one carried out in [@CalabreseCiandrini2024], the authors noticed
that RNA polymerase, and mRNA levels correlate in experiments with
growth rates in contrast to the belief that ribosomes should be the sole
drivers of the growth rate. To explain these observations, the authors
developed a theoretical framework building on [@RoyGoberman2021], which
account for the joint role of all these factors in the observed growth
rate.

Another recent application of the above framework concerns a model for
the inhibition of bacterial growth by antibiotics [@LedouxLacoste2025].
In that work, the cell metabolism is modeled as two coupled
autocatalytic cycles, in which one cycle describes the production of
ribosomes, while the other describes RNA-polymerase production as shown
in Fig. [1.3](#AUT:fig:antibio){reference-type="ref"
reference="AUT:fig:antibio"}.

<figure id="AUT:fig:antibio" data-latex-placement="t!">
<p>(A) (B)<br />
<embed src=".//images/AUT_antibio.pdf" style="width:44.0%" /></p>
<figcaption>(A) Scheme of coupled autocatalytic networks interacting
with a toxic agent. The orange box linking two arrows represents the
Leontief production function. <span class="math inline">\(B_1\)</span>
represents active ribosomes; <span class="math inline">\(C_1\)</span>
active RNA polymerases; similarly <span class="math inline">\(B_2, ...,
B_{N-1}\)</span> and <span class="math inline">\(C_2, ...,
C_{K-1}\)</span> are intermediates, <span
class="math inline">\(R_N,R_K\)</span> are building blocks. We suppose
that “toxic” inhibiting agents in numbers <span
class="math inline">\(A\)</span> can bind to one of the autocatalysts
(chosen here to be <span class="math inline">\(B_1\)</span> for
simplicity). (B) Illustration of the growth laws when varying either the
amount of antibiotics or the nutrient quality linked to pre-exposure
growth rate <span class="math inline">\(\lambda_0\)</span> displayed on
the right scale. This figure is reproduced from <span class="citation"
data-cites="LedouxLacoste2025"></span> with permission.</figcaption>
</figure>

It is assumed that the antibiotic inhibits one of these two essential
autocatalytic cycles by targeting some essential metabolites in them.
Growth laws can be recovered from the model as shown in
Fig. [1.3](#AUT:fig:antibio){reference-type="ref"
reference="AUT:fig:antibio"}B. A first law describes the increase of
ribosome fraction as a function of growth rate when nutrient quality is
increased (solid magenta curve) while a second growth law describes the
up-regulation of ribosomes as a result of the inhibition of translation
by ribosome inhibitors (colored solid lines). In addition, the model
successfully describes the experimental dependence of the growth rate on
various types of antibiotics and confirms the existence of growth
bistability, namely a regime in which two possible values of the growth
rates are possible in the same range of physical parameters.

## Concluding remarks

In this chapter, we have established a connection between the universal
constructor model and the expanding economic model, which were both
introduced by von Neumann. Interestingly, von Neumann himself did not
discuss the relation between these two works, which we make in this
chapter. This expanding economic model of von Neumann (1945) and the
input-output model of Leontief (1936, 1941) laid the foundation of a
modern framework for economic analysis. Their framework turned out to be
essential to quantify the relative interdependency of various parts of
an economy and the nature and the structure of economic equilibria.
Remarkably, these tools continue to inspire developments in other fields
as recent studies of autocatalytic chemical networks show. Thanks to
linear programming methods, we are now able to identify autocatalytic
subnetworks efficiently and characterize them using notions such as the
maximum growth factor or using thermodynamic bounds. More work is needed
to understand the interactions between autocatalytic networks, and their
role in the emergence of chemical complexity linked to pre-Darwinian
evolution.

## Acknowledgements {#acknowledgements .unnumbered}

We thank R. Pugatch, Y. De Decker, A. Despons and P. Gagrani for
insightful comments and a careful reading of this chapter. We thank R.
Pugatch for providing us with a nice logo for this chapter.

## Recommended readings {#recommended-readings .unnumbered}

This book chapter is mainly based on these two recent articles: "A
unifying autocatalytic network-based framework for bacterial growth
laws" by @RoyGoberman2021, and "Universal motifs and the diversity of
autocatalytic systems" by @BlokhuisLacoste2020.

## Problems {#problems .unnumbered}

::: exercise
[]{#AUT:ex:Leontief label="AUT:ex:Leontief"} We model a workstation with
a single resource and a single product [@MustafinKantarbayeva2018]. Let
$x$ be the amount of available resource or stock, $r$ the supply rate of
this stock, $q$ the specific rate with which the stock is being lost or
degraded. Further, let $u$ (resp. $v$) be the number of idle
(resp. busy) machines which can process the stock. The processing time
is $1/\beta$, $b$ is the number of output products per machine, $a$ is
rate of capture of stock by machines, $\alpha$ is how many machines get
involved per unit resource/stock.

1.  Assuming mass action law for the processing of the stock, show that
    the equations of the problem are $$\begin{eqnarray}
        \dot{x} &=& r -a ~u~ x -q~ x, \nonumber \\
        \dot{u} &=& \beta v  -\alpha~  u~ x , \nonumber \\
        \dot{v} &=& -\beta v  +\alpha~  u ~x , \nonumber \\
        \dot{y} &=& b  v. \nonumber
    \end{eqnarray}$$

2.  Show that the total number of machines is a constant denoted $u_0$.
    Derive the steady state number of busy machines $\bar{v}$ in terms
    of the steady state amount of stock $\bar{x}$. Comment on the form
    of the output production that you find.

3.  Introduce the variables $\gamma=q/(a ~u_0)$ and
    $\rho=\alpha ~r /(a~ \beta~ u_0)$. Derive the expression of
    $\bar{v}$ in the limit $\gamma \ll 1$ and $\gamma \ll | \rho -1 |$
    and show that it has a Leontief form. Interpret this form in terms
    of how the stock is handled in the regime $\rho <1$ and $\rho>1$.

4.  Show that for small but non-zero $\gamma$, the input-output function
    falls below the line boundary defined by the Leontief function.
:::

::: exercise
[]{#AUT:ex:UPF label="AUT:ex:UPF"}

The UPF model is a toy model of metabolism made of two coupled
autocatalytic cycles [@RoyGoberman2021]. In the model, a fraction
$\alpha$ of machines of type $U$ catalyze themselves. The remaining
machines synthetize another type of machines $P$. The $P$ machines
convert an external substrate $f$ to an internal substrate $F$, which is
used by $U$ to make more copies of itself and new $P$s. To simplify, we
assume that to make one more unit of $U$ by the first reaction, one unit
of $F$ is needed, and one unit to make one unit of $P$ by the second
reaction.

The model is defined by the following set of equations $$\begin{gather}
     \ce{U  + F  ->[$\alpha$] 2U}, \hspace{1em}  \nonumber \\
    \ce{F + U  ->[$1-\alpha$] P + U}, \hspace{1em}  \nonumber \\
    \ce{f + P  -> F + P}, 
    \hspace{1em} \nonumber \\
    \ce{U -> \emptyset}. \nonumber
\end{gather}$$

1.  Let $n_i$ be the number of molecules of type $i$, where
    $i \in \{ U,P,F,f \}$. The life type of a machine of type $U$ is
    $\tau_L$, the incorporation time of $f$ into $F$ is $\tau_F$ and the
    incorporation time of one unit $F$ is $\tau_a$. Show that within the
    framework of Leontief production functions, the equations of the
    model are $$\begin{align}
     \begin{split}
            \frac{\intd n_U}{\intd t} &= \frac{\alpha \min(n_U,n_F)}{\tau_a}- \frac{n_U}{\tau_L} \\
            \frac{\intd n_P}{\intd t} &= \frac{(1-\alpha) \min(n_U,n_F)}{\tau_a} \\
            \frac{\intd n_F}{\intd t} &= \frac{\min(n_P,n_f)}{ \tau_F}- \frac{\min(n_U,n_F)}{ \tau_a}\,.
    \end{split}
    \end{align}$$

2.  Discuss the four limiting regimes of the model: (i) $n_F \gg n_U$
    and $n_f \gg n_P$, (ii) $n_F \gg n_U$ and $n_f \ll n_P$, (iii)
    $n_F \ll n_U$ and $n_f \gg n_P$ and (iv) $n_F \ll n_U$ and
    $n_f \ll n_P$. Simplify the equations for each regime by introducing
    a common growth rate $\mu$.

3.  Summarize your results by deriving the growth laws of the various
    regimes in a single plot representing $\alpha$ vs. $\mu$.
:::

::: exercise
[]{#AUT:ex:MGF label="AUT:ex:MGF"}

1.  Calculate the MGF introduced in
    Eq. ([\[AUT:eq:MGF\]](#AUT:eq:MGF){reference-type="ref"
    reference="AUT:eq:MGF"}) for the following two simple networks :
    $$\begin{align}
        \ce{A} &\longrightarrow \ce{B} \nonumber \\
        \ce{B} &\longrightarrow \ce{2A}
    \end{align}$$ and $$\begin{align}
         \ce{2A &\longrightarrow B} \nonumber \\
        \ce{B &\longrightarrow A}.
    \end{align}$$

2.  Comment on the values obtained in the previous question.
:::
