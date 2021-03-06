---
title: BOSC2008 Abstract
---

BOSC2008 Abstract
-----------------

The abstract was submitted as appears below. Please send an email to the
biojava-dev mailing list with any further changes to be made.

[BOSC2008\_Abstract.odt](http://shore.net/~heuermh/BOSC2008_Abstract.odt)

[BOSC2008\_Abstract.pdf](http://shore.net/~heuermh/BOSC2008_Abstract.pdf)

### General information

**Paper Title:** BioJava Project Update

**Student Paper?** No

### Author(s) Information

### Technical Areas

Bio \* Open Source Project Updates

### Content

**Keywords:**

OBF O|B|F open-bio biojava bioperl biosql sequence alphabet feature
annotation alignment protein structure phylogenetic trees

**Abstract:**

BioJava is a mature free and open-source project that provides a
framework for processing biological data. BioJava contains powerful
analysis and statistical routines, tools for parsing common file
formats, and packages for manipulating sequences and 3D structures.
BioJava is available freely under the terms of version 2.1 of the GNU
Lesser General Public License (LGPL) from <http://biojava.org/>. Here we
present the latest BioJava release (version 1.6, released on 13 Apr
2008) which provides improvements in the packages for phylogenetic
trees, processing PDB files, and genetic algorithms.

**Paper:**

BioJava Project Update

BioJava was conceived in 1999 by Thomas Down and Matthew Pocock as an
API to simplify bioinformatics software development using Java (Pocock
et al., 2000). It has since then evolved to become a fully-featured
framework with modules for performing many common bioinformatics tasks.

As a free and open-source project, BioJava is developed by volunteers
coordinated by the Open Bioinformatics Foundation (O|B|F,
<http://open-bio.org/>) and is one of several Bio\* toolkits (Mangalam,
2002). Over the past eight years, the BioJava has brought together
nearly fifty different code contributors, hundreds of mailing list
subscribers, and several wiki contributors. All code and related
documentation is distributed under version 2.1 of the GNU Lesser General
Public License (LGPL) license (Free Software Foundation, Inc., 1999).
All wiki documentation is made available online under version 1.2 of the
GNU Free Documentation License (Free Software Foundation, Inc., 2000).

BioJava has been used in a number of real-world applications, including
Bioclipse (Spjuth et al., 2007), BioWeka (Gewehr et al., 2007),
Cytoscape (Shannon et al., 2003), and Taverna (Oinn et al., 2004), and
has been referenced in over fifty published studies. A list of these can
be found on the BioJava website.

The latest BioJava release (version 1.6, released on 13 Apr 2008) offers
more functionality and stability over the previous official releases.
The phylogenomics package was improved and expanded by our 2007 Google
Summer of Code (GSOC'07) student Boh-Yun Lee. It now contains
fully-functional Nexus and Phylip parsers, and tools for calculating
UPGMA and Neighbour Joining, Jukes-Kantor and Kimura Two Parameter, and
MP. The PDB file parser was improved by Jules Jacobsen for better
dealing with PDB header records. Andreas Dräger provided several patches
for improving the genetic algorithm packages. The version 1.6 release
also contains numerous bug fixes and documentation improvements.

The BioJava website is <http://biojava.org/>. The version 1.6 release
can be downloaded from <http://biojava.org/wiki/BioJava:Download>.

**References**

Free Software Foundation, Inc. (1999) GNU Lesser General Public License,
version 2.1, <http://www.gnu.org/licenses/old-licenses/lgpl-2.1.html>,
accessed 10 May 2008.

Free Software Foundation, Inc. (2000) GNU Free Documentation License,
version 1.2, <http://www.gnu.org/licenses/fdl-1.2.html>, accessed 10 May
2008.

Gewehr JE, Szugat M, Zimmer R. (2007) BioWeka—extending the Weka
framework for bioinformatics Bioinformatics 2007 23(5):651-653.

Mangalam H. (2002) The Bio\* toolkits – a brief overview. Brief
Bioinform., 3, 396-302.

Oinn T, Addis M, Ferris J, Marvin D, Greenwood M, Carver T, Pocock MR,
Wipat A, Li P. (2004) Taverna: a tool for the composition and enactment
of bioinformatics workflows. Bioinformatics, 20, 3045–3054.

Pocock M, Down T, Hubbard T. (2000) BioJava: Open Source Components for
Bioinformatics. ACM SIGBIO Newsletter 20(2), 10-12.

Shannon P, Markiel A, Ozier O, Baliga NS, Wang JT, Ramage D, Amin N,
Schwikowski B, Ideker T. (2003) Cytoscape: a software environment for
integrated models of biomolecular interaction networks. Genome Research
2003 Nov; 13(11):2498-504.

Spjuth O, Helmus T, Willighagen EL, Kuhn S, Eklund M, Wagener J,
Murray-Rust P, Steinbeck C, Wikberg JE. (2007) Bioclipse: an open source
workbench for chemo- and bioinformatics. BMC Bioinformatics. 2007 Feb
22;8:59.

Notes
-----

**Save for talk**

As a mature project, BioJava faces several challenges:

how one deals with a large established code base

what happens when committers move on, get married, have kids, etc.

how difficult it is to deprecate and remove existing code

the BioJava3 use case & refactoring/redesign criteria gathering process

evolutionary vs. revolutionary changes

<http://incubator.apache.org/learn/rules-for-revolutionaries.html>

the "second system" problem

<http://www.joelonsoftware.com/articles/fog0000000069.html>

**Version 1.6 release announcement to biojava-dev and biojava-l**

Date: Sun, 13 Apr 2008 19:02:41 +0100  
From: Andreas Prlic  
To: biojava-dev at biojava.org, biojava-l at biojava.org  
Subject: [Biojava-dev] biojava 1.6 released  
 Biojava 1.6 has been released and is available from <http://>
biojava.org/wiki/BioJava:Download

Biojava 1.6 offers more functionality and stability over the previous
official releases. BioJava now depends on Java 1.5+. We highly recommend
you to upgrade as soon as possible.

In detail, the phylo package org.biojavax.bio.phylo was improved and
expanded by our GSOC'07 student Boh-Yun Lee. It now contains fully-
functional Nexus and Phylip parsers, and tools for calculating UPGMA and
Neighbour Joining, Jukes-Kantor and Kimura Two Parameter, and MP. It
uses JGraphT to represent parsed trees.

The PDB file parser was improved by Jules Jacobsen for better dealing
with PDB header records. Andreas Draeger provided several patches for
improving the Genetic Algorithm modules. Additionally this release
contains numerous bug fixes and documentation improvements.

Thanks to the entire biojava community for making this possible!

Happy Biojava-ing,

Andreas

From
[<http://www.ohloh.net/projects/6798>](http://www.ohloh.net/projects/6798)

**As of 08 May 2008**

181,197 lines of code in "biojava-live/trunk"

Estimated effort using COCOMO [1](http://en.wikipedia.org/wiki/COCOMO)
metric: 47 Person Years

48 contributors (committers with at least one commit to cvs and/or
subversion repository)

also compare with:

BioJava StatSVN:
[<http://www.spice-3d.org/statsvn/stats/>](http://www.spice-3d.org/statsvn/stats/)

top 10 authors:

    mrp     114161 (25.5%)
    thomasd 82637 (18.5%)
    holland 58798 (13.1%)
    kdj     43546 (9.7%)
    andreas 40727 (9.1%)
    mark_s  36616 (8.2%)
    dhuen   25610 (5.7%)
    gcox    5954 (1.3%)
    birney  4087 (0.9%)
    draeger 3994 (0.9%)

**First commit**

This commit was generated by cvs2svn to compensate for changes in r2,
which included commits to RCS files with non-trunk default branches.

by birney on 2000-01-26 15:53 (over 8 years ago)

Interesting to find out what happened before this administrative commit,
as there were 6539 lines of code already.

Statsvn lists the files that were addded in the first commit:

        4087 lines of code changed in:

            * org/biojava/bio: BioError.java (new 92), BioException.java (new 88)
            * org/biojava/bio/alignment: AbstractCursor.java (new), AbstractState.java (new 1), AbstractTrainer.java (new), Alignment.java (new 29), AmbiguityState.java (new), BaumWelchSampler.java (new), BaumWelchTrainer.java (new), Column.java (new), ComplementaryState.java (new), DNAState.java (new), DNAWeightMatrix.java (new), DP.java (new 10), DPCursor.java (new), DoubleAlphabet.java (new), EmissionState.java (new), FlatModel.java (new), IllegalTransitionException.java (new), MarkovModel.java (new), MarkovModelWrapper.java (new), MatrixCursor.java (new), ModelInState.java (new), ModelTrainer.java (new), SimpleAlignment.java (new 77), SimpleMarkovModel.java (new 3), SimpleModelInState.java (new), SimpleModelTrainer.java (new), SimpleState.java (new), SimpleStateLabeledSequence.java (new), SimpleStateTrainer.java (new), SimpleTransitionTrainer.java (new), SimpleWeightMatrix.java (new), SmallCursor.java (new), State.java (new), StateFactory.java (new), StateLabeledSequence.java (new), StateTrainer.java (new), StateWrapper.java (new), StoppingCriteria.java (new), SuffixTree.java (new 35), TrainerTransition.java (new), TrainingAlgorithm.java (new), Transition.java (new), TransitionTrainer.java (new), WMAsMM.java (new), WeightMatrix.java (new), WeightMatrixAnnotator.java (new 23), XmlMarkovModel.java (new)
            * org/biojava/bio/gui: BarLogoPainter.java (new 85), DNAStyle.java (new 84), LogoPainter.java (new 45), PlainStyle.java (new 56), ResidueStyle.java (new), StateLogo.java (new 7), TextLogoPainter.java (new 209)
            * org/biojava/bio/program: Meme.java (new 151)
            * org/biojava/bio/seq: AbstractAlphabet.java (new), AllSymbolsAlphabet.java (new), Alphabet.java (new 4), Annotatable.java (new 1), Annotation.java (new 2), Annotator.java (new 5), CompoundLocation.java (new 2), Feature.java (new 66), FeatureFactory.java (new), FeatureFilter.java (new 81), FeatureHolder.java (new 34), FixedWidthParser.java (new), HashSequenceDB.java (new 1), IllegalResidueException.java (new), Location.java (new 7), NameParser.java (new), PointLocation.java (new 2), RangeLocation.java (new), Residue.java (new), ResidueList.java (new), ResidueParser.java (new), SeqException.java (new), Sequence.java (new 63), SequenceDB.java (new), SequenceFactory.java (new 28), SequenceIterator.java (new 33), SimpleAlphabet.java (new), SimpleAnnotation.java (new), SimpleFeature.java (new 14), SimpleFeatureFactory.java (new), SimpleFeatureHolder.java (new 65), SimpleResidue.java (new 1), SimpleResidueList.java (new 2), SimpleSequence.java (new 1), SimpleSequenceFactory.java (new), SymbolParser.java (new)
            * org/biojava/bio/seq/io: DefaultDescriptionReader.java (new), EmblFormat.java (new 60), FastaDescriptionReader.java (new), FastaFormat.java (new 109), SequenceFormat.java (new 37), StreamReader.java (new 93), StreamWriter.java (new 50)
            * org/biojava/bio/seq/tools: AlphabetManager.java (new 1), DNATools.java (new)
            * org/biojava/stats/svm: LinearKernel.java (new 37), ListSumKernel.java (new 74), PolynomialKernel.java (new 89), RadialBaseKernel.java (new 67), SMORegressionTrainer.java (new 429), SMOTrainer.java (new 283), SVMKernel.java (new 39), SVMModel.java (new), SVMRegressionModel.java (new 170), SigmoidKernel.java (new 83), SparseVector.java (new 113), TrainingContext.java (new 31), TrainingEvent.java (new 39), TrainingListener.java (new 34)
            * org/biojava/stats/svm/tools: ClassifierExample.java (new 387), Classify.java (new 80), SVM_Light.java (new 199), Train.java (new 90), TrainRegression.java (new 86)
            * org/biojava/utils/xml: XMLDispatcher.java (new), XMLPeerBuilder.java (new), XMLPeerFactory.java (new)

**Latest commit**

started to develop a mmcif parser

by Andreas.Prlic (Using name ‘andreas’) on 2008-04-28 07:27 (11 days
ago)

**BioJava group on LinkedIn**

There is a BioJava group on LinkedIn:

Developers of the BioJava open-source bioinformatics project.

Not sure how to link to it though.

To join the BioJava linkedin group: You need to be a linkedin member.
You then need to find the group and ask to join. I then get notified and
asked to approve it, which I will if your name sounds vaguely familiar :
) You don't need to be a contributor just a user or interested
party. --[Mark](User:Mark "wikilink") 14:39, 22 May 2008 (UTC)

**Wiki edits for later**

Clarify reference to LGPL.

Update references to "open source" with "free and open source". Link to
FOSS page on wikipedia?

DengueInfo link on BioJavaInside is broken.

BioJava in Anger is now on the wiki (so under FDL?) but has a separate
vague Copyright section, see
<http://biojava.org/wiki/BioJava:CookBook#Copyright>

This copyright section is a direct copy from the old BioJava in Anger
page. This means the statement is outdated and can probably be
removed. --[Mark](User:Mark "wikilink") 14:39, 22 May 2008 (UTC)
