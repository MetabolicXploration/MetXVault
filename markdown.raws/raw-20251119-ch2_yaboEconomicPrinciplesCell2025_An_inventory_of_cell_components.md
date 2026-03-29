# An inventory of cell components {#CEN}

::: chapterhighlights
- The main components of a cell are proteins, RNA, DNA, lipids and
  carbohydrates.

- The quantities of these components vary depending on the cell type and
  the cell's environment.

- These components are synthesized by enzymes and molecular machines
  such as ribosomes and DNA/RNA polymerases.

- There are many parallel processes happening in cells and they have to
  be coordinated.

- Cellular processes are constrained by factors like temperature,
  diffusion limits, and density.
:::

## Describing and counting cellular components {#CEN:Sec:Introduction}

Cells contain a diverse spectrum of molecules, needed to create two
cells out of one (as Rudolf Virchow proposed, *omnis cellula e cellula*,
all cells come from cells). These molecules come in different sizes and
properties and therefore create a demand for a cell to keep these
components in different places (*spatial* organization) with different
patterns of use (*temporal* organization), and book-keep their
quantities. Cell composition directly influences cell function: thus we
observe different cellular make-up in different organisms or even in
different cells of the same organism.

Historical research and the latest advances in instrumentation allow us
to characterize the constituents of cells in increasing depth. Today,
collections of such biological numbers, like
[BioNumbers](https://bionumbers.hms.harvard.edu/search.aspx)
[@MiloJorgensen2010], store thousands of values available at your
fingertips, a long way from scouting the numbers in original
publications. Specialized open databases, e.g. [Human Serum Metabolome
Database](https://serummetabolome.ca/) [@PsychogiosHau2011], bring
increasing amounts of measurement data available to the community.

Being able to operate basic biological numbers has multiple benefits
when thinking of the cellular economy. To name a couple, first, it
allows "back-of-envelope" calculations, where we aim to estimate the
plausible order of magnitude of a derived value, rather than the exact
value. This sort of thinking boosts interpretation of results
considerably, as it allows us to rule out unrealistic outcomes. Second,
computational models of cell growth (Chapter ) usually use numbers like
average cell size or protein mass as parameters. Consequently, the
choice of parameters has a direct influence on the quantitative
predictions. Last but not least, these simple calculations allow us to
establish relationships between different components of the cells - and
cells are nothing but heavily intertwined networks of molecules.

Counting molecules in a cell is as important to the cellular economy as
counting different sorts of fruits and vegetables in a warehouse -- and
is a key ingredient in the journey towards understanding of the
principles behind the cellular economy. As we unveil throughout the
book, it seems that cells can be treated as "little bookkeepers under
the microscope". Thus in this chapter, we will do a census of cellular
components: we will discuss what molecules make up a cell, what they are
derived from, how to measure these components in the lab, and we will
briefly consider allocation of resources, directed to synthesize
individual cellular components.

## The components of a cell

### Elemental composition of the cell {#CEN:Sec:cellComposition}

Although living matter comes in different shapes and sizes, over 99% of
the cellular mass can be described by only a handful of chemical
elements. 6 most abundant elements form the famous CHNOPS notation:
carbon (C), hydrogen (H), nitrogen (N), oxygen (O), phosphorus (P), and
sulfur (S). Taken together, these 6 elements encompass the vast majority
of the mass, namely, ca. 97.5% in budding yeast *Saccharomyces
cerevisiae* [@LangeHeijnen2001]. Living cells also contain minute
amounts of different metal ions, such as sodium (Na), potassium (K),
iron (Fe), molybdenum (Mo) and others -- usually facilitating signal
transduction or supporting enzymatic catalysis.

### Biological molecules {#CEN:Sec:biomolecules}

Although cells contain many different molecular *species* ("molecular
identities"), we can crudely categorize them into *small molecules* and
*macromolecules* based on their molecular weight and complexity. Small
molecules, as the name suggests, are small chemical compounds, up to
1000 Daltons in mass (1 Dalton = 1 atomic mass unit, 1 amu), and are
usually composed of a non-repeating single chemical unit (called
*monomer*). Macromolecules, on the contrary, are up to several
megadaltons (MDa = $10^6$ Da) in weight, and are frequently composed of
multiple monomers (forming so-called *polymers*). Compounds in the
cells, both macro- and small molecules, based on their chemical nature,
fall into 5 big groups: proteins, nucleic acids (both macromolecules),
carbohydrates (exist as both small molecules and polymers), lipids
(small molecules), and cofactors/other small molecules.

Proteins are polymers, composed of amino acids. Proteins are an
exceptionally diverse class of molecules: in Nature, 20 amino acids can
be incorporated into proteins (so-called *proteogenic* amino acids),
which, combinatorially provides 20 options for each position in the
protein chain. Therefore, there is an enormous amount of possible
combinations to make a protein of a length of 100 amino acids
($20^{100}$, to be precise), even for a amino acid chain way shorter
than the average in *E. coli*, around 325 amino acids
([BioNumbers](https://bionumbers.hms.harvard.edu/search.aspx) ID (BNID)
108986). This diversity gives rise to the spectrum of functions proteins
can do, for instance, catalysis (catalytic proteins are also called
*enzymes*), transport of molecules, keeping structural integrity of
membranes, and others. Also two notable properties of proteins are that
they (1) need to acquire a specific three-dimensional structure ("to
fold") in order to become functionally active, and (2) sometimes, they
also need to form complexes of the same or other proteins (called
*multimers*). Protein production is a major consumer of energy and
biosynthetic intermediates in the cell, therefore, in this book we will
frequently consider proteins as central players in implementing economic
principles in cell physiology.

Nucleic acids are another category of macromolecules; their monomers are
called nucleotides. There are two major classes of nucleic acids, RNA
(ribonucleic acid) and DNA (deoxyribonucleic acid). RNA and DNA
chemically have a slight, yet critical difference: the sugar, which is a
part of the nucleotides, differs between RNA (ribose) and DNA
(deoxyribose). The two sugars are almost the same but for one chemical
group: one of the carbon atoms in ribose is connected to two another
carbon atoms, a hydrogen atom, and a chemical group, called hydroxy-
($-OH$). In deoxyribose, the hydroxy-group is substituted with another
hydrogen atom, hence the prefix "deoxy-" ("minus oxygen"). RNA and DNA
have different functions in the cell: the primary function of DNA is to
store genetic information, while RNA can work both as an intermediate
agent to transfer that genetic information to protein production
(messenger RNA, mRNA) or to participate in catalysis and protein
production in general (e.g. transfer and ribosomal RNA, tRNA and rRNA,
respectively). Outside the polymers, nucleotides can also act as
energy-accumulating compounds (e.g. ATP, adenosine triphosphate) or
signaling molecules (e.g. cyclic adenosine monophosphate, cAMP). In this
text, we will mostly refer to the energy-storing function of the
nucleotides, although other functions, such as signaling, also are
essential aspects of describing cell physiology.

Carbohydrates are another major class of biological molecules, and are
important both as monomers and high molecular-weight polymers. Monomeric
carbohydrates (sometimes also referred to as simple sugars) are mainly
used as carbon and energy sources for organisms, e.g. glucose or
fructose. Oligosaccharides made up of two or three linked monomers can
also used as energy source and many of them are specific to certain
groups of organisms (e.g. melezitose, a trisaccharide found in insect
honeydew). In oligomeric form (up to 10 monomers), carbohydrate chains
are essential for cellular sensing systems: proteins can be "decorated"
with chains of carbohydrate monomers to be recognized by receptor
molecules on the surface of the cell. Finally, polymers of carbohydrates
usually serve as structural components (part of peptidoglycan, major
part of bacterial cell walls) or energy/carbon storage (glycogen in,
e.g. yeasts and animal cells, or starch in plants).

Lipids are a vaguely-described class of compounds, which have an
overarching similarity, being water-insoluble. The major function of
lipids in biological cells is structural: a very abundant subclass of
lipids, phospholipids, is an essential constitutent of biological
membranes. As discussed in
Section [1.2.1](#CEN:Sec:cellComposition){reference-type="ref"
reference="CEN:Sec:cellComposition"}, membranes themselves have a
variety of functions, which are mostly carried out by lipids
(structural) or proteins (transport, sensing, signaling etc.). Some
lipids can also undertake other functions, such as signaling (various
sterols), or energy storage (tryglycerides, or fats).

As we see, the metabolism of biological molecules is tightly
interlinked, although they exhibit major differences in their abundance,
size and chemical properties. Macromolecules are present in very low
concentrations, and their biosynthesis usually takes minutes. Meanwhile,
the time scale of small molecule reactions is usually seconds (or
fraction of), and the concentrations of small molecules are usually
several magnitudes higher than these of macromolecules. Yet, despite
acting at different rates and concentrations, these two types of
biological molecules work in an orchestrated manner. To begin with, a
number of different small molecules are required to produce both other
small molecules and the macromolecules. In return, the macromolecules
ensure cell integrity and growth by, among other functions, operating
the reaction networks of small molecule interconversions (which we
usually refer to as metabolism). Additionally, presence of some small
molecules can influence the function of macromolecules, both directly
(e.g. essential cofactors, needed for enzymatic reactions; enzyme
activation or inhibition), and indirectly (e.g. modulation of gene
expression, signaling). Therefore, a lot of different processes have to
happen in parallel to ensure the operation of the cells. Having defined
the major types of molecules we find in living cells, next we will
discuss how abundant are different components of the cells.

:::: Generalblock
An important consideration about both proteins and nucleic acids is that
they are polymerized by very specialized protein- and protein-nucleic
acid complexes. These molecular machines use energy (in terms of ATP
equivalents) to form chains of the respective monomers.

::: center
![image](.//images/CEN_ProtSyn.pdf){width="60%"}
:::

For proteins, amino acids (AA) are combined into a so-called *peptide
chain* in a process called translation, which is catalyzed by ribosomes
-- large complexes made from proteins and RNA. Nucleic acids (RNA and
DNA) are synthesized from nucleotides (NT) though a process called
transcription by enzyme complexes known as *nucleic acid polymerases*.
There are two major classes of them, RNA and DNA polymerases, each
specific to their respective nucleic acid.
::::

## Cell organization and size

In an extremely simplified way, cells can be looked at as bags of
fluid-like material, kept together by a membrane. These "bags of things"
can also contain other membrane structures inside them, forming
so-called organelles. In cell biology, we call cells *prokaryotic* if
they do not possess these membrane structures, and *eukaryotic* if they
do. The divide between prokaryotes and eukaryotes can be illustrated by
comparing two organisms: the prokaryotic bacterium *Escherichia coli*
and the eukaryotic yeast *Saccharomyces cerevisiae*. They both are
organisms, composed of a single cell (thus called *unicellular*), and
they both are very small, compared to a typical human cell. However,
*E. coli* does not contain any additional membrane structures except
from the plasma membrane (which encompasses the cellular contents).
Meanwhile, a handful of different organelles can be observed in
*S. cerevisiae*. The cellular organization of these cells is shown in
Figure [1.2](#CEN:fig:BioCellStruct){reference-type="ref"
reference="CEN:fig:BioCellStruct"}.

### Membrane-bound structures of the cell

Most biological membranes and membrane-based structures, including the
plasma membrane itself, have multiple functions (not only separating
space), and are highly dynamic. Some membranes can fold into very
compact structures with extremely high surface area (endoplasmic
reticulum, Golgi apparatus), occupy different volumes - from small
vesicles to large vacuoles, occupying a major fraction of the cell
volume. Moreover, some molecules can form very large structures, which
might be transient (short-lived), thus capturing and defining them
remains a major challenge. For these reasons, the fine structure of
cells is unclear - some findings (e.g. organelle contact sites, see
[@CohenValm2018] for a recent review) hint into some functional
organization of organelles, yet the canonical way to look at the
cellular structure remains as to a "bag of things".

A notable example of a highly specialized organelle is the
mitochondrion. The mitochondrion is separated from the rest of the cell
by two (outer and inner) membranes; this feature is essential for their
function. In eukaryotes, mitochondria are a major hub of metabolism:
they house essential biochemical pathways, such as tricarboxylic acid
cycle (also known as citric acid-, or Krebs cycle), as well as the
so-called *respiratory chain*, the machinery for generating energy with
the use of oxygen (see Chapter  for more details). While the most
biochemical interconversions happen inside the mitochondria (in
mitochondrial *matrix*), the respiratory chain proteins are located in
the inner mitochondrial membrane: these proteins create an
*electrochemical gradient* across this membrane, and use it to drive the
conversion of energy, stored in nutrients, into the energy the cell can
use (in a form of ATP). What makes mitochondria even more interesting is
that they also contain mitochondria-specific genetic information
(mitochondrial DNA), which is essential for mitochondria to function
inside the cell. In many organisms, the loss of mitochondrial DNA
results in impaired growth (in yeasts, that is called the *petite*
phenotype) [@CarlsonOsmond1981], and some organisms cannot grow unless
mitochondrial DNA is present (*petite-negative* yeasts).

### Cell size {#CEN:Sec:Size}

There is a remarkable variability of cell sizes in nature
(Figure [1.1](#CEN:fig:Sizes){reference-type="ref"
reference="CEN:fig:Sizes"}).
Figure [1.2](#CEN:fig:BioCellStruct){reference-type="ref"
reference="CEN:fig:BioCellStruct"} shows the typical sizes of bacterial,
yeast and mammalian cells, which range from 1 to 15 μm. However, we can
easily find more extreme values. For example, one of the largest cells
in the human body, the egg cell, is 100 μm in diameter (BNID 111184).
Bacteria are usually considered very small, in fact, the diameter of the
smallest known bacterium *Mycoplasma* is only 0.2 μm (BNID 104717).
Meanwhile, on the other side of the spectrum, the largest bacteria
*Thiomargarita magnifica* can reach up to 2 cm
[@VollandGonzalez-Rizzo2022] which is even more than most mammalian
cells. However, this giant bacteria looks very different from typical
bacteria like *E. coli* -- it has hundreds of thousands of genome copies
in organelle-like structures. There are exceptional cases where cells
can reach even bigger sizes. The largest known single-celled organism is
the alga *Caulerpa taxifolia*. It has many nuclei that are not separated
by a membrane and reaches up to one meter [@Jacobs1994]. Another special
case is a neuron -- its body has a small diameter (100 μm), but its
axons can extend to more than a meter (BNID 109548).

<figure id="CEN:fig:Sizes" data-latex-placement="b">
<div class="center">
<embed src=".//images/CEN_Sizes.pdf" style="width:90.0%" />
</div>
<figcaption>Variability of cell size across organisms</figcaption>
</figure>

For many organisms, cell size changes with environmental conditions. As
already mentioned in
Section [1.4.1](#CEN:Sec:variablity){reference-type="ref"
reference="CEN:Sec:variablity"}, the size of the cell varies with the
growth rate, and depends on how a particular growth rate is reached.
More than 60 years ago, Schaechter et al. discovered the nutrient growth
law -- cell volume increases exponentially with growth rate (as a result
of the nutrient availability in the medium) [@SchaechterMaaloe1958].
Since then, the correlation between cell size and growth rate was also
observed for other organisms
[@VadiaLevin2015; @AldeaJenkins2017; @SzeliovaRuckerbauer2020] (BNID
107948, 110191, 105103). However, when the growth rate is changed by
other means, for example by temperature, this relationship is not
observed [@SchaechterMaaloe1958; @BremerDennis2008].

### Variation of single-cell sizes and shapes

The relationships above refer to an average cell volume in the
population. However, at the single-cell level, size changes throughout
the cell cycle. Before cells divide, they essentially need to double
their size. Otherwise, they would get smaller and smaller with each
division. However, they also cannot grow too much, or the average cell
size would get bigger and bigger. There are various mechanisms of how
cells maintain a cell size homeostasis, and they are discussed in detail
in Chapter .

Aside from cell size, we need to consider the importance of cell shape.
Different cell types come in different shapes, such as spheres, ovals,
rods, or spirals. Differently shaped cells may have the same volume but
very different surface area and surface area to volume ratio (SA/V).
Spheres have the lowest possible SA/V while more complicated shapes have
higher SA/V. What happens to the shape when a cell changes its volume
(for example, in response to environmental conditions)? For many cells,
the shape remains roughly the same -- for example *E. coli* always looks
like a rod. As a result, SA/V decreases as cells get larger. On the
other hand, some cells vary their size and shape but maintain a constant
condition-specific SA/V [@HarrisTheriot2018].

The changing SA/V ratio can impact cell biology in various ways. For
example, it can change cell composition -- a larger membrane area
increases the lipid fraction of the cell. The SA/V ratio also affects
nutrient uptake. A bigger surface area allows faster nutrient uptake per
unit volume because more transporters can fit into the membrane.
Additionally, cell shape influences the rate at which molecules diffuse
from one end of the cell to another. Understanding these effects is
relevant for some modeling approaches, especially those that consider
membrane synthesis or diffusion.

## Cell composition in numbers

Throughout this book, we will explore various ways to model cells
mathematically. For that, we need to know not only what the main
components are but also what are their quantities. For example, proteins
are usually the most abundant constituent of the biomass, and many
simplified mathematical models focus solely on proteins. However, some
models include a much more detailed description of the biomass
composition. Additionally, we need to know how biomass composition
changes in different environments. For instance, the observation that
RNA/protein ratio increases with growth rate hinted how cells reallocate
resources to grow faster, inspiring the development of mathematical
models that capture this behavior.

<figure id="CEN:fig:BioCellStruct" data-latex-placement="t!">
<div class="center">
<p><img src=".//images/CEN_BioCellStruct.png" style="width:100.0%"
alt="image" /><br />
</p>
</div>
<figcaption>Biomass composition and cell structure of a typical
bacterial, yeast, and a mammalian cell – The area of each polygon
corresponds to a mass fraction of a component per cell. While the
average composition is quite similar in the three groups, there are
major differences in size and internal organization (especially when
comparing prokaryotes with eukaryotes). Data for proteome groups
(length-weighted protein abundances) was obtained from <a
href="https://www.proteomaps.net/download.html">Proteomaps</a>. Sources
of composition data: bacteria <span class="citation"
data-cites="MiloPhillips2015"></span>, yeast (BNID 108200, 108196,
107234, 100261, <span class="citation"
data-cites="KuenziFiechter1972"></span>), mammalian cells (BNID 107131,
107235, 107234). Pictures of cells were created using <a
href="https://bioicons.com/">Bioicons</a>.</figcaption>
</figure>

Cells are composed of around 70% water and 30% dry mass. As mentioned
previously in the chapter, we can describe the composition of the dry
mass with the most abundant chemical elements. For example, the
elemental formula for *E. coli* is CH~1.77~O~0.49~N~0.24~ (BNID 101800)
and for *S. cerevisiae* CH~1.61~O~0.56~N~0.16~ (BNID 101801). However,
this kind of description is not particularly useful for understanding
cells because it does not capture the variety of molecules that exist in
a cell.

Therefore, we are more interested in biomass composition in terms of the
main macromolecules (proteins, nucleic acids, lipids, and carbohydrates)
and small molecules (metabolites, cofactors, and ions).
Table [1.1](#CEN:tab:composition){reference-type="ref"
reference="CEN:tab:composition"} summarizes an average composition of
*E. coli* and *S. cerevisiae* during exponential growth, the typical
molecular masses and copy numbers of the components. The most abundant
component is protein, which forms around half of the dry mass of the
cell. When we divide the proteome into functional groups, we find that
the biggest fractions belong to translation, central carbon metabolism,
folding, sorting and degradation, and biosynthesis. A substantial
fraction belongs to proteins that are not mapped (especially in
mammalian cells), illustrating that we still lack knowledge about the
function of many proteins
(Figure [1.2](#CEN:fig:BioCellStruct){reference-type="ref"
reference="CEN:fig:BioCellStruct"}).

RNA forms 20% of dry cell mass in *E. coli*, but this number is lower in
eukaryotes, such as yeast (11%) or mammalian cells (4%). While the total
amount of RNA is variable in different organisms, its relative
composition is similar -- most of the RNA mass is formed by rRNA (80%),
followed by tRNA (15%) and mRNA (5%) (BNID 100258, 100261, 106154).
Lipid content is the highest in mammalian cells (13%) compared to yeast
and bacteria (4-10%, BNID 111209,
Table [1.1](#CEN:tab:composition){reference-type="ref"
reference="CEN:tab:composition"}). Remarkably, there are cases where
engineered yeast cells accumulated up to 80 % of lipids per cell dry
mass [@WangLedesma-Amaro2020]. The content of storage carbohydrates
varies from around 30% in yeast to 3% in bacteria
(Table [1.1](#CEN:tab:composition){reference-type="ref"
reference="CEN:tab:composition"}). In bacteria, carbohydrates are stored
as the polysaccharide glycogen, while yeast cells use glycogen and the
disaccharide trehalose. Yeast cells also contain structural
polysaccharides, such as mannan and glucan [@KuenziFiechter1972].
Bacteria contain the structural molecule peptidoglycan (3% of dry mass)
-- a polymer of sugars and amino acids, which forms bacterial cell
walls. In addition, some bacteria (e.g. *E. coli*) also have
lipopolysaccharides on their cell wall (3% of dry mass).

A small fraction of the cell mass (2- 3%) is formed by small molecules
(\< 1000 Da) such as metabolites and ions. This group contains thousands
of different molecules with vastly different functions and
concentrations. For illustration, the concentrations of the most
abundant metabolites in *E. coli* range from $10^{-1}$ to $10^{-7}$
moles per cell, corresponding to a range of $10^8$ to only 100 copies
per cell [@MiloPhillips2015]. Possibly, there are metabolites with even
lower concentrations, but these are much more difficult to quantify.
Similarly, the concentrations of the most common inorganic ions (, , , ,
) span several orders of magnitude [@MiloPhillips2015].

::: {#CEN:tab:composition}
+:----------------------+:--------+:--------+:-----------+:-----------+:--------------+:----------------+:--------------+:--------------+
|                       | \% of dry mass    | Mass per cell \[fg\]    | Molecular mass \[Da\]           | Copy number                   |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
|                       | *E. c.* | *S. c.* | *E. c.*    | *S. c.*    | *E.c.*        | *S. c.*         | *E. c.*       | *S. c.*       |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Proteins              | $55$    | $51$    | $165$      | $7650$     | $40000$       | $55000$         | $3\times10^6$ | $10^8$        |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| RNA                   | $20$    | $11$    | $60$       | $1650$     | $10^4$-$10^6$ | $10^4$-$10^6$   | $3\times10^5$ | $4\times10^6$ |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| DNA (chromosomal)     | $3$     | $0.5$   | $9$        | $75$       | $3\times10^9$ | $2.5\times10^8$ | $2$           | $16$          |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Lipids                | $9$     | $6$     | $27$       | $900$      | $800$         | $800$           | $2\times10^7$ | $10^9$        |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Storage carbohydrates | $3$     | $0.5$   | $9$        | $75$       | $10^6$        | variable        | $4000$        | --            |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Structural polymers   | $6$     | $23$    | $18$       | $3450$     | variable      | variable        | --            | --            |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Metabolites/cofactors | $3$     | $2$     | $9$        | $300$      | $<1000$       | $<1000$         | --            | --            |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+
| Other                 | $1$     | $6$     | $3$        | $900$      | --            | --              | --            | --            |
+-----------------------+---------+---------+------------+------------+---------------+-----------------+---------------+---------------+

: Amounts, characteristic molecular masses and copy numbers of the main
biomass components for *Escherichia coli (E. c.)* and *Saccharomyces
cerevisiae (S. c.)*. The composition data is shown for *E. c.* with a
doubling time of 40 minutes (BNID 104954) and for *S. c.* with a
doubling time of 110 minutes ([@CanelasRas2011], BNID 111755). The
storage carbohydrates include glycogen for *E. c.* / glycogen and
trehalose for *S. c.*. The structural carbohydrates include
peptidoglycan and lipopolysaccharides for *E. c.* / mannan and glucan
for *S. c.*. Sources for molecular masses (BNID 105861, 115091, 101838,
104886, 107678, 109645, 102502, 100459); molecule copy numbers (BNID
108248, 108197, 114950).
:::

:::: Generalblock
The quantities of biomass components are usually expressed in relation
to other quantities. The most common units are copy numbers, moles,
grams, or fractions which can be expressed per cell, per gram dry mass,
or per cell volume. Membrane components can also be expressed per
surface area. Often, experimental data for these quantities is not
readily available, so we need to extract it from literature. Useful
sources for average or "rule of thumb" values include [BioNumbers
database](https://bionumbers.hms.harvard.edu/search.aspx)
[@MiloJorgensen2010] and the book [Cell Biology by the
numbers](http://book.bionumbers.org/) [@MiloPhillips2015]. Some useful
quantities are summarized in the table below. They are organized in
increasing order with respect to the dimensions (1 -- mass, size,
thickness; 2 -- area; 3 -- volume, density). Notice how the dimensions
influence the numerical values. For example, while the cell size differs
only about 3-fold between bacteria and yeast, the surface area differs
by more than tenfold and the volume by about 60-fold. Because volume
grows faster than area, the ratio of cell surface area to volume (SA/V)
gets smaller and smaller as cells get bigger (see more in
Section [1.3.2](#CEN:Sec:Size){reference-type="ref"
reference="CEN:Sec:Size"}). Note that these are just "rule of thumb"
values. In reality, these values typically cover a broad range and
depend on environmental conditions.

::: center
  Name                           Unit       *E. coli*   *S. cerevisiae*   BNID/Reference
  ------------------------------ ---------- ----------- ----------------- -----------------------------
  Surface area/volume (SA/V)      μm        $6$         $1.2$             calculated here
  Dry cell mass                  pg         $0.3$       $15$              104954, 108315
  Total cell mass (with water)   pg         $1$         $60$              104954, 108315
  Bilayer membrane thickness     nm         $4$         $4$               [@MiloPhillips2015]
  Cell size                      μm         $1$-$2$     $5$               [@MiloPhillips2015], 101796
  Cell surface area              μm^2^      $6$         $70$              101792, 113854
  Cell volume                    μm^3^      $1$         $60$              101788, 101794
  Cell density                   g mL^−1^   $1.1$       $1.1$             103875, 103876
:::
::::

### Variability of biomass composition {#CEN:Sec:variablity}

Table [1.1](#CEN:tab:composition){reference-type="ref"
reference="CEN:tab:composition"} shows biomass composition of a typical
*E. coli* and *S. cerevisiae* cell -- these are average values in
certain environmental conditions. However, cell size, mass, and
composition vary with growth rate and environmental conditions. One of
the most extensively studied relationships in the literature is the
correlation of growth rate with cell size. The increase of cell mass and
volume with growth rate has been observed in bacteria
(Figure [1.3](#CEN:fig:GrowthLaws){reference-type="ref"
reference="CEN:fig:GrowthLaws"}), yeast, and mammalian cells
[@SchaechterMaaloe1958; @VadiaLevin2015; @AldeaJenkins2017; @SzeliovaRuckerbauer2020]
(BNID 107948, 110191, 105103). For example, the cell mass of *E. coli*
can vary fivefold -- 150 to 870 fg per cell for generation times between
100 and 24 minutes [@MiloPhillips2015]. Larger cell mass goes hand in
hand with larger amounts of individual biomass components. The absolute
amounts of protein, RNA, and DNA increase with cell size. However, the
ratios of the components do not stay the same and the relative
composition changes with growth rate
[@SchaechterMaaloe1958; @BremerDennis2008].

One of the most consistent observations is that the relative amount of
RNA per cell increases with a higher growth rate
[@SchaechterMaaloe1958; @BremerDennis2008; @PramanikKeasling1997], (BNID
111460, 111755, 108200). On the other hand, the data for relative
protein content is more variable. For example, in bacteria, protein
content decreases with growth rate in some studies
[@BremerDennis2008; @PramanikKeasling1997] but goes up and down in
another (BNID 111460); in yeast, it increases (BNID 108200, 111755).
Nevertheless, when looking at RNA/protein *ratio* we consistently find a
positive correlation with growth rate across various species of bacteria
(see Figure [1.3](#CEN:fig:GrowthLaws){reference-type="ref"
reference="CEN:fig:GrowthLaws"}) and yeast
[@ScottGunderson2010; @KarpinetsGreenwood2006]. RNA/protein ratio is a
measure of protein production capacity since most RNA is dedicated to
protein synthesis. 80% is rRNA, which forms 2/3 of the mass of a
bacterial ribosome -- the molecular machine that makes proteins, and 15%
is tRNA which brings new amino acids to the ribosome (for more details
about ribosomes, see
Section [1.5](#CEN:sec:macrosyn){reference-type="ref"
reference="CEN:sec:macrosyn"}). Indeed, we also observe a correlation
between ribosome content and growth rate. The increase of RNA/protein
ratio and ribosome content with increasing growth rate reflect higher
biosynthetic needs of faster-growing cells. To support higher growth
rate, cells need to reallocate resources according to the growth demands
(for example, make more ribosomes which can then make more proteins)
[@ScottGunderson2010]. For more details about resource allocation and
how it is modeled see Chapters  and .

<figure id="CEN:fig:GrowthLaws" data-latex-placement="b">
<div class="center">
<p>(A)</p>
<p>(B)</p>
<p><br />
<embed src=".//images/CEN_GrowthLaws.pdf" style="width:80.0%" /></p>
</div>
<figcaption>Growth laws in <em>E. coli</em> – (A) Cell volume grows
exponentially with growth rate (data from <span class="citation"
data-cites="SiLi2017"></span>). (B) RNA/protein ratio grows linearly
with growth rate (data from <span class="citation"
data-cites="ScottGunderson2010"></span>). In both cases, growth rate was
varied by changing medium composition.</figcaption>
</figure>

Similarly to protein content, there is no clear correlation between the
relative DNA and lipid content with growth rate across studies
[@BremerDennis2008] (BNID 111460, 111755, 108196). The content of
storage carbohydrates decreases at higher growth rates in yeast and
bacteria [@PramanikKeasling1997] (BNID 111755, 111460).

As we have seen, the composition of the biomass changes with the growth
rate, and for some components, we can describe this relationship with
simple mathematical equations
[@PramanikKeasling1997; @BremerDennis2008]. However, the growth rate is
the result of environmental conditions such as the amount or quality of
a carbon source, temperature, oxygen concentration, or presence of
inhibitors, among others. Different conditions may lead to the same
growth rate but may not result in the same changes in cell physiology
[@VadiaLevin2015]. For example, modulation of growth rate by temperature
rather than medium composition does not significantly affect cell size
and composition [@SchaechterMaaloe1958; @BremerDennis2008]. Inhibition
of ribosomes with an antibiotic decreases the growth rate but increases
the ribosome content, contrasting to the nutrient law shown in
Figure [1.3](#CEN:fig:GrowthLaws){reference-type="ref"
reference="CEN:fig:GrowthLaws"} [@ScottGunderson2010].

In contrast, environmental factors can influence cell composition
without affecting growth rate. This shows that cell metabolism is
flexible -- cells can reach the same growth rate in different ways,
depending on the conditions. For example, in yeast, changes in O~2~
concentration lead to changes in biomass composition while keeping
growth constant using a chemostat [@CarnicerBaumann2009]. In mammalian
cells, a change in a culture medium leads to significant changes in
lipid composition without having a considerable effect on the growth
rate [@SzeliovaRuckerbauer2020].

### Biomass composition varies within and between cells

In the previous paragraphs, we considered average cells with a
homogeneous composition across the cell. However, we must keep in mind
that cells have an internal structure and that biomass components are
not uniformly distributed throughout the cell (as illustrated in
Figure [1.4](#CEN:fig:NonuniformMolecules){reference-type="ref"
reference="CEN:fig:NonuniformMolecules"}). Although prokaryotic cells do
not have compartments separated by membranes, they have some internal
organization. For example, DNA is not spread across the cytoplasm, but
wrapped around proteins and packed in a compact structure called a
nucleoid. Another example is that certain proteins are preferentially
localized on the poles in rod-shaped bacteria. Eukaryotes have
compartments with different compositions, pH, and membrane potential.
DNA is localized only in the nucleus and mitochondria, and many proteins
localize only in a particular compartment. Small molecules and ions also
have different concentrations in the different compartments. Often they
cannot freely diffuse through membranes, but transport is regulated and
requires energy.

<figure id="CEN:fig:NonuniformMolecules" data-latex-placement="b!">
<div class="center">
<p><embed src=".//images/CEN_NonuniformMolecules.pdf"
style="width:45.0%" /><br />
</p>
</div>
<figcaption>Two cells with the same numbers of molecules, but different
spatial distributions. Although the average concentration is the same in
both cells, the second cell has varying concentrations in different
compartments. </figcaption>
</figure>

These differences in concentrations have implications for cellular
functions. Some processes are restricted only to a particular
compartment/area. For example, transcription only occurs in the nucleus
and mitochondria (nucleoid), and some metabolic pathways occur only in a
specific compartment (e.g. tricarboxylic acid cycle in the
mitochondria). Even if the same enzyme is present in several
compartments, it might work at a different rate or in the opposite
direction because of the different concentrations of substrates or
products. In eukaryotes, certain digestive enzymes only work at low pH
present in lysosomes (thus preventing a cell from digesting itself).
Sometimes, consecutive enzymes in a metabolic pathway do not freely
float in a cell but form an assembly or bind to a scaffold, allowing
intermediates to be channeled directly from one enzyme to another. This
accelerates metabolic reactions because intermediates do not diffuse
away into the bulk solution and are not consumed by competing reactions.

Finally, we need to zoom out from a single-cell (or average) view of a
cell and consider the heterogeneity at the population level. This
heterogeneity is often neglected, and we use a single number to describe
a concentration of a molecule in a cell/compartment -- an average value
of the population. However, biological processes are *stochastic*
(noisy), and the actual molecule numbers follow a certain distribution
(Figure [1.5](#CEN:fig:PopulationDistribution){reference-type="ref"
reference="CEN:fig:PopulationDistribution"}), which can be characterized
by mean and variance. The effect of the heterogeneity becomes especially
important at low copy numbers.

<figure id="CEN:fig:PopulationDistribution" data-latex-placement="t!">
<div class="center">
<embed src=".//images/CEN_PopulationDistribution.pdf"
style="width:45.0%" />
</div>
<figcaption>Number of molecules per cell in a population (for example
protein or mRNA) – The red line is the population mean, which is often
the value we use (for modeling). However, the values at a single-cell
level can differ several fold.</figcaption>
</figure>

The heterogeneity in molecule copy numbers leads to a heterogeneity in
cell phenotypes such as generation time, cell size, stress tolerance,
and others. The heterogeneity of the population can affect fitness in a
positive or negative way, depending on the conditions. For example, when
a cell population encounters an unexpected environment, a certain
subpopulation might be better suited to survive. In a different
environment, another subpopulation might thrive. We can view this as a
microbial "bet-hedging" which increases the chances that at least some
part of a population will survive the new conditions. However, when
cells try to maximize the growth rate, the variability in the population
can decrease fitness because it decreases the average population growth
rate [@LinAmir2017]. This topic is discussed in detail in Chapter .

::: Expblock
We can measure biomass composition at different levels of detail -- from
a coarse elemental or macromolecular composition of an average cell to
the quantities of individual molecules in each cellular compartment.

To quantify the main chemical elements (CHNOPS), we can use devices
called elemental analyzers. The main macromolecular components -- the
total protein, lipid, carbohydrate, DNA, and RNA content -- can be
quantified with simple assays such as detection with fluorescent dyes,
chemical reactions that lead to color change, or extraction and weighing
of a component. Going into more detail typically requires more
sophisticated methods such as liquid or gas chromatography (LC, GC),
mass spectrometry (MS) or nuclear magnetic resonance (NMR). For example,
for proteins, we can measure an average amino acid composition, and for
lipids, the main lipid classes (glycerophospholipids, sphingolipids,
sterols, etc.).

If we go down to the level of individual molecules, we enter fields of
study collectively termed as *omics*, which aim to characterize and
quantify certain pools of biomolecules. Omics methods typically involve
high-throughput measurements of hundreds or thousands of different
molecules and require a lot of resources (specialized equipment,
computational resources) and expertise. The classic omics fields include
genomics, transcriptomics, and proteomics which study DNA, RNA and
proteins, respectively. Other examples include metabolomics which
focuses on small metabolites or fluxomics which measures metabolic
fluxes (for example ^13^C metabolic flux analysis).

Combinations of different omics can help us obtain other parameters that
are difficult to measure. For example, turnover numbers of enzymes
($\kcat$) are notoriously difficult to quantify because the measurements
are error-prone and low-throughput. With proteomics and fluxomics data
we can calculate apparent turnover numbers ($\kapp$) at various
conditions (see Figure [1.9](#CEN:fig:Gauges){reference-type="ref"
reference="CEN:fig:Gauges"}) and use the maximum value
($\kapp^{\rm max}$) as an estimate of *in vivo* $\kcat$
[@DavidiNoor2016].
:::

:::: Expblock
::: center
  **Component/parameter**     **Examples of quantification methods**
  --------------------------- ---------------------------------------------------------------
  Cell size                   microscopically
  Dry cell mass               weighing of a defined amount of dry cells
  Buoyant density             Percoll gradient
  Protein                     colorimetric (Bradford assay; Lowry assay)
  Lipid                       weighing of extracted and dried lipids
  Carbohydrates               colorimetric (anthrone assay; phenol-sulphuric acid assay)
  RNA                         fluorimetric (RiboGreen), spectrophotometric
  DNA                         fluorimetric (PicoGreen, Hoechst), spectrophotometric
  Amino acids/lipid classes   LC/MS, GC/MS
  Genomics                    next-generation sequencing (NGS) - Illumina, PacBio, Nanopore
  Transcriptomics             NGS (RNA-seq), DNA microarrays
  Proteomics/metabolomics     LC/MS, GC/MS, NMR
:::

To visualize composition data, consider using Voronoi diagrams instead
of the traditional pie charts or bar plots. An online tool is available
at
[bionic-vis.biologie.uni-greifswald.de](http://bionic-vis.biologie.uni-greifswald.de/)
for proteomics data, but there is also a tool that works with any type
of input data (GitLab repository on the [book
website](https://gitlab.com/principlescellphysiology/principles-cell-physiology/-/tree/master/open-code?ref_type=heads)).
::::

## Macromolecule synthesis and the resources needed {#CEN:sec:macrosyn}

In the previous sections, we have explored the diversity of nature and
the abundance of biological molecules. The combination of smaller
building blocks into functional units, let it be proteins, membranes, or
DNA that conserves information about the organism, is the major stepping
stone from an unorganized pack of molecules into what we could call a
living system. Therefore, in this section, we will consider the
coordination of how cell components are produced, focusing on the
biosynthesis of macromolecules.

The overall cell growth can be called *self-replication*: a cell makes a
copy of itself by synthesizing macromolecules by using molecules it
either produces or takes up from the environment, all in the right
amounts and proportions. How, how fast and how big two cells rise from a
single parent cell is the question we explore in our field, and often
try to complement the experimental observations (*what* and *in what
amounts* produced) with computational models of growth (*how* and *why
like that*).

In general, three essential types of resources are needed for the
synthesizing of macromolecules: (1) small molecule precursors, (2)
catalysts, and (3) physical space/volume for the process to happen
(Figure [1.6](#CEN:fig:SelfReplication){reference-type="ref"
reference="CEN:fig:SelfReplication"}). We will thus discuss how these
resources are primed and used for macromolecule synthesis, together with
different considerations surrounding each type of these resources. We
will first start with discussing the "demand" side of the balance,
requirement for the small molecule precursors of the cells, and will
continue to zoom out towards the whole-cell economy of volume.

<figure id="CEN:fig:SelfReplication" data-latex-placement="b">
<div class="center">
<embed src=".//images/CEN_SelfReplication.pdf" style="width:60.0%" />
</div>
<figcaption>The basic building blocks of cells are small molecule
precursors – The precursors are needed to make catalysts such as enzymes
and machines. In turn, these catalysts synthesize both the precursors
and themselves, forming a self-replicating system. These processes need
to be coordinated while being constrained by space.</figcaption>
</figure>

### Precursors of macromolecules

Biosynthesis of macromolecule precursors (e.g. amino acids, nucleotides,
energy equivalents) is an important part of every metabolic network.
Many microorganisms can grow on a very limited number of nutrients (in
the laboratory context, the so-called minimal media), which usually
consist of a single source of carbon, nitrogen, phosphorus, and sulfur.
For instance, a minimal growth medium with glucose as the sole carbon
source can fully support growth: glucose enters glycolysis as the main
energy-harvesting route; however, some of the glycolytic intermediates
serve as substrates for, e.g. amino acid, lipid, or nucleotide
biosynthesis.

A particularly interesting fact is that metabolic networks can be
described as *bow-tie* structures [@FriedlanderMayo2015]: a large
variety of nutrients can be converted into a very small number (usually
counted up to 12) essential metabolic intermediates, which give rise to,
again, a diverse set of molecules (for a detailed discussion, see
Chapter ). This provides two important insights into metabolic networks.
First, this plasticity of the metabolic networks allows organisms to
grow in various environments, where different nutrients are available.
Second, because of this organization, the biosynthesis of macromolecule
precursors competes for the same starting molecules independently of the
initial nutrients.

::: Ecoblock
The diversity of metabolic intermediates/end products, stemming from
small number of nutrients (e.g. minimal mineral media for yeast growth,
containing glucose, ammonium, phosphate and sulphate salts), can be
imagined as a bakery. Every pastry starts with a small array of
ingredients (flour, water, salt, sugar, \...) and using some machinery
(e.g. ovens), one ends up baking bread, pretzels, cookies, muffins etc.,
which are way diverse in their features, compared to the starting
mixture. Likewise, by taking only a handful of compounds, cells,
especially microorganisms, can synthesize most of the molecules they
need to eventually replicate.
:::

### Catalysts needed for macromolecule synthesis

Many steps of the biosynthesis of macromolecules, as discussed
previously, need catalysis to proceed. Therefore, another kind of
investment into macromolecule synthesis is expression of necessary
proteins and RNAs (in the latter case - ribosomal RNA). Expression of
proteins, starting from transcription of messenger RNAs, their
translation into proteins, folding, and degradation, involve many steps
with energy investment (ATP hydrolysis) and consume large amounts of
precursors (nucleotides, amino acids). Talking in energetic terms alone,
protein expression accounts for about 40% of energy investments in yeast
*S. cerevisiae* [@LahtveeSanchez2017], and the energy investments for
every stage of protein expression are illustrated in
Table [1.2](#CEN:tab:biosyntheticCosts){reference-type="ref"
reference="CEN:tab:biosyntheticCosts"} for typical bacterial and
eukaryotic cells. This concerted action of several systems, as described
above, with substantial investments at every intermediate step, means
that these investments thus happen on two levels: investments in the
metabolic machinery and in the machinery, producing proteins themselves.
We will consider these two levels in the following.

::: {#CEN:tab:biosyntheticCosts}
+-------------------+---------------------------------------+--------------------------------------------------------------------+
| Expression stage  | Bacteria                              | Eukaryotes                                                         |
+:==================+:======================================+:===================================================================+
| DNA synthesis     | $101~ L_{g}$                          | $263~ L_{g}$ ($\times 2$ for diploids)                             |
+-------------------+---------------------------------------+--------------------------------------------------------------------+
| RNA transcription | $2~ N_{r}~ L_{g} (23 + \delta_{r} t)$ | $N_{r}(46 \times L_{r, mat} + 2.17 \times \delta_{r} t L_{r,pre})$ |
+-------------------+---------------------------------------+--------------------------------------------------------------------+
| Protein synthesis | $N_{p} L_{p}[(\bar{c}_{AA} - 1) + 5 \delta_{p} t]$                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------+

: The estimated energetic costs (units of ATP hydrolysis) of
biosynthesis of a gene, as computed by [@LynchMarinov2015]. The
estimates are represented as functions of the following parameters:
$L_{g}$, gene length; $N_{r}$, the steady-state number of mRNAs;
$L_{r, pre}$ and $L_{r, mat}$, the length of precursor and mature mRNA,
respectively; $\delta_{r}$, the degradation rate of mRNA; $t$, division
time of a cell; $N_{p}$, the steady-state number of protein molecules;
$L_{p}$, length of the protein chain; $\bar{c}_{AA}$, average cost of an
amino acid; $\delta_{p}$, the degradation rate of proteins.
:::

 \

##### Metabolic enzymes.

First, metabolic enzymes need to be expressed to convert nutrients into
biosynthesis precursors. Some enzymes are active only in a form of
complexes, which also creates a demand to express proteins at defined
ratios. Enzymes and their complexes come in different sizes and flavors,
and their activity can be described (in very coarse-grained way, for
more details see Chapter ) by two kinetic aspects: the efficacy
(represented by the turnover number $\kcat$) and substrate specificity
(Michaelis constant $\km$) of an enzyme. Importantly, these two
parameters are intertwined: high substrate specificity usually comes at
the cost of efficacy and vice versa. Therefore, although some enzymes
tend towards extremes in terms of their specificity or efficacy, most of
the enzymes land close to the average/median values of these parameters,
when considering the distribution of enzyme parameters among different
organisms [@BarEvenNoor2011]
(Figure [1.7](#CEN:fig:kcatKm){reference-type="ref"
reference="CEN:fig:kcatKm"}).

<figure id="CEN:fig:kcatKm" data-latex-placement="t!">
<div class="center">
<embed src=".//images/CEN_kcatKm.pdf" />
</div>
<figcaption>Distributions of the <span
class="math inline">\(\kcat\)</span> and <span
class="math inline">\(\km\)</span> values (in <span
class="math inline">\(s^{-1}\)</span> and <span
class="math inline">\(mM\)</span>, respectively), collected for
<em>E. coli</em>, yeast and human enzymes – The vertical solid line
depicts the median of each distribution. Values were collected from the
BRENDA database, release 2022.1 <span class="citation"
data-cites="ChangJeske2021"></span>.</figcaption>
</figure>

The metabolic networks need to work in a concerted manner, even though
different enzymes need to perform different amounts of "work" (described
as metabolite *flux* through these enzymes, $\flux$). Thus, even given
the similarities in "average" (or "moderate") enzyme properties, the
expression of proteins and the abundance of their substrates span
several orders of magnitude. Based on the kinetic interpretation of
enzyme kinetic parameters, we can link them to either expression level
of the enzyme $\enzconc$ ($\enzconc \varpropto \frac{\flux}{\kcat}$) or
substrate concentration $s$ (usually, $0.1 \km \le s \le 10 \km$). Note
that for substrate concentrations, the suggested range
(order-of-magnitude difference from the $\km$ to each side) is
arbitrary, yet supported by empirical observations. On the higher end,
the benefit from high substrate concentration becomes negligible
(saturation kinetics) as the concentration moves from the order of
magnitude of $\km$ (see Exercises for an example). The lower bound of
concentrations is defined through high demand of enzymes: in order to
sustain flux, a lot of enzyme would have to be produced. As cells have a
finite volume to accommodate proteins, such a strategy works only for a
very small number of enzymes. Taken together the limitations on the both
sides of the spectrum, enzyme kinetics set the bounds for the
concentrations of metabolites in the cells.

To illustrate the diversity of enzyme turnover values $\kcat$ and the
condition-dependent expression of enzymes (dictated by the flux $\flux$
these enzymes have to sustain), we can consider the proteome composition
of *E. coli* under two conditions: growth medium with the complete
supplement of amino acids (all 20 proteogenic amino acids present in
medium), in contrast to the supplement with a single amino acid not
present in the mix (a "dropout" medium)
(Figure [1.8](#CEN:fig:MetE){reference-type="ref"
reference="CEN:fig:MetE"}). The growth of *E. coli* in a nutrient-rich
medium (glucose + amino acid supplement) is indeed a very fast one (with
doubling time of $\tau_{d,rich} = 21.5 \pm 0.4$ vs.
$\tau_{d,minimal} = 56.3 \pm 0.5$ minutes). The omission of methionine
from the amino acid supplement does increase the doubling time
($\tau_{d,-Met} = 26.5 \pm 1.1$ minutes), yet the growth rate remains
high, and so is the methionine biosynthesis demand in these conditions.

<figure id="CEN:fig:MetE" data-latex-placement="t!">
<p>(A) Methionine dropout</p>
<p>(B) Complete medium</p>
<p><br />
<embed src=".//images/Fig_MetE-old.pdf" /></p>
<figcaption>Proteome composition of <em>E. coli</em>, grown on the
growth medium with full amino acid supplement (B) or its version without
amino acid methionine (A). Proteome composition data from <span
class="citation" data-cites="LiBurkhardt2014"></span>. Each polygon
represents a protein, and its size indicates the amount. Proteins are
grouped into sections based on their functions. You can create
Proteomaps like this using <a href="https://www.proteomaps.net/"
class="uri">https://www.proteomaps.net/</a>. </figcaption>
</figure>

Methionine is an amino acid that is energetically the most expensive to
make [@KaletaSchaeuble2013], and the final enzymatic reaction in the
methionine synthesis pathway is so-called *rate-limiting*, or the
reaction which dictates the flux through the whole pathway. Moreover,
the enzyme methionine synthase (*MetE*) is a very slow enzyme
(Figure [1.8](#CEN:fig:MetE){reference-type="ref"
reference="CEN:fig:MetE"}, table on the bottom), thus required at large
quantities to provide enough methionine for protein synthesis at high
growth. Consequently, it was observed that *MetE* alone could occupy up
to ca. 7.5% of the total proteome (by mass) in medium lacking
methionine, and growth on a medium, containing methionine, would reduce
the proteome fraction by ca. 800-fold, to 0.009% [@LiBurkhardt2014]. To
contrast this highly condition-dependent expression of *MetE*, we
considered a protein in the lower glycolysis, enolase (*Eno*) (Table
[1.3](#CEN:tab:MetE_figure){reference-type="ref"
reference="CEN:tab:MetE_figure"}). The expression of glycolytic
proteins, including *Eno*, was determined to be similar, as both the
complete- and the methionine-free media contained glucose as the main
carbon source. A noticeable contrast of *Eno* *vs.* *MetE* is also a ca.
3 orders-of-magnitude higher $\kcat$ value compared to the one of
*MetE*: having to invest less (per mass) into this enzyme contributes to
the ability to sustain a very high flux through enolase when cells grow
fast on glucose [@LiBurkhardt2014] (see Chapter for a more detailed
discussion).

::: {#CEN:tab:MetE_figure}
+:------------:+:-----------:+:-----------:+:-----------:+:-----------:+
| Pathway      | Enzyme      | Proteome mass fraction    | $\kcat$     |
|              |             | (%)                       | ( s)        |
+--------------+-------------+-------------+-------------+-------------+
|              |             | Met dropout | Complete    |             |
+--------------+-------------+-------------+-------------+-------------+
| Glycolysis   | Enolase     | 0.53        | 0.53        | 192.95      |
|              | (Eno)       |             |             |             |
+--------------+-------------+-------------+-------------+-------------+
| Amino acid   | Methionine  | 7.45        | 0.009       | 0.12        |
| biosynthesis | synthase    |             |             |             |
|              | (MetE)      |             |             |             |
+--------------+-------------+-------------+-------------+-------------+

: Abundance and $\kcat$ values of two selected proteins from Figure
[1.8](#CEN:fig:MetE){reference-type="ref" reference="CEN:fig:MetE"}:
enolase (independent on amino acid supplementation) and methionine
synthase (dependent on amino acid supplementation).
:::

The variable concentrations of metabolic substrates, and their relation
to the enzyme parameters ($\km$ in this case), also bring additional
kinetic considerations. The above-introduced turnover value $\kcat$
represents the highest possible efficacy of the enzyme, where all
substrates are accessible in concentration needed to sustain this
efficacy (also called *saturating* concentrations). Turnover values are
usually measured *in vitro*, with all the substrates highly in excess,
thus deliberately minimizing many kinetic effects (enzyme saturation,
reversibility of reactions, etc.) that are prevalent in more
physiological conditions (see Chapter  for details). Therefore, what we
usually observe in living cells is not the enzyme efficacy in terms of
$\kcat$, but rather their *apparent turnover value* $\kapp$
(Figure [1.9](#CEN:fig:Gauges){reference-type="ref"
reference="CEN:fig:Gauges"}). The ratio of these values
($\frac{\kapp}{\kcat}$) is then called the *enzyme efficiency* and can
be used to infer how far the enzyme is from its optimal working
conditions. The $\kapp$ value of an enzyme *in vivo* can be computed as
follows: knowing the $\kcat$ value, the flux through the reaction, one
can calculate the minimal demand (in moles) of the enzyme to maintain
that flux. Then, the $\kapp$ value can be computed by taking the ratio
between the predicted minimal enzyme demand and the abundance of enzymes
in the cells.

<figure id="CEN:fig:Gauges" data-latex-placement="t!">
<div class="center">
<p><embed src=".//images/CEN_Gauges.pdf" style="width:100.0%" /><br />
</p>
</div>
<figcaption>The relation between the apparent and measured turnover
value (<span class="math inline">\(\kapp\)</span> and <span
class="math inline">\(\kcat\)</span>, respectively) – Factors, leading
to low net rate of reaction per unit of protein (e.g. low substrate
concentration) lead to <span class="math inline">\(\kapp\)</span> being
significantly lower than the measured <span
class="math inline">\(\kcat\)</span> value, latter of which corresponds
to the maximal rate of the reaction. </figcaption>
</figure>

##### Macromolecule polymerization.

Moving from metabolic enzymes to macromolecular synthesis machinery, the
polymerization of macromolecules (DNA replication, RNA transcription,
and protein translation) is catalyzed by large enzyme complexes (and
RNA, in the case of ribosomes). DNA and RNA polymerases (DNAP, RNAP) and
ribosomes. The resources needed for their expression also contribute
significantly to the total costs of macromolecule biosynthesis. For
example, the molecular weight of an intact ribosome in *E. coli* is ca.
2.3 MDa (BNID 111560), and the *E. coli* ribosome consists of 62% RNA
and 38% protein (in mass %, BNID 109047). Meanwhile, eukaryal ribosomes
are even larger, ca. 3.3 MDa for *S. cerevisiae* and ca. 4.3 MDa for
human *H. sapiens* (BNID 111560), and have higher protein content
[@WilsonCate2012]. For a comparison, the average length of a protein in
*E. coli* is ca. 300 amino acids (BNID 100017) and average amino acid
weight is ca. 109 Da (BNID 104877). By multiplying these numbers, the
molecular mass of an average protein is ca. 32.7 kDa, roughly $70\times$
lower than the ribosome that synthesizes this protein.

The nature of these large complexes requires an exceptional coordination
of resources. The first consideration is the number of individual
proteins that form these complexes: the RNA polymerases of
*S. cerevisiae* contain up to 17 subunits (BNID 111568), and 79
ribosomal proteins form a fully functional ribosome
[@WoolfordBaserga2013]. Therefore, the assembly of these complexes must
be fast and robust: Thus, cells contain a number of assembly factors to
facilitate these processes. Next, the coordination also has to be
temporal, especially for prokaryotes, where both messenger RNA
transcription and protein translation can happen simultaneously. In
*E. coli*, this is well illustrated by the 3-fold difference between
elongation rates of mRNAs and proteins, ca. 62  s^−1^ and 21  s^−1^,
respectively (BNID 103021, 107868). This coordination is essential for
coordinated transcription and translation happening at the same time
[@ProshkinRahmouni2010], as translation happens in steps, 3 nt each
(so-called *triplets*). Even in eukaryote *S. cerevisiae* we observe a
similar pattern: mRNA elongation rate of ca. 30  s^−1^ (BNID 103016) and
protein chain elongation rate of ca. 10.5  s^−1^ [@MetzlRazKafri2017],
nearly a $3\times$ difference. Also, the polymerization of
macromolecules is very tightly connected to the metabolism: different
kinds of growth limitations (limiting amounts of nutrients) were shown
to create bottlenecks at different stages of protein expression
[@KafriMetzlRaz2016], and the optimal regulation of these processes were
selected for by the evolution [@BerkhoutBosdriesz2013; @MaitraDill2015].

### Physical proteome space

A final type of asset required for macromolecule synthesis is the
physical volume in the cell. As the cells are, again, "bags of things",
they possess a finite volume, thus different processes compete for
available proteome volume (also called "proteome space"
interchangeably). A general trend across microorganisms is that
ribosomes occupy larger proteome mass fraction (in the range of 10-40%
total proteome) with increasing growth rate
[@ScottGunderson2010; @ElsemmanRodriguez2021], with an estimated maximum
in *E. coli* of ca. 55% of total proteome mass [@ScottGunderson2010].
Alongside ribosomes, biosynthetic pathways also occupy a substantial
share of total proteome (e.g. enzymes, required for amino acid
biosynthesis occupy up to 15% of the proteome space in *S. cerevisiae*
[@ElsemmanRodriguez2021]). Experimentally, the optimal allocation of
proteome space can be challenged by, e.g. varying expression of an
unneeded (gratuitous) protein. Both for *E. coli* and *S. cerevisiae* it
was shown that increasing gratuitous protein expression directly affects
the maximal growth rate on both minimal and rich media
[@DekelAlon2005; @KafriMetzlRaz2016], suggesting that the decrease in
growth rate is not dependent on the nutrient status of the cell.

Numbers provided above were measured for cells, grown in minimal medium,
and some of the costs we discussed -- not only proteome space, but also
precursors and enzymes -- could be alleviated by growth in rich medium.
Uptake of biosynthetic precursors usually is less costly than
biosynthesis, as expression of a single type of transporter can
substitute the need of expressing a biosynthetic pathway with tens of
enzymes associated. Indeed, transfer of *S. cerevisiae* cells to a amino
acid-rich growth medium resulted in an increase of growth rate, caused
by increased proteome allocation to ribosomes, in place of the proteins
of *de novo* amino acid biosynthesis [@BjorkerothCampbell2020]. In
conclusion, the physical space that proteins can occupy is also an asset
that the proteins are competing for, and thus the optimal allocation of
the available space is key for the cells to grow in the most favorable
way under specific conditions.

## Physicochemical considerations about cells

### Cell density {#CEN:Sec:Density}

Most cellular parameters we discussed so far -- cell size, mass, and
composition -- vary greatly with the cell type, growth rate, or
conditions. However, one quantity does not show such variability --
buoyant cell density. Buoyant density is the ratio of cell mass to
volume, usually expressed as g mL^−1^. For most organisms, prokaryotic
or eukaryotic, the buoyant cell density is around 1.05-1.15 g mL^−1^
[@Kubitschek1987; @MiloPhillips2015]. This range results from the fact
that cells are 70% water which has a density of 1 g mL^−1^ and that most
dry mass is formed by proteins, which have a density of 1.2-1.4 relative
to water (BNID 111208, 104272, 101502). Other components range from 1
for lipids (BNID 108142) to 1.4-2 for nucleic acids (BNID 111208). To
try the calculation of bacterial density, see
Problem [\[CEN:Exerc:density\]](#CEN:Exerc:density){reference-type="ref"
reference="CEN:Exerc:density"}.

For many organisms (*E. coli*, the yeast *Schizosaccharomyces pombe*,
Chinese hamster ovary cells, mouse cells), cell density is constant
throughout the cell cycle and at different growth rates when growing
exponentially. However, it was observed to increase in stationary phase
for *E. coli* and *S. pombe* [@Kubitschek1987; @KubitschekWard1985]. On
the other hand, the density of *S. cerevisiae* fluctuates during the
cell cycle, which might be related to a different division mode. The
organisms mentioned earlier divide by binary fission -- cells divide in
the middle and produce two (roughly) identical daughter cells. In
contrast, *S.cerevisiae* divides asymmetrically -- it grows a bud that
breaks away and becomes a smaller daughter cell.

Nevertheless, despite the variability, the range of the observed values
is relatively small and similar for most organisms, from bacteria to
mammalian cells. There are special cases where cell density deviates
from the characteristic values -- for example, cells with very high fat
content or gas bubbles have lower densities. However, assuming the
density of 1.1 g mL^−1^ is probably a good guess unless you work with a
particularly fatty or gassy cell type.

The invariability of cell density suggests that this property is highly
regulated and brings us to the next question -- is there an optimal
density? And what are the constraints that (possibly) determine this
optimum? These questions (among others) are discussed in the next
section.

### Physical constraints of cell growth

The living cells are constantly subject to a handful of so-called
*physical constraints*, which are directly linked to the physics and the
chemistry of life. Cells cannot override (evolve to bypass) these limits
-- only try to cope with them. Thus, sometimes these constraints are
also called "hard" constraints. Notice that we consider the "hardness"
of these constraints only in the space where conditions can still
sustain life: some of these limitations could be relaxed by changing
abiotic conditions, but would result in breakdown of biological systems.

One of the abiotic factors would be temperature; however, increased
temperatures cause proteins to *denature* (lose their 3D-folded
structure, thus functionality) and destabilize biological membranes.
Although there are organisms, which live in extremely high temperatures
(so-called *thermophiles*), as a rule of thumb, we usually consider the
temperature above 393 K (120 °C) to be close to the limit of life. There
is an organism known as *Strain 121* (*Geogemma barossii*) which can
grow at 121 °C (hence the name), currently the highest temperature known
[@KashefiLovley2003]. Next, the suboptimal concentration of inorganic
salts (osmolarity) or pH could also drive similar changes, disfavoring
life. Here we will consider two prominent physical limits in life: the
diffusion and density limits. These two limits describe two aspects of
how molecules move in aqueous environments, in our case -- living cells.

The diffusion limit describes the state where enzymatic catalysis is so
specific and so fast that the reaction speed is determined only by the
collisions of substrate molecules to the enzymes, which all result in
conversions (i.e. no futile collisions) [@DavidiLongo2018]. Usually, the
number of futile collisions vary between 1 and 10$^{4}$ per successful
conversion, and thus having as little futile collisions as possible
greatly enhances the overall rate of the reaction. Enzymes approaching
(operating at) the diffusion limit are also called *perfect* enzymes.
Currently there are no enzymes reported which are considerably "above"
diffusion limit (see [@DavidiLongo2018] for an in-depth discussion),
suggesting the universality of the underlying constraint. Nonetheless,
cells do have a strategy to counter the diffusion limit. Consecutive
enzymes from a pathway can be placed on a scaffold, which allows the
product of one reaction to be channeled directly into the next reaction
without diffusing away.

Another aspect to consider is the density, or sum concentration of
molecules, of the fluid. As described in previous sections, cell cytosol
contains a spectrum of different molecules at different sizes and
concentrations. We normally assume that some sort of optimal cell
density that maximizes fitness exists, however, the density is known to
fluctuate substantially in time and across conditions
[@OdermattMiettinen2021]. One of the most prevalent properties, linked
to cytosolic density, is *macromolecular crowding*. As the name
suggests, it describes the concentration of biological macromolecules,
mainly proteins, in cytosol (thus in bacteria, the genomic DNA also
contributes to molecular crowding). For example, the macromolecular
crowding is suggested to impose a limit on the protein translation
[@KlumppScott2013], therefore, increased crowding would result in a
growth rate decrease. The state of macromolecular crowding is relevant
for the cellular function, and is proposed to be in homeostasis
(reviewed in [@VanBergBoersma2017]): optimal macromolecular crowding
corresponds to a state where crowding reduces the path proteins have to
diffuse, yet does not substantially decrease the speed of diffusion. In
such a way, maintaining high macromolecular crowding is suggested to
maximize reaction rates in the cytosol [@DillGhosh2011].

## Concluding remarks

In this chapter, we discussed the properties and the quantities of the
main cellular components, how the composition changes in different
environmental conditions, and what resources are needed for a cell to
replicate itself. It may seem that we already have a vast amount of
data, but a lot is still missing. Most available data comes from model
organisms such as *E. coli*, *S. cerevisiae*, or humans, but the data
for other organisms is still limited. Single-cell data (ideally with
subcellular resolution) is also not widely available. Even though we can
sequence a genome within a few hours or days, we still do not know the
functions of many genes. Many experiments still need to be done, and new
high-throughput experimental methods developed to fill the gaps in our
knowledge.

Nevertheless, with the basic knowledge from this chapter, we can dive
deeper into studying cellular economics and resource allocation with
mathematical modeling. How is biomass represented in mathematical
models? Often, models only focus on proteome as it is a cell's most
abundant and expensive component. However, some models also include
other major components (RNA, DNA, lipids, carbohydrates, cofactors,
etc.). The components can be modeled at different levels of detail. For
example, the cell proteome can be represented simply as a total
proteome, divided into protein subgroups (e.g. metabolic, ribosomal,
other), or modeled as individual proteins. Finally, there are two
contrasting ways to include biomass in mathematical models. On the one
hand, some models consider a fixed biomass composition based on
measurements or literature (see Chapters  and ). On the other hand, some
models *predict* the biomass composition (i.e. they calculate optimal
resource allocation or enumerate all possible compositions, see
Chapter ).

Apart from biomass composition, we can include other cellular properties
as constraints or parameters in the models, depending on the type of a
model and how detailed it is. For example, we can constrain the
transcription/translation rates, enzyme turnover rates, cell surface
area or volume.

In conclusion, this chapter introduced the basic building blocks of a
cell, processes that make them, how they are coordinated and how they
depend on environmental conditions. In the next chapters you will learn
how to translate this information into mathematical models and how to
use them to gain deeper knowledge of cell biology.

## Recommended readings {#recommended-readings .unnumbered}

##### Cell biology

- Alberts, B., et al. (2022). Molecular Biology of the Cell. WW Norton &
  Co.

##### Numbers in cell biology

- Moran, U., Phillips, R., & Milo, R. (2010). SnapShot: key numbers in
  biology. Cell, 141(7), 1262-1262.

- Milo, R., & Phillips, R. (2015). Cell biology by the numbers. Garland
  Science.

## Problems {#problems .unnumbered}

::: exercise
[]{#CEN:Exerc:intuition label="CEN:Exerc:intuition"}

Try to answer the following questions, and only then look up the
results:

- What is the volume of a cell?

- What is the size of a protein?

- What is bigger, a protein or the mRNA that encoded it?

- How many protein molecules are there in a cell?

- What is the number of genes in a genome?

- How long does it take to transcribe a gene?

- How long does it take to produce a protein molecule?

- What is the minimal doubling time of a cell?

- What other questions come to your mind?

Precise values do not matter here -- think about orders of magnitude.
:::

:::: exercise
[]{#CEN:Exerc:proteins label="CEN:Exerc:proteins"}

How many proteins are there in a bacterial/yeast/mammalian cell
[@MiloPhillips2015]? Use data from the following table:

::: center
  ----------------------------- -----------------------------
  Protein mass per volume       $0.2$ g mL^−1^
  Molecular mass of a protein   $40000$ g mol^−1^
  Avogadro's number             $6 \cdot 10^{23}$ 1 mol^−1^
  *E. coli* volume              $1$ μm^3^
  *S. cerevisiae* volume        $60$ μm^3^
  Mammalian cell volume         $3000$ μm^3^
  ----------------------------- -----------------------------
:::
::::

::: exercise
[]{#CEN:Exerc:proteinsribosomes label="CEN:Exerc:proteinsribosomes"}

A typical protein has a volume of 25 nm^3^ (BNID 101828) and a ribosome
3400 nm^3^ (BNID 104919). Given that 70% of a cell volume is water, what
is the maximum number of protein/ribosome molecules that fit into a
typical *E. coli* cell (see
Table [\[CEN:Exerc:proteins\]](#CEN:Exerc:proteins){reference-type="ref"
reference="CEN:Exerc:proteins"})? Compare your answers with the previous
problem/values in BioNumbers database.
:::

:::: exercise
[]{#CEN:Exerc:density label="CEN:Exerc:density"}

Calculate the buoyant density of a typical bacteria using the following
data:

::: center
  Component       Density (g mL^−1^)   Mass fraction per cell
  --------------- -------------------- ------------------------
  Water           $1$                  $0.7$
  Proteins        $1.3$                $0.18$
  Nucleic acids   $1.7$                $0.08$
  Lipids          $1$                  $0.03$
  Carbohydrates   $1.5$                $0.01$
:::
::::

::: exercise
[]{#CEN:exercise:metabolite label="CEN:exercise:metabolite"}

Dourado *et al.* [@DouradoMori2021] suggested that there is a
relationship between the concentrations of enzymes and their substrates
in *E. coli*, which is a result of a constraint on the biomass density.
They showed that the reaction flux is maximal when the dry mass of each
substrate is equal to the dry mass of the unsaturated (free) enzyme.
What is the concentration of one enzyme per cell for *E. coli* (in
mol L^−1^)? What would be the optimal concentration of its substrate?
Use protein mass and cell volume from Problem
[\[CEN:Exerc:proteins\]](#CEN:Exerc:proteins){reference-type="ref"
reference="CEN:Exerc:proteins"} and the mass of glucose as substrate.
:::

::: exercise
[]{#CEN:exercise:size label="CEN:exercise:size"}

Imagine a spherical cell that increases its diameter from 1 to 2μm. How
much do the surface area, volume, and SA/V change? Think about how this
could influence the import of nutrients and the diffusion across the
cell.
:::

::: exercise
[]{#CEN:exercise:aliens label="CEN:exercise:aliens"}

Imagine alien lifeforms. Would they be composed of cells? Why? What
features of cells could be completely different? What features are so
much dictated by physics that they could not be different in any type of
alien cell?
:::

::: exercise
[]{#CEN:exercise:substrateNeeds label="CEN:exercise:substrateNeeds"}

Take the following rate law: $\flux = \vmax \frac{S}{\km + S}$ (also
known as irreversible Michaelis-Menten rate law, see Chapter ), where
$\vmax$ is the maximal reaction velocity. Plug in the values for $\flux$
and compare the substrate concentration needed for the reaction rate to
increase from (i) 10% to (ii) 90% of the maximal rate $\vmax$. Hint:
express the $S$ in terms of $\km$ and take the ratio.
:::
