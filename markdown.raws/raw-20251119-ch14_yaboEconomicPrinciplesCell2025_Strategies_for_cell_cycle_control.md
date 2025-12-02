# Strategies for cell cycle control {#CDC}

::: chapterhighlights
- Cells require coordination of growth and division, as well as
  coordination of cell-cycle progression with several essential
  sub-tasks, such as chromosome replication and segregation.

- Single-cell dynamics data offer correlation patterns that can be used
  to understand these decisional processes.

- The cell-cycle progression and cell-division decisional process can be
  described by continuous-time and discrete-time stochastic processes.

- There are quantitative relationships that connect growth, cell-cycle
  progression, and resource allocation.

- There are differences and common points in the decisional processes by
  which single cells of different organisms commit to divide (sizers,
  adders, accumulators, titration-dilutors, etc.)
:::

## Introduction: the decision to divide illustrated through single-cell *E. coli* data. {#CDC:Sec:Introduction}

As nicely put by the Nobel prize winner François Jacob, "the dream of
every cell is to become two cells". Achieving this dream often requires
multiple steps, such as growing by a certain size, replicating DNA, and
dividing. The previous chapters have addressed cell growth as a
consequence of optimization of catabolic and biosynthetic fluxes through
optimally regulated resource allocation; this chapter deals with the
decision to divide (and to progress the cell cycle), based on growth and
other important cellular processes and cues. Clearly this decision to
divide or progress the cell cycle must be based on a set if inputs
(growth, production processes such as DNA replication and cell-wall
biosynthesis, partitioning processes, etc.) and entails several outputs,
prominently cell division, but also intermediate key cell-cycle
substeps, such as initiation of DNA replication or construction of a
"divisome" organelle. The questions that we will consider concern the
characterization of the known aspects of this decisional process and its
coupling to cell size, to cell growth, and to the chromosome cycle. We
will use throughout the chapter *E. coli* as an example. This section
provides a description of the main problem through an introduction to
the data, based on *E. coli* bacteria. Sections 2-5 start from a
mathematical toolbox of models that are useful in this context and
compare them with data. Finally, section 6 describes applications to
other organisms than *E. coli*.

<figure id="CDC:fig:EcoliExample" data-latex-placement="t!">
<p><embed src=".//images/CDC_EcoliExample.pdf" /><br />
</p>
<figcaption>Salient quantitative features of cell-division control,
explained through <em>E. coli</em> data – (A) <em>E. coli</em> cells are
rod-like. Within a condition they grow by increasing their length, and
they divide symmetrically. Following single-cell lineages, growth in
length or volume is close to exponential. (B) Size-growth plots quantify
the strength of division control. For a timer, multiplicative growth
quantified by <span class="math inline">\(G=\log(s_{d}/s_{0})\)</span>
is uncoupled to birth size, for a sizer, it is maximally coupled. The
single-cell data show an intermediate trend. (C) Since <span
class="math inline">\(G=\log(s_{d}/s_{o}) = \alpha \tau\)</span>, the
size-growth plot can be split into contributions correlationg birth size
to growth rate (top) and/or interdivision time. The data show that
<em>E. coli</em> bacteria only compensate by modulating interdivision
times. (D) Two equivalent quantifications of the strength of the
division control size. The intermediate control strategy adopted by
<em>E. coli</em> adds a size that is independent from the initial size
(“adder”). This strategy is sufficient to achieve size homeostasis.
</figcaption>
</figure>

Capturing the key processes regulating cell division is a fundamental
question in biology, which remains open despite a history of more than
60 years. During the years, scientists have learned a great deal about
the size and shape of bacteria in different nutrient conditions, what
most of the molecular players involved in the division process are, how
the DNA replication machinery is formed and how it proceeds along the
chromosome, how the septum and the new cell wall are synthesized.
However, the vast majority of these data are based on population
averages, out of which it turns out to be impossible to extract any
direct and/or causal link between the different processes involved in
cell growth that set cell division [@Osella2017]. Today, a new
generation of data has the potential to answer several open
questions [@Osella2017; @Jun2018; @Willis2017]. These data differ from
the previous generation in the ability to measure single bacterial cells
over multiple division events in controlled conditions. At the same
time, the expression of a specific gene or the concentration of specific
proteins of interest can be monitored using fluorescent reporters. For
example, fluorescent tags on the proteins involved in replication are
used to score the initiation of replication in each cell cycle.
Single-cell data allow for validating mathematical models and thus bring
insights into the causal link between the several processes a cell need
to complete before dividing.

By following lineages of cells over multiple generations under
controlled environmental conditions, scientists collected different
important pieces of evidence
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}): First, within a cell cycle, the cell
size $s(t)$ is well-described by a single exponential in
time[^1] [@Wang2010; @Osella2014]: $s(t) = s_0 \exp(\alpha t)$, where
$s_0$ is the size at birth, $\alpha$ is the growth rate, and $t$ is the
time since cell birth.

If division occurs at time $\tau_d$, a simple relationship connects the
size at division $s_d$ with the other cell properties:
$s_d = s_0 ~\exp(\alpha \tau_d)$. All the four parameters of this
equation are subject to stochasticity in time and vary across single
cells, even when they grow in controlled conditions. Second, in steady
growth, the size distribution of newborn cells does not change over
time, an observation that is referred to as cell-size
homeostasis [@Cadart2019]. Equivalently, cells show specific correlation
patterns between size at growth and size at division, which are related
to their cell-division strategy [@Skotheim2013; @Cadart2019].

Let us try to understand more in detail how single-cell correlation
patterns can be used to understand cell-division behaviors. The
observation of near-exponential growth immediately suggests a change of
variables that is useful to formulate mathematical models and to
understand how single cells control cell division. Indeed, if we can
assume that growth is exponential, we can use logarithmic sizes instead
of linear sizes. One robust observation, is that the elongation
$G = \log(s_{d}/s_{0}) = \alpha \tau$ depends on the size at birth $s_0$
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}B). This allows us to generate
so-called "size-growth" plots
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}B), in which the log-multiplicative
growth during a cell cycle of a single cell is plotted as a function of
the logarithmic size at birth [@Skotheim2013]. Different mechanisms of
size control predict different slopes for this plot. A cell division set
by a "timer", for instance, would predict no relation between $G$ and
size. Since $G = \log s_d - \log s_0$, if instead $\log s_d$ were
independent of the initial size, a "sizer", one would predict a slope
$=-1$. The *E. coli* data typically fall half way in between these two
predictions, a negative slope of about 0.5
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}B).

By noticing that the overall logarithmic growth $G$ during a cell cycle
is the product of the single-cell growth rate and inter-division time
($G = \alpha \tau$), we can ask the question of which one of these
variables is responsible for the correlation. This analysis disentangles
the contributions to cell division control due to growth rate and
inter-division timing
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}C). In other words, the dependency of
$G$ on initial size can be further decomposed on the dependency of
growth rate $\alpha$ and division time $\tau$. In *E. coli*, when growth
rate and interdivision times are plotted separately as a function of the
logarithmic size at birth, the negative slope is only observed in the
interdivision-time plot, suggesting that cell control size by adjusting
the single-cell interdivision time rather than their single-cell growth
rates. Hence, *E. coli* data indicate that $\tau$ does depend strongly
on initial size, while the growth rate has only a weak
dependency [@Osella2014].

One can visualize and quantify the mutual dependencies between cell
sizes and growth properties in other equivalent ways
(Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}D). For example, in *E. coli* data, the
scatter plot relating size at division in the y-axis to size at birth in
the x-axis for single cells has a slope of around 1 (and once again this
observation holds true for different strains and under different
environmental conditions). In this plot, a slope of 0 would suggest that
cells on average need to reach a threshold in size upon division, a
sizer. More technically, the division size $s_d$ is independent on the
initial size $s_0$ in the case of a sizer. Instead, a slope of 2 in this
plot would suggest that cells on average need to wait a fixed time upon
division, a timer. The observed intermediate slope of 1 can also be
understood using the equivalent plot in which the added size between
birth and division is used on the y-axis, studying the dependency of the
added size $s_d-s_0$ on $s_0$. This latter way to plot the data is
particularly popular, given that, for many datasets it shows no
dependency, suggesting that adding a constant added size is the
mechanism of size control effectively in place. Indeed, for *E. coli*
the experimentally observed slope is always close to
0 [@Campos2014; @Taheri-Araghi2015; @Cadart2019], an observation that
goes under the name of "adder" behavior since cells appear to add on
average a constant size during the cell cycle (Figure
[1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}(B,D)).

It is fairly simple to rationalize why, for exponentially growing cells,
a cell division strategy based on a timer does not achieve a homeostatic
size. In order to do this, we can call $q(i)=\log(s_0(i))$ the
logarithmic cell size at birth of cell-cycle $i$, and look at its
dynamics through subsequent cell cycles. Since
$s(\tau) = s_0 \exp(\alpha \tau)$, and
$\langle \alpha \tau \rangle = \log2$, and assuming that cells divide
perfectly in two halves, one immediately gets that
$$q(i+1) - q(i) = \nu(i)$$ where $\nu(i)$ is a zero-average random
variable independent for each cell-cycle, arising from the
size-independent fluctuations of inter-division times (hence, in
technical jargon, we can model $\nu$ as a discrete-time Markovian random
process). Since the jumps in logarithmic size between subsequent cell
cycles are random and independent, cell size at birth makes a
discrete-time multiplicative random walk, hence, within a population,
the distribution of cell sizes at birth tends to get wider and wider
across divisions. The following two sections will explain how size
homeostasis can be achieved by size-coupled cell divisions.

## Hazard rate approach to cell division {#CDC:Sec:2}

As we have seen in the previous section, *E. coli* cells grow roughly
exponentially. Hence, we can describe their growth by a trajectory for
size $s$ (measured as cell mass or volume) of the kind
$s(t) = s_0 \exp(\alpha t)$, where $t$ is time from cell birth. While
experimentally the growth rate $\alpha$ fluctuates with time, we will
neglect its variability and assume for the moment that it is constant.
As a consequence, the cell grows as a simple exponential function of
time. We will address different hypotheses regarding this point in the
later sections.

A simple way to describe the decision processes leading to division (or
other cell cycle progression events) is the so-called "hazard rate"
model [@Davis1952; @Osella2014; @Taheri-Araghi2015]. In this framework,
as the cell cycle progresses, each cell has a certain probability to
divide, and we call $h_d$ the rate of cell division. In principle, this
rate can be a function of many different internal cellular parameters,
all the processes that contribute setting cell division. However, since
we have in mind experiments measuring cell size versus time and
recording cell divisions, the most general "empirically accessible"
$h_d$ can depend on $s,t,s_0,\alpha$ with the constraint that
$s/s_0 = \exp(\alpha t)$. This means that there can be at most three
free parameters. We can also consider simplified models, such as
$h_d = h_d(s)$ or $h_d=h_d(s,t)$. Empirically, the lack of correlation
between $\alpha$ and birth size suggests a smaller role for this
parameter. It is important to realize that this formalism is very
powerful, as it can be applied more widely to any sub-cell cycle
decision (for example, entry into a specific phase, such as initiation
of DNA replication, mitosis, etc.), and to measurements of different
relevant cell-cycle processes (for example chromosome configurations or
the expression of cell-cycle proteins or other factors), which the
hazard rate may depend on.

<figure id="CDC:fig:HazardRate" data-latex-placement="t!">
<p><embed src=".//images/CDC_HazardRate.pdf"
style="width:85.0%" /><br />
</p>
<figcaption>Illustration of the inverse hazard rate approach on data –
Data from many lineages of dividing cells can be used to estimate the
cumulative distribution of non-divided cells, which can also be
conditioned on different variables. The drawn example refers to the case
where the tested variable is the added size <span
class="math inline">\(s-s_0\)</span>. In this case, the formalism allows
to extract mathematically the hazard rate <span
class="math inline">\(h_d(s-s_0)\)</span> from this distribution.
Experimental <em>E. coli</em> data are consistent with this adder
scenario, with an hazard rate that peaks at a characteristic added size,
after which the division control weakens.</figcaption>
</figure>

Given a model for the hazard rate, we are interested in the cumulative
probability $F(t|s_0,\alpha)$ that a cell born at $t=0$ has not divided
at time $t$, given that its initial size is $s_0$ and its exponential
growth rate $\alpha$. Box
[\[CDC:mathbox:hazard\]](#CDC:mathbox:hazard){reference-type="ref"
reference="CDC:mathbox:hazard"} discusses the mathematical formalism to
obtain this probability.

::: MathDetailblock
This box derives the probability distribution of (un)divided cells from
the hazard rate. The probability that a cell divides between time $t$
and $t+dt$ is the probability of not having divided so far times the
probability of dividing between $t$ and $t + dt$, in turn given by the
product of the hazard rate and the time interval $dt$,
$F(t|s_0,\alpha) h_d(s(t),t,s_0,\alpha)
dt$. During the same time interval, the cumulative probability of not
having divided will decrease by the same amount. Hence, we can write
$$\begin{equation}
  F(t+dt|s_0,\alpha)= 
  F(t|s_0,\alpha) [1-h_d(s(t),t,s_0,\alpha)dt]  \ .
  \label{p0eq}
\end{equation}$$

In the limit of $dt \to 0$ we obtain a differential equation, which
governs the evolution of our system $$\begin{equation}
  \frac{\intd}{\intd t}F(t|s_0,\alpha) = -h_d(s(t),t,s_0,\alpha)
  F(t|s_0,\alpha) \ ,
  \label{eq:p0eq_cont}  
\end{equation}$$ and whose formal solution is (for $t \geq 0$)
$$\begin{equation}
  F(t|s_0,\alpha) =e^{-\int_{0}^{t} dz h_d(s(z),z)} \ .
\end{equation}$$

Since we said that the probability of a cell division event in the time
interval $[t,t+dt]$ is $P(t|s_0,\alpha) dt = F(t|s_0,\alpha) h_d dt$,
the corresponding probability density is $$\begin{equation}
  P(t|s_0,\alpha)  = h_d(s,t)e^{-\int_{0}^{t} dz h_d(s(z),z)} =
  -\frac{\intd}{\intd t} F(t|s_0,\alpha). 
\end{equation}$$

Alternatively, the size $s$ can be used as a coordinate, considering for
$s>s_0$, $$\begin{equation}
  F(s|s_0,\alpha) =e^{-\int_{s_0}^{s} dz h^*_d(z,t(z))} \ ,
\label{p0x}
\end{equation}$$ while $F(s|s_0,\alpha)=0$ for $s<s_0$. Here,
$h^*_d(s,t(s)) dx$ is the probability of cell division in the size range
between $s$ and $s+ds$. The two rates are simply related by
$h^*_d(s,t(s)) ds = h_d(s(t),s)dt$, where $ds/dt = h_g(s) = \alpha s$ is
the rate of growth.
:::

The considerations we made so far are sufficient to produce "forward
models" where a hazard rate is assumed, and one explores its
consequences on the division dynamics. The simulation of such a model is
straightforward. For each discretized time increment $dt$, the cell will
grow by the prescribed dynamics $s(t)$ and will divide with hazard rate
$h_d$. If a division occurs, the mother's cell size will halve, and go
from $s$ to $s/2$ (we assume for simplicity perfect binary divisions,
but this assumption can easily be relaxed). What is a "sizer" in this
framework? We can define it as a model where
$h_d = h_d(s)$ [@Tyson1985]. Equally, a timer is a model where
$h_d = h_d(t)$, and an adder has $h_d = h_d(s-s_0)$. At this stage, it
is only intuitive, but not formally grounded, that the scatter plots of
the previous section correspond precisely to these models. This problem
will be discussed in section [1.3](#CDC:Sec:3){reference-type="ref"
reference="CDC:Sec:3"}. Note that not all the choices of hazard rates
will guarantee a steady-state cell size distribution. As a particular
case, one can consider a constant division rate $h_d(t) = r$, which is a
simple Poisson process (see the problem above). This is a pure timer and
we expect that it will not maintain a steady-state cell size
distribution (the reader can verify it, e.g. by simulations).

Beyond the forward approach, we would like to recognize the trends in
the data that favor one model rather than another. In particular, we can
ask which model best describes the *E. coli* data, presented in the
first section of this chapter. This question is a "reverse problem", and
is equivalent to the inference of the hazard rate $h_d$ from data
(Figure [1.2](#CDC:fig:HazardRate){reference-type="ref"
reference="CDC:fig:HazardRate"}). It is a very common reverse problem
for the literature, used for example in the so-called "survival
analysis" in clinical studies [@Clark2003]. In that case, the hazard
rate typically corresponds to a one-time negative outcome (death of the
patient) and the process is not repeated along lineages as in the case
of cell divisions. However, the mathematical ingredients are very
similar. Consequently, there are many regression methods available in
the literature, which can be transferred to our case. One of the most
famous is Cox regression [@Bassetti2017]. However, most of these
regression methods need an ansatz for the parameterization of the model,
which might be a nuisance, as it would require some previous knowledge.
Here we consider a simpler, direct inference method, which does not need
any parameterization (but is effective only with a sufficient amount of
data, *i.e.*, for many cell divisions).

Suppose for simplicity we deal with a sizer. In this case, it is
possible generate an estimator for the functional form of $h_d(s)$ using
Eq. ([\[p0x\]](#p0x){reference-type="ref" reference="p0x"}). By
inversion, we obtain $$\begin{equation}
  h_d(s)= - \alpha s \frac{\intd}{\intd s} \log[F(s|s_0)],
\end{equation}$$ where $F$ can easily be estimated from data, from the
cumulative fraction of undivided cells at size $s$ with initial size
$s_0$. In our case, we can use the mean value of the growth rate
$\langle \alpha \rangle$, since we are neglecting fluctuations in growth
rate.

Since we do not know whether our assumption of a sizer apples to data,
we can first combine the data and the inference to falsify the
assumption [@Osella2014]. In order to do this, we can further condition
our histograms in order to fix $s_0$. If $h_d$ depends solely on $s$,
then the inferred function $\tilde{h}_d$ should not change with varying
$s_0$. This is indeed the case if the procedure is applied to simulated
data. However, when we apply the same procedure to the experimental data
shown in the previous section, the inferred $h_d(s)$ changes if it is
inferred for different bins of birth size $s_0$. Hence, we conclude that
our *E. coli* data do not behave as a sizer, in the sense of the hazard
rate. Instead, if we consider the adder ansatz for the hazard rate
$h_d(s-s_0)$, and we repeat the procedure, we find that further
conditioning by birth size or time from birth does not change our
inferred hazard rate [@Taheri-Araghi2015]. Hence, we can conclude that a
hazard-rate analysis of the data supports an adder (or at least that the
data cannot falsify this simple model).

How does the inferred $h_d$ depend on size? Curiously, for any fixed
$s_0$, $h_d$ increases superlinearly for small cell sizes, then reaches
a maximum after which it *decreases*. In other words, some cells may
"miss" a cell division event and keep growing until they find a better
occasion to divide. This process is called "filamentation" (because the
cells that miss one or more division elongate and end up looking like
filaments), and is typically the consequence of stress, but also present
in stress-free growth conditions. experimental observations show that
*E. coli* forms filaments in response to DNA damage, antibiotics, host
immune systems, temperature, starvation, and many other stresses. As a
consequence, size plasticity may be in many cases an adaptive strategy.
The quantitative division rules of filamentous *E. coli* cells have been
studied experimentally [@WehrensErshov2018], but we lack a comprehensive
mathematical model.

One very robust observation of cell division statistics, in *E. coli*
and
beyond [@Giometto2013; @Taheri-Araghi2015; @Kennard2016; @Iyer-Biswas2014],
is that the distributions of size at birth, size at division, and
division times measured across conditions, collapse onto the same curve
when rescaled by their mean. For instance, the distributions around
these values are clearly non-overlapping: the single-cell birth-size
distribution in glucose $p_{glu}(s_0)$ strongly differ from the one in
TSB medium $p_{TSB}(s_0)$. In particular, the typical size at birth for
*E. coli* growing in glucose $\langle x_0 \rangle_{glu}$ is about $2/3$
the size of *E. coli* growing in TSB $\langle s_0 \rangle_{TSB}$ and the
average division time $\langle \tau_d \rangle_{TSB}$ is TSB is half the
one of *E. coli* in glucose $\langle \tau_d \rangle_{glu}$. This appears
to be valid across different environmental conditions (*e.g.*, nutrient
quality, temperature, pH, etc.). The remarkable empirical observation is
that, when comparing two conditions, the rescaled distribution is
universal. If we introduce the rescaled size
$\tilde{s}_0 = s_0 / \langle s_0 \rangle_{c}$, the distribution of
$\tilde{s}_0$ is universal, independent of the condition. This
observation applies also to size at division, added size between
divisions, interdivision time, and, to a certain extent, growth
rate [@Kennard2016].

An obvious question that follows from this observation is how the
size-scaling properties of cell-size at birth constrain the mechanisms
of homeostasis and the properties of stochasticity at the single-cell
level. A necessary consequence of the distribution collapse is that the
processes leading to single-cell heterogeneity and homeostasis must have
common underlying properties across conditions. Conditions differ
because they are characterized by different *dimensional* scales, but,
phenomenologically, division control is governed by the same underlying
principles (although the key molecular players may vary). The collapse
of all the distributions, when the variables are rescaled by the mean
has another, stronger, consequence: whatever the division control
mechanism is, it depends on only two scales, a size-scale (setting the
typical cell size) and a temporal scale (setting growth rate and
division time).

This constraint has strict consequences on the variability of the hazard
rate across conditions. In particular, it implies that the hazard rate
must take the mathematical form [@Grilli2017] $$\begin{equation}
    h_d(s(t), s_0, t \alpha) = \alpha \tilde{h}\left(
    \frac{s(t)}{\langle s \rangle_c}, \frac{s_0}{\langle s \rangle_c}
    \right) \ ,
\end{equation}$$ where the function $\tilde{h}(\cdot,\cdot)$ is the same
across conditions. The dependency on $\alpha$ and $t$ disappears, as the
scaling of division time, implies the existence of a unique time scale.
Since $\tilde{h}(\cdot,\cdot)$ is by definition adimensional, it can
only depend on the product $\alpha t$, which can always be re-expressed
as a function of $s$ and $s_0$, as $\alpha t = \log(s(t)/s_0)$. While
this is a powerful observation, as it allows to naturally connect
division mechanisms across conditions, it does not provide any evidence
to a particular decisional mechanism enforcing cell division, which is
encoded in the function $\tilde{h}(\cdot,\cdot)$. Addressing this
question needs further experimental details.

## Cell-division control as a discrete-time linear response process {#CDC:Sec:3}

In the previous section, we have seen how the cell-division control
mechanism can be mathematically defined using the hazard-rate framework.
This approach uses as a fundamental ingredient the probability per unit
time of cell division $h_d$, which is, *a-priori*, a function of many
internal cellular parameters. This approach is, in some sense, very
general, as it allows to characterize any complex cellular decision
process. However, this generality limits the tractability and
interpretability of the model. In this section, we introduce an
alternative discrete-time mathematical framework which greatly
simplifies the parameterization and the interpretation of a
cell-division control model [@Amir2014; @Grilli2018], and easily maps to
the empirical parameters discussed in
Figure [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}.

Specifically, instead of tracking the division rate at different stages
of the cell-cycle, it is often convenient to model directly the cell
size at birth across different generations. In this case we can, in full
generality, write $$\begin{equation}
s_0^{i+1} = f( s_0^i, \alpha, \dots ) + \eta^i( s_0^i, \alpha, \dots )    \ .
  \label{eq:discgen}
\end{equation}$$ where $s_0^i$ is the birth size of the cell at
generation $i$. The function $\eta(\cdot)$ represents a random variable
whose mean is equal to $0$ and having, a priori, arbitrary probability
distribution. The function $f( \cdot)$ described the control over cell
division. Specifically, the function $f(\cdot)$ can be simply (almost
tautologically) defined as the conditional average of the size at birth
at generation $i+1$ given all the variables that contribute to cell
division control (the previous size at birth, the growth rate, and
others), $$\begin{equation}
 f( s_0^i, \alpha, \dots ) := \langle s_0^{i+1} \rangle\vert_{x_0^i, \alpha, \dots}    \ .
\end{equation}$$ The random variable $\eta( s_0^i, \alpha, \dots )$
characterizes the fluctuations around this conditionally averaged birth
size.

This formulation of the process is as general as the hazard-rate
formalism as it allows to express any division probability
$F(s|s_0,\alpha,\dots)$.
Eq. ([\[eq:discgen\]](#eq:discgen){reference-type="ref"
reference="eq:discgen"}) simply isolates the contribution of the
(conditional) average size at division from the deviations from this
average. This separation is useful because it allows a clear
interpretation of the mechanism of division control, and because the
conditional average size at division is typically accessible from
single-cell experiments. For instance, a timer corresponds to
$f( s_0^i, \alpha ) \propto s_0^i$, where the proportionality constant
equals $\exp( \alpha \tau_d) / 2$. A sizer corresponds to $f( \cdot )$
being a constant, independent of the initial size $s_0^i$. Along the
same lines, an adder is defined as
$f( s_0^i, \alpha ) = ( s_0^i + \Delta(\alpha) )/2$, where
$\Delta(\alpha)$ corresponds to the (average) added size. The formalism
also shows how there is a continuum of possible intermediate behaviors
besides these three limit cases.

Given the facts that growth is exponential, and the distribution of
sizes at birth is approximately
Lognormal [@Taheri-Araghi2015; @Kennard2016], it is once again
convenient to introduce the logarithmic size $q_0^i = \log s_0^i$. One
can derive the dynamics of the variable $q_0^i$ as a function of the
dynamics defined in
Eq. ([\[eq:discgen\]](#eq:discgen){reference-type="ref"
reference="eq:discgen"}) [@Grilli2017]. Since the fluctuations of this
variable are small, this dynamics is fully specified by a set of
linear-response parameters $\lambda_{ab}$ relating the main observables
(i.e. in our case each of the variables $a,b$ can be
$q_0, \alpha, \tau, G$).

The linear-response framework offers a flexible and analytically
tractable tool to formulate and explore different models of division
control. The models can be constrained by correlation patterns measured
in data, quantified for example by covariances, which relate to the
coupling parameters $\lambda_{ab}$. However, the question remains of
whether such models are consistent with data. For *E. coli* data, the
linear-response framework predicts the correct consistency relations
between experimental measurements, thereby confirming its usefulness to
characterize empirical data [@Grilli2018]. A second, more biologically
relevant, question is identifying the biological mechanism reproducing
the observed dependency patterns. As already discussed, the observation
that $\lambda_{qq} \sim 0.5$ is a strong indication of adder-like
size-control
mechanisms [@Amir2014; @Taheri-Araghi2015; @Grilli2017; @Grilli2018].
Interestingly, one can show that the non-zero correlation between growth
rate and log-initial size
$\langle \delta \alpha^{i+1} \delta q_0^i \rangle$ can be explained
because of the correlation between mother and daughter single cell
growth rates (the presence of a non-zero value $\lambda_{\alpha \alpha}$
and a dependency of the division size on the growth rate (a non-zero
term $\lambda_{q \alpha}$). Such a relation between parameters point to
some dependency on the size at division on the single cell-growth rate.
For *E. coli*, it is possible [@Grilli2018] to reproduce the empirical
values of these coupling parameters by assuming an adder model where the
added size depends exponentially on the single-cell growth rate,
following the same dependency it has on the population growth rate (this
behavior will be discussed in more detail below, and is sometimes termed
Schaechter's Law [@Schaechter1958]).

## Coordination of cell division with different cell-cycle processes {#CDC:Sec:4}

<figure id="CDC:fig:CellCycleModels" data-latex-placement="t!">
<p><embed src=".//images/CDC_CellCycleModels.pdf"
style="width:87.0%" /><br />
</p>
<figcaption>Comparison of different cell-cycle models including
chromosome sub-periods proposed in the literature for <em>E. coli</em> –
(A) The DNA replication-segregation cycle divides of the cell cycle into
sub-periods. The B-period is the period between cell birth and
initiation of DNA replication; the C-period is the period needed for
completing DNA replication; and the D-period is the period between the
termination of DNA replication and cell division. Finally, the I-period
is the period between two consecutive initiations of DNA replication,
which usually spans two generations. (B) Scheme of the
‘replication-centric’ class of models in which DNA
replication-segregation sets division (first column). These models
usually assume that the CD and the I periods are adders (blue lines in
the third and fourth column, respectively), in agreement with data (red
lines in the same panels). The G-period correlation pattern is a
prediction of the model in general agreement with data (yellow vs red
lines in the second column). (C) Schematic for the
‘replication-agnostic’ class of models in which a process starting at
cell birth drive division (first column). These models assume the G and
I periods to be adders (blue lines in the second and fourth panels,
respectively). The C+D period correlation pattern is a prediction of
this model which does not agree with the available data (yellow vs red
lines in the third panel). (D) Schematic for the ‘concurrent cycles’
class of models in which two processes compete to set division through
an AND gate (first column). These models assume the I periods to be an
adder (blue lines in the fourth column) and using additional parameters
predict both adders in the G and C+D periods (yellow lines in the second
and third column). (E) Plotting the slope of the G versus the C+D-period
allows to compare the different models with data. Schematic similar
Figure 4 in <span class="citation" data-cites="Colin2021"></span>.
</figcaption>
</figure>

In the previous sections, we learned that *E. coli* single-cell dynamic
data reveal the adder size-control behavior, which allows bacterial
cells to maintain size homeostasis. We also discussed a mathematical
framework that describes how size control is achieved, and, in
particular, how the key measured variables (logarithmic size at birth,
interdivision time, growth rate, and total growth during a cell cycle)
are connected. Here, we introduce a joint description of the DNA
replication cycle, which at the modeling level makes it necessary to
partition the cell cycle into sub-periods. We then present the key
elements and observations around the debate on whether and how DNA
replication and genome segregation is limiting cell division in
*E. coli*. In presenting this debate we aim to (i) highlight the
positive and innovative aspects of some of the cornerstone studies of
recent years, (ii) provide the reader with robust tools necessary to
compare mathematical models against data. Finally, we conclude the
section by underlying a few open questions.

It is a classic question in biology [@Meselson1958; @Cooper1968] how
cells achieve the precise coordination of the cell cycle with chromosome
replication and segregation is necessary for cell survival. DNA
replication defines a way to subdivide the cell cycle into sub-periods.
In *E. coli*, the period between cell division and initiation of DNA
replication is normally referred as the B-period. The C-period is the
period needed to complete replication. Bacterial DNA is organized in
circular chromosomes which replicate starting from a well-defined
"origin" region (called *ori* locus). The replication machinery moves
bi-directionally, and the two "replication forks" proceed approximately
at the same speed and terminate in a "terminus" region of the chromosome
called *ter* locus [@Bates2005; @Kleckner2018; @Magnan2015]. For
*E. coli* cells dividing at mean interdivision times from about 20
minutes to about one hour, the replication speed is approximately
constant, resulting in an approximately constant C period of around 40
minutes [@Michelsen2003]. The D-period is the period that lasts from the
end of replication to the next division which thus includes segregation
and septum formation. Note that the inter-division time, *i.e.* the time
between two consecutive division events, can be as short as 20 minutes
in *E. coli*. How can a cell with a division time shorter than the
C-period duration have at least two copies of the DNA? Classical studies
have shown that *E. coli* and other bacteria can set up multiple
overlapping rounds of replication, as summarized by Cooper and
Helmstetter in 1968 [@Cooper1968]. For example, a cell at birth is
already replicating DNA and has two forks. During the cell cycle, two
new initiation events take place, which will only terminate in the
daughter cells [@Grant2011]. We will refer to the "G-period" and the
"I-period" as the periods between two consequent division and initiation
events, respectively.

As briefly mentioned in the introduction of this chapter, the recent
single-cell experiments allow to score initiation and termination of DNA
replication by fluorescently tagging proteins involved in the formation
of the replication forks or directly the *ori*
locus [@Adiciptaningrum2015; @Wallden2016; @Si2019; @Witz2019; @Colin2021].
The scoring of initiation and termination makes it possible to produce
the size-growth, and the equivalent adder, plots for any of the
sub-periods BCD [^2] as well as for the G- and I-periods (jointly). In
the remainder of this section, we will refer to the slope of the
size-growth plot of a sub-period X (X= B,C,D,G, or I) as $\lambda_X$,
and to the slope of the corresponding adder plot as $\zeta_X$. The two
slopes are linked by the equation
$(1-\lambda_X) = \frac{\zeta_X +1}{Q_X}$, where
$Q_X = \exp(\left< \text{growth during X}\right>)$ (see Mathematical
Detail Box
[\[mathbox:zetaformalism\]](#mathbox:zetaformalism){reference-type="ref"
reference="mathbox:zetaformalism"}).

Having formally defined sub-periods for the cell cycle and the
corresponding linear-response formalism, we now proceed by discussing a
schematic overview of the experimental observations in *E. coli* that
any mathematical model should reproduce:

- The G-period shows an adder behavior, ($\lambda _G=-0.5$,
  $\zeta_G=0$) [@Campos2014; @Taheri-Araghi2015].

- The C-period duration is approximately constant across cells and
  experimental conditions with, a tendency to increase for slow growth
  rates and the C-period generally shows a timer behavior[^3]
  ($\lambda _C=0$,
  $\zeta_C=Q_C-1$) [@Zheng2020; @Zheng2016; @Si2017; @Adiciptaningrum2015; @Kleckner2018].

- The I-period shows an adder behavior, ($\lambda _G=-0.5$,
  $\zeta_G=0$)[@Micali2018; @Witz2019; @Si2019].

- The CD-period shows an adder behavior
  ($\lambda _{CD}=\frac{Q_{CD}-1}{Q_{CD}}$,
  $\zeta_{CD}=0$)[@Witz2019; @Logsdon2017].

- The single-cell growth rate and the duration of the CD period are
  inversely proportional [@Wallden2016].

Other interesting observations that are considered in the mathematical
models we will present shortly are

- *E. coli* cells divide symmetrically with a narrow distribution of
  division length with CV = 0.05 [@Osella2014]. Note that this CV is
  lower than the CV of both the growth-rate distribution (CV $\approx$
  0.1) and interdivision time distribution (CV $\approx$ 0.2).

- The growth rate of the mother cell is correlated positively with the
  growth rate of the daughter cells, with a Pearson correlation of
  around 0.5 [@Wang2010].

::: MathDetailblock
This box shows how to translate the linear response
("$\lambda$-formalism") to an equivalent formalism based on the slopes
of adder plots ("$\zeta$-formalism"). The interested reader can find
more information
in [@Amir2014; @Grilli2018; @Micali2018; @Micali2018a; @Colin2021]. As
discussed previously,
Eq. [\[eq:linfin\]](#eq:linfin){reference-type="eqref"
reference="eq:linfin"} makes it possible to estimate the linear-response
parameter $\lambda$ in experimental data from the covariance of log-size
fluctuations between subsequent generations, by noticing that
$\left(1 - \lambda_G \right) = \frac{ \left< \delta q^{i+1}_0 \delta
    q^i_0 \right> }{ \sigma^2_{q_0} }$, where we refer to $\lambda$ in
Eq. [\[eq:linfin\]](#eq:linfin){reference-type="eqref"
reference="eq:linfin"} as $\lambda_G$, to highlight the fact that this
equation refers to the G-period. Exponential growth dictates that
$2 s_0^{i+1} = s^i_0 e^{\alpha^i \tau^i}$, where $s_0^i$, $\alpha^i$,
and $\tau^i$ are the size at birth, the growth rate and the
interdivision time, respectively. For the cell cycle $i$ one can expand
the logarithmic growth $G_G^i:=\alpha^i\tau^i$ around its average value
($\left<G_G\right> \simeq \log 2$) in terms of variations around the
logarithmic size at birth $q^i_0:=\log s^i_0$. Following this procedure,
the cell size at birth of generation $i+1$ within a lineage can be
expressed as a function of the parameters of generation $i$, as follows,
$$\begin{align}
\label{eq:Variel}
  2s^{i+1}_0 =
  Q_G \left( s^i_0 \right)^{1-\lambda_G} \left< s_0 \right>^{\lambda_G} + \nu_0^i
  \ ,
\end{align}$$ where
$Q_G = e^{\left<G_G\right>} = \exp \left< \log s_d / s_0 \right>$, $s_d$
is the cell size at division and $\nu_0^i$ is a discrete-time Gaussian
noise with mean zero and standard deviation $\sigma_{s_0}$. Expanding
around the average size, for small fluctuations we obtain a mapping
between added size and slope of the size-growth plot, $$\begin{align}
\nonumber
2s^{i+1}_0 &=  Q_G \left< s_0 \right> + (1-\lambda_G) Q_G  \delta s^i_0 + \nu_0^i \\
\nonumber
\delta \Delta^i_G &=  + \left[ (1-\lambda_G) Q_G - 1\right] \delta s^i_0 + \nu_0^i. 
\end{align}$$ Here $\Delta^i_G = s^{i}_f - s^i_0$ is the added size
during a cell cycle, and
$\delta \Delta^i_G = \Delta^i_G - \left<\Delta^i_G \right>$ is its
fluctuation. Hence, by definition, the term in square brackets must be
the slope of the adder plot $$\begin{align}
\zeta_G := (1-\lambda_G) Q_G - 1.
\end{align}$$ Solving the equation for $\lambda_G$, we get
$$\begin{align}
  \left(1-\lambda_G \right)= \frac{\left( \zeta_G + 1 \right)}{Q_G} \ , 
\label{eq:mapping1}
\end{align}$$ which can be used (assuming as usual small fluctuations)
to convert the slope $\zeta_G$ of the adder plot into the slope of the
size-growth plot $\lambda_G$, and vice-versa.
:::

The mathematical models proposed in the literature can all be described
with the general framework we provided so far. However, they are
different in terms of ingredients and relevant variables
(Fig. [1.3](#CDC:fig:CellCycleModels){reference-type="ref"
reference="CDC:fig:CellCycleModels"}). Specifically, they can be grouped
into two broad classes with fundamentally different views on the role of
DNA replication, its impact on cell division control, and ultimately on
how the cell division and replication cycles are
coupled [@Micali2018a; @Harris2018; @Kleckner2018; @Si2019; @Witz2019].
A class of 'replication-centric' models see the completion of DNA
replication as the crucial checkpoint for cell-cycle progression, which
fundamentally limits division and initiation
events [@Wallden2016; @Witz2019]. Instead, 'replication-agnostic' models
assume that cell division is limited by a cell cycle-related process
such as septum or cell wall formation and not by DNA
replication [@Harris2016; @Si2019].

The linear-response theory over sub-periods coupled with the
new-generation experimental observations on single cells gives us a
powerful tool to compare the different models (see
Box [\[mathbox:limitingmodels\]](#mathbox:limitingmodels){reference-type="ref"
reference="mathbox:limitingmodels"}). Crucially, while the slopes of the
size-growth plots are ultimately correlation patterns, the
interpretation of the *causal* link between them changes across
different models. For instance, the replication-centric models generally
assume that two parameters among $\lambda_I$, $\lambda_B$,
$\lambda_{CD}$ are input variables, fixed by an underlying molecular
mechanism, while $\lambda_G$ is an output of the model, *i.e.* an
emergent correlation pattern predicted by the model. In contrast, the
replication-agnostic models assume a mechanism for the G-period
($\lambda_G$ is fixed), and the other correlation patterns are outputs
of the model. Hence, the observed relationships between linear-response
constants across conditions can be used to select a specific model. In
the following, we present replication-agnostic theories first, then
replication-centric models, then we introduce a class of models that
find a solution of this dichotomy.

::: MathDetailblock
This box describes the quantitative tools necessary to systematically
compare cell-cycle sub-periods models with data using the
linear-response formalism and size-growth plots. Since the formalism may
become very heavy, to avoid complications we will present the the case
of slow-growth conditions, in which there are no overlapping replication
rounds. In addition, we will assume that the growth rate is a constant
parameter and we will assume perfectly symmetric division.

Replication-centric models assume $\lambda_{CD}$ and either $\lambda_B$
or $\lambda_I$ to be input parameters in the model. Here, we focus on
the case in which $\lambda^*_{CD}$ and $\lambda^*_I$ are fixed, which is
the case for the Cooper and Helmstetter, Ho and Amir, and Witz et al
models [@Cooper1968; @Ho2015; @Witz2020]. In these models, one has that
$\delta q_I^{i+1} = (1-\lambda^*_I) \delta q_I^i + \alpha \nu^i_I$ and
$\delta q_0^{i+1} = (1-\lambda^*_{CD}) \delta q_I^i + \alpha
\nu^i_{CD}$, where $q^i_0$ and $q^i_I$ are the logarithmic sizes at
birth and initiation of the cell cycle $i$, respectively; $\alpha$ is
the growth rate, and $\nu^i_I$ and $\nu^i_{CD}$ are the white noise
contribution related to the I and CD periods, respectively. In this
class of models, $\lambda_G$ and $\lambda_B$ are mathematically linked
to $\lambda^*_{CD}$ and $\lambda^*_I$, which provides predictions that
can be validated or falsified with data: $$\begin{align}
    \label{eq:labdaG_ICDmodels}
    \left(1 - \lambda_G \right) &:= \frac{ \left< \delta q^{i+1}_0 \delta q^i_0 \right> }{\sigma^2_{q_0} } = \frac{ (1-\lambda^*_{CD})^2 (1-\lambda^*_I) \sigma^2_{q_I} }{\sigma^2_{q_0} } , \\
    \label{eq:labdaB_ICDmodels}
    \left(1 - \lambda_B \right) &:= \frac{ \left< \delta q^{i}_I \delta q^i_0 \right> }{\sigma^2_{q_0} } = \frac{ (1-\lambda^*_{CD}) (1-\lambda^*_I) \sigma^2_{q_I} }{\sigma^2_{q_0} }. 
\end{align}$$ Note that by combining
[\[eq:labdaG_ICDmodels\]](#eq:labdaG_ICDmodels){reference-type="eqref"
reference="eq:labdaG_ICDmodels"} with
[\[eq:labdaB_ICDmodels\]](#eq:labdaB_ICDmodels){reference-type="eqref"
reference="eq:labdaB_ICDmodels"}, we also get the relationship
$$\begin{align}
    \label{eq:labdaG_lambdaCDB}
    \left(1 - \lambda_G \right) = \left(1-\lambda_{CD}\right)
  \left(1-\lambda_B \right) \ .
\end{align}$$
:::

The replication-centric models are in line with the classic views on the
*E. coli* cell cycle, but they are challenged by recent
findings [@Cooper1968; @Donachie1968; @Micali2018a; @Harris2016; @Zheng2020].
The 1968 Cooper and Helmstetter model was based only on the available
population-average data at that time. The model posits that cell
division happens within a defined period (CD) of time after initiation.
Shortly after, Donachie [@Donachie1968] combined the Cooper and
Helmstetter observation of a constant (population average) CD period
with the even older observation that population-average cell size
increases with the growth rate with a trend that is compatible with an
exponential (Schaechter's law [@Schaechter1958], which we mentioned
above) and postulated that the population-average mass-per-origins is
constant with the growth rate. Crucially, the classic paradigm by which
replication limits division rested on indirect conclusions based on
population averages, but these assumptions needed to be verified by
single-cell data, which showed that things are much more
complex [@Osella2017].

In recent times, Ho and Amir [@Ho2015] were the first to connect the
Cooper-Helmstetter-Donachie ideas with the new observation of adder
correlation patterns over the G-period. The authors assumed an adder
mechanism during the I-period and a timer mechanism during the CD
period. This model produces (in the limit of small noise in the timing
of the CD period) an adder behavior in the G-period. Note that in this
model $\lambda _I=-0.5$ and $\lambda_{CD}=0$ are inputs while
$\lambda _G \approx -0.5$ is an output of the model. This model, by
definition, fails in reproducing the adder behavior in the CD period
(which was not known at the time). Although it turned out to be an
oversimplification, this work has the merit of connecting the old
theories with new single-cell data into a simple and elegant
replication-centric model.

The first studies measuring the initiation of DNA replication in single
cells [@Adiciptaningrum2015; @Wallden2016] brought two new experimental
pieces of evidence into the field: they observed the duration of the CD
period was inversely proportional to the single-cell growth rate and
that the C period does not display any size compensation. Based on their
data, Wallden and coworkers proposed a replication-centric model with a
sizer in the B-period ($\zeta_B=-1$), which was later
falsified [@Micali2018; @Witz2019; @Si2019]. A subsequent study by a
different group [@Witz2019] measured consecutive initiation events in
single cells and observed three adders in the G, I, and CD periods. They
then designed an improved version of the Ho-Amir model (already proposed
for mycobacteria [@Logsdon2018]) in which the initiation of DNA
replication triggers both the next initiation and a division event with
an adder mechanism. In this model, the adder in the G-period is an
output of the model, which emerges from the adder in I and CD when the
growth rate is a random variable and a sufficiently skewed asymmetry in
cell division is added into the model. This replicaiton-centric model is
unable to capture the growth rate -- CD period inverse relationship
discovered by Wallden and coworkers. However, it has the merit of
improving the Ho and Amir model accounting for both adders in I and CD
and introducing a debate over the importance of asymmetric division.

The replication-agnostic models entered the debate more recently. Based
on dynamic cell-wall and cell-geometry measurements, Harris and Theriot
proposed a model in which the completion of the division septum, and not
the chromosome, was the limiting factor for cell
division [@Harris2018; @Harris2016]. This model proposes a simple
molecular mechanism for the adder based on three main ingredients: (i) a
crucial factor involved in setting division is produced at a rate
proportional to the cell size; (ii) this factor needs to reach a
threshold in the number in order the cell to divide; (iii) the factor in
the next generation has to be reset, with no history dependencies on the
previous cell cycle (in the case of the septum, this is natural, as a
new septum needs to be produced from zero at every cell cycle). This
model structure is still the basis for different mechanistic models
explaining the adder during the G period, but the mechanistic factor was
also proposed to be a protein [@Ojkic2019; @Panlilio2021; @Si2019].
Further evidence in favor of a replication-agnostic view came from
experiments performed by the Jun lab [@Si2019] aiming to perturb
independently the adder correlation pattern in the G-period, while
maintaining intact the adder pattern over the I-period, and viceversa.
The perturbations were achieved by inducing oscillating levels of the
FtsZ protein, which forms a contractile ring structure at the future
cell-division site and of the DnaA protein, responsible for the
initiation of replication, respectively. The authors interpreted the
results of these experiments as a proof that the replication and
division cycles are independently regulated, and in particular that
completion of DNA replication and segregation is not a limiting factor
for cell division. Additionally, the authors re-interpreted the
'molecular adder' model proposed by Harris and Teriot, suggesting that
the FtsZ may be the "adder protein" setting division. This work has the
merit of providing precious experimental information. However, the model
fails to explain the adder behavior over the CD period, as well as the
correlation patterns related to how the replication and the division
cycles are coordinated [@Micali2018; @Micali2018a; @Colin2021].

The replication-centric and replication-agnostic views have been firmly
opposing each other in recent years (see
e.g. [@Treut2020; @Witz2020; @LeTreut2021]). However, a standpoint that
is gaining consensus is that neither of these views is able to capture
the full complexity of the correlation patterns in the
data [@Micali2018; @Micali2018a; @Colin2021; @Zheng2020; @Kleckner2018; @Tiruvadi-Krishnan2022].
The recently proposed "concurrent-cycles"
scenario [@Micali2018; @Micali2018a; @Colin2021] bridges the two
opposing views and is in better agreement with the data compared to all
the above models. The key innovative element in this theoretical
framework lies in the assumption that there is no unique process
limiting cell division. Rather a set of competing processes have to be
completed before division, and some "downstream control" module
(modelled as a logic gate) has to process the input from these
processes. In its original formulation [@Micali2018; @Micali2018a],
based on the available data the competing processes are the DNA
replication processes defined by an adder in the I-period, a timer in
the replication-segregation period cycle, and a cell division process
that adds constant size between two consecutive divisions
(division-related cycle). The division is decided by an AND gate, which
triggers when both of two actions are completed, the interdivision
period is complete and the replication-segregation period is complete.
Therefore, the AND gate selects the slowest of the two random processes
(which vary across single cells) to set the timing. Note that in this
framework the CD period can be set by the intrinsic
replication-segregation period of this is the slowest process, or by the
interdivision period in case this other process is the slowest one. The
concurrent-cycles framework makes precise predictions on how the
sub-periods correlations of size change when either the
replication-related or the division-related cycles are perturbed.
Recently, experiments in which cell wall insertion is delayed confirmed
the prediction of the model [@Colin2021]. Other recent studies proposed
similar frameworks, adding mechanistic details, where the onset of
constriction at the divisome [@Tiruvadi-Krishnan2022] and/or a
"progression control complex" including the chromosome and the divisome
play the role of the gate deciding cell
division [@Zheng2020; @Kleckner2018]. Technically, concurrent cycle
models need an additional set of parameters compared to the
replication-centric and agnostic models (see
Box [\[mathbox:concurrent\]](#mathbox:concurrent){reference-type="ref"
reference="mathbox:concurrent"}). These parameters are ultimately
summarized by one extra relevant parameter, which can be expressed as
the probability that the division-related process to sets division (in a
given cell cycle). Thus, the replication-centric and
replication-agnostic models can be seen as limit cases of the
concurrent-cycles framework, where this probability is zero or one
respectively.

Despite the large improvement that the concurrent-cycles framework
provides in the agreement with data, many questions remain open. For
example, we do not know the probability of either of the concurrent
processes limiting division varies under different conditions. Recent
surveys of the available data [@Colin2021; @Tiruvadi-Krishnan2022]
suggest that the probability of a chromosome-agnostic cycle increases
with increasing growth rate. At very slow growth (interdivision times of
300 minutes or more), it has been been suggested that
replication-segregation is the limiting process. Additionally, we
currently do not know what tunes such probability and what the role of
the growth rate may be. We also do not know how many concurrent
processes there are and which precisely are the relevant players at the
molecular level. Finally, the regulation of initiation of DNA
replication could also be set by a "gate" integrating a set of
processes, a hypothesis that remains underexplored in the literature.

::: MathDetailblock
This box provides the mathematical relationships that correspond to the
ones appearing in
Box [\[mathbox:limitingmodels\]](#mathbox:limitingmodels){reference-type="ref"
reference="mathbox:limitingmodels"} for the more general
concurrent-cycles framework. Given the complexity of this model, we
restrict to the case of no overlapping rounds. In particular, we will
show how
Eq. [\[eq:labdaG_lambdaCDB\]](#eq:labdaG_lambdaCDB){reference-type="eqref"
reference="eq:labdaG_lambdaCDB"} is no longer valid in the
concurrent-cycles framework (without the need to include additional
ingredients such as asymmetric division or mother-daughter growth rate
correlations).

In the concurrent-cycles model, cell division is determined by the
slowest of two processes. The first process is an interdivision,
(chromosome-agnostic) cycle that is concluded, for generation $i$, at a
log-size $q^i_H$, which is expressed as $q^i_H = q^*_H + (1 -
\lambda^*_H) \left( q^i_0 - \left(q^*_H - \log2\right) \right) +
\alpha \nu^i_H$, with $\lambda_H$ size control parameter of this
process. The second process is a chromosome replication-segregation
cycle (replication-centric), that is concluded, for generation $i$, at a
log-size $q^i_R$, which is expressed as $q^i_R = q^*_R + \delta
q^i_I + \alpha \nu^i_I$. Note that this equation assumes a timer for
this process, $\lambda^*_{CD'}=0$, where $CD'$ identify the time needed
for completing DNA replication, which is identical to the measurable
CD-period only when this second cycle sets division. The cell size at
division is determined by the slowest process, *i.e.*
$q^i_d = \max \left(q^i_H,q^i_R\right)$. The initiation of DNA
replication decides the next initiation independently on the size at
birth or division, generating the fluctuation around the logarithmic
size at initiation that we already found in Box
[\[mathbox:limitingmodels\]](#mathbox:limitingmodels){reference-type="ref"
reference="mathbox:limitingmodels"}, $\delta
q_I^{i+1} = (1-\lambda^*_I) \delta q_I^i + \alpha \nu^i_I$.

To calculate the fluctuations of the logarithmic size at division, we
assume that the replication-centric process sets the division of
generation $i$ with probability $p_H$ independently on $q^i_0$ and
$q^i_I$. With this assumption, and considering $\lambda^*_H$,
$\lambda^*_I$ and $\lambda^*_{CD'}=0$, the model predicts the following
values for the strength of the size-growth plots in the B-, CD- and
G-period, $$\begin{align}
\left( 1-\lambda_B \right) &= \left( 1-\lambda_{CD} \right) \left( 1-\lambda_I \right) \frac{\sigma^2_{q_I}}{\sigma^2_{q_0}} \\     
\left( 1-\lambda_{CD} \right) &= \left(1 - p_H\right) + p_H \left( 1-\lambda^*_H \right) \left( 1-\lambda_B \right)  \frac{\sigma^2_{q_I}}{\sigma^2_{q_0}}, \\
\left( 1-\lambda_G \right) &= \left(1-p_H\right)\left( 1-\lambda_B \right) + p_H \left( 1-\lambda^*_H \right)
\end{align}$$ Overall, the concurrent-cycles model allows to match the
experimental trends in the size-growth plots with an additional
parameter ($p_H$). In particular, it allows to break the relationship in
Eq. [\[eq:labdaG_lambdaCDB\]](#eq:labdaG_lambdaCDB){reference-type="eqref"
reference="eq:labdaG_lambdaCDB"} without including asymmetric divisions
or mother-daughter correlations in growth
rates [@Micali2018; @Micali2018a; @Colin2021].
:::

## Protein sectors and cell division {#CDC:Sec:5}

This chapter focuses on quantitative descriptions of the cell cycle and
cell division control, and it is natural to wonder whether and how these
consideration relate to the topic of previous Chapters and which deal
with resource allocation models where cell growth is set by catabolism
and biosynthesis. There is a strong link between regulation of growth
and cell-cycle progression, which remains a largely open area of
investigation both in biology and in quantitative biology / physics of
living systems. This section discusses some recent models aimed to
describe some specific aspects of the coordination between cell growth
and cell-cycle progression. We will start by presenting the main
questions that we want to address with the aid of mathematical models.
Then we will discuss the main ideas and ingredients behind the models
that address these questions, and present some relevant predictions that
can be tested and validated against experimental data.

The maintenance of an interplay between cell growth and cell cycle is
crucial for the correct functioning of the cell. Specifically, a cell
has to adapt both growth and division rates concertedly when either one
is perturbed. For example, the response and adaptation to environmental
stresses, such as sudden shifts in nutrient conditions or exposure to
drugs or toxins, requires the ability to reprogram in a coordinated way
cell growth and cell division. Consequently, cells across all kingdoms
of life have developed specific mechanisms to precisely coordinate cell
cycle progression with cell growth and
biosynthesis [@Bruggeman2020; @Amir2019; @Cadart2019; @Bertaux2018; @Skotheim2013; @Fishov1995].
There are many mechanisms involved in this coordination, and we lack a
complete and coherent quantitative understanding of how this
coordination works in different contexts. Sometimes we even lack simple
ways to frame questions concerning the effects on cell cycle progression
of cell growth perturbations/inhibitions, or the effects of cell growth
of cell-cycle perturbations (such as cell cycle arrest).

To formulate and address these questions quantitatively, we would need a
theoretical framework where both growth physiology (as in "how does a
cell grow?") and cell-cycle decisions/progression (as in "how does a
cell decide when to divide?") aspects are allowed to play a role and
influence each other. However, while both cell growth and cell cycle
progression alone have been subject of intense study in the past
(especially in bacteria [@Jun2018], but see ref. [@Xie2022] for a recent
review of these themes in eukaryotes), comparatively little effort has
been directed so far toward the development of such unified framework.
Nonetheless, recent work has advanced our quantitative understanding of
the cross-talk between cell growth and cell cycle progression in
bacteria. The remainder of this section will focus on discussing these
aspects.

Relatively to the bacterium *E. coli*, recent and current efforts aimed
at integrating already existing coarse-grained models of cell physiology
and cell cycle control. More precisely, several studies have extended
the classic proteome allocation theory, (presented in chapters and ),
which has proven successful in describing several physiological laws, to
include also a cell-division proteome sector "$X$", whose dynamics
should implement cell-division control (or cell-cycle progression
control) strategies at a phenomenological or molecular level
(Fig. [1.4](#CDC:fig:CellDiv){reference-type="ref"
reference="CDC:fig:CellDiv"}). The current models for *E. coli* usually
include a threshold accumulation process for cell division, i.e.,
proteins of the division sector accumulate during cell cycle progression
up to a threshold level that triggers cell division. The previous
section has mentioned some candidate molecular players for this
accumulation (the FtsZ protein and the cell wall insertion).

::: MathDetailblock
The model consists of two different layers of dynamical equations, and
one relationship connecting them. The first set of equations describes
cell growth and division as cellular processes $$\begin{equation}
  \frac{ds}{dt} = \lambda s \ ,
    \quad \quad  \frac{dX}{dt} = k_X s - \frac{d_X}{m_X}X, \ \quad \quad  \ X(\tau_d)=X_{th}  \implies \begin{cases}
        s(\tau_d) \to s(\tau_d)/2 \\  X(\tau_d) \to 0
    \end{cases},
    \label{eq:macro}
\end{equation}$$ where cell size $s$ (mass or volume) grows
exponentially at a rate $\lambda \ ([\lambda] = [T]^{-1})$, while
division proteins $X$, of mass $m_X$ being synthesized and degraded at
rates $(k_X \ ([k_X] = [s]^{-1}[T]^{-1}), d_X ([d_X] = [M][T]^{-1}))$,
accumulate until a threshold amount of them is reached and cell division
occurs, after that cell size is divided exactly in half and division
proteins number is reset to zero.

The second set of equations describes the dynamical allocation of the
proteome and the biosynthesis layer underlying cell growth, as follows
$$\begin{equation}
    \begin{aligned}
      \frac{dA}{dt} &=
        \frac{1}{m_a} \left(k_n P - a k_t R f_a
        + \sum_{P_i \in \lbrace Q, P, R, X \rbrace} d_{P_i} P_i\right), \\
      \frac{dP_i}{dt} &=
        \frac{1}{m_{P_i}} \left( a k_t f_{P_i} R f_a  -
        d_{P_i} P_i \right) \  .
    \qquad \qquad P_i \in \lbrace Q, P, R, X \rbrace \ .
  \end{aligned}
\label{eq:micro}
\end{equation}$$ According to
Eq. ([\[eq:micro\]](#eq:micro){reference-type="ref"
reference="eq:micro"}), free amino-acids ($A$) are produced from
import/catalysis of nutrients at a rate $k_n$ ($[k_n]=[M][T]^{-1})$) per
number of catabolic/transport proteins $P$, and from protein
degradation, occurring at a rate $d_{P_i} P_i$ (where
$d_{P_i} ([d_{P_i}]=[M][T]^{-1})$ is the degradation rate) for each
specific sector. Free amino-acids are taken up to synthesise each
proteome sector $P_i$ at a rate equal to the number of active ribosomes
($R f_a$), times the fraction of ribosomes synthesising the specific
sector $f_{P_i}$, times an overall protein translation rate, which in
this particular model is equal to a constant translation rate per
ribosomes $k_t \ ([k_t]=[s][T]^{-1})$ times the concentration of free
amino-acids $a\equiv (m_a A)/ \ ([a]=[M][s]^{-1})$.

Finally, there must be a connection between the two levels of
description, in the sense that cellular rates should be regarded as the
result of the underlying biosynthesis dynamics. To make this connection
explicit, we write the equation $$\begin{equation}
  s=\gamma M=\gamma (m_AA + m_PP + m_RR+ m_QQ +
    m_XX) \ ,
  \label{eq:micromacro}
\end{equation}$$ representing mass conservation (if \"size\" stands for
\"mass\" $s=M$), or the assumption of constant density (if \"size\"
stands for \"volume\" $s=V$), verified in *E. coli* for population
averages but not for single cells, or for certain
perturbations [@Oldewurtel2021; @Dennis2008]. Together,
Eqs. [\[eq:macro\]](#eq:macro){reference-type="eqref"
reference="eq:macro"}, [\[eq:micro\]](#eq:micro){reference-type="eqref"
reference="eq:micro"} and
[\[eq:micromacro\]](#eq:micromacro){reference-type="eqref"
reference="eq:micromacro"} fully specify the model.
:::

Let us take a closer look at the ingredients of this modeling framework.
The two main ingredients are (i) the standard proteome allocation theory
extended to include a division sector $X$, alongside to the standard
main sectors (see Chapter ), $Q$ (house-keeping), $R$ (ribosomes), $P$
(catabolism and transport), together with (ii) a threshold-accumulation
division strategy to set the decision to divide
(Fig.[1.4](#CDC:fig:CellDiv){reference-type="ref"
reference="CDC:fig:CellDiv"}A). Note that the fact that the division
factor $X$ is a protein is an implicit assumption in these framework and
experimentally things could be more complex. Crucially, the fact that
cell division is a proteome sector couples the rates of cellular growth
and division, by controlling the synthesis of division proteins.
Specifically, the models encode a trade-off between ribosomes and
division protein synthesis, which as we will see determines many salient
predictions.

Box [\[mathbox:predictions\]](#mathbox:predictions){reference-type="ref"
reference="mathbox:predictions"} shows how these ideas and ingredients
can be translated into a mathematical model. The framework that we are
now going to discuss is consistent with different models recently
developed in the
literature [@Serbanescu2020; @Serbanescu2021; @Bertaux2020; @Pandey2018; @Bertaux2018].

In order to exemplify how this framework can generate relevant
predictions, we dedicated an appendix \"Growth Laws\" at the end of this
document where some concrete examples taken from the literature are
discussed. The mathematical derivations are not exhaustive, but aimed to
give the reader a feeling of the \"recipe\" followed to obtain a given
prediction starting from the model's ingredients. The interested reader
should have sufficient information to work out the mathematical
calculations autonomously or follow the complete derivation in the cited
references (for example by @Serbanescu2020 [@Serbanescu2021]).

<figure id="CDC:fig:CellDiv" data-latex-placement="t!">
<p><embed src="./
    /images/CDC_CellDiv.pdf" style="width:90.0%" /><br />
</p>
<figcaption>Ingredients and predictions of modeling frameworks
integrating sector models with cell-division control – (A) The framework
unifies growth and cell division by extending the standard proteome
allocation model to include a division sector X, implementing a
threshold-accumulation process setting the decision to divide. (B) The
model is naturally suited to uncover general relationships and growth
laws involving proteome composition and growth rate, as well as
trade-offs between different proteome sectors. The inclusion of a
division protein sector <span class="math inline">\(X\)</span>
regulating cell division allows the model to make predictions on cell
size control and study the transient dynamics in nutrient
shifts.</figcaption>
</figure>

## Control of cell division across species and kingdoms {#CDC:Sec:6}

The concepts described in the previous sections are widely applicable,
but there are many relevant species-specific aspects, so that different
crucial assumptions that we have taken so far might break down for
different species and kingdoms. Additionally, it should be noted that
the approach described here is purely phenomenological, while a
biological investigation might be concerned with the detailed molecular
players responsible for the cell division and cell-cycle progression
decisions. Even in this case, the approach is useful and is being
applied in recent work. For example, if the goal is to understand how
the size control phenomenon is regulated, the phenomenological analyses
can quantify how the phenomenology of size correction behaves under
different mutants and perturbations, helping to identify molecular
players and their effects on cell-cycle decisions.

Let us consider briefly some important variations of the approach used
so far, relevant for the understanding of different species-specific
behaviors. First, it is not granted that single cells grow
exponentially, or even that exponential growth is a good approximate
description. Even in the cases where exponential growth appears to be a
good average description, these averages may emerge from more complex
behaviors at the single-cell level or in cell cycle sub-periods. For
bacteria, most studies conclude that exponential growth is a
sufficiently good description, although recent accounts show
deviations [@Nordholt2020; @Kar2021]. In budding yeast
(*S. cerevisiae*), the average growth rate was reported to change at
regulatory checkpoints with the cell-cycle
phase [@Goranov2009; @Goranov2010; @Mitchison1958]. In the fission yeast
*S. pombe*, a systematic study of single-cell growth concludes that the
majority of growth trajectories are best described by a bi-linear
growth [@Baumgrtner2009]. In cell lines of animal cells, most studies
suggest that, on average, cells grow exponentially until a certain
saturation size after which they slow down, but this mean behavior hides
many details [@Cadart2019]. For example, it seems that cells in the G1
phase of the cell cycle grow at a slightly slower rate than in later
stages of the cell cycle [@Cadart2022].

A second important aspect to consider is whether division is symmetric
or not. In *E. coli*, cells divide symmetrically, giving rise to two
daughter cells that are nearly equal in size, with a precision of a few
percent [@Osella2014]. However, different species use very different
strategies for cell division, which increase variability or explicitly
aim for asymmetry. For example, *S. cerevisiae* reproduces through
budding (hence the term "budding yeast"). The parent cell creates a
small outgrowth that eventually becomes a daughter cell. Both division
strategies are common among unicellular organisms (many filamentous
fungi grow via budding). Budding creates a parent/offspring distinction
in which age-related aspects are not transmitted equally. Since aging
may correspond to a decrease in fitness/growth rate, it can also create
diversity along lineages. A third important aspect to consider is that
the growth rate may be coupled to size and enforce size homeostasis. In
other words, homeostasis can be achieved by modulating cell-cycle
duration based on size at birth, but also if large-born cells grow
slower than small-born ones.

As an example of how different issues can be analyzed with extensions of
the phenomenological approaches discussed so far, it is instructive to
discuss in more detail how one can use the linear-response framework to
detect indications of growth-based size homeostasis. As we mentioned
previously, the overall multiplicative growth of a cell in one cycle is
quantified by $G = q_f - q_0 = \log\frac{s_f}{s_0} =: \alpha \tau$. The
slope $\lambda$ of the size-growth plot is equivalent to considering the
conditional average of $G$ over logarithmic size $q$, $$\begin{equation}
\langle G \rangle_q = \langle G \rangle - \lambda \delta_q 
\label{SizeGrowthPlot}
\end{equation}$$ As we have seen in
Fig [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"}, we can consider the separate
contributions of timing and growth to the coupling by taking separate
scatter plots with growth rate and cell division time. We can give a
more formal quantification of their contributions as follows. We call
$\theta$ the coupling strength derived from the slope the first plot
quantifying control by modulation of interdivision time,
$$\begin{equation}
  \langle \tau \rangle_q
  = \langle \tau \rangle - \langle \tau \rangle \theta \delta_q \ ,
\label{TauConditionalAverage}
\end{equation}$$ and $\gamma$ the slope quantifying modulation of growth
rate based on birth size, $$\begin{equation}
  \alpha -\langle \alpha \rangle
  = - \langle \alpha \rangle  \left(\gamma \delta_q \right) + \nu_\alpha \ .  
\label{eq:alphacorrection}
\end{equation}$$ For positive values of $\gamma$, cells that are born
larger than average can correct their sizes by growing with a slower
growth rate, and cells that are born with a smaller size than average
can correct by growing at a faster rate. Conversely, for negative values
of $\gamma$, birth-size related specific growth rate variations
increases systematically size variability.

Intuitively, we can understand that $\theta$ $\gamma$ and $\lambda$ must
be related. First, the overall homeostasis must be the result of the one
enforced by growth-rate modulation and the one enforced by
interdivision-time modulation. More formally, the slopes of the
correlation plots illustrated in
Fig. [1.1](#CDC:fig:EcoliExample){reference-type="ref"
reference="CDC:fig:EcoliExample"} for $G$, $\alpha$ and $\tau$ *versus*
logarithmic birth size must be related, because $G = \alpha \tau$.

Using the linear response approach defined in
section [1.3](#CDC:Sec:3){reference-type="ref" reference="CDC:Sec:3"},
one can derive the following equation $$\begin{equation}
  \lambda = \theta \langle\alpha\rangle \langle\tau\rangle
  + \gamma \langle\alpha\rangle \langle\tau\rangle \ . 
\label{eq:TimeVsGrowthModulationPlot}
\end{equation}$$
Eq. [\[eq:TimeVsGrowthModulationPlot\]](#eq:TimeVsGrowthModulationPlot){reference-type="eqref"
reference="eq:TimeVsGrowthModulationPlot"} states that the overall
correction to size over a cell cycle has to be the sum of a correction
due to modulation of timing and a correction due to the modulation of
specific growth rate based on size at birth. For example, if the overall
strength is an adder, and the size coupling of the duration of the cell
cycle is already an adder, the growth rate must be uncoupled from
initial size.

Going back to the data, one can use
Eq. [\[eq:TimeVsGrowthModulationPlot\]](#eq:TimeVsGrowthModulationPlot){reference-type="eqref"
reference="eq:TimeVsGrowthModulationPlot"} to evaluate the different
strategies, by evaluating the couplings $\theta$, $\gamma$ and $\lambda$
from the different scatter plots. Importantly, the constraint imposed by
Eq. [\[eq:TimeVsGrowthModulationPlot\]](#eq:TimeVsGrowthModulationPlot){reference-type="eqref"
reference="eq:TimeVsGrowthModulationPlot"} is realized in data from
several bacterial species and growth conditions, indicating that the
framework is sufficient to describe the data. Work on different bacteria
shows widespread adder correlations [@Jun2018], hence
$\lambda \simeq 0.5$. What is more surprising is that adder behavior has
been reported for in budding yeast and cultured human cells. Hence, for
many species, the inter-division correlation patterns are nearly always
close to an adder. One interesting exception is the fission yeast
*S. pombe*, discussed below. The widespread adder patterns may suggest
common general principles underlying the division control of
microorganisms and cultured single mammalian cells. Considering the
couplings $\theta$, $\gamma$ shows a different scenario, with a clear
distinction between microorganisms and cultured mammalian cells. In the
studied unicellular microbes, the inter-division adder is always due to
the modulation of cell-cycle duration. Instead, cultured mammalian cells
also rely on growth rate modulation to correct their size. In
particular, this rejects the hypothesis that adder behavior may be
favored by common underlying mechanisms. Additionally, for budding yeast
and mammalian cells, the overall adder behavior emerges from homeostatic
regulations acting close to the initiation of replication (G1/S
transition) during the cell cycle, and from a weaker regulation of the
subsequent parts of the cell cycle [@Cadart2019]. Cell growth outside of
G1 is critical in setting the average cell size but appears to be less
significant for the size homeostasis effect setting cell-to-cell
variability in birth size. This is not the case in bacteria, where we
have seen that key questions regarding the specific events in the cell
cycle where homeostasis is exerted are still under debate.

The fission yeast *S. pombe* is an interesting case to discuss. This
rapidly dividing microorganism is a yeast but uses symmetric division
(hence it is sometimes called "fission yeast"), and was the central
model system in pioneering studies of the cell cycle. Its
size-correction mechanism is the strongest observed in nature, because
it can correct size fluctuations in a single cell cycle. Its
inter-division size pattern is close to a sizer, but recently the study
of mutants with different cell widths has shown that the mechanism that
triggers division is based on a surface-area sensor, triggered at a
critical cell surface. The molecular effector of this sensing, a protein
called Cdr2, has been indentified [@Facchetti2019]. Curiously, genetic
knockout of this protein does not lead to an ablation of size
homeostasis. Rather, fission yeast cells fall back to a volume-based
mechanism, suggesting that multiple biochemical circuits play a role in
the decision to divide.

Finally, since cells of different species and in different conditions
use a range of ways to control cell division, for example sizers or
adders. An important question is why a particular species would
implement one particular strategy. One possibility is that this trait is
under selection, and the fitness of individual cells decreases away from
the optimal size. In this case sizers would be favored, because they can
compensate for deviations in one cell cycle and minimize fluctuations. A
second, more likely, possibility is that intrinsic physiological
constraints linking cell cycle and growth are important in determining
cell division control. For example, it has been argued that in bacteria
size control is a result of a cell's attempt to exert a tight control
over the initiation of DNA replication -- rather than cell
division [@Amir2017].

## Concluding remarks {#CDC:Sec:7}

This chapter focused on modeling the cell cycle. The reader should have
acquired an overview of some of the key recent experimental results in
this area, as well as the basic mathematical toolbox to address
biological questions motivated by single-cell dynamic data, concerning
(i) decisional processes during the cell cycle and primarily the
decision to divide, (ii) coordination between different cell-cycle
processes, and primarily the chromosome cycle with cell division and
(iii) the coordination of cell cycle progression with growth.

This chapter is connected with Chapters and describing resource
allocation models used here to describe growth, and with Chapter ,
describing models of growth rate variability, because it provides a
framework to include a description of the division rate variability.

## Recommended readings {#recommended-readings .unnumbered}

- Osella M, Tans SJ, Cosentino Lagomarsino M. (2017). Step by step, cell
  by cell: Quantification of the bacterial cell cycle. Trends Microbiol
  25(4):250-256. doi:
  [10.1016/j.tim.2016.12.005](https://doi.org/10.1016/j.tim.2016.12.005).

- Willis L, Huang KC (2017). Sizing up the bacterial cell cycle.
  Nat. Rev. Microbiol. 15(10):606-620. doi:
  [10.1038/nrmicro.2017.79](https://doi.org/10.1038/nrmicro.2017.79).

- Cadart, C., Venkova, L., Recho, P. et al. (2019). The physics of
  cell-size regulation across timescales. Nat. Phys. 15, 993--1004.

- Jun S, Si F, Pugatch R, Scott M. (2018). Fundamental principles in
  bacterial physiology-history, recent progress, and the future with
  focus on cell size control: a review. Rep. Prog. Phys. 81(5):056601.
  doi:
  [10.1088/1361-6633/aaa628](https://doi.org/10.1088/1361-6633/aaa628).

- Serbanescu D, Ojkic N, Banerjee S. (2021). Cellular resource
  allocation strategies for cell size and shape control in bacteria.
  FEBS J. doi: [10.1111/febs.16234](https://doi.org/10.1111/febs.16234).

- Amir A, Männik J, Woldringh CL, Zaritsky A. (2019). Editorial: The
  bacterial cell: Coupling between growth, nucleoid replication, cell
  division, and shape Volume 2. Front. Microbiol.  4;10:2056. doi:
  [10.3389/fmicb.2019.02056](https://doi.org/10.3389/fmicb.2019.02056).

- Kleckner NE, Chatzi K, White MA, Fisher JK, Stouf M. (2018).
  Coordination of Growth, Chromosome Replication/Segregation, and Cell
  Division in E. coli. Front. Microbiol. 9:1469. doi:
  [10.3389/fmicb.2018.01469](https://doi.org/10.3389/fmicb.2018.01469).

## Problems {#problems .unnumbered}

::: exercise
Show that for cells that grow linearly in time an adder and a timer are
the same.
:::

::: exercise
Analyze the consequences of a constant per-size hazard rate
$h_d^* = 1/\tilde{s}$ and compare them to the consequence of a constant
per-time $h_d = r$ (a Poisson process).
:::

::: exercise
Analyze the forward hazard rate model for cell division where
$h_d(s)= (s/\tilde{s}^2)$ by simulation and/or analytical calculations.
:::

::: exercise
Find the hazard rate corresponding to the process defined by appendix
Eq. ([\[eq:linfin\]](#eq:linfin){reference-type="ref"
reference="eq:linfin"}).
:::

::: exercise
Write an explicit expression of the four parameters $\lambda_{ab}$
appearing in appendix Eqs
([\[eq:alphalinear\]](#eq:alphalinear){reference-type="ref"
reference="eq:alphalinear"}) and
([\[eq:qlinear\]](#eq:qlinear){reference-type="ref"
reference="eq:qlinear"}) as a function of the covariances between the
fluctuations of growth rates and log-size at the same or different
generations.
:::

::: exercise
Prove that the adder strategy rapidly achieves cell size homeostasis
(that is, a controlled cell size at birth) after a few cell generations,
independently of the starting initial size. Prove that convergence to
homeostasis and loss of memory of the initial cell size is exponential
in the number of cell cycles. Write down a simple numerical code to
simulate this process and verify your analytical predictions. What is
the role of noise in setting the inter-division added size?
:::

::: exercise
Write the equivalent of
Eq. ([\[eq:linfin\]](#eq:linfin){reference-type="ref"
reference="eq:linfin"}) for the I-period and for sub-periods B and CD,
and prove the following relationships: $$\begin{align}
  \nonumber
  \left(1 - \lambda_I \right) = \frac{ \left< \delta q^{i+1}_I \delta q^i_I \right> }{\sigma^2_{q_I} },  \ \ \ \ \ \
  \left(1 - \lambda_B \right) =\frac{ \left< \delta q^{i}_I \delta q^i_0 \right> }{\sigma^2_{q_0} }, \ \ \ \ \ \
  \left(1 - \lambda_{CD} \right) =\frac{ \left< \delta q^{i+1}_0 \delta q^i_I \right> }{\sigma^2_{q_I} },
\end{align}$$ where the log-size fluctuation at initiation for the cell
cycle $i$ is $\delta q^i_I := q^i_I - \left< q_I \right> \approx
\log(s^i_I/\left<s_I\right>)$, with $s^i_I$ the cell size at initiation.
:::

::: exercise
Write the equivalent of
Eq. ([\[eq:mapping1\]](#eq:mapping1){reference-type="ref"
reference="eq:mapping1"}) for the I-period and for sub-periods B and CD.
:::

::: exercise
Write the predicted $\lambda_G$ and $\lambda_I$ for a model in which
$\lambda^*_{CD}$ and $\lambda^*_B$ are input parameters of the model.
Does
Eq. [\[eq:labdaG_lambdaCDB\]](#eq:labdaG_lambdaCDB){reference-type="eqref"
reference="eq:labdaG_lambdaCDB"} still hold?
:::

::: exercise
Extend the models in Box
[\[mathbox:limitingmodels\]](#mathbox:limitingmodels){reference-type="ref"
reference="mathbox:limitingmodels"} for:

1.  Overlapping rounds of DNA replication. This case is more difficult
    to address analytically, but can be easily simulated.

2.  The $\zeta$-formalism (without overlapping rounds). Use the model to
    answer the question: can an adder in the I- and CD-period provide
    the adder behavior in the G-period[^4]?
:::

::: exercise
Run numerical simulations of
Eqs. [\[eq:macro\]](#eq:macro){reference-type="eqref"
reference="eq:macro"}. Prove that in order to obtain an adder, the
ingredients of a size-specific (rather than constant) production rate of
the division protein $k_X$ and a reset to zero (rather than partitioning
in half in the two daughter cells) of the division factor $X$ turn out
to be essential.
:::

::: exercise
Rewrite the system of
equations [\[eq:micro\]](#eq:micro){reference-type="eqref"
reference="eq:micro"} in terms of protein fractions, either defined as
protein mass fractions $\phi_i \equiv M_i/M_{\mathrm{prot}}$ or protein
number fraction $\psi_i \equiv P_i/\sum_i P_i$, where
$M_{\mathrm{prot}} = m_Q Q + M_P P + m_R R + m_X X = M-m_A A$. In both
cases one has the obvious constraint $\sum \psi_i = 1 = \sum_i \phi_i$.
Find the connection between $\psi_i$ and $\phi_i$. What can be generally
said about the stationary composition of the proteome? How does the
senario change if degradation can be neglected?
:::

::: exercise
For the mathematically curious readers, show that the model described in
Box [\[mathbox:predictions\]](#mathbox:predictions){reference-type="ref"
reference="mathbox:predictions"} far can be written in more general
mathematical terms as $$\begin{equation}
    \begin{aligned}
  \frac{dX_i}{dt} &= f_i(\mathbf{X});
                    \qquad \frac{dZ}{dt} = h(\mathbf{X}, Z) \\
   V(\mathbf{X}, Z) &= \sum_{i=1}^N v_i X_i + v_Z Z
\end{aligned}
\end{equation}$$ where $V$ is the volume of the cell and $X_i, Z$ its
chemical constituents. Identify the functions $f_is$ and $h$. Show that
the $f_is$ satisfy the property of homogeneity, $f_i(\beta
\mathbf{X}) = \beta f_i(\mathbf{X})$. The predictions of this model have
been studied in the wider framework of dynamical systems
theory [@Pandey2020; @Lin2020].
:::

::: exercise
By directly integrating
Eq. ([\[eq:macro\]](#eq:macro){reference-type="ref"
reference="eq:macro"}), derive the following expression for the
threshold number of division proteins $X_{th} \equiv X(\tau_d)$
$$\begin{equation}
  X(t) = \frac{k_X s_0}{\lambda + \frac{d_X}{m_X}} \left( 2^{\frac{t}{\tau_d}} - 2^{-\frac{d_X}{m_X\lambda}\frac{t}{\tau_d}} \right)\implies X_{th} = \frac{k_X }{\lambda + \frac{d_X}{m_X}} \left( s_d  - s_0 2^{-\frac{d_X}{m_X\lambda}}\right). 
  \label{eq:threshold}
\end{equation}$$
:::

::: appendix
:::

[^1]: Note that most of the studies today use cell length as a proxy for
    size. However, different choices are possible such as volume or
    mass, and the differences are not fully
    characterized [@Cadart2019; @Oldewurtel2021].

[^2]: Note that under fast-growing conditions the termination is
    experimentally harder to score reliably and hence in many studies
    the C and D periods of single cells are considered together as a "CD
    period".

[^3]: Given the difficulty in observing the C-period in single cells,
    this last question requires further experimental investigation.

[^4]: Note that the adder behavior can be recovered introducing
    asymmetric divisions [@Witz2019]
