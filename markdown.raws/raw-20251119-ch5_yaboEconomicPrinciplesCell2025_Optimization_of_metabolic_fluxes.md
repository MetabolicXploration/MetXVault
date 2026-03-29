# Optimization of metabolic fluxes {#FLX}

::: chapterhighlights
- An optimization objective can be added to constraint-based models to
  make more specific predictions.

- Different purposes can be served by choosing different optimization
  objectives and constraints

- The optimal solutions can be understood in terms of elementary flux
  modes
:::

## Can optimality principles help us predict metabolic behavior?

In the previous chapter, we characterized an organism's metabolism by
listing all the biochemical reactions that can be catalyzed by the
enzymes encoded within the organism's genome. To understand how the
genome constrains patterns of metabolic flux we needed to make several
simplifying assumptions. The first important assumption was that
intracellular metabolism is at steady-state, i.e., that the production
and consumption of all metabolites is balanced such that their
concentrations are constant in time. These resulted in the mass-balance
constraints on the flux vector $\fluxv$. The flux cone of all flux
vectors satisfying the mass-balance constraints could be further reduced
by additional constraints on $\fluxv$, based on extra physical and
biological assumptions about the magnitude and directionality of certain
reactions within the network. We introduced several ways in which the
entire flux space could be explored.

When applied to very large metabolic networks, the flux space will often
contain an infinite number of flux vectors $\fluxv$ that simultaneously
satisfy all constraints. From a mathematical perspective, this implies
that the constraints do not include enough information to uniquely
specify a flux vector $\fluxv$. This makes sense biologically, since if
we imagine constraints are related to experimental observations it is
very unlikely that we will ever be able to make enough to fully account
for every reaction encoded within the entire genome of an organism (no
matter how simple it might be). Often, however, researchers do want to
further narrow down the set of flux vectors that they think biologically
relevant to the organism and conditions they are studying, perhaps even
to a unique $\fluxv$ imagined to describe the metabolic state of an
organism at a given moment in time. One popular approach for doing so is
to provide an additional assumption (or set thereof) in the form of an
objective function: it is assumed that the metabolic state of an
organism is such that some function of $\fluxv$ (e.g. growth rate) is
maximized to satisfy some criteria (e.g. evolutionary selective
advantage). The computational problem then becomes one of
constrained-optimization: find a flux vector $\fluxv$ that is optimal in
terms of the objective function(s) that simultaneously satisfies all
constraints. The resulting space of optimal flux vectors (sometimes
containing just one unique vector) is often considerably smaller than
the space of those that satisfy only the constraints.

In this chapter, we will study metabolic models based on
constrained-optimization. We will introduce a selection of commonly used
objective functions and the computational methods used to solve the
associated constrained-optimization problem. We will also characterize
optimal solutions that we get in terms of the minimal metabolic
strategies that we identified in the previous chapter: elementary flux
modes. Finally, we will explain how we can handle the cases where the
solutions are, even after optimization, not unique.

[]{#FLX:Sec:Introduction label="FLX:Sec:Introduction"}

## Metabolic modeling based on linear optimization {#FLX:Sec:optimization}

We begin by introducing linear programs and transforming them into
standard form. (For the history of linear programming, see Box
[\[FLX:BoxEconomicPlanning\]](#FLX:BoxEconomicPlanning){reference-type="ref"
reference="FLX:BoxEconomicPlanning"}.) Then, we discuss two types of
inhomogeneous constraints in Flux Balance Analysis (FBA), the
application of linear programming to metabolic modeling. Finally, we
illustrate FBA in an example.

### Linear programming problems

Linear programs (LPs) are specified for a vector $\mathvectorfont{x}$
(of real variables) and involve a vector $\mathvectorfont{c}$ (defining
the objective function) as well as a matrix $\mathmatrixfont{A}$ and a
corresponding vector $\mathvectorfont{b}$ (defining the linear
inequalities), $$\begin{equation}
 \label{eq:LPorig}
    \begin{gathered}
        \max_{\mathvectorfont{x}} \, \mathvectorfont{c}\trans \mathvectorfont{x} \\
        \text{s.t. } \mathmatrixfont{A}~ \mathvectorfont{x} \le \mathvectorfont{b} .
    \end{gathered}
\end{equation}$$ In general, an individual inequality
$\mathvectorfont{a}\trans \mathvectorfont{x} \le b$ (where the vector
$\mathvectorfont{a}$ denotes a row of the matrix $\mathmatrixfont{A}$
and $b$ denotes the corresponding component of $\mathvectorfont{b}$)
constrains a weighted sum of the variables. However, if
$\mathvectorfont{a}$ has only one nonzero component, e.g. $a_i=1$ and
$a_j=0$ for all $j\neq i$, then it restricts a single variable,
$x_j \le b$.

*Towards LP standard form.* Some variables may have nonnegativity
constraints. Hence, we order the variables such that $$\begin{equation*}
\mathvectorfont{x} 
=
\begin{pmatrix} 
\mathvectorfont{x}^\circ \\ 
\mathvectorfont{x}^\ast
\end{pmatrix} ,
\end{equation*}$$ where the superscripts $\circ$ and $\ast$ refer to the
index sets of nonnegative and "free" variables, $\mathcal{I}^\circ$ and
$\mathcal{I}^\ast$, respectively. Now, we can formulate the
nonnegativity constraints as $\mathvectorfont{x}^\circ \ge 0$. To obtain
nonnegativity constraints for *all* variables, we will consider free
variables as differences of nonnegative variables. Given the order on
the variables, we first write $$\begin{equation*}
\mathmatrixfont{A} ~\mathvectorfont{x} 
=
\begin{pmatrix}
\mathmatrixfont{A}^\circ & \mathmatrixfont{A}^\ast
\end{pmatrix}
\begin{pmatrix} 
\mathvectorfont{x}^\circ \\ 
\mathvectorfont{x}^\ast 
\end{pmatrix} .
\end{equation*}$$ Next, for every $i \in \mathcal{I}^\ast$ (for every
free variable $x_i$), we introduce $y_i^+, y_i^- \ge 0$ such that
$y_i^+ - y_i^- = x_i$. In vector notation, we have $$\begin{equation*}
\mathvectorfont{y}^+ - \mathvectorfont{y}^- = \mathvectorfont{x}^\ast .
\end{equation*}$$ Note that this transformation is not one-to-one. There
are infinitely many pairs $\mathvectorfont{y}^+ , \mathvectorfont{y}^-$
that have the same difference $\mathvectorfont{x}^\ast$. Analogously,
for every $i \in \mathcal{I}^\circ$ (for every nonnegative variable
$x_i$), we introduce $y_i^\circ = x_i \ge 0$ to obtain a uniform
notation. That is, $$\begin{equation*}
\mathvectorfont{y}^\circ = \mathvectorfont{x}^\circ .
\end{equation*}$$ Now, we can write $$\begin{equation*}
\mathmatrixfont{A}~ \mathvectorfont{x} 
=
\begin{pmatrix}
\mathmatrixfont{A}^\circ & \mathmatrixfont{A}^\ast & -\mathmatrixfont{A}^\ast
\end{pmatrix}
\begin{pmatrix} 
\mathvectorfont{y}^\circ \\ 
\mathvectorfont{y}^+ \\ 
\mathvectorfont{y}^-
\end{pmatrix} .
\end{equation*}$$ In short, $$\begin{equation*}
\mathmatrixfont{A} ~\mathvectorfont{x} = \mathmatrixfont{\bar A} ~\mathvectorfont{y} 
\quad \text{with} \quad
\mathmatrixfont{\bar A} 
:= 
\begin{pmatrix}
\mathmatrixfont{A}^\circ & \mathmatrixfont{A}^\ast & -\mathmatrixfont{A}^\ast
\end{pmatrix}
\quad \text{and} \quad
\mathvectorfont{y} 
:= 
\begin{pmatrix} 
\mathvectorfont{y}^\circ \\ 
\mathvectorfont{y}^+ \\
\mathvectorfont{y}^-
\end{pmatrix} ,
\end{equation*}$$ involving the augmented
matrix $\mathmatrixfont{\bar A}$ and the non-negative
vector $\mathvectorfont{y}$. Correspondingly, we have to transform the
vector $$\begin{equation*}
\mathvectorfont{c} 
=
\begin{pmatrix} 
\mathvectorfont{c}^\circ \\ 
\mathvectorfont{c}^\ast
\end{pmatrix} .
\end{equation*}$$ Indeed, $$\begin{equation*}
\mathvectorfont{c}\trans \mathvectorfont{x} = \mathvectorfont{\bar c}\trans \mathvectorfont{y}
\quad \text{with} \quad
\mathvectorfont{\bar c} 
:= 
\begin{pmatrix} 
\mathvectorfont{c}^\circ \\ 
\mathvectorfont{c}^\ast \\
-\mathvectorfont{c}^\ast
\end{pmatrix} .
\end{equation*}$$ As a result, we obtain an LP in standard form,
$$\begin{equation}
 \label{eq:LPstand}
    \begin{gathered}
        \max_{\mathvectorfont{y}} \, \mathvectorfont{\bar c}\trans \mathvectorfont{y} \\
        \text{s.t. } \mathmatrixfont{\bar A}~ \mathvectorfont{y} \le \mathvectorfont{b} \\
        \text{and } \mathvectorfont{y} \ge 0 ,
    \end{gathered}
\end{equation}$$ which is equivalent to the original
LP [\[eq:LPorig\]](#eq:LPorig){reference-type="eqref"
reference="eq:LPorig"} in the following sense:

$\bullet$ On the one hand, if $\mathvectorfont{x}$ is a *feasible
solution* of [\[eq:LPorig\]](#eq:LPorig){reference-type="eqref"
reference="eq:LPorig"}, that is,
$\mathmatrixfont{A} ~\mathvectorfont{x} \le \mathvectorfont{b}$, with
*objective value* $\mathvectorfont{c}\trans \mathvectorfont{x}$, then
every $\mathvectorfont{y}$ with
$\mathvectorfont{y}^\circ = \mathvectorfont{x}^\circ$ and
$\mathvectorfont{y}^+ - \mathvectorfont{y}^- = \mathvectorfont{x}^\ast$
is a feasible solution of
[\[eq:LPstand\]](#eq:LPstand){reference-type="eqref"
reference="eq:LPstand"}, that is,
$\mathmatrixfont{\bar A} ~\mathvectorfont{y} \le \mathvectorfont{b}$ and
$\mathvectorfont{y} \ge 0$, with the same objective value
$\mathvectorfont{\bar c}\trans \mathvectorfont{y} = \mathvectorfont{c}\trans \mathvectorfont{x}$.

In particular, we can choose $\mathvectorfont{y}^+$ and
$\mathvectorfont{y}^-$ as follows: for every free variable $x_i$, if
$x_i \ge 0$, then we set $y_i^+ = x_i$ and $y_i^- = 0$, and if
$x_i \le 0$, then we set $y_i^+ = 0$ and $y_i^- = -x_i$. Equivalently,
we can choose $\mathvectorfont{y}^+$ and $\mathvectorfont{y}^-$ such
that
$\mathvectorfont{y}^+ - \mathvectorfont{y}^- = \mathvectorfont{x}^\ast$
and $y_i^+ \cdot y_i^- = 0$ for all indices $i \in \mathcal{I}^\ast$.

*Note.* The latter choice involves if--then statements or nonlinear
equations. Hence, it cannot be written in terms of linear inequalities,
that is, it cannot be directly incorporated into an LP. Still, the
choice can be used to obtain equivalent (but simpler) formulations of
LPs. See the next subsection, in particular, the formulation of enzyme
constraints in FBA.

$\bullet$ On the other hand, if $\mathvectorfont{y}$ is a feasible
solution of [\[eq:LPstand\]](#eq:LPstand){reference-type="eqref"
reference="eq:LPstand"}, then $\mathvectorfont{x}$ with
$\mathvectorfont{x}^\circ = \mathvectorfont{y}^\circ$ and
$\mathvectorfont{x}^\ast = \mathvectorfont{y}^+ - \mathvectorfont{y}^-$
is a feasible solution of
[\[eq:LPorig\]](#eq:LPorig){reference-type="eqref"
reference="eq:LPorig"} and $\mathvectorfont{y}$ and $\mathvectorfont{x}$
have the same objective value.

### Metabolic modeling via linear programs *aka* Flux balance analysis

Flux balance analysis (FBA) studies metabolic models via linear
programs. The feasible solutions (fluxes) are specified by

- homogeneous equations arising from mass-balance constraints,

- homogeneous inequalities (nonnegativity conditions) arising from
  irreversible reactions,

- and extra inhomogeneous (in-)equalities encoding lower/upper bounds
  for individual fluxes or enzyme constraints involving weighted sums of
  fluxes.

(See also the previous chapter.)

The objective function can be an individual flux or a weighted sum.
Hence, a general FBA problem can be written as $$\begin{equation}
 \label{eq:FBAv}
    \begin{gathered}
        \max_{\fluxv} \, \mathvectorfont{c}\trans \fluxv \\
        \text{s.t. } \Stoichmat~\fluxv = 0 , \,
        \fluxv^\to \ge 0 , \\
        \text{and } \mathmatrixfont{G} ~\fluxv \ge \mathvectorfont{h} .
    \end{gathered}
\end{equation}$$

*Two types of extra constraints.* As already mentioned, the
inhomogeneous inequalities may involve lower/upper bounds for (all)
individual fluxes, $$\begin{equation}
 \label{eq:box}
\mathvectorfont{\ell} \le \fluxv \le \mathvectorfont{u} ,
\end{equation}$$ so-called box constraints. Componentwise,
$\ell_i \le \flux_i \le u_i$ for reaction $i$. (If there is no lower or
upper bound, one may set $\ell_i = - \infty$ or $u_i = \infty$.) Of
course, the bounds must be consistent with the irreversibility
constraints.

Additionally/alternatively, one may consider enzyme constraints. First,
for every reaction $i \in \mathcal{R}^\to \cup \mathcal{R}$, one
introduces the concentration $e_i$ of the corresponding enzyme. Then,
for every irreversible reaction $i \in \mathcal{R}^\to$, enzyme kinetics
implies the inequality $0 \le \flux_i \le k_i^{\text{cat},\to} e_i$.
Similarly, for every reversible reaction $i \in \mathcal{R}^\rlhp$, one
obtains $$\label{eq:ec}
\begin{equation} \label{eq:kcat}
    \begin{cases}
        \phantom{-} \flux_i \le k_i^{\text{cat},\rhp} e_i & \text{if } \flux_i \ge 0 , \\
        -\flux_i \le k_i^{\text{cat},\lhp} e_i & \text{if } \flux_i \le 0 .
    \end{cases}
\end{equation}
Finally, using nonnegative weights $\omega_i$,
one formulates a capacity constraint
\begin{equation} \label{eq:cap}
    \sum_{i \in \mathcal{R}^\to \cup \mathcal{R}^\rlhp} \omega_i \, e_i 
    = \mathvectorfont{\omega}\trans \mathvectorfont{e} \le \Omega 
\end{equation}
(or several such constraints).$$ Clearly, the
inequalities [\[eq:kcat\]](#eq:kcat){reference-type="eqref"
reference="eq:kcat"} involve if--then statements. Hence, they cannot be
directly incorporated into an LP. To resolve this problem, we perform
reaction splitting, which ultimately leads to an LP in standard form. In
the following, we describe this transformation in detail.

*Reaction splitting.* As described in the previous chapter, for every
reversible reaction $i \in \mathcal{R}^\rlhp$ with net reaction rate
$\fluxi$, we define a forward reaction "rate" $\fluxw_i^\rhp \ge 0$ and
a backward reaction "rate" $\fluxw_i^\lhp \ge 0$ such that
$\fluxi = \fluxw_i^\rhp - \fluxw_i^\lhp$. In vector notation,
$\fluxv^\rlhp = \fluxwv^\rhp - \fluxwv^\lhp$ with
$\fluxwv^\rhp,\fluxwv^\lhp\ge0$. Again, we note that the "rates"
$\fluxw_i^\rhp, \fluxw_i^\lhp$ do not denote the (microscopic) forward
and backward reaction rates $\fluxi^\rhp, \fluxi^\lhp$ that determine
the net reaction rate $\fluxi = \fluxi^\rhp - \fluxi^\lhp$. They are
auxiliary quantities, and only their difference
$\fluxw_i^\rhp - \fluxw_i^\lhp = \fluxi$ has a biochemical meaning.
Further, for every irreversible reaction $i \in \mathcal{R}^\to$, we
write $\fluxi = \fluxw_i^\to \ge 0$ to obtain a uniform notation. That
is, $\fluxv^\to = \fluxwv^\to \ge 0$. We introduce the augmented
stoichiometric matrix $\Stoichmataug$ and the corresponding non-negative
flux vector $\fluxwv$, $$\begin{equation*}
\Stoichmataug 
:= 
\begin{pmatrix}
\Stoichmat^\to & \Stoichmat^\rlhp & -\Stoichmat^\rlhp
\end{pmatrix}
\quad \text{and} \quad
\fluxwv 
:= 
\begin{pmatrix} 
\fluxwv^\to \\ 
\fluxwv^\rhp \\
\fluxwv^\lhp
\end{pmatrix} ,
\end{equation*}$$ and find $$\begin{equation*}
\Stoichmat~\fluxv 
= 
\Stoichmataug \, \fluxwv .    
\end{equation*}$$ Analogously, we introduce the augmented matrix
$\overline{\mathmatrixfont{G}}$ and the (objective) vector
$\mathvectorfont{\bar c}$, $$\begin{equation*}
\overline{\mathmatrixfont{G}} 
:=
\begin{pmatrix}
\mathmatrixfont{G}^\to & \mathmatrixfont{G}^\rlhp & -\mathmatrixfont{G}^\rlhp
\end{pmatrix}
\quad \text{and} \quad
\mathvectorfont{\bar c}
:=
\begin{pmatrix} 
\mathvectorfont{c}^\to \\ 
\mathvectorfont{c}^\rlhp \\
-\mathvectorfont{c}^\rlhp
\end{pmatrix} ,
\end{equation*}$$ and obtain the LP $$\begin{equation}
 \label{eq:FBAw}
    \begin{gathered}
        \max_{\fluxwv} \, \mathvectorfont{\bar c}\trans \fluxwv \\
        \text{s.t. } \Stoichmataug \, \fluxwv = 0 , \,
        \fluxwv \ge 0 , \\
        \text{and } \overline{\mathmatrixfont{G}} \, \fluxwv \ge \mathvectorfont{h} ,
    \end{gathered}
\end{equation}$$ which is equivalent to the original
LP [\[eq:FBAv\]](#eq:FBAv){reference-type="eqref" reference="eq:FBAv"}.

*Choice of $\fluxwv$.* To incorporate the enzyme
constraints [\[eq:kcat\]](#eq:kcat){reference-type="eqref"
reference="eq:kcat"}, we choose $\fluxwv^\rhp$ and $\fluxwv^\lhp$ as
follows: for every reversible reaction $i \in \mathcal{R}^\rlhp$, if
$\flux_i \ge 0$, then we set $\fluxw_i^\rhp = \flux_i$ and
$\fluxw_i^\lhp = 0$, and if $\flux_i \le 0$, then we set
$\fluxw_i^\rhp = 0$ and $\fluxw_i^\lhp = -\flux_i$. We find
$$\begin{equation*}
    \begin{cases}
        \fluxw_i^\rhp = \fluxw_i^\lhp + \flux_i \le \phantom{-} \flux_i \le k_i^{\text{cat},\rhp} e_i 
        & (\text{and } \fluxw_i^\lhp = 0) \quad \text{if } \flux_i \ge 0 , \\
        \fluxw_i^\lhp = \fluxw_i^\rhp - \flux_i \le - \flux_i \le k_i^{\text{cat},\lhp} e_i 
        & (\text{and } \fluxw_i^\rhp = 0) \quad\text{if } \flux_i \le 0 
    \end{cases}
\end{equation*}$$ and hence $$\begin{equation}
 \label{eq:wsum} \tag{$\rlhp$}
\fluxw_i^\rhp / k_i^{\text{cat},\rhp} +
\fluxw_i^\lhp / k_i^{\text{cat},\lhp} \le e_i ,
\end{equation}$$ independently of the sign of $\flux_i$ (that is, not
involving an if--then statement). To summarize, the if--then statement
[\[eq:kcat\]](#eq:kcat){reference-type="eqref" reference="eq:kcat"} for
$\fluxv$ together with our choice for $\fluxwv$ (another if--then
statement) imply the
inequality [\[eq:wsum\]](#eq:wsum){reference-type="eqref"
reference="eq:wsum"} which can be incorporated into the
LP [\[eq:FBAw\]](#eq:FBAw){reference-type="eqref" reference="eq:FBAw"}.
In fact, we further
rewrite [\[eq:wsum\]](#eq:wsum){reference-type="eqref"
reference="eq:wsum"} as $$\begin{equation*}
\fluxw_i^\rhp / k_i^{\text{cat},\rhp} \le e^\rhp_i , \quad
\fluxw_i^\lhp / k_i^{\text{cat},\lhp} \le e^\lhp_i , \quad \text{and} \quad
e^\rhp_i + e^\lhp_i \le e_i ,
\end{equation*}$$ where we introduce the forward and backward enzyme
"concentrations", $e^\rhp_i$ and $e^\lhp_i$, respectively.

The treatment of the other extra constraints is simple. First, for every
irreversible reaction $i \in \mathcal{R}^\to$, we get
$\fluxw_i^\to = \flux_i \le k_i^{\text{cat},\to} e_i$ or, equivalently,
$\fluxw_i^\to / k_i^{\text{cat},\to} \le e_i$. Altogether,
$$\label{eq:ecw}
\begin{equation}
\fluxw_i \le k_i^\text{cat} \, \bar e_i, 
\quad \text{for } i \in \mathcal{R}^\to \cup \mathcal{R}^\rhp \cup \mathcal{R}^\lhp ,
\end{equation}
where we use the vectors
\begin{equation*}
\mathvectorfont{k}^\text{cat}
:=
\begin{pmatrix} 
\mathvectorfont{k}^{\text{cat},\to} \\ 
\mathvectorfont{k}^{\text{cat},\rhp} \\
\mathvectorfont{k}^{\text{cat},\lhp}
\end{pmatrix} 
\quad \text{and} \quad
\mathvectorfont{\bar e}
:=
\begin{pmatrix} 
\mathvectorfont{e}^\to \\ 
\mathvectorfont{e}^\rhp \\
\mathvectorfont{e}^\lhp
\end{pmatrix} 
\end{equation*}
to streamline the notation.
%
Second,
we adapt the capacity constraint \eqref{eq:cap}.
Using the augmented vector 
\begin{equation*}
\mathvectorfont{\bar \omega}
:=
\begin{pmatrix} 
\mathvectorfont{\omega}^\to \\ 
\mathvectorfont{\omega}^\rlhp \\
\mathvectorfont{\omega}^\rlhp
\end{pmatrix} ,
\end{equation*}
we obtain
\begin{align*}
\sum_{i \in \mathcal{R}^\to \cup \mathcal{R}^\rhp \cup \mathcal{R}^\lhp} \bar \omega_i \, \bar e_i
&= \sum_{i \in \mathcal{R}^\to} \omega_i \, e_i + \sum_{i \in \mathcal{R}^\rlhp} \omega_i \, \underbrace{(e^\rhp_i + e^\lhp_i)}_{\le e_i} \\
&\le \sum_{i \in \mathcal{R}^\to \cup \mathcal{R}^\rlhp} \omega_i \, e_i \\
%&= \mathvectorfont{\omega}\trans \mathvectorfont{ e}  \\
&\le \Omega ,
\end{align*}
in short,
\begin{equation}
\sum_{i \in \mathcal{R}^\to \cup \mathcal{R}^\rhp \cup \mathcal{R}^\lhp} \bar \omega_i \, \bar e_i 
= \mathvectorfont{\bar \omega}\trans \mathvectorfont{\bar e} 
\le \Omega .
\end{equation}$$

Of course, box constraints [\[eq:box\]](#eq:box){reference-type="eqref"
reference="eq:box"} for $\fluxv$ can also be written in terms of
$\fluxwv$: for the irreversible reactions, we get
${\mathvectorfont{\ell}^\to \le \fluxwv^\to \le \mathvectorfont{u}^\to}$
(with $\mathvectorfont{\ell}^\to \ge 0$), and for the reversible
reactions, we get
$\mathvectorfont{\ell}^\rlhp \le \fluxwv^\rhp-\fluxwv^\lhp \le \mathvectorfont{u}^\rlhp$
(with $\mathvectorfont{\ell}^\rlhp < 0$ and
$\mathvectorfont{u}^\rlhp>0$). The latter inequalities can be further
simplified using our choice of $\fluxwv$.

*Summary.* We have shown that an FBA problem
[\[eq:FBAv\]](#eq:FBAv){reference-type="eqref" reference="eq:FBAv"}
involving box constraints [\[eq:box\]](#eq:box){reference-type="eqref"
reference="eq:box"} and enzyme constraints
[\[eq:ec\]](#eq:ec){reference-type="eqref" reference="eq:ec"} can be
transformed into an *equivalent* LP problem
[\[eq:FBAw\]](#eq:FBAw){reference-type="eqref" reference="eq:FBAw"} in
standard form. In particular, for every feasible $\fluxv$ (and
$\mathvectorfont{e}$) in $\Stoichmat~\fluxv = 0$, $\fluxv^\to \ge 0$,
and [\[eq:ec\]](#eq:ec){reference-type="eqref" reference="eq:ec"}, there
is a feasible $\fluxwv$ (and $\mathvectorfont{\bar e}$) in
$\overline \Stoichmat~\fluxwv = 0$, $\fluxwv \ge 0$, and
[\[eq:ecw\]](#eq:ecw){reference-type="eqref" reference="eq:ecw"},
namely, our choice of $\fluxwv$. Conversely, for every feasible
$\fluxwv$ (not necessarily in the form of our choice) in the standard LP
problem, there is a feasible $\fluxv$ in the original FBA problem.

::: Ecoblock
Linear programming as an algorithmic approach to solving constrained
linear optimization problems was first developed by soviet mathematician
and economist Leonid Kantorovich in the 1930s
[@Kantorovich1960; @Kantorovich1965]. Kantorovich was tasked with
helping to optimize production in the soviet plywood industry, but soon
discovered that the underlying problems could not be solved using
analytical methods. He instead developed a method for solving linear
optimization problems using an iterative process through which a
solution is continuously improved until an optimum is reached.
Kantorovich argued that this could be used to make soviet economic
planning more efficient.

Soviet planning was primarily based on material balancing, which aimed
to create a consistent plan with regards to the inputs and outputs of
various industries. For example, the input requirement of steel
consuming industries ought not to exceed steel production targets. In a
balanced plan the input requirements for steel would match the
production of steel. But a balanced plan is not necessarily an optimal
one. There can well be several consistent plans of which some lead to
higher overall production output than others. Kantorovich observed that
productive resources were often not used where they could yield the
greatest benefit. By using linear programming, planners could in
principle calculate a plan that made the best use of economic resources
and maximized production output.

One of the problems that needed to be overcome by Kantorovich was that
optimization always aims to optimize a singular objective function.
However, there was no obvious way of measuring the output of
qualitatively distinct products on a single scale. Without prior
valuation of the products (for example through market prices) it is not
clear whether 3 tanks and 10 trucks should be counted as more than 4
tanks and 8 trucks. Kantorovich circumvented this problem by assuming
that outputs ought to be produced at given proportions. For example, it
might be specified that 2 trucks ought to be produced for every tank.
Linear programming can then be used to calculate the plan that maximizes
output at these proportions. Unlike most contemporary economic
applications of linear programming, this does not depend on a monetary
objective function. So, what's being maximized is not monetary value.
Instead, the objective function measures purely physical quantities
(such as number of trucks or tons of steel).

In the context of economic planning, constraints are used to represent
limits to available economic resources (such as fertile land). A plan
that uses more resources than are available will not be feasible and
must thus be excluded. Constraints can also be used to fix the
proportions at which distinct outputs ought to be produced
[@Dapprich2022]. While it was first developed for economic planning, the
fundamental principles of linear programming can also be applied to
other problems (for example in biology).
:::

### Optimization problems for metabolic fluxes

In the previous chapter, we described how *linear* homogeneous and
inhomogeneous constraints arising from biological and physical knowledge
can be combined into matrix and vector notation and written in the
general form presented in Equations
[\[CBM:mass\]](#CBM:mass){reference-type="eqref" reference="CBM:mass"}
and [\[CBM:inhomogeneous\]](#CBM:inhomogeneous){reference-type="eqref"
reference="CBM:inhomogeneous"}. The resulting space of all flux vectors
$\fluxv$ satisfying these constraints is called the flux polyhedron. The
flux polyhedron can remain high-dimensional and, as explained above, an
objective function $f$ can be used to narrow down the set of flux
vectors to only those that are optimal (i.e., maximize the objective
function). The general form in which we can write the resulting
constraint-based optimization problem is therefore: $$\begin{equation}
    \max_{\fluxv} f(\fluxv), \; \text{such that} \;
    \mathmatrixfont{A} ~\fluxv \geq \mathvectorfont{b},
    \label{FLX:eq:generaloptproblem}
\end{equation}$$ with $$\begin{equation}
    \mathmatrixfont{A} = \begin{pmatrix} \Stoichmatint  \\ - \Stoichmatint  \\ \mathmatrixfont{I}  \\ \mathmatrixfont{G}  \end{pmatrix} , \quad \mathvectorfont{b} = \begin{pmatrix} \mathvectorfont{0}  \\  \mathvectorfont{0}  \\ \mathvectorfont{0}  \\ \mathvectorfont{h}  \end{pmatrix}.
    \label{FLX:eq:generaloptproblem2}
\end{equation}$$ Recall that $\Stoichmatint \fluxv = \vec{0}$ models the
steady-state assumption, while the multiplication with the identity
matrix ($\mat I_{n\times n} \fluxv \geq \vec{0}$) captures the fact that
we forced all reactions to be irreversible by splitting reversible
reactions into a forward and a backward reaction. Finally,
$\mat G \fluxv \geq \vec{h}$ can be used to impose additional
'inhomogeneous' constraints that can be used to input additional
biological knowledge such as an experimentally measured upper bound on
the uptake rate of a certain nutrient.

In many cases, the objective function is chosen to be a linear function
of the fluxes, i.e., $$\begin{equation}
    f(\fluxv) = \sum_i c_i \fluxi,
\label{eq:linearobjective}
\end{equation}$$ where coefficients $c_i$ weigh the relevance of the
different reaction rates in the objective function. Problems of the form
[\[FLX:eq:generaloptproblem\]](#FLX:eq:generaloptproblem){reference-type="eqref"
reference="FLX:eq:generaloptproblem"},
[\[FLX:eq:generaloptproblem2\]](#FLX:eq:generaloptproblem2){reference-type="eqref"
reference="FLX:eq:generaloptproblem2"}, and
[\[eq:linearobjective\]](#eq:linearobjective){reference-type="eqref"
reference="eq:linearobjective"} in general are called *linear
programming problems* and as the name suggests can be solved using
*linear programming*. Applied to metabolic models, linear programming is
called *Flux Balance Analysis* (FBA). Linear programming problems are
well studied, such that FBA is perhaps the most popular approach to
genome-scale metabolic models [@fang2020reconstructing; @cuevas2016dna].
FBA problems are relatively easy to solve using specialized optimization
software, which have been highly developed due to the general
applicability of linear programming in economics, logistics, and many
other fields also. In the following subsections we will briefly describe
various choices that can be made for the linear objective function
$f(\fluxv)$ in FBA.

As an example FBA problem, in Figure
[1.1](#FLX:fig:NetworkWithBM){reference-type="ref"
reference="FLX:fig:NetworkWithBM"} we have extended the minimal example
from the previous chapter to include ATP and biomass ($X$) production,
assuming the latter is produced from pyruvate using a single reaction
that consumes $\stoich_X$ molecules of ATP with flux value $\flux_X$. We
also introduce as a linear objective function the total rate of ATP
production, $\flux{ATP}$. Since in this example, reactions $\flux_1$ and
$\flux_3$ produce ATP with stoichiometric coefficients $\stoich_1$ and
$\stoich_3$, respectively, the total rate of ATP production is given by
$\flux_{ATP} = \stoich_1 \flux_1 + \stoich_3 \flux_3-\stoich_X \flux_X$.
The FBA problem is then given by simply maximizing $\flux_{ATP}$ subject
to $\flux_0,\flux_{O_2},\flux_1,\flux_2,\flux_3,\flux_4,\flux_X$
satisfying the mass-balance constraints but, as we will see in the next
subsection, this would result in a problem that is unbounded: the flux
vectors and resulting optimal value of $\flux_{ATP}$ could be
indefinitely large. Biologically, this is because there are no bounds on
the uptake rates of glucose $v^{ub}_0$ and the fermentation product
$\flux_4^{ub}$. Thus, if we re-impose these bounds as in the last
chapter, the result is an FBA problem that is bounded and therefore has
a finite objective value: $$\begin{equation}
    \begin{split}
    & \max_{\fluxv}\; \flux_{ATP} = \stoich_1 \flux_1 + \stoich_3 \flux_3 - \stoich_X \flux_X, \quad \text{such that}:\\
    &0 =\flux_0 - \flux_1,\\  
    &0 =\flux_{O_2} - \flux_3,\\  
    &0 = 2~\flux_1 - \flux_2 - \flux_3 + \flux_4 - \flux_X,\\
    &\flux^{ub}_0   \geq \flux_0, \\
    &\flux^{ub}_4   \geq \flux_4, \\
    &\flux_0, \flux_1, \flux_2 , \flux_3 , \flux_4 \geq 0 .
    \end{split}
\end{equation}$$

<figure id="FLX:fig:NetworkWithBM" data-latex-placement="t!">
<div class="center">
<p> <br />
<embed src="./images/FLX_NetworkWithBM.pdf" /></p>
</div>
<figcaption> A simple representation of the metabolic reaction network
for central carbon metabolism – Extracellular glucose is imported into
the cell via a reaction with flux <span
class="math inline">\(\flux_0\)</span> and converted via intracellular
glucose, <span class="math inline">\(G\)</span>, to pyruvate, <span
class="math inline">\(P\)</span>, via the reaction with flux <span
class="math inline">\(\flux_1\)</span> that has a stoichiometric
coefficient of two pyruvate molecules to each glucose molecule. Pyruvate
can then either be converted to a fermentation product, <span
class="math inline">\(P_1\)</span>, via the reaction with flux <span
class="math inline">\(\flux_2\)</span> or, in the presence of oxygen,
<span class="math inline">\(O_2\)</span> imported via <span
class="math inline">\(\flux_{O_2}\)</span>, converted to an oxidative
phosphorylation (OXPHOS) terminal product <span
class="math inline">\(P_2\)</span> via the reaction with flux <span
class="math inline">\(\flux_3\)</span>. It can also be converted to
biomass <span class="math inline">\(X\)</span> with rate <span
class="math inline">\(\flux_X\)</span>. The reactions with flux values
<span class="math inline">\(\flux_1\)</span> and <span
class="math inline">\(\flux_3\)</span> produce ATP from ADP (in red)
with stoichiometry <span class="math inline">\(\stoich_1\)</span> and
<span class="math inline">\(\stoich_3\)</span>, respectively, which can
vary between species. The production of 1.0 grams of new cells, in a dry
weight basis, requires one molecule of pyruvate and <span
class="math inline">\(\stoich_X\)</span> molecules of ATP.</figcaption>
</figure>

To illustrate a particular instance of this FBA problem, we consider the
very simple case where $\flux_4^{ub} = 0$, $\flux_0^{ub} > 0$ and
$\stoich_3 = \stoich_1 = 1$. It can be checked by hand that an optimal
solution is given by $\flux_0 = \flux_1 = \flux_2/2 = \flux^{ub}_0$,
with $\flux_2 = \flux_4 = \flux_X=0$. The optimal objective value is
given by $\flux_{ATP} = 3 \flux^{ub}_0$.

## Choice of objective functions in Flux Balance Analysis

Solving the constraint-based optimization problem of
[\[FLX:eq:generaloptproblem\]](#FLX:eq:generaloptproblem){reference-type="eqref"
reference="FLX:eq:generaloptproblem"} will reduce the set of flux
vectors to those that are optimal (maximize the objective function), but
the biological validity of this prediction is critically dependent on
the particular choice of $f$. Consequently, there has been a lot of
consideration and debate among researchers working on FBA about the
appropriate objective functions to use in different contexts and how
best interpret the results. Below, we will provide some popular
examples, but for a more systematic comparison of different objective
functions we refer the reader to
[@SchuetzKuepfer2007; @KnorrJain2007; @GarciaSanchezTorresSaez2014].

##### Evolutionary justifications for objective functions: the rate of biomass production

Objective functions are often based on evolutionary arguments: the
objective is chosen to capture some proxy for the evolutionary fitness
of an organism. The motivation behind this is that cells with a
metabolic state that scores well on this fitness-proxy would come to
dominate the cell-population because they outgrow their competitors.
Proxies for fitness are in principle very hard to choose since
evolutionary fitness is mostly related to the average net reproduction
rate of a cell over a very long time[@Bruggeman2020]. Therefore, to know
the metabolic objective that aligns with the maximization of fitness
would require us to know what the cell has been selected for in its
evolutionary history. This is a non-trivial question, for example, is an
*E. coli* cell growing in the human gut selected for the same metabolic
objective as a muscle cell in your body?

An objective that is used very often is the maximization of a biomass
production rate, because this is used as a proxy for maximizing growth
rate. It is indeed arguable that unicellular organisms with high growth
rates are selected, since in stationary conditions these cells will come
to dominate the population. Indeed, FBA models in which the biomass
production rate is optimized seem to predict metabolic states reasonably
well [@ibarra2002; @lewis2010omic; @Harcombe2013].

But what exactly do we mean by "biomass"? This is extensively discussed
in the Chapter , but for our purposes it is sufficient to say that it is
the entirety of all components that constitute a new cell. In metabolic
models, however, "biomass" refers to all precursors that are outputs of
the model and that are needed to produce a new cell. This has two
consequences. First, biomass in our model does not only consist of the
components of which the cell is built, but also of components needed to
do the building itself, such as a certain amount of ATP. Second, what is
contained in biomass will depend on where we draw a line around the
metabolic network - all necessary cell components that are not inside
are regarded as biomass. In practice, biomass appears in metabolic
networks in the form of a virtual *biomass reaction* that consumes all
necessary precursor molecules in the right proportions and produces one
unit of "standard biomass". Maximizing the biomass production rate thus
takes the very simple form of just maximizing the rate through the
biomass reaction.

The use of such a fixed biomass reaction represents an important
assumption, because in reality the biomass composition will be condition
dependent. For example, if a cell grows faster and contains more
ribosomes, this increases the cellular fraction of proteins and
polynucleotides, and hence the need for the respective precursors (amino
acids and nucleotides). Moreover, biomass composition can even depend on
the choice of metabolic strategy. If a pathway includes enzymes that
contain a lot of iron, then depending on the flux solution (which uses
this pathway or not), more or less iron will be contained in the
biomass. So, the flux solution must be known to know the biomass
composition, but the biomass composition must also be known to get to a
flux solution. To resolve this, we would need a model of the entire
cell, including the synthesis reactions of all enzymes. Such models will
be discussed later, in the Chapter on large cell models.

##### Evolutionary justifications for objective functions: alternative fitness-proxies

In some cases, modeling the maximization of the instantaneous growth
rate through the biomass reaction is an unrealistic proxy of the
evolutionary fitness. For example, in multicellular organisms each cell
performs a task that contributes to the fitness of the whole organism,
but this is not related to the reproduction rate of the individual
cells. In those cases, we may still try to capture an evolutionary
objective when we know the main task of the cell-type. For example,
beta-cells in the pancreas have as their main task to produce insulin,
and we may thus model their metabolism by maximizing the production of
insulin.

In other cases, our metabolic model is focused only on a very small part
of the true metabolic network, and therefore does not model the
production of all biomass precursors. In such cases, energy production
rate in the form of ATP production rate is often maximized. Yet other
objective functions that are sometimes used and have a (somewhat vague)
evolutionary motivation are the minimization of overall ATP usage and
the minimization of overall fluxes.

##### Synthetic design-oriented objective functions

Metabolic modeling can also be used to identify metabolic states that
lead to a certain desired behavior of a microorganism. For example, we
may seek to genetically perturb a microbe such that it produces a
certain compound of industrial or medicinal interest, while it also
retains a certain minimal growth rate [@KampKlamt2017]. Indeed, it is
often desired to retain a certain minimal ability to grow such that the
genetically engineered organisms can be lab-grown after which the
produced compound of interest can be harvested. In that case, we can
combine maximizing the production rate of the compound while imposing an
inhomogeneous constraint that sets a lower bound on the biomass
production rate. This can even be combined with a calculation in which
we solely maximize the biomass production rate: maximizing the biomass
production rate is a model for the wild-type cell, whereas maximizing
the generation of the compound models the desired phenotype. By
comparing the flux distributions between these 'strains', we can search
for target genes that should be up- or downregulated.

## Enzyme-constrained FBA

In its most simple form, flux balance analysis requires a stoichiometric
matrix, an objective function, and at least one flux constraint to
ensure that the problem is bounded. Solving an FBA problem allows for
the prediction of intracellular fluxes and essential gene knockouts,
given measured uptake and secretion rates.

However, whilst classical FBA can capture the effects of essential gene
knockouts well, it falls down when it comes to non-lethal knockdowns,
and the prediction of growth phenotypes. For example, overflow
metabolism in *E. coli*, and similarly the Crabtree and Warburg effects
in *S. cerevisiae* and cancer cells respectively, cannot be captured in
FBA models without ad-hoc flux constraints being imposed. These names
refer to the seemingly wasteful strategy of cells at high growth rates
using a combination of respiration and fermentation, despite the higher
ATP-yield of respiration.

It has been proposed that overflow metabolism results from optimal
protein allocation in the
cell [@basan2015overflow; @bruggeman2020searching]. In FBA models, we
capture this by imposing total proteome constraints to perform
enzyme-constrained flux balance analysis (ecFBA). The usual formulation
for ecFBA can be written as follows [@sanchez2017improving]:
$$\begin{equation}
 \label{eq:ecFBA}
    \begin{split}
        \max_{\fluxv,\mathbf{e}} & \; \; \flux_r \\
        \text{s.t. }\; & \textsf{(C1)} \; \; \Stoichmat~\fluxv = 0 , \\
        &\textsf{(C2)} \; \;\flux_i \ge 0 \forall i , \\
        &\textsf{(C3)} \; \;\flux_i \leq  k_i^{\text{cat}} \cdot e_{i} \; \; \forall i \in R \\ 
        &\textsf{(C4)} \; \;\sum_{i \in R_k} e_{i} \leq E_{k} \; \; \forall k \in [1,\dots,K]
    \end{split}
\end{equation}$$ Here, we wish to maximise flux through the objective
reaction $\flux_r$, subject to four conditions. The matrix $\Stoichmat$
is our stoichiometric matrix, with all reversible reactions split into a
forward and a reverse reaction, and the condition [C2]{.sans-serif}
ensures that all fluxes are positive. In this formulation, we give all
metabolic reactions an associated catalysing enzyme, and stipulate that
the flux through a reaction is equal to the concentration of this enzyme
multiplied by the apparent turnover number ($k^{\text{cat}}$) value
[(C3)]{.sans-serif}. Finally, we constrain total proteome constraints,
in the form of enzyme pools. The total concentration of enzymes in the
$k$-th enzyme pool must not exceed the constraint $E_k$
[(C4)]{.sans-serif}.

Predictions using ecFBA do not rely on the input of flux constraints,
but rather good estimates for the total protein in different cellular
compartments (for example the membrane and the cytosol), as well as the
$k_{\text{cat}}$-values (for details, see Chapter ).

The ecFBA formulation ensures that all metabolic enzymes have an
associated cost, relative to the gene product molar mass and turnover
number. A simplified technique to provide a proxy for these costs is
parsimonious flux balance analysis (pFBA). Central to pFBA is the
assumption that cells minimize their total enzyme usage. Here, an
optimal objective value is calculated via standard FBA, and the sum of
the gene-associated reaction fluxes is then minimized. pFBA
significantly reduces flux variability compared to standard FBA, but
still does not typically capture overflow metabolism [@yeo2020enzyme].

### Optimal metabolism in terms of elementary flux modes

In the previous chapter we introduced elementary flux modes (EFMs) and
identified them as the fundamental metabolic pathways that carry flux
through the metabolic reaction network. Here, we will show how
elementary flux modes also can be very useful for describing optimal
metabolic states. We briefly recapitulate the notion of elementary flux
modes. All metabolic flux vectors $\fluxv$ that satisfy both the
mass-balance and irreversibility constraints form a pointed polyhedral
cone, called the flux cone. The EFMs are the extreme rays of this cone,
so that they can be used to decompose all steady-state flux vectors
$$\fluxv = \sum_i \lambda_i ~\enzconcv_i,$$ where $\enzconcv_i$ is the
$i$-th EFM and $\lambda_i \geq 0$ its coefficient in $\fluxv$. Moreover,
the EFMs turn out to be the minimal metabolic subnetworks that a cell
can use in steady-state without needing any other reaction, so that we
can view EFMs as minimal metabolic strategies.

In Figure [1.2](#FLX:fig:FluxConeTwoConstraints){reference-type="ref"
reference="FLX:fig:FluxConeTwoConstraints"} we depict the EFMs as black
lines, and the region in-between these lines is the steady-state
solution space that is spanned by the EFMs. Note that this illustration
is great simplification, usually the flux cone is a high-dimensional
object that can only be visualized in trivial toy examples. In fact, the
flux cone is a subspace of $\Real^n$ where $n$ (the number of reactions)
can be in the thousands for a typical genome-scale metabolic network.
Moreover, the number of extreme rays of the cone would be overwhelming,
due to the complexity issues associated with EFM enumeration as
described in the previous chapter.

<figure id="FLX:fig:FluxConeTwoConstraints" data-latex-placement="t!">
<div class="center">
<embed src="./images/FLX_FluxConeTwoConstraints.pdf" />
</div>
<figcaption>We show a cartoon of the solution space of a metabolic
network, the so-called flux cone, with respectively (A) zero, (B) one
and (C) two constraints. With one constraint, the optimal solution for
any linear objective can be attained in a vertex of the space, which
means that it can be attained in a single EFM. With two constraints, we
need to combine at most two EFMs to describe the optimal
solution.</figcaption>
</figure>

Figure [1.2](#FLX:fig:FluxConeTwoConstraints){reference-type="ref"
reference="FLX:fig:FluxConeTwoConstraints"}**a** also shows that there
is a direction in which the objective increases fastest. This direction
is determined by the choice of objective function, to be specific: the
direction of maximal increase of the objective is given by the vector of
coefficients, $[ c_1 \cdots c_n]\trans$, appearing in the linear
objective function
[\[eq:linearobjective\]](#eq:linearobjective){reference-type="eqref"
reference="eq:linearobjective"}. However, as long as we do not impose an
inhomogeneous constraint, the flux cone is unbounded, so that we can
usually reach infinite values. This makes sense when we think of the
metabolic states in terms of elementary flux modes: when we have an EFM
that reaches some nonzero objective value, we can always multiply it by
any positive scalar. This multiplication will increase the objective
value, while the steady-state and irreversibility constraints will not
be affected.

Metabolism, however, is never unconstrained, so we will always have at
least one inhomogeneous constraint. In the previous chapter,
inhomogeneous constraint were written in the general form
$$\begin{equation}
\label{inhomogeneous}
    \sum_{i} \enzymeprice^p_i \flux_i \leq h_p, \quad p=1,\ldots P  
\end{equation}$$ where each $h_p$ corresponds to a component of the
$P$-dimensional vector $\mathvectorfont{h}$ and $n$ weights $w^p_i$
$(i=1,\ldots,n)$ are supplied for each of the $P$ constraints. The
second panel of Figure
[1.2](#FLX:fig:FluxConeTwoConstraints){reference-type="ref"
reference="FLX:fig:FluxConeTwoConstraints"} shows how a single
inhomogeneous constraint (i.e. the case $P=1$) can constrain the flux
cone and theory dictates an optimal flux vector is found at a vertex of
the resulting flux polyhedron, which geometrically corresponds to the
intersection of the flux cone and the hyperplane of the inhomogeneous
constraint. One particular biological argument for such a constraint is
related to resource allocation[@Berkhout2013; @chen2021proteome]: only a
limited number of macromolecules (proteins, ribosomes, etc) fit inside a
cell. Since these molecules catalyze reactions, reaction rates are
proportional to their concentrations: $$\begin{equation}
\flux_i = \enzconc_i ~\krate_i(\metconcv),
\end{equation}$$ where $\enzconc_i$ is the concentration of the enzyme
that catalyzes reaction $i$, and $\krate_i(\metconcv)$ is a function
that describes enzyme kinetics in a non-linear way that is for most
reactions unknown. The resource-allocation constraint then takes the
form $$\begin{equation}
    \sum_i \enzymeprice_i ~\enzconc_i \leq 1,
\end{equation}$$ where $\enzymeprice_i$ are weights that determine how
much of the resources are taken up by one unit of the $i$th enzyme;
these weights can for example be proportional to the volume, the mass,
or the number of amino acids of the enzyme. Making a change of variables
to express the constraint in terms of fluxes gives: $$\begin{equation}
    \sum_i \frac{\enzymeprice_i}{\krate_i} \flux_i \leq 1,
\end{equation}$$ such that these resource-allocation constraints again
fit the form presented in Equation
[\[inhomogeneous\]](#inhomogeneous){reference-type="eqref"
reference="inhomogeneous"}. A well-known example of a modeling framework
that uses such a constraint is *FBA with macromolecular crowding*
(FBAwMC, [@beg2007intracellular]) where such a constraint arises due to
a physical limitation on the number of enzymes contained within the
cell.

It is not necessarily always the case that an inhomogenous constraint
applies to all EFMs. For example, in a metabolic model of an organism
able to grow on multiple carbon sources, many EFMs may remain unbounded.
For treatment of these cases, the reader is referred to
[@deGrootBoxtel2019]. Moreover, we may have multiple inhomogenous
constraints on flux values as Equation
[\[inhomogeneous\]](#inhomogeneous){reference-type="eqref"
reference="inhomogeneous"} suggests. The third panel of Figure
[1.2](#FLX:fig:FluxConeTwoConstraints){reference-type="ref"
reference="FLX:fig:FluxConeTwoConstraints"} illustrates how a second
inhomogenous constraint can further constrain the solution space where
theory implies an optimal flux vector is found on a vertex lying on the
edge between two EFMs (as shown in the example in the figure). Imposing
additional inhomogenous constraints can therefore lead to the
superposition of additional EFMs in the solution. In general, if we
consider a constraint-based model with $K$ inhomogeneous constraints it
can be proved that an optimal flux vector will be built out of at most
$K$ EFMs [@deGrootBoxtel2019]. We therefore see another important
property of EFMs: not only do they form the minimal building blocks that
span all metabolic capabilities of the cell, they are also optimal
building blocks. When metabolism is optimized, only few of these EFMs
are used. As a result, solutions to linear constraint-based
optimizations can usually be rationalized in terms of the properties of
the available EFMs [@vanPeltKleinJan2021], for example, a flux balance
analysis with only one constraint on a nutrient uptake will just return
the EFM with the highest 'yield', i.e. the highest efficiency of making
biomass per nutrient.

## Multi-objective flux analysis and flux variability

### Phenotypic phase plane analysis

The analysis of the metabolic response to environmental changes is often
sought assuming that there is only one substrate limiting growth (or
other metabolic reaction). For example, we could be interested in the
growth and ethanol production by *S. cerevisiae* under oxygen limitation
in a chemostat. In this experimental setup, every other substrate should
be provided in excess, including the carbon and energy source. If no
oxygen is supplied, ATP must be produced only using oxidative
phosphorylation reactions and a fermentation product, such as ethanol,
will be produced. On the other extreme, if enough oxygen is available, a
fraction of the carbon source will be completely oxidized, producing ATP
via respiration. In both cases, the fraction of the carbon and energy
source not used for energy generation will be used for the production of
biomass at an specific growth rate equal to the dilution rate of the
chemostat.

This behavior can be analyzed using the phenotypic phase plane analysis.
To calculate a phenotypic phase plane (PPhP), the uptake fluxes values
under analysis, typically the uptakes of oxygen and the carbon source
are discretized between their upper and lower values and used to
construct a meshgrid containing the 2-D grid coordinates based on the
coordinates contained in the discretized vectors of oxygen and carbon
uptake fluxes. At each tuple in the 2-D grid, an FBA problem is solved
after fixing the lower and upper bounds of the corresponding fluxes to
the values in the tuple. Figure
[1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}. A shows the PPhP of the
metabolic network presented in Figure
[1.1](#FLX:fig:NetworkWithBM){reference-type="ref"
reference="FLX:fig:NetworkWithBM"} with $\stoich_X = 10$,
$\stoich_1 = 1$, $\stoich_3 = 4$, $\flux_4 = 0$, $\flux_0^{ub} = 10$,
and $\flux_{O_2}^{ub} = 15$ $\si{\milli\mol\per\gram\per\hour}$ (cell
dry mass).

<figure id="FLX:fig:PhenotypicPhasePlanes" data-latex-placement="t!">
<div class="center">

</div>
<figcaption>Phenotypic phase plane of the metabolic model shown in
Figure <a href="#FLX:fig:NetworkWithBM" data-reference-type="ref"
data-reference="FLX:fig:NetworkWithBM">1.1</a>, calculated as a function
of the uptake rates of oxygen and glucose. </figcaption>
</figure>

At zero oxygen uptake, Figure
[1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}.A shows that growth is
possible reaching a specific growth rate of 1 $\si{1\per\hour}$ at the
maximum glucose uptake. Notice that the slope of the line connecting the
origin of coordinates and the point of the highest growth rate at a
glucose uptake of 10 $\si{\milli\mol\per\gram\per\hour}$ (cell dry mass)
is 0.1 $\si{\gram\per\milli\mol}$ (cell dry mass). Biologically, this
slope corresponds to the biomass yield on glucose under anaerobic
conditions, and in terms of linear programming to the negative of the
shadow price defined as: $$\begin{equation}
    \gamma_i = \dfrac{-\mathrm{d}z}{\mathrm{d}b_i^v},
\end{equation}$$ where $z$ is the objective function optimal value
(specific growth rate in this case) and $b_i^v$ corresponds to the
violation of a mass balance constraint and is equivalent to the uptake
reaction of the $i$-th metabolite (glucose in this
example)[@Edwards2002]. Figure
[1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}.C shows that the glucose
shadow price is equal to -0.1 at every point in the feasible region of
the problem. Figure
[1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}.D shows the shadow price
values for oxygen uptake. For every unit increase in the oxygen uptake
flux, the biomass specific growth rate increases by 0.4
$\si{1\per\hour}$. Thus, the plane of increasing growth rate values in
Figure [1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}.A can be described by the
equation $0.1\flux_G + 0.4\flux_{O_2}$. Concomitantly, as the oxygen
uptake increases, the flux of product P1 decreases as more ATP is
generated in reaction $\flux_3$. For every constant glucose uptake flux,
the specific growth rate increases and the production of P1 decreases
until the optimally line (red line) is reached in Figure
[1.3](#FLX:fig:PhenotypicPhasePlanes){reference-type="ref"
reference="FLX:fig:PhenotypicPhasePlanes"}.A. This line represents the
optimal relation between the two metabolic fluxes in the PhPP
[@Edwards2002]. In this example, the optimally line represents the
combinations of glucose and oxygen uptake fluxes leading to a complete
oxidation of the substrate, and thus supporting the maximal biomass
yield. Finally, increasing the oxygen consumption beyond the optimally
line, at a constant glucose uptake, leads to an infeasible problem since
there is no further glucose to be oxidized.

### Non-uniqueness of optimal metabolic states: possible reasons

Although the optimization of some objective function strongly reduces
the number of solutions, it is still possible that many different
metabolic states satisfy the constraints *and* reach the same maximal
value for the objective. In that case, we are again undecided on which
of the solutions gives the most useful information about the biological
problem. This non-uniqueness of the optimum can be explained in terms of
the elementary flux modes. In the second panel of Figure
[1.2](#FLX:fig:FluxConeTwoConstraints){reference-type="ref"
reference="FLX:fig:FluxConeTwoConstraints"} we saw that the optimal
solution was located on the vertex that was as far as possible in the
optimization direction. One can imagine, however, that the flux cone can
be located in the space such that there are two vertices that both reach
out equally far into that direction. In that case, the two corresponding
elementary flux modes perform equally well, and consequently, all convex
combinations of these elementary flux modes also reach the same
objective value. In metabolic modeling we often work in a
high-dimensional space with constraints that concern only few of those
dimensions (for example a bound only on a nutrient uptake rate). In such
cases it is very likely that many elementary flux modes perform equally
well, so that there is a whole subspace of equivalent solutions.

### Flux Variability Analysis

The equality and inequality constraints of the FBA problem form a
polytope where the problem is feasible, a cone if the problem is written
in canonical form. The optimal solutions of the LP problem can lay on a
vertex of the polytope, and be unique, or be non-unique solutions if the
objective function hyperplane is parallel to a facet of the constraint
polytope at the solution. This means that one or several variables can
change their values without affecting the value of the objective
function. These variables can be identified using flux variability
analysis (FVA), where each flux of the reactions in the metabolic
network (the set of $J$ reactions with $N$ elements and $I$ metabolites)
maximized and minimized, one at a time, while fixing the value of the
objective function to a fraction of the optimal value obtained in the
original FBA problem.

$$\begin{equation}
    \begin{split}
    & \max_{\fluxv} \; \flux_{j} (\textrm{or} \min_{\fluxv} \flux_{j}), \quad \text{such that}:\\
    & \sum_{j \in J}N_{i,j}\flux_j=0,\,\,\forall i \in I,\\  
    &\flux_j^{lb}\leq \flux_j\leq \flux_j^{ub},\\
    &\flux_{biomass}=f\cdot \flux_{biomass}^*, \\
    &\flux_{j}\in \Real, \,\,\forall j \in J. \\
    \end{split}
\end{equation}$$

Hence, $2N$ optimization problems need to be solved if there are $N$
unconstrained fluxes. The results of the FVA analysis should be
carefully interpreted. Since the maximum and minimum fluxes are
calculated one at a time, and although changes in this flux might not
affect the objective function, this typically requires changes in the
remaining fluxes. Therefore, the polytope that describes all alternate
optimal solutions is not captured by FVA. Instead, FVA inscribes this
polytope in the smallest possible "box" [@Mahadevan2003]. Besides being
useful for the identification of alternative solutions, FVA can be
utilized to identify blocked reactions under a given growth condition.
These reactions are characterized by minimum and maximum flux values (as
calculated by FVA) equal to zero and arise due to regulatory constraints
imposed to the FBA or due to network gaps, for example, metabolites
lacking a consumption or production pathways for whom a steady-state
mass balance is impossible. Thus FVA, could help in the identification
of dead-end metabolites, and in the long run, in model improvement.

::: Philblock
When have we made a good model? Is the quality of a model determined by
whether it fits all experimental observations? What is the ideal size of
a model? Is the purpose of a model that it predicts, or rather that it
provides insight into the biological processes?

The answers to these questions are as common as it is unsatisfying: 'it
depends'. Sometimes a model can be very useful if it just predicts, and
does not explain, as witnessed by the undebatable success that machine
learning models have across the sciences. However, only true
understanding of the studied process can lead to hypotheses and
predictions on phenomena that are far away from the currently available
data. The more a model is fitted to a specific dataset, the less we are
able to extrapolate it beyond this dataset.

These questions are very relevant in the context of metabolic modeling.
Metabolic models have many unknown parameters, stemming from our
ignorance of the biological process: What is the true objective? What
constraints are relevant for determining metabolism? It is a deceptive
trap to view the success of the model in reproducing the observed data
as a validation that the right parameters, objective and constraints
were chosen. A successful model only indicates that the modeled
mechanism can be similar to the true biological mechanism, but it does
not show it actually is. The problem is that, since we have many
different parameters to choose from, many different models can explain
the same metabolic observations [@deGrootLischke2020].

An especially important question is whether metabolism is truly
optimized for some evolutionary function. It is now an attractive option
to view the success of optimization-based models as proof that the cells
are indeed optimized, but this would be wrong because we can also
explain the data with models that do not require optimization. To really
quantify whether metabolism is optimized we should therefore devise
quantitative tests that distinguish between randomly chosen and
optimized metabolic states. An interesting approach for describing the
metabolic outcome of cells, relying on statistical mechanics rather than
on a selected objective function, has already been introduced
[@deMartinoTkacik2018].
:::

## Concluding remarks

In this and the previous chapter, we have introduced constraint-based
analysis of genome-scale metabolic models. We started by pointing out
many of the simplifying assumptions that are associated with the study
of large metabolic reaction networks. For example, we only considered
systems in chemical steady state with their environment, we ignored the
effects of metabolite dilution, and we made semi-informed choices for
which intracellular molecules are contained in our model or summarized
in a biomass reaction. All these assumptions can be relaxed, at the cost
of making models more complex. Although it is tempting to think that the
more complex a model the more realistic it will be, there is not much
use to adding additional complexity if we don't have the data to support
it. Constraint-based analysis therefore provides one way to study
metabolism at genome-scale when data are limited. In the following
chapters we will study the consequences of lifting one or more of these
simplifying assumptions.

In constraint-based analysis, one considers reaction rates (fluxes) as
the variables in the model, giving the illusion that these are directly
set by the cell to regulate its metabolic state. In reality, however,
the reaction fluxes are the combined consequences of enzyme expression,
regulation and metabolite concentrations. If we wish to model metabolism
in more detail, we we should build models that incorporate gene
expression and metabolite concentrations systematically. Some of the
next chapters attempt this, but we have described that FBA is useful
when experimental data are limited. Certain extensions of FBA discussed
in later chapters also move beyond the steady state assumption, allowing
the environment to change with time. One example is the method dynamic
FBA, which will also be discussed in a later chapter.

In this chapter we built upon the exploration of flux spaces derived
from constraints by imposing optimality criteria in terms of an
objective function. The choice of the objective function(s) and the
constraints depend on the modeling purpose. We will summarize some of
the possible choices by listing three purposes that this type of models
can have.

First, constraint-based optimization can be used to collect, integrate
and extrapolate data on the metabolism of a specific organism. In this
case, as much experimental information as possible can be used to refine
the model. For example, measured fluxes can be fixed with constraints,
measured metabolite concentrations can be used to determine the
thermodynamically feasible direction of reactions, and transcriptome
information can be used to exclude some reactions because the
corresponding genes are not expressed. One of the applications is then
that unknown variables can be inferred such that they are in accordance
with the metabolic network and all the measured variables.

Second, hypotheses can be tested on why the studied organism attains its
metabolic state. By choosing an objective function we can propose what
*drives* the metabolic behavior and by choosing the constraints we
propose what *limits* the metabolic behavior. If the model is then in
accordance with the experimental observations, we know that at least the
hypotheses were not proven wrong. On the other hand, we must be careful
not to conclude from this that the hypotheses must be right, as we
discussed in the box with philosophical remarks.

Third, we may use these models to search for a metabolic state that
results in a certain desired behavior, for example in the secretion of a
product that is useful for industrial or medicinal reasons. In this
case, the objective function is picked such that exactly the desired
behavior is maximized, often while requiring that some biomass
production is still possible because the cells need to be able to grow
before the harvesting of the product can start.

Despite these useful purposes, we have also identified several
limitations of the FBA-type models that we described here, such as
ignoring metabolite concentrations, enzyme kinetics, and the assumption
of a stationary metabolic state. The reason that these models are still
very popular is their computational simplicity: as long as the objective
function and constraints are linear in the reaction rates, the optimal
solution is relatively easy to find using linear programming. This makes
it feasible to make and run these models on genome-scale metabolic
networks, which are networks that comprise all the metabolic enzymes for
which the genome encodes, and can include thousands of reactions.

Understanding the solutions of such large models can also be very
difficult due to their dimensionality. This is made easier when one uses
elementary flux modes: we have seen that a solution is always a
combination of a relatively small number of EFMs. More precisely, the
number of EFMs that are active in the optimal solution cannot exceed the
number of imposed constraints. This means that to understand the
solution, we only need to understand which EFMs are selected and why. As
such, we can interpret optimal solutions in terms of the EFMs, i.e. the
minimal metabolic strategies, that are used.

## Recommended readings and tools {#recommended-readings-and-tools .unnumbered}

##### Escher FBA

Escher FBA
([sbrg.github.io/escher-fba/](https://sbrg.github.io/escher-fba/)) is a
nicely illustrative tool for FBA on an *E. coli* core model. Bounds on
all reactions can be changed and different objectives can be explored.
The resulting flux distribution is shown graphically.

## Problems {#problems .unnumbered}

Computer exercises for this chapter can be found on the book website.

::: exercise
[]{#FLX:Exerc:FLX_Prob1 label="FLX:Exerc:FLX_Prob1"}

Augment the metabolic network of *Spirallus insilicus* (Problem
[\[CBM:Exerc:CBM_Prob1\]](#CBM:Exerc:CBM_Prob1){reference-type="ref"
reference="CBM:Exerc:CBM_Prob1"}) by adding the in-homogeneous
constraint $\flux_{upt}\leq 10 \si{\mmol\per\gram\per\hour}$ (cell dry
mass) and calculate the flux distribution if biomass is the objective
function (maximize $\flux_5$).

1.  Using a spreadsheet and its associated linear programming optimizer.

2.  Using an LP solver in Python such as `linprog` available in
    `scipy.optimize`.

3.  Is the flux distribution unique? Calculate the maximum and minimum
    values of each flux (except for the uptake of substrate and biomass
    production) if $\flux_5$ should be equal to its optimal value
    ($\flux_5^*$) and if this constraint is relaxed to
    $\flux_5\geq 0.9~\flux_5^*$.
:::

:::::: exercise
[]{#FLX:Exerc:FLX_Prob2 label="FLX:Exerc:FLX_Prob2"}

The metabolic network illustrated in Figure
[1.1](#tab:PPh_reactions){reference-type="ref"
reference="tab:PPh_reactions"}, adapted from [@Edwards2002], was
designed to include four phenotypes that can be reached depending on the
ratios of the oxygen and carbon source (A) uptake, defining zones of
single nutrient and dual nutrient limitation.

1.  If the uptake of the carbon source $A$ is bounded between $0$ and
    $10$ $\si{\mmol\per\gram\per\hour}$ and no restrictions on the
    oxygen uptake are imposed, prepare a plot showing the biomass, $C$,
    $D$ and $E$ fluxes attained at different uptakes of $A$.

2.  Repeat the preceding analysis, but limit the maximum uptake rate of
    oxygen to $10$ $\si{\mmol\per\gram\per\hour}$.

3.  If substrates uptakes are bounded between $0$ and $10$
    $\si{\mmol\per\gram\per\hour}$ for $A$ and $0$ and $20$
    $\si{\mmol\per\gram\per\hour}$ for oxygen, calculate the phenotype
    phase plane. In each region of the phase plane (defined by a
    different slope), pick a combination of $A$ and oxygen uptakes and
    analyze the fluxes of $C$, $D$ and $E$.

::::: minipage
:::: center
::: {#tab:PPh_reactions}
  --------------------------------------- -----------------------------------
  $\ce{->[q_{A}] A}$                      $\ce{ATP ->[R_{ft}]}$
  $\ce{A + ATP ->[R_{1}] B}$              $\ce{C + 10 ATP ->[R_z] Biomass}$
  $\ce{B ->[R_{2}] 2 ATP + 3 NADH + C}$   $\ce{->[q_{O_2}] O_2}$
  $\ce{0.2 C ->[R_3] 2 NADH}$             $\ce{C ->[C_{out}]}$
  $\ce{C ->[R_4] ATP + 3 D}$              $\ce{D ->[D_{out}]}$
  $\ce{C + 2 NADH ->[R_5] 3 E}$           $\ce{E ->[E_{out}]}$
  $\ce{NADH + O_2 ->[R_{Res}] 2 ATP}$     
  --------------------------------------- -----------------------------------

  : Stoichiometry of the metabolic network for problem
  [\[FLX:Exerc:FLX_Prob2\]](#FLX:Exerc:FLX_Prob2){reference-type="ref"
  reference="FLX:Exerc:FLX_Prob2"}. Adapted from [@Scott2018] after
  [@Edwards2002].
:::
::::
:::::

\
::::::
