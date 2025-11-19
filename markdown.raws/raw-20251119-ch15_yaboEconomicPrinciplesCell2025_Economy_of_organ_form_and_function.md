# Economy of organ form and function {#ORG}

::: chapterhighlights
- This chapter extends the concept of economy that previous chapters
  have elaborated by considering its application to the organ and the
  living organisms.

- The development of organs in pluricellular living organisms is
  conditioned by a number of factors such as nutrients, energy, and form
  that are here considered in the context of the economy of the organ
  function

- The mammalian respiratory system is subject to a high degree of
  constraint, primarily energetic and morphometric in nature, that
  played a decisive role in shaping the lung through evolutionary
  processes.

- The lung is the organ that is most directly responsible for
  respiration, a process that involves connecting the external
  environment to the cellular compartment through the ventilation.

- We show that the constraints on this major organ imply a high level of
  complexity of the organ's shape and a precise control of the
  ventilation.

- The scaling laws that govern the development and function of lung and
  are common to the entire mammalian class condition the lung's growth
  and determine its shape have been treated in previous works

- Through several examples, we demonstrate how these scaling i.e.,
  *allometric* laws control the ventilation, and the respiratory
  processes in general.
:::

## Optimization of organs and systems {#ORG:Sec:Introduction}

In the previous chapters, the central model of the cell has been deeply
explored. On another scale, the integration of cells into larger
structures such as tissues, organs, and entire systems in multicellular
organisms requires an extension of the main concepts presented in this
book. Nevertheless, the completion of the multiple functions of an organ
follows the same general principles as for individual cells, including
the economic aspects.

### Organs and constraints

The way that a cell population aggregates itself into a high-level
structure, as part of a pluricellular organism, has been determined
through evolutionary processes, following a more general path of
specialization of structures and functions. Each organ evolved to
fulfill its functions in the most optimized manner. This observation
leads us to interrogate the concept of optimization for such a large
structure -- from a cellular point of view. In the context of organ
function, optimization can be defined through the processes by which the
functions are fulfilled as best as possible while minimizing the
associated cost variables. Among those variables, energy plays a central
role. Thus, one possibility for constraining the organ would be to
maintain its function at an optimal level while minimizing its cost in
energy. This effect can be expressed mathematically. Let us define the
cost in energy $\mathcal{E}$ which depends on one or more variables
$x \in \mathbb{R}^n$ ($n \geqslant 1$). Furthermore, let us define one
or more equality constraints to our problem, $c(x) = 0$, where
$c \, : \, \mathbb{R}^n \to \mathbb{R}^m$. The optimization problem
under constraints comes down to finding an optimal value for $x$ that
minimizes the function $\mathcal{E}(x)$ while $x$ satisfies $c(x) = 0$.
This results in $$\begin{equation}
\label{eq:opti}
    \min \limits_{x \in \mathbb{R}^n} \mathcal{E}(x), \text{  such that  } c(x) = 0.
\end{equation}$$ The optimization under constraint problem can be solved
using the Lagrangian function,
$$\mathcal{L}(x,\lambda) = \mathcal{E}(x) - \sum_{k=1}^m \lambda_k c_k(x),$$
where the $\lambda_k$ are Lagrange multipliers. Indeed, if we assume
that $x_*$ is the optimal solution to the
problem [\[eq:opti\]](#eq:opti){reference-type="eqref"
reference="eq:opti"}, then thanks to the Lagrange multiplier theorem,
there exists a unique Lagrange multiplier $\lambda_*$ such that,
$$\nabla \mathcal{E}(x_*) = \lambda_*^T J_c(x_*),$$ where $J_c$ is the
Jacobian of the function $c$. It implies that the optimal solution $x_*$
is a stationary point of $\mathcal{L}$, satisfying the condition of
minimal energy expenditure.

A study of the constraints on the cardiac system offers an excellent
example of energy optimization, due to high consumption of the heart.
The cardiac pump delivers deoxygenated blood to the lung through
pulmonary circulation and brings oxygenated blood to the whole body
through systemic circulation [@West2011]. Interestingly, blood pressure
developed in both ventricles are not of the same order of magnitude,
with a left ventricular pressure approximately ten times larger than the
right ventricular one [@West2011]. This makes sense from an energetic
point of view; the heart requires a non-negligible amount of energy to
fulfill its role of blood pumping. Furthermore, as with any mechanical
system, only a fraction of the energy consumed (mainly in the form of
ATP) is converted in mechanical work -- around
25% [@KnaapenGermans2007], the rest being dissipated as heat. Thus, the
pumping work tends to be optimized from an energy consumption point of
view. On one hand, the pressure needed to irrigate the pulmonary
circulation is low; the lung presents a small value of resistance to
perfusion, and its apex is located only centimeters above the heart
position. And on the other hand, the pressure developed in the systemic
circulation must allow the oxygenated blood to irrigate all the organs,
including high-energy consumers -- muscles, brain -- that located
further above heart position, developing a hydrostatic pressure that the
blood flow has to overcome [@West2011]. It is to be noted that this
energetic optimization is also connected to the metabolism requirements,
with a pumping work closely related to the body's O$_2$ consumption,
which ensures an optimized adaptation of the cardiac output to the body
energy requirements.

Although often considered as a major aspect, this energetic constraint
is far from being the only condition for a proper functioning of the
organ. Other variables such as nutrient consumption, metabolic
integration or physical constraints participate in shaping the organ
function. Brain development in primates, and humans especially, is a
prime example of effect that combination of several constraints has on
energetic and nutrients availability. The underlying mechanisms that
determine the evolution towards a large and complex brain structure in
humans are still debated [@dunbar_why_2017]. However, it is evident that
the development and normal function of this organ is dependent on
adequate and specific energetic and nutrients inputs. From the energetic
point of view, brain metabolism largely depends on glucose consumption.
However, in case of high consumption and/or deprivation, ketones
metabolism takes place in order to furnish a fast and rich source of
energy for the organ. Ketones are catabolized mainly in the
liver [@CotterSchugar2013], and have the important property of being
able to cross the blood-brain barrier, to the contrary of long chains of
saturated fatty acids [@MitchellHatch2011]. In parallel, proper brain
development and function require a large input of specific nutrients
that are not common in every food source [@CunnaneCrawford2014]. Among
those, iodine and iron appear to be essential for the brain, and exert a
strong constraint on its adequate growth and functioning. The notable
presence of iodine-enriched food sources close to the sea shores,
compared to traditional terrestrial food sources, is thought to have
favored the recent development of the so-called *shore-based paradigm*
of human brain evolution i.e., that the access to seafood produce
supported and enhanced brain development in early hominid populations,
leading to increased brain mass and cognitive functions in those
populations [@CunnaneCrawford2014]. Among these considerations, let us
remind that any organ has to develop and function in specific
localization and body environment. Thus, the constraints applied to an
organ and its development and function can also be of morphometric
nature.

### Energy conversion in living systems

When energy is transferred to a system, its response manifests itself at
the microscopic level by the excitation of its individual degrees of
freedom, and at the global level when collective excitations are
possible. In generic terms, a thermodynamic machine is defined as a
system where an incident energy flow *dispersed* is converted into an
energy flow *aggregated* and a loss flow. This conversion is performed
by a thermodynamic *working fluid* which, carrying entropy, leads to a
coupling between the respective potentials through the equations of
state.

In the case of thermal machines, the dispersed form of energy is called
heat and its associated potential is temperature, while the aggregated
form is called work and its associated potential is, for example,
pressure. Temperature and pressure are linked by one or more equations
of state. The system response results from the collective response of
the microscopic degrees of freedom of the working fluid. Thus, part of
the energy received by the working fluid can be made available to a load
on a global, and possibly macroscopic, scale for a given purpose as
useful work, the remainder being redistributed (dispersed) at the
microscopic level and dissipated due to internal friction and any other
dispersion processes imposed by the boundary
conditions [@Volkenshtein1983]. Conversion efficiency is therefore
closely related to the proportion of energy allocated to the system's
collective modes.

Living organisms are open, out-of-equilibrium and dissipative systems,
as they continuously exchange energy and matter with their
environment [@GlansdorffPrigogine1971]. Unlike classical thermodynamic
engines, for which equilibrium models can be constructed using extremal
principles, such a possibility does not exist in the case of living
organisms due to the absence of truly identifiable equilibrium states
and the absence of principle for non-equilibrium systems. Nevertheless,
assuming a global system close to equilibrium, the development of a
tractable thermodynamic model of metabolism can be based on notions from
classical equilibrium thermodynamics. In this approach, the working
fluid acts as a conversion medium, characterized by its thermoelastic
properties, or chemicoelastic coefficient for chemical systems.

### The example of the lung

As an example of an organ submitted to geometric limitations, the lung
has to face, from its early development to its mature state, multiple
constraints on its morphometry and proper functioning. The principal
role of this organ is, as well known, to establish the connection
between the respiratory gases in the atmosphere and these in circulation
in the body i.e., O$_2$ as a reactive agent, and CO$_2$ as a by-product
that has to be eliminated from the organism. To fulfill its role, the
lung has evolved in a manner that maximizes the gas exchange surface --
as diffusion is a surface phenomenon -- in a reduced thoracic volume.
This surface-to-volume requirement has forged the lung structure has it
is known; an intricate dichotomic bronchial tree that conducts the air
inwards and outwards, to and from the alveolar sacs, respectively. This
semi-fractal, space-filling structure, presents the advantages of an
extremely wide exchange surface enclosed in a relatively small
volume [@West2011].

The mechanisms of development of the lung branching structure in a
closed environment is still a debated question [@ClementBlanc2012].
Indeed, the tree structure presents a series of specific characteristics
necessary for a proper functioning of the organ. Among these, the
space-filling aspect of the bronchial tree is remarkable, as it solves
the problem of the surface-to-volume constraint of the organ. In
addition, the whole bronchial tree is a self-avoiding structure, as no
bronchus enters in contact with other ones in its local environment,
which ensures a proper circulation of the air in the structure. It is
striking that these properties, which can be found in fractal
geometries, are observed in any well-functioning lung structure, leading
to important developmental questionings. For example, the pattern of
branching of the bronchi, although strongly stereotyped in the first
generations starting from the trachea, appears to follow a space-filling
procedural development rather than a deterministic branching
pattern [@ClementBlanc2012]. Accordingly, some authors have developed a
set of hypotheses that tend to explain these mechanisms. A group of
restricted genes would encode the steps of branching and growth of the
bronchi during the organ development, ensuring a proper structure of the
adult lung, following procedural steps somehow encoded in genes or
groups of genes coding for periodicity, bifurcating and rotating
routines. However, to the best of our knowledge, these genes have not
been determined nor a proper molecular mechanism of stereotypical
branching.

Among the questions raised by the *programmed morphogenesis* approach,
the link between the molecular dimensions and the organ world are still
elusive. Another path for branching procedure, which could reconcile the
deterministic point of view with the problem of the transfer of
information along different orders of magnitude is the *self-organized
morphogenesis* approach. Several
authors [@ClementBlanc2012; @BlancCoste2012] suggested that the
branching routine of the bronchial tree is less stereotyped than
thought, especially in the central and distal generations. This
hypothesis is supported by the observation that modeling approaches
using stochastic space-filling routines, constructed based on a
stereotyped proximal tree, are capable of generating tri-dimensional
branched structures that satisfy the constraints of a morphometric adult
lung. On another side, the core concept of the *self-organized
morphogenesis* approach relies on the observation that key molecular
components are necessary and sufficient for proper growth and branching
of the bronchial epithelium. Among these, the fibroblast growth factor
10 encoded by the *fgf10* gene has been demonstrated to play a central
role in epithelial proliferation, whose activity is highly
regulated [@ClementBlanc2012].

<figure id="ORG:fig:BranchStruct" data-latex-placement="t">
<div class="center">
<embed src=".//images/ORG_BranchStruct.pdf" style="width:75.0%" />
</div>
<figcaption>Proposed mechanism for the morphogenesis of biological
branched structures – In this approach, the gradient of concentration of
a key molecular activator guides the growth of specific tissue layer
through the activation of the associated receptor. In this example, the
local gradient of concentration of FGF10 (black arrows) activates the
budding of the epithelium layer (<em>branching mechanism</em> – left).
As the tissue curvature flattens, the local concentration vanishes and
the growth stops, preventing the tissue overlap (<em>avoiding
mechanism</em> – right) <span class="citation"
data-cites="ClementBlanc2012"></span>.</figcaption>
</figure>

In 2012, Clément et al. [@ClementBlanc2012] proposed a scenario for the
spontaneous emergence of a tree structure. This scenario is based on the
sole diffusion of a protein promoting cell proliferation, such as FGF10,
in an environment with two layers that mimic the bronchial epithelium
and the lung mesothelium. In addition, the layers present a resistance
to folding and are growing as a function of the received flow of
proteins. This scenario forms a model for the lung development and has
been studied using mathematical and numerical tools. To mimic the
diffusion process from the outer layer of the organ (mesothelium) to the
inner layer (bronchial epithelium), Clément et al. solved the Laplace
equation applied on the protein concentration $c$:
$$\bigtriangleup c = 0$$ Then, they considered that each layer was
growing according to a function of the local protein gradient:
$$\begin{array}{ll}
\frac{d \mathbf{x}}{d t} = f_m\left(||\nabla c (\mathbf{x})||\right) & \text{ for $\mathbf{x}$ in the mesothelium}\\
\frac{d \mathbf{x}}{d t} = f_e\left(||\nabla c (\mathbf{x})||\right) & \text{ for $\mathbf{x}$ in the bronchial epithelium}
\end{array}$$ The functions $f_m$ and $f_e$ are increasing functions,
typically with a sigmoid shape. To avoid the epithelium to catch up with
the mesothelium, $f_e$ is kept smaller than $f_m$. A smoothing of the
layers based on a fixed characteristic size is then performed in order
to mimic the layers resistance to folding. With this model, Clément et
al. observed the spontaneous formation of branching patterns similar to
those observed during bronchial development, as depicted in Figure
[1.1](#ORG:fig:BranchStruct){reference-type="ref"
reference="ORG:fig:BranchStruct"} and, based on an extended model, in
Figure [1.2](#ORG:fig:TreeGrowth3D){reference-type="ref"
reference="ORG:fig:TreeGrowth3D"}. Hence, this compact modeling approach
is sufficient for observing *de novo* branching and growth patterns in a
simulated tissular environment. Since then, this *self-organized
morphogenesis* approach has been used as a framework for other
organs [@MenshykauMichos2019] and other branched
systems [@FacchiniLazarescu2020]. To date, the question of the
mechanisms of development of branching organs is not clearly elucidated.
However, the link between the molecular and cellular components requires
further investigation, in order to unveil the determinants at the scale
of the tissues and organs.

::: Philblock
How growth and organ specialization define the shape and structure of a
mature organ is a long-debated scientific question that has not yet
unveiled all its secrets and mysteries. Organs are rarely functional
during development, at least not in the early stages. Thus, the function
of an organ cannot directly drive its growth and ultimately its mature
shape. So how can development build an organ that, when mature, has the
correct shape and function? Evolution is the answer: if development
fails to achieve a functional, efficient organ, the associated organism
has little chance of being selected by evolution. But this answer raises
many other questions. What is the evolutionary cost of organogenesis?
What about the biological path selected by evolution for growing an
organ? Is it so robust that once such a path has been selected, it
renders all other paths inaccessible? Do these paths and costs form
bottlenecks for the organs in terms of possible shapes, functions, and
functional efficiencies? Insights into these questions will be given in
Section [1.3](#ORG:Sec:Allometry){reference-type="ref"
reference="ORG:Sec:Allometry"}.
:::

However, these examples of constrained organ development raises several
issues that need to be discussed in details. Among these, one can notice
that the shape of the system appears as central in the developmental
considerations, especially under constraints.

<figure id="ORG:fig:TreeGrowth3D" data-latex-placement="t">
<div class="center">
<img src=".//images/ORG_TreeGrowth3D.png" style="width:35.0%" />
</div>
<figcaption>Tridimensional spontaneous emergence of a tree
(<em>budding</em>) based on the model of Clément et al. (2014)  <span
class="citation" data-cites="ClementMauroy2014"></span> – An eighth of
the budded sphere has been sliced out to show the branching core (blue).
Notice the self-avoiding and space-filling branching, which are commonly
found in biological tree structures.</figcaption>
</figure>

:::: Physicsblock
Despite the complexity of biological systems, it is possible to apply
the Onsager's phenomenological approach of locally linearized
non-equilibrium thermodynamics Onsager [@OuerdaneApertet2015]. Through
this approach, it is possible to identify the non-equilibrium processes
that link the degradation of the chemical potential of food by its
digestion into a macroscopic form of energy made available for muscular
work. By applying Onsager's approach and integrating it with macroscopic
systems, we can describe the behavior of certain thermodynamic
conversion machines under mixed boundary
conditions [@Volkenshtein1983; @DemainFang2000; @Blumenfeld1981]. In the
case of Dirichlet boundary conditions the system is driven by the
potential differences, meanwhile in Neumann boundary conditions the
system is driven by the fluxes. Mixed conditions are located between
these two extreme configurations. These lead to feedback effects and the
emergence of complex dynamic behaviors [@JusupSousa2017].

::: center
![image](.//images/ORG_Muscle.pdf){width="85%"}
:::

(A) Illustration of muscle as an energy converter. The incoming energy
flow $\Phi_+$ is converted into mechanical power $P=F_MI_M$ and a waste
fraction $\Phi_-$. $I_M$ is the so-called *metabolic intensity*. (B)
Plot of the system's response under varying metabolic intensities $I_M$.
The response extends from the basal resting point to the point of
exhaustion, via the point of maximum work production.\

If we apply this description to the case of living organisms that have
been reduced to chemical conversion machines, we obtain a thermodynamic
formalism (see Figure above) that regains the phenomenological
description of the muscular response proposed by
Hill [@Vivian1938; @GoupilOuerdane2019]. In Hill's phenomenology, the
metabolic force $F_M$ and the contracting velocity $v$ are linked by
three constants represented by the equation $F_M=\frac{c}{v+b}-a$. The
thermodynamic formulation gives
$F_M=\frac{F_{iso}+R_{fb}}{I_M+I_T} \, I_T - \left(R_{fb}I_T+R_MI_M\right)$
where $I_M \propto v$. The thermodynamic approach gives us access to the
physical meaning of the parameters i.e., $F_{\mathrm{iso}}$ is the
isometric force of the muscle, $I_T$ defines the threshold of acceptable
metabolic intensity, $R_{M}$ is the viscous resistance to displacement
and $R_{fb}$ the feedback resistance induced by the mixed conditions
previously mentioned .

A proxy for the flow released by the muscle is the quantity of oxygen
breathed in during ventilation [@YangHeinemann2021]. To achieve an
effort of a given intensity, the level of O$_2$ adjusts accordingly.
Naturally, this quantity cannot grow indefinitely, and is limited by the
absolute size of the organ that enables this exchange and by the
relative size of this organ compared to the size of the individual.

For an individual, this is an intrinsic limitation on the ability to
produce effort. So, depending on the size of the individual, which
constrains its volume, the respiratory system must be optimized to
maximize the flow of O$_2$. By comparing inter-species data and using a
generic description, it is then possible to find an allometric law, as
we shall see in this chapter.
::::

In the next section, the respiratory system, and the lung as its central
organ, will be studied in details in light of the concepts of organ
optimization. Indeed, the lung, its structure, its functioning, its
efficiency, are all the result of a series of optimization under
constraints that shaped the organ through evolution.

## The lung as a model organ for optimization under constraints

At the core of the respiration process, the lung is the organ that
connects the ambient air to the blood, allowing to transport oxygen from
the ambient air to blood and carbon dioxide from blood to the ambient
air. The needs of the body in oxygen and carbon dioxide, the respiratory
gases, determines the lung function, which is based on a complex
geometrical structure and on several physical and chemical processes.

### Lung morphology, a complex structure

A basic description of the lung structure would consist in dividing it
in two parts: the bronchial tree and the exchange surface with blood.
The function of the bronchial tree is limited to the transport of the
respiratory gases and no exchange occurs in this part of the lung. It
forms a cascade of bifurcating airways with cylindrical shapes. There is
an average of seventeen successive bifurcations in the human lung. The
trunk of the tree is called the trachea; it is connected to the ambient
air through the tracheo-pharyngeal pathway. The leaves of the tree are
called the terminal bronchioles; they are connected to the exchange
surface with blood. At each bifurcation the size of the airways is
decreasing, with a tracheal diameter of about $2$ cm and a diameter of
the terminal bronchioles of about $0.3$ to $0.5$ mm. The exchange
surface with blood consists in a foam-like structure that is an assembly
of exchange units called the acini. Each acinus is also shaped as a
bifurcating airway tree, but the size of the airways is conserved at the
bifurcations. There is an average of six successive bifurcations in a
typical acinus. The acinar airways are called the alveolar ducts and
their walls are garnished with bubble-like structures, the alveoli. The
alveoli walls are mainly blood capillaries, called pulmonary
capillaries, and they are the location of the respiratory gas exchanges.
Each terminal airway of the bronchial tree feeds an average of two
acini. The auto-similar, multi-scaled structure of the bronchial tree
and of the acini allows the lung to contain a very large exchange
surface that is folded in the thorax. In a typical human, the exchange
surface is about $70$-$100$ m$^2$ [@West2011].

Since the morphology of the lung is complex, it becomes necessary to
make assumptions in order to have a simple model while conserving the
principal geometrical properties. Our model is then based on the
assembly of self-similar trees with cylindrical branches and symmetric
bifurcations that mimic the two functional zones (see Figure
[1.3](#ORG:fig:TreeCrop){reference-type="ref"
reference="ORG:fig:TreeCrop"}). To account for the core geometrical
properties of the lung, we assume that the dimensions of the branches in
the conductive tree decreases from one generation to the next with a
ratio $h = \left(\frac{1}{2}\right)^{\frac13}$ [@Weibel1963], while in
the acinus we assume that the size of the bronchi remains constant
[@Weibel1963]. Note that the airways spatial distribution such as the
branching angles or the orientations of the branching planes is not
taken into account in our model since it is not really relevant for the
computation of oxygen transport in the lung.

<figure id="ORG:fig:TreeCrop" data-latex-placement="t">
<embed src=".//images/ORG_TreeCrop.pdf" style="width:50.0%" />
<figcaption>Illustration of the lung model used in this chapter – The
tree in beige mimics the bronchial tree, where oxygen and carbon dioxide
are only transported along the branches. The tree in blue mimics the
acini, where the respiratory gases are transported along the branches.
They are also captured by the alveoli that cover the walls of the
branches.</figcaption>
</figure>

### Lung dynamics: where physics enters the play

The transport of the respiratory gases to and from blood involves a
combination of physical processes which ensure that the needs of the
body in respiratory gases are fulfilled.

**Diffusion : no energy costs, but too weak.** As blood entering the
pulmonary capillaries has an oxygen partial pressure lower than the
oxygen partial pressure in the alveolar air, oxygen flows to the blood
by the process of diffusion that tends to balance the partial pressures
between blood and the alveolar air. For the lung's point of view, the
blood acts as an oxygen sink. The transport of carbon dioxide in the
lung relies on the same processes than that for oxygen, except that
blood flowing in the alveoli membranes acts as a source of carbon
dioxide. The diffusion process is passive in the lung i.e., no energy is
spent by the organ to perform the transport. Notice that this is not
true from the pulmonary blood circulation point of view, as blood has to
be incessantly renewed to maintain the respiratory gas partial pressure
difference between the alveolar air and the blood. However, at the
metabolic time scale, the diffusion process has a limited range in the
airway tree. Were the transport of the respiratory gas only based on
diffusion, the lung could not maintain the respiratory gas flow at a
level compatible with the mammals metabolisms. The reason behind this
limitation stands in the size of the airway tree. The pathways from the
ambient air to the respiratory zone are too long and narrow for the
diffusion to provide gas flows compatible with the metabolism of
mammals. In the case of the human lung, the typical length of these
pathway is of about $L_p = 30$ cm [@MauroyFiloche2004]. The
characteristic time $t_p$ for an oxygen molecule to travel by diffusion
through all such a pathway can be estimated using a dimensional
analysis. Using $L_p$ and the diffusion coefficient of oxygen in air
$D = 0.2$ cm$^2 \cdot \mathrm{s}^{-1}$ [@SapovalFiloche2002], the order
of magnitude of $t_p$ can be estimated with:
$$t_p = \frac{L_p^2}{D} \simeq 4500 \, \text{s} = \text{$1$ hour and $15$ minutes!}$$
Hence, a pure diffusive transport of the respiratory gas cannot fit the
mammals needs. Actually, in human, the order of magnitude of the length
$L_D$ traveled by diffusion during the typical time of inspiration i.e.,
$t_i = 2$ seconds, is $L_D = \sqrt{D \times t_i} \simeq 6.3$ mm. Thus,
in the resting human, diffusion can transport oxygen from the terminal
bronchioles to the nearby exchange surface. However, at a time scale
compatible with the metabolism, diffusion cannot reach the upper part of
the bronchial tree. It cannot either reach the deeper parts of the
respiratory zone, which is non active at rest. Actually, this last
phenomenon, called the *screening effect* [@SapovalFiloche2002], plays a
crucial role in the lung. It is described in details later in this
chapter. More generally, the limited spatial range of diffusion has many
consequences on the living systems. An emblematic example is its role on
the size limitation of insects [@HarrisonKaiser2010], where diffusion in
the tracheal tubes is the only mean of respiratory gas transport. It
participates to the explanation of why the increased atmospheric oxygen
concentration during the Palaeozoic era allowed insects to be larger
than today as, following Fick's law, the diffusive flow is proportional
to the gradient of partial pressure between the ambient air and the
inner body.

**Convection : the rescuer.** We have seen that the diffusion process is
too weak to transport the respiratory gas through the whole airway tree.
In the absence of other transport mean, the oxygen partial pressure in
the lung would decrease and the flow of oxygen to blood would drop.
Similarly, the carbon dioxide partial pressure would increase and
prevent the exchanges with blood to occur. Consequently, the air in the
lung has to be renewed in order to expel the excess of carbon dioxide
and to refresh the inhaled air volume with oxygen. This phenomenon is
called the ventilation. The ventilation is a dynamic i.e.,
time-dependent, process based on the succession of inhalation and
exhalation of a volume of air, the tidal volume, at a given rate, the
breathing frequency. Ventilation is performed thanks to a set of muscles
that surround the lung and modify its volume. At rest regime, the main
acting muscle is the diaphragm, located at the base of the lung. By
first pulling onto the lung, this muscle deforms the lung tissues,
creating a negative pressure drop and the transport a volume of ambient
air inside the lung; this is the inspiration phase. At rest, the elastic
energy stored in the tissues during the inspiration phase allows for a
passive recoil of the lung and a volume of air equal to the volume
inhaled is expelled; this is the expiration. Then the cycle repeats
following the same procedure, at least at rest. Since the duration of a
breath cycle for a resting human is about four to five seconds, a human
performs, on average, about six to seven hundred millions breaths during
her/his lifetime.

**Modeling the oxygen transport.** The transport of oxygen in the lung
is then driven by three phenomena: diffusion, convection by the airflow
and exchange with blood through the alveoli walls in the alveolar ducts.
The partial pressure of oxygen averaged over the lumen area is
transported along the longitudinal axis $x$ of the airway. Hence, in
each airway of our idealized lung, the mean partial pressure of oxygen
$P$ over the airway section follows, $$\begin{equation}
\label{eq:transport}
    \frac{\partial P}{\partial t} - D \frac{\partial^2 P}{\partial x^2} + u\frac{\partial P}{\partial x} = \beta \left( P_{\text{blood}} - P\right),
\end{equation}$$ where $D$ is the oxygen diffusion coefficient, $u$ is
the velocity of the airflow, $\beta$ is a reactive term and
$P_{\text{blood}}$ is the partial pressure of oxygen in the capillary
blood. The reactive term $\beta$ mimics the exchanges with blood through
the alveolar membrane. This coefficient depends on the diffusion
coefficient of oxygen in water, on the solubility coefficient of oxygen
in water, on the thickness of the alveolar-capillary membrane, and on
the radius of the alveolar duct. It is equal to zero in the bronchial
tree since no exchange with the blood happens in this part of the lung
and is positive in the acini. The oxygen partial pressure in blood is
determined by assuming that the flow of oxygen leaving an alveolar duct
through the alveolar-capillary membrane is equal to the flow of oxygen
captured by blood, accounting for the oxygen captured by hemoglobin and
for the oxygen dissolved in plasma [@West2011]. Finally, all generations
are linked through bifurcations by assuming continuity between
generations and conservation of the quantity of oxygen at each
bifurcations.

:::: samepage
::: MathDetailblock
Our model takes as input the ventilation parameters: the tidal volume
$V_T$ (in mL) and the breathing frequency $f_b$ (in min$^{-1}$) and
outputs the mean amount of oxygen exchanged with blood over a
respiratory cycle. To validate our model, we performed computations at
rest by assuming that a human breathes around $12$ times per minute and
inhales around $500$ mL of air for each breathing cycle. With these
parameters, our transport model gives an oxygen flow exchanged with
blood of $230$ $\text{mL} \cdot \text{min}^{-1}$, which is close to the
average physiological value of $250$ $\text{mL} \cdot \text{min}^{-1}$
[@West2011].
:::
::::

### The energy expenditure or the cost of breathing

Breathing is part of the basal metabolism, meaning that it is a regular
and mandatory energy cost for the maintenance of the body. Yet, natural
selection, one of the main processes driving evolution, tends to select
for minimal energetic cost so that the organisms can allocate most of
their resources to their reproduction. Hence, in order to understand
breathing, it is important to determine the origin of the energetic
costs and how they are affected by the breathing process. We already
pointed out that diffusion, considered from the lung point of view, is a
passive process. So, most of the energetic costs involved in the lung
function arise from the process of ventilation. Energy is spent through
the action of the muscles on the lung. This action has two main effects:
it deforms the tissues and it displaces the air along the bronchial
tree. On the one hand, the tissues are deformed due to the action of the
thoracic muscles, especially the diaphragm. This deformation is
considered as elastic in the normal range of ventilation [@Maury2013],
and energy is dissipated along the displacement of the tissues. On the
other hand, as every gas, air acts as a fluid with specific viscosity.
As the bronchial tree is an assembly of a high number of narrow tubes
with decreasing size, the energy spent for the displacement of the air
in the bronchial tree is dominated by the energy dissipated by the
friction of air in the bronchi. The air kinetic energy is negligible
relatively to the dissipation. This can be summarized in term of the
power spent by the muscles (energy per unit of time):
$$\underbrace{\mathcal{P}_{\rm{m}}}_{\text{muscle power}} \simeq \underbrace{\mathcal{P}_{\rm{e}}}_{\text{elastic power}} + \underbrace{\mathcal{P}_{\rm{a}}}_{\text{air viscous dissipation}}.$$
These quantities depend on several lung characteristics, on the
breathing frequency $f$ and on the amount of air inhaled during on
breath cycle $V_T$. This raises the trade-off shown in
Figure [1.4](#ORG:fig:Power){reference-type="ref"
reference="ORG:fig:Power"} and, using optimization theory, optimal
ventilation frequencies and tidal volume can be be predicted.

<figure id="ORG:fig:Power" data-latex-placement="t">
<div class="center">
<p><embed src=".//images/ORG_Power.pdf" style="width:55.0%" /><br />
</p>
</div>
<figcaption>Trade-off between elastic energy stored in the tissue and
viscous energy dissipated in the air circulation (exercise regime,
computed from our model).</figcaption>
</figure>

The viscous dissipation of air in the bronchial tree is characterized by
the lung hydrodynamic resistance $\mathcal{R}$, which is directly
related to the geometry, size, number and structuring of the
bronchi [@Maury2013]. The hydrodynamic resistance is a physical quantity
that represents how the energy put in the system is divided between
kinetic energy and heat energy. It connects the volume of air displaced
per unit of time, also called air flow $F$, to the force per unit of
surface applied to the air, also called air pressure $p_a$:
$p = \mathcal{R} F$. For the same pressure applied on the lung, the
higher the hydrodynamic resistance, the lower the air flow and the
higher the dissipation. Then, the power dissipated by viscous friction
of the air inside all the bronchi can be estimated by
$\mathcal{P}_{\rm a} = p F = \mathcal{R} F^2$. By assuming in our case
that the velocity of the air follows a sinus function, we can deduce the
power dissipated by viscous friction as follows:
$$\mathcal{P}_{\rm a} = \frac14 \mathcal{R} \left(\pi f_b V_T \right)^2,$$
where $\mathcal{R}$ is the hydrodynamic resistance, $f_b$ the
respiratory frequency and $V_T$ the tidal volume.

The elastic power is characterized by the compliance $\mathcal{C}$ of
the lung, that relates the force per unit of surface applied by the
muscles ($p_m$) to the volume change of the lung [@Stephano2021]. The
compliance depends on the lung's volume, especially when the deformation
of the lung is high although the compliance can be considered constant
while healthy. That is why, in our case, we assume that the compliance
is a constant and we neglect the non-linearities arising at large lung's
deformations [@Noel2021]. The elastic power can be estimated by
integration of the volume along the inspiration phase and it gives us,
$$\mathcal{P}_{\rm e} = \frac{V_T^2 f_b}{2 \mathcal{C}},$$ where
$\mathcal{C}$ is the compliance of the lung previously defined. Finally,
the total energetic cost of breathing $\mathcal{P}$ can be written as
the sum of the power dissipated by viscous friction
$\mathcal{P}_{\rm a}$ and the elastic power $\mathcal{P}_{\rm e}$. The
total power has to be minimized relatively to the tidal volume $V_T$ and
the breathing frequency $f_b$ with a constraint on the oxygen flow to
blood that has to match the oxygen flow demand (see
Equation [\[eq:opti\]](#eq:opti){reference-type="ref"
reference="eq:opti"}). Thanks to our model previously defined, we can
compute the oxygen flow to blood as a function of tidal volume and
breathing frequency and compare it to the oxygen flow
$\dot{V}_{\mathrm{O}_2}$ requested by the body at the regime considered.

<figure id="ORG:fig:FredOptiVentil" data-latex-placement="t">
<div class="center">
<p><embed src=".//images/ORG_FredOptiVentil.pdf"
style="width:60.0%" /><br />
</p>
</div>
<figcaption>Total power expenditure during ventilation (W) as a function
of the respiratory frequency (s<span
class="math inline">\(^{-1}\)</span>) for different intensities of
exercise – Dots correspond to the optimal ventilation frequency i.e.,
that minimizes the dissipated power. Adapted from <span class="citation"
data-cites="NoelMauroy2019"></span>.</figcaption>
</figure>

Our model predicts (see
Figure [1.5](#ORG:fig:FredOptiVentil){reference-type="ref"
reference="ORG:fig:FredOptiVentil"}), for a human at rest, an optimal
breathing frequency of $12.2$ breaths per minute and an optimal tidal
volume of $497$ mL, which are very close to the average physiological
values [@Weibel1984]. The model exhibits a robustness in term of
frequency perturbation around the optimal. A $5\%$ shift in the energy
brings the frequency into a range between $8$ breaths per minute up to
$18.5$ breaths per minute. This effect is due to the fact that, at low
regimes, a low tidal volume $V_T$ is sufficient to perform an optimal
ventilation. When the exercise intensity increases, the power profiles
as a function of the frequency become steeper and steeper and focus the
optimal value within a tighter region. It implies that a shift from the
optimal configuration at high intensities is predicted to be costly in
term of energy spent. This behavior is fully compatible with the fact
that the control of ventilation is stronger at exercise, preventing even
talking. The question of the optimal conditions of ventilation in human
leads naturally to a series of extensions that need to be considered. We
have seen previously that the optimization under constraints occurs in
almost every organ in all the living beings. Thus, could we expect the
present model to be extended to all mammals, as the control of
ventilation is, more than probably, present in the whole mammalian
class?

## Allometric scaling laws for respiration and ventilation {#ORG:Sec:Allometry}

The answer to this question of generalization leads us to a vast
scientific question that will bring us back to the late 19$^{\text{th}}$
century and which is still open on many aspects.

### The emergence of scaling relations in nature {#ORG:SubSec:allom_emergence}

In 2007, Savage and West published a seminal work in which they present
a collection of data of sleep duration in a set of mammalian species.
Among other major results, their analysis confirmed the previous
observation that the larger the animal, the shorter the duration of its
sleep cycle [@SavageWest2007]. More precisely, the sleep duration
correlates negatively with the body mass of the mammal and follows,
based on the data from Savage & West, an interesting exponential law of
the form $t_s = 10.1 \, M^{-0.103}$, with $t_s$ the sleep duration in
hours during a 24 hours period and $M$ the body mass of the mammal in
kilograms, as seen in Figure [1.6](#ORG:fig:PlotCL){reference-type="ref"
reference="ORG:fig:PlotCL"} [@SavageWest2007]. Thus, by taking the
logarithm of both sides of the equation, one can write this
sleep-to-mass relation as $\text{log} \, t_s = \,$ 10.1 - 0.103
$\text{log} \, M$ i.e., a linear relation between the logarithm of the
sleep duration and the logarithm of the mass of the animal, see Figure
[1.6](#ORG:fig:PlotCL){reference-type="ref" reference="ORG:fig:PlotCL"}.
As we will see later, this type of exponential relation is now referred,
in ecological sciences, as an *allometric* scaling. In general, an
allometric law will write $Y = Y_0 M^b$, where $Y$ is the studied --
physiological, morphometric -- property, $M$ the mass of the living
organism, $Y_0$ and $b$ the allometric prefactor and exponent,
respectively [@WestBrown1997]. Actually, the concept presented by Savage
& West is far from being recent. The history of the study of allometric
relations dates back to the 19$^{\text{th}}$ century. Scientists from
various disciplines started to analyze the changes in shape and form of
living beings in relation with their overall size.

<figure id="ORG:fig:PlotCL" data-latex-placement="t">
<embed src=".//images/ORG_PlotLog.pdf" />
<figcaption>Distribution of total sleep duration (<span
class="math inline">\(S\)</span>) in mammals – The plot is based on data
from Savage &amp; West <span class="citation"
data-cites="SavageWest2007"></span>. The data is best fitted by the red
curve which represents the corresponding allometric relation <span
class="math inline">\(S = 10.1 \times M^{-0.103}\)</span>.</figcaption>
</figure>

### A brief history of allometry {#ORG:SubSec:allom_history}

In a pioneer work from 1897, Eugène Dubois described the relation that
guides the evolution of brain's mass and that of the individual in a
variety of mammal species [@Dubois1897]. He observed that brain is
smaller, relatively to the their mass, in bigger animals. He then
derived an adequate expression for this relation, such as
$e = c \, s^r$, where $e$ is the brain's mass, $s$ the body mass and $c$
and $r$ two coefficient that define the relation, with $r$ close to 1/2,
justifying the relative decrease in brain's mass that he observed. As
far as we know, this represents the first mathematical expression of an
allometric law, years before this term was even coined as it. It is in
1907 that Lapicque [@Lapicque1907] had the idea to transform Dubois'
relation in a log-log dependency, giving a straight line representation
in logarithmic coordinates that is now familiar to us, cf.
Figure [1.6](#ORG:fig:PlotCL){reference-type="ref"
reference="ORG:fig:PlotCL"}. At that time, this work was purely
descriptive and empirical. However, biological and ecological data
started to accumulate in the following years that led, mainly in animal
species, to a variety of scaling laws. Thus, the ubiquity of allometric
relations in every ecological discipline raised the question of the
nature of the biological mechanisms underlying their observation.

In parallel, the question of the emergence of forms in living organisms
arose in the literature. One of the major works at that time came from
the Scottish naturalist D'Arcy Wentworth Thompson, whose main
contribution came from his book *On Growth and Form*, first published in
1917 [@Bonner1992]. In this publication, he adopted the -- still debated
-- thesis that the living systems as we know are submitted, in addition
to the process of natural selection, to the physical laws of nature that
can modify, transform and adapt their form and their path of development
i.e., their growth. This reference publication paved the way to the new
disciplinary research field of biomathematics and, even in present
times, is still considered as a major contribution to this field.
However, the D'Arcy Thompson's approach has not been accepted by the
whole community, and the debate is still vivid more than a century after
the publication of the first edition of his work [@Esposito2014].
Indeed, D'Arcy Thompson was not entirely convinced by the pure Darwinian
approach that dominated the field of developmental biology in his time.
Although a strong Darwin's admirer, he rather considered that the paths
of development of the organisms were not dictated purely by acquired
mutations and hard-encoded routines. At the contrary, he was convinced
that these paths could only follow a number of sequences, a series of
schemes that, following the laws of physics and chemistry, would allow
for the formation of the variety of shapes and developments observed in
nature [@BriscoeKicheva2017]. Critics emerged about his teleological --
in some ways -- conception of evolution, or at least of emergence of
form. In essence, his work was one of his time, and his theories of
forces of development were not supported by the genetic and molecular
knowledge that has since been accumulated [@Esposito2014]. D'Arcy
Thompson was an author of his time. He paved the way, with others
developmental naturalists, to numerous concepts in biomathematics that
influenced a number of past and present works, as discussed in
Section [1.1](#ORG:Sec:Introduction){reference-type="ref"
reference="ORG:Sec:Introduction"}. But D'Arcy Thompson was also an
author among his peers. Motivated by his conception of developmental
shaping forces, he started to correspond with a younger British
naturalist named Julian Huxley, who will later forge a prolific
international career as a biologist and science advocate, although
carrying with him some controversies that are beyond the scope of this
chapter.

The scientific correspondence started slightly after one of Huxley's
major publication, dated from 1924. In this article, Huxley studied the
dynamics of growth of chelae in a crab species whose individuals possess
one small and one large chela [@Huxley1924]. What seems at first a
highly specific topic is enlarged by the idea to measure the mass of the
chelae *relatively* to the mass of the individual. Following the steps
of Dubois and Lapicque, Huxley weighted around 400 specimens of crab and
plotted in a logarithmic scale the mass of the large chela against the
total weight of the animal minus the weight of the large chela. He then
observed that the experimental data could be joined by a straight line
in this logarithmic plot. The originality of Huxley's work resides in
his interpretation of the results that he obtained. He noticed that the
slope $k$ of the regression line remained larger than one, in accordance
with the observation of the relative larger i.e., heterogonic growth of
the chela compared to the growth of each individual. He then provided a
proposed mechanism for this relative growth: the rate of cellular
division in the chela is larger than the one in the rest of the body,
more precisely in a $k:1$ ratio [@Huxley1924]. With this -- still
emergent -- mechanistic approach, Huxley provided for the first time a
simple method for deciphering heterogonic growth of a characteristic,
that will be observed as a straight line of slope $k>1$ when plotted
against the normalized mass of the individual in logarithmic
coordinates.

Finally, the works of Lapicque, Dubois, D'Arcy Thompson and all their
contemporaries emerged in 1936 in a joint paper between Huxley and a
younger scientist, Georges Teissier, in which they agreed for the
terminology of *allometry* and the associated law that is now famous
$y = b x^\alpha$ [@HuxleyTeissier1936]. Altogether, this brief section
on the historical emergence of the allometric concept in ecological
sciences depicts a vibrant and active research theme, developed in the
late $19^{\text{th}}$ century, which extends the Darwinian concept of
natural selection towards the emergence of growth, form and function.
However, the reader will notice that the allometric approach of these
times is still largely descriptive, with limited causal explanations of
the nature of the scaling coefficients and the putative mechanisms that
drive their behavior.

### Allometry: a mechanistic approach {#ORG:SubSec:allom_mecha}

Many years later, a possible approach that compensates for this lack of
mechanistic causality would be found in the work of West, Brown and
Enquist (*WBE*), published in 1997 [@WestBrown1997]. In this major
article, the authors focused on the allometries in metabolic properties
that have been described in the past decades, with the aim of developing
a new mechanistic framework that would explain these allometries i.e.,
be able to derive the allometric exponents for the numerous
physiological properties at stake here. The question of the existence of
a general allometry for the metabolic rate of the living beings is a
thrilling question. This would imply that all the organisms, from the
tiny bacteria to the massive trees or mammals, do possess shared
mechanisms of energy expenditure that would reflect on the presence of a
common exponent all over the different orders of magnitudes among the
species. Furthermore, the exponent should reflect somehow, by its value,
the nature of the energetic mechanisms, and thus could be derived by a
comprehensive modeling approach. WBE answer positively to these strong
hypotheses, and developed a structured approach that focuses on the
modeling of energy and mass fluxes in biological networks --
cardiovascular and respiratory systems for example -- which they
consider as the common ground for all the species [@WestBrown1997]. The
hypotheses of WBE are of strong nature, and have been discussed largely
in the literature (see for example [@KozlowskiKonarzewski2004]. Although
this important -- and still open -- debate lies beyond the scope of this
chapter, it appears important to emphasize that the WBE approach created
a mechanistic, mathematical framework for the study of allometric
relations that, somehow, acted as a bridge between the traditional
descriptive allometry and the modern mechanistic approach.

### Allometric relations for the respiratory system {#ORG:SubSec:allom_respi}

As far as the respiratory system is concerned, the model of WBE appears
to act as a promising framework for the study of the allometric
relations of this system [@NoelKaramaoun2022]. Indeed, the lungs of
mammals are built as a network of mass and energy transfer, as described
before, and share morphological and functional properties, raising the
question on whether the previous results for human can be extended or
not to all mammals. These properties are known to be dependent on the
mass $M$ of the mammal with allometric scaling
laws [@WestBrown1997; @HuxleyTeissier1936]. Furthermore, the physics of
ventilation, and hence its control, is linked to the geometry of the
lung. Consequently, the morphological differences among mammals also
affect the control of ventilation.

First, our gas transport model for the human lung presented in the
previous section can be slightly modified to be valid for all mammals.
Indeed, we know that the lungs of mammals share invariant
characteristics [@Weibel1984] such as the tree-like structure with
bifurcating branches and the decomposition into two parts: the bronchial
tree and the acini. The derivation of a lung model that depends only on
mammal mass requires to relate explicitly the morphological parameters
involved in our model such as the tracheal radius and length, with the
animal mass. We used the datasets from [@WestBrown1997]. The oxygen
transport and exchange now occur in the idealized lung that has been
generalized to fit any mammal. The transport of oxygen in the mammals
lung is still driven by the tree phenomena: convection by the airflow,
diffusion and exchange with blood through the alveoli walls. Hence, in
each airway, the partial pressure of oxygen follows the
convection-diffusion-reaction
equation [\[eq:transport\]](#eq:transport){reference-type="eqref"
reference="eq:transport"} previously defined. The exchange coefficient
$\beta$ is dependent on the mammals mass since it depends on the radius
of the alveolar duct which follows an allometric law. Finally, we search
for the minimum of the total energetic cost of breathing $\mathcal{P}$
relatively to the tidal volume $V_T$ and the breathing frequency $f_b$
with a constraint on the oxygen flow to blood that has to match the
oxygen flow demand $\dot{V}_{\mathrm{O}_2}$. Since allometric scaling
laws for oxygen flow demands for mammals at basal, field and maximal
metabolic rates are available in the
literature [@Peters1986; @Kleiber1932; @HudsonIsaac2013; @WeibelHoppeler2005],
we can compute the desired oxygen flow $\dot{V}_{\mathrm{O}_2}$
depending on the mammal mass and on the metabolic regime.

<figure id="ORG:fig:OptiMammalFV" data-latex-placement="t">
<p>(A) Frequency<br />
<embed src=".//images/ORG_OptiMammalFreq.pdf" /></p>
<p>(B) Tidal volume<br />
<embed src=".//images/ORG_OptiMammalVol.pdf" /></p>
<p><br />
</p>
<figcaption> Scaling laws for lung usage – Predicted ventilation
frequency (s<span class="math inline">\(^{-1}\)</span> – <em>left</em>)
and tidal volume (L – <em>right</em>) as a function of the mammal mass
(kg – log-log scale) at different metabolic regimes. BMR: Basal
Metabolic Rate, FMR: Field Metabolic Rate, MMR: Maximal Metabolic
Rate.</figcaption>
</figure>

Our model predicts that breathing frequencies and tidal volumes follow
indeed allometric scaling laws. Furthermore, these laws can be derived
in three different metabolic regimes: basal metabolic rate (BMR), field
metabolic rate (FMR) and maximal metabolic rate (MMR), as seen in
Figure [1.7](#ORG:fig:OptiMammalFV){reference-type="ref"
reference="ORG:fig:OptiMammalFV"}, $$\begin{align*}
    f_b^{\text{BMR}} \approx 0.61 \, M^{-0.27} \text{ Hz}, \, \, & V_T^{\text{BMR}} \approx 6.1 \, M^{1.04} \text{mL}, \\
    f_b^{\text{FMR}} \approx 1.17 \, M^{-0.31} \text{ Hz}, \, \, & V_T^{\text{FMR}} \approx 11.8 \, M^{0.97} \text{mL}, \\
    f_b^{\text{MMR}} \approx 1.37 \, M^{-0.17} \text{ Hz}, \, \, & V_T^{\text{MMR}} \approx 29.7 \, M^{1.01} \text{mL}. 
\end{align*}$$

It predicts exponents that are in accordance with the values observed in
the literature. Indeed, breathing rate at BMR has been estimated to
follow the law
$f_{b}^{\text{\rm{BMR}}} \simeq 0.58 \ M^{-\frac14} \ \rm{Hz}$ [@WorthingtonYoung1991]
and tidal volume to follow the law
$V_{T}^{\text{\rm{BMR}}} \simeq 7.14 \ M^1 \ \rm{mL}$ [@WestBrown1997].
At other metabolic rates, less data is available in the literature
except for the breathing rate of mammals at MMR, estimated to follow the
law
$f_{b}^{\text{\rm{MMR}}} \simeq 5.08 \ M^{-0.14} \ \rm{Hz}$ [@AltringhamYoung1991].
The validation of our model at both minimal and maximal metabolic
regimes suggests that its predictions should be coherent whatever the
regime, in the limit of the availability of its input parameters. This
indicates that the mechanical power spent for ventilation might have
driven the selection by evolution of the ventilation patterns.

The idealized representation of the bronchial tree and of the exchange
surface used in this study accounts for five core characteristics common
to all the mammals lungs, as identified in the
literature [@Weibel1984; @MauroyFiloche2004; @NoelMauroy2019; @WestBrown1997]:
a bifurcating tree structure; an homogeneous decrease of the size of the
bronchi at the bifurcations; the size of the trachea; the size of the
alveoli; and the surface area of the exchange surface. These
characteristics are the main determinants for the tuning of the
ventilation in order to minimize its energetic cost. This indicates that
once the metabolic regime is fixed, the morphology of the lung is
probably the primary driver of the physiological control of ventilation.
We tested this hypothesis by altering, in our analysis, the allometric
scaling laws related to the geometry of the lung. We observed
corresponding alteration of the laws predicted for tidal volumes and
breathing frequencies. Since morphology itself has probably been
selected by evolution in order to minimize the hydrodynamic resistance
in a constrained volume [@MauroyFiloche2004], morphology and ventilation
patterns are intertwined together in order for the lung to function with
a low global energetic cost i.e., a low hydrodynamic resistance $R$ and
a low ventilation cost $\mathcal{P}(V_T,f_b)$ that also depends on $R$.
Interestingly, our representation of the lung does not account for
interspecific differences known to exist between the lungs of mammals,
such as different degrees of branching asymmetry, monopodial or bipodial
lungs, etc. [@MauroyBokov2010].

<figure id="ORG:fig:PecletBM" data-latex-placement="t">
<embed src=".//images/ORG_PecletBM.pdf" style="width:95.0%" />
<figcaption>Localization in terms of lung generation index of the
conductive zone and of the exchange surface (acini) as a function of the
mammal species mass (kg) – Both the green line (rest regime –
<em>left</em>) and the red line (maximal exercise regime –
<em>right</em>) represent the transition from a transport of the
respiratory gas by convection to a transport by diffusion. Adapted
from <span class="citation"
data-cites="NoelKaramaoun2022"></span>.</figcaption>
</figure>

:::: Physicsblock
The allometric relationship found applies to the pulmonary organ. This
is a crucial link in muscular activity, and therefore in locomotion or
any activity requiring an effort, even moderate. As such, its properties
must also be present during physical exercise. A useful quantity, based
on oxygen consumption $\dot{V}_{\mathrm{O}_2}$ and frequently used in
the literature, is the Cost of Oxygen Transport (COT). This corresponds
to the ratio $\dot{V}_{\mathrm{O}_2}/v$ with $v$ the locomotion
velocity. Using the correct metabolic conversion factor COT is the
energy dissipated per unit length. It is known empirically that COT
shows a local minimum corresponding to an optimal situation in which the
minimum energy is dissipated per unit length. Building on this property,
Tucker in 1975 [@Tucker1975] noted that this minimum follows distinct
allometric laws according to the major locomotion families, runners,
swimmers and fliers, see the Figure below.

::: center
![image](.//images/ORG_TuckerNOS.pdf){width="90%"}
:::

The COT is defined here as the ratio $P/(M \, v)$, with $P$ the power
production and $v$ the velocity as a function of the body mass $M$ for
several species (adapted from [@Tucker1975]). Green are swimmers, red
are fliers, black are runners, blue are engines designed by engineers.
Continuous lines correspond to linear fits on data shown with filled
markers.
::::

:::: Physicsblock
::: center
In walking or running animals, the cost of oxygen transport (see Box
[\[ORG:Block:Int2\]](#ORG:Block:Int2){reference-type="ref"
reference="ORG:Block:Int2"}) depends on an animal's speed, as shown in
the figure on the right. On top is oxygen consumption
$\dot{V}_{\mathrm{O}_2}$ of a horse plotted against the speed
$v/v^\star$ for walk (red stars), trot (blue dots), and gallop (green
squares), and their fits with our modeling. Bottom is COT for the same
set of data. The three gaits data are normalized by the muscle fiber
ratio leading to a unique master curve.

Based on the model proposed in Box \"[Energy
conversion](#ORG:Block:Int1)\", it has been demonstrated that a living
system can be described as a collection of $N$ identical, *standard*,
muscle units operating in parallel [@HerbertOuerdane2020]. Then the COT
expression becomes: $$\begin{eqnarray}
    \text{COT} &=& 
    \frac{N}{N_H} \left( a_0 \, k + r_M \, k^2 \, v + \frac{b}{v}\right)
    \label{eq:COT}
\end{eqnarray}$$ with $a_0 \, k$ a constant, $r_M$ a dissipative term
and $b$ the basal consumption i.e., out of effort. This last three
parameters describing the standard muscle unit.

![image](.//images/ORG_COT.pdf){width="38%"}
:::

We are then allowed to derive the minimum of the COT as an intrinsic
property of energy conversion machines,
$\text{COT}_\mathrm{min} \propto \sqrt{r_M \, b}$. It is found
independent of the number of standard muscle fibers involved in the
effort. Thus, effort is a combination of the number $N$ of standard
muscle fibers used and their characteristics $b$ and $r_M$. The
parameterization of the standard muscle fiber depends on the specific
implementations for an organism. It can be expected to be identical for
a single animal. We have carried out this work in the case of the horse,
which exhibits three well-differentiated gaits: walk, trot and gallop
(see the Figure above. We show that the COT curves, or equivalently
$\dot{V}_{\mathrm{O}_2}$, of the different gaits can be found using $N$
as the only adjustable parameter, leaving the muscle fiber parameters
unchanged.

As muscle is the most common means of producing power in animals, the
typical behavior described here should be found in the most general way,
without barriers between species, genera or classes. Of course, muscular
implementation is specific to each animal, constrained by its own
characteristics (intensity of effort, size, etc.), which suggests the
origin of the observed scaling laws.
::::

As in the human lung, the transport of gases in the mammalian lung
relies on the two major processes of diffusion and convection. We know
that, in humans, the diffusive transport in the alveolar ducts is
submitted to a physical phenomenon called the *screening effect*
[@SapovalFiloche2002]. Indeed, as gas exchanges occur through the
alveoli walls lining the alveolar ducts, the diffusion can transport the
respiratory gases only on a limited range of generations. This range
depends on the physico-chemical properties affecting the diffusion of
the gas in the alveolar air and through the alveolo-capillary membrane.
This range has been estimated to be of about four generations for oxygen
and one for carbon dioxide [@SapovalFiloche2002] in humans. The
description of the screening effect in mammals requires several
additional hypotheses. Because of the screening effect, the alveolar
ducts far from the convection--diffusion transition get only a small
diffusive oxygen flow, as most of the available oxygen has been captured
by the alveolar ducts closer to the transition. In these deep parts of
the acini, the oxygen partial pressure gradient between the deoxygenated
blood and the alveolar ducts, which drives the oxygen capture by blood,
is low. Carbon dioxide is mostly evacuated from the alveolar ducts very
close to the transition: they are refilled by carbon dioxide too quickly
for the deeper ducts to be drained of gas by diffusion. Hence, the ducts
far from the transition cannot be relieved of the carbon dioxide and the
exchange with blood in these ducts is low. As a consequence, the deeper
part of the exchange surface is not available for the exchanges. The
location of the transition between convective and diffusive transport of
the respiratory gas drives the magnitude of the screening, and this
transition depends on the geometry of the airway tree and of the
ventilation regime. The screening phenomenon in mammals has been studied
mathematically in [@NoelKaramaoun2022]. Within the framework of the
models hypotheses, the authors show that the number of conductive
airways $N_{\rm{conD}}$ and the number of alveolar ducts $N_{\rm{ad}}$
follow allometric scaling laws:
$$N_{\rm{conD}} \propto N_{\rm{ad}} \propto M^{\frac78}.$$ Additionally,
they show that the number of airways $N_{\rm{conV}}$ in which the gases
are transported by convection also follows an allometric scaling law.
This law depends on the ventilation regime: $$N_{\rm{conV}} \propto
\left\{
\begin{array}{ll}
\left\{
\begin{array}{ll}
M^{0.56} & \text{if $M<150$ kg}\\
M^{0.405} & \text{if $M\geq150$ kg}
\end{array}
\right.
&\text{at rest} \\
&\\
M^{0.63} & \text{at maximal exercise}
\end{array}
\right.$$ These equations translate into linear relationships in terms
of $\log(M)$, as shown in
Figure [1.8](#ORG:fig:PecletBM){reference-type="ref"
reference="ORG:fig:PecletBM"}. Rest regime is represented on the left
plot and maximal exercise regime on the right plot. The figure indicates
that, at rest regime, the small mammals use their lung very efficiently,
as only a few of their acini generations are fed by diffusion, as
indicated by the green curve in
Figure [1.8](#ORG:fig:PecletBM){reference-type="ref"
reference="ORG:fig:PecletBM"}. Hence, the screening effect in small
mammals is weak. However, this suggests that they have few reserve for
increasing their metabolism at
exercise [@SapovalFiloche2002; @NoelKaramaoun2022]. As suggested by the
red curve on the right plot in
Figure [1.8](#ORG:fig:PecletBM){reference-type="ref"
reference="ORG:fig:PecletBM"}, the shift of the transition between
convection and diffusion to deeper generations does not increase
significantly the available exchange surface. To the contrary, large
mammals are submitted to large screening effects at rest regime, and a
large part of their exchange surface is not used. However, during
exercise, the shift of the transition towards a deeper lung generation
allows to recruit a significantly larger exchange surface.

It is to be noted that the predictions of our model for the localization
of the convection--diffusion transition in idealized lungs lead to good
estimations of the allometric scaling laws for tidal volumes and
breathing frequencies, indicating that the morphological parameters
included in our model might drive primarily the control of ventilation.

Through this short introduction to allometry of constrained organs, we
started to decipher the latent mechanisms of development of a
constrained organ inside a class of organisms. The example of the lung
is emblematic: how a complex and central organ can develop, specialize
and evolve to fulfill the needs of organisms, while sharing among
species its particularities, and efficiency.

## Concluding remarks

Biological optimization, making the most effective use of limited
resources within a set of given constraints, is a multifaceted subject
that has been a source of content for countless articles and a stimulus
for related discussion. To make the optimization of biological systems
more readily comprehensible, this chapter has focused attention on a
single organ, the human lung, and used it as a stage on which to
introduce basic principles and a canvas on which to illustrate their
application. The range of constraints, for the most part energetic or
morphometric in nature, that have conditioned the development of the
lung over the long course of its evolutionary history and given the
mammalian respiratory system its particular shape is expansive. The
characteristics of these constraints and the conditions that govern
their interplay can be represented as mathematical equations that form
the basis for models that describe the scale of the effect constraints
have on biological systems and illuminate the magnitude of their impact.
The insights into the lung's form that these models yield also provide a
more thorough understanding of its function, characterizing, for
example, modulations in the regulation of respiratory ventilation that
occur in response to changes in the body's state -- e.g., when the body
is at rest or in motion; when it is healthy or when its health is
compromised. The models are also a source of results that can be
abstracted and subsequently applied to both human organs and those of
other species that are larger and more complex. Considered within this
broader context, they can also be seen as integral elements of much
larger systems and as instances of the general allometric laws to which
those systems adhere. The significance of the larger orthogenetic and
phylogenetic implications that this abstraction of specific models into
generalized laws carries cannot be overstated and discussion of those
implications is vigorous and far-reaching. Through these discussions,
many aspects of allometry have been illuminated and a deeper
understanding of the complex systems that determine the ways
individuals, species and systems function and interact has been
achieved. Yet many of the field's underlying mechanisms and governing
principles remain to be discovered. This chapter is the prelude to a
journey into a space at the intersection of biology, ecology, and
mathematics that the allometric universe occupies and the fuel for the
exploration of the mysteries those hidden mechanisms are waiting to
reveal.

## Recommended readings {#recommended-readings .unnumbered}

- For a proper introduction to respiratory physiology, in healthy and
  pathological conditions: John B. West, *Respiratory Physiology: The
  Essentials* [@West2011].

- A reading for a deeper understanding of the lung morphometry: Ewald R.
  Weibel, *Morphometry of the human lung* [@Weibel1963] and one for the
  respiratory gases exchange: Ewald R. Weibel, *The Pathway for Oxygen:
  Structure and Function in the Mammalian Respiratory
  System* [@Weibel1984].

- A nice thesis about (in)organic mechanisms of morphogenesis: Raphaël
  Clément, *Morphogénèse et développement pulmonaire* [@Clement2011].

- The old but gold textbook in morphogenesis of living beings: D'Arcy
  Wentworth Thompson, *On Growth and Form* [@Bonner1992].

- On allometric relations, in general: Robert H. Peters, *The Ecological
  Implications of Body Size* [@Peters1986] and from a modeling
  approach: G. B. West et al., *A general model for the origin of
  allometric scaling laws in biology* [@WestBrown1997].

## Problems {#problems .unnumbered}

::: exercise
[]{#Exerc:Energy label="Exerc:Energy"} Recover the expression of the
power dissipated by viscous friction $\mathcal{P}_a$ and the elastic
power $\mathcal{P}_e$ while assuming that:

- the air velocity is a sine function,

- the power obtained is a mean value over inspiration.

**Hint:** The instantaneous elastic power is written as follow,
$$\mathcal{P}_e = \frac{1}{\mathcal{C}}V(t)F(t),$$ where $\mathcal{C}$
is the compliance of the lung, $V(t)$ is the volume of the lung and
$F(t)$ is the air flow.
:::

::: exercise
[]{#Exerc:Peclet label="Exerc:Peclet"} The localization of the
transition between convective and diffusive transport can be estimated
with the Péclet number. This number measures the relative influence of
the transport of oxygen by convection on the transport by diffusion. It
depends on the generation and can be written as follow,
$$Pe_i(t) = \frac{l_i u_i(t)}{D},$$ where $l_i$ is the length of the
bronchi of generation $i$, $u_i(t)$ is the air velocity, and $D$ is the
diffusion coefficient.

1.  Compute the average of the time-dependent Péclet number $Pe_i(t)$
    over a half breath cycle while assuming that,

    - the length of the bronchi of generation $i$ depends on the length
      of the trachea as follow : $l_i = l_0 h^i$,

    - the air velocity in generation $i$ depends on the air velocity in
      the trachea as follow, $u_i(t) = u_0(t) \left(2h^2\right)^{-i}$,

    - $u_0$ is a sine function,

    - the tidal volume is the integral over the inspiration of the
      product of the cross section of the trachea and the velocity of
      the air, $V_T = \int_0^{T/2} \pi r_0^2 u_0(t) dt$.

    The expected expression is :
    $$Pe_i = \frac{2V_Tf_bl_0}{\pi r_0^2 D} \left(\frac{1}{2h}\right)^i.$$

2.  The generation k at which the transition between convection and
    diffusion occurs is computed by solving the equation $Pe_k$ = 1.
    Compute the value $2^k$ for which $Pe_k$ = 1.
:::
