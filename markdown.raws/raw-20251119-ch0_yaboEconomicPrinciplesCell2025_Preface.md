# Preface {#preface .unnumbered}

[]{#PRE label="PRE"}

How can a cell maintain itself as a living being? Living cells, shaped
by billions of years of evolution, have developed many ways to adapt to
their environment, for example, by regulation of gene expression. But
the rules of physics and chemistry enforce certain boundaries on what
cells can achieve and how they can allocate their own resources. Shaped
by evolution, cells "do certain things right", and computational models
of cells often assume that this \"doing something right\" can be
described by evoking optimality principles. The goal of this book is to
uncover some of these governing principles. Although biological
optimality is often contested for good reasons, theories based on
economic principles can explain many observations (about cell growth or
the usage of cellular resources) much better than purely mechanistic
models. Methods such as Flux Balance Analysis are well established, but
the idea of resource allocation is gaining ground, and metaphors like
\"currency metabolites\" or \"energy budget\" are common in cell
biology. Optimality principles are often applied ad hoc, and a coherent
picture in which many single observations or models would have their
place is still missing. This book - a free and open textbook to which
anyone is invited to contribute - gives an overview of established
approaches to \"cellular economics\", from descriptions of simple
metabolic systems to cell growth, variability, and dynamic behavior.

Compared to non-living matter, living organisms have some very specific
abilities. How can a tiny cell maintain itself, while a cloud fades
away? How can it grow and divide, how can it make copies of itself? Or
in other words, what does it take to be alive? There is no special "life
force"; what makes matter alive is its microscopic structure or
molecular organization. Living matter follows the laws of physics.
However, to understand life, physics alone is not enough! On the one
hand, living beings are complex at many levels of organization, from
biomolecules to cells, body, population, and ecosystem. Each of these
levels follows its own laws, but in some cases, a change on the lowest
level, a point mutation, may change the fate of a population. On the
other hand, living systems do not just exist as they are, but have been
shaped by billions of years of evolution. This is also why some of their
features look like they were perfectly engineered. Since we do not know
-- and certainly cannot always consider -- evolution in its entirety, we
often use \"optimality\" as a shortcut. To explain a biological feature,
like the shape of dolphins, we might tell all the story of dolphin
evolution and how changes in shape appeared and some were conserved. But
instead, we may simply say: this is the shape that functions best, and
apparently evolution, by mutation and selection, converged to this
shape.

In this book, we mostly focus on microbes, and how they function
internally: what compounds they need to produce, and how, in order to
live and self-replicate. We can describe this at three different levels.
Level 1, the 'inventory' of a cell, from a molecular point of view,
consists of molecules and biochemical reactions, which form a complex
chemical network. Level 2, the dynamics of molecule concentrations, is
determined by physical laws like the conservation of mass and by
specific biochemical regulation mechanisms, for example molecular
recognition. But there is also a third level, concerning the function
(or possibly optimality) of these dynamics, for which economic metaphors
are appropriate. Given a limited \"protein budget\", what biochemical
pathways should a cell prioritize to thrive, grow, and survive? In this
book, we focus on the third layer, the \"economy of the cell\", which,
in fact, encompasses the previous two.

<figure data-latex-placement="t!">
<div class="center">
<p><img src=".//images/sce_Nagaraj_cost_lv3.jpg" alt="image" /> <img
src=".//images/sce_Nagaraj_cost_lv5.jpg" alt="image" /></p>
</div>
<figcaption> Protein abundances in the yeast Saccharomyces cerevisiae.
Measured amounts of different sorts of proteins are shown as areas,
proteins of related functions are arranged into larger regions, shown by
colors. Why does the cell invest such a large fraction of their protein
budget into the glycolysis pathway? Such "economic" questions are
central in this book.</figcaption>
</figure>

What do we mean by the \"economy of the cell\"? Economic theory is, of
course, vast and only a small bit of it has made its way into biology so
far. In this book, by \"economy\" we mean primarily resource allocation
and scheduling problems: What is the best allocation of protein
resources in a bacterial cell (see the graphic above)? How should
photosynthetic bacteria adjust these investments during the day-night
cycle? Our answers to such questions, also in this book, are often based
on an underlying assumption of optimality. But often we simply consider
all the constraints under which a cell needs to act and figure out what
cellular behaviors are possible.

As we look at cells from the perspective of resource allocation, we will
neglect other aspects: we will rarely talk about regulation (e.g. the
mechanisms for regulation of gene expression), and even more rarely
about gene or protein sequences. Instead, we assume that certain
mechanisms are in place in the cell, and that molecules encoded by
sequences exist, and either ask why (that is, for what functional
reason) they are the way the are, or what the cell can do with them to
perform certain tasks. This often means that we assume a mechanistic
system with possible 'choices' (among flux profiles, expression levels,
enzyme parameters, etc.) and ask, first, what choices exist (considering
all the constraints) and, second, how profitable these choices are for
the cell (assuming certain objectives). While we are hardly concerned
with genetics, we are certainly interested in how optimality may arise
from evolution - to connect the two, we need to think about fitness (how
long-term fitness can be defined and how it gives rise to "momentary" or
"local" optimization objectives in a given part of the cell).

The source of inspiration for the book and the questions (discussions)
that motivated the investigation of the various mechanisms the cell uses
to allocate resources in the most efficient way possible were a series
of events in formal settings such as an annual summer workshop, the
monthly online Forum \"Economic principles in cell physiology\", and
more informal hackathons. The development of the book is an endeavor
that is truly global in scope, drawing on the expertise and integrating
the contributions of scientists located in more than a dozen countries
on three continents. Those who contributed to the creation of the book
recognize that the success they achieved in bringing it to a
satisfactory conclusion is due, in no small part, to the support of the
institutions with which they are affiliated and are grateful to INRAE,
the Learning Planet Institute Paris, and the home institutions of all
other authors (as well as the taxpayers who finance these institutions)
who encouraged the creation of the book by providing its authors and
contributors with the time and space necessary to sustain its
development and achieve its completion.

Finally, why did we choose to write this textbook as a collaborative,
open book? Publishing with a commercial publisher has several downsides,
most of which reflect a clash of interests between publishers, authors,
and readers. We wish to write this book as a community for the
community. Many colleagues were and are involved, and we would be glad
to welcome you as part of the team! If you would like to join for
writing, reviewing chapters, designing graphics, or discussing new
ideas, please have a look at our website and get in touch.
