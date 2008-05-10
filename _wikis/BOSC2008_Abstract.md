---
title: BOSC2008 Abstract
---

BOSC2008 Abstract
-----------------

### General information

**Paper Title:** BioJava Project Update

**Student Paper?** No

### Author(s) Information

#### Author \#1

**Name:**

**Organization:**

**Country:**

**Email:**

#### Author \#2

**Name:**

**Organization:**

**Country:**

**Email:**

#### Author \#3

**Name:**

**Organization:**

**Country:**

**Email:**

#### Author \#4

**Name:**

**Organization:**

**Country:**

**Email:**

#### Author \#5

**Name:**

**Organization:**

**Country:**

**Email:**

**Additional Authors:**

### Contact Author

**Contact Author:** Author \#1

**Alternate Email:** xxx

**Telephone:** xxx

### Technical Areas

Bio \* Open Source Project Updates

Lightning Talks ?

### Content

**Keywords:**

OBF open-bio biojava bioperl biosql sequence alphabet feature annotation
alignment protein structure phylogenetic trees

**Abstract:**

The small Abstract text should be a summary, while the longer abstract
should provide more details, including the open-source license
requirement details.

Copied from BioJavaBioinformatics.odt
[1](http://code.open-bio.org/svnweb/index.cgi/biojava/browse/biojava-paper?rev=4751)
abstract summary with minor revision:

BioJava is a mature Open Source project that provides a framework for
processing of biological data. BioJava provides tools for parsing common
file formats, manipulating sequences and 3D structures. Powerful
analysis and statistical routines enable the rapid bioinformatics
application development in the Java programming language
[[2](http://java.sun.com)](http://java.sun.com). Here we present the
latest BioJava release (version 1.6, released on 13 Apr 2008) which
provides improvements in the packages for phylogenetic trees, processing
PDB files, and genetic algorithms.

The second sentence needs further revision, an additional clause
perhaps.

**Paper:**

Full-length abstracts are limited to one page with one inch (2.5 cm)
margins on the top, sides, and bottom. The full-length abstract should
include the title, authors, and affiliations.

I have added myself to the author's list from the application note near
the end. Hopefully this is reasonable to the other authors.

BioJava Project Update

Holland, R.C.G.<sup>1</sup>, Down, T.<sup>2</sup>, Pocock,
M.<sup>3</sup>, Prlic, A.<sup>4</sup>, Huen D.<sup>5</sup>, James
K.<sup>4</sup>, Foisy, S.<sup>6</sup>, Dräger, A.<sup>7</sup>, Yates,
A.<sup>1</sup>, Heuer M.<sup>8</sup>, and Schreiber, M.J.<sup>9</sup>

<sup>1</sup> European Bioinformatics Institute (EMBL-EBI), Genome
Campus, Hinxton, Cambridgeshire CB10 1SD, UK <sup>2</sup> Wellcome
Trust/Cancer Research UK Gurdon Institute, Cambridge CB2 1QN, UK
<sup>3</sup> University Newcaste Upon Tyne, Newcastle Upon Tyne, NE1
7RU, UK <sup>4</sup> Wellcome Trust Sanger Institute, Genome Campus,
Hinxton, Cambridgeshire CB10 1SA, UK <sup>5</sup> Department of
Genetics, University of Cambridge, Cambridge CB2 3EH, UK <sup>6</sup>
Laboratory in Genetics and Genomic Medicine of Inflammation, Montreal,
Canada. <sup>7</sup> Eberhard Karls University Tübingen, Center for
Bioinformatics (ZBIT), Germany <sup>8</sup> Harbinger Partners, Inc.,
St. Paul, Minnesota, USA <sup>9</sup> Novartis Institute for Tropical
Diseases, 10 Biopolis Road, Chromos \#05-01, Singapore 138670

Notes
-----

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

Estimated effort using COCOMO [3](http://en.wikipedia.org/wiki/COCOMO)
metric: 47 Person Years

48 contributors (committers with at least one commit to cvs and/or
subversion repository)

also compare with:

BioJava StatSVN:
[<http://www.spice-3d.org/statsvn/stats/>](http://www.spice-3d.org/statsvn/stats/)

**First commit**

This commit was generated by cvs2svn to compensate for changes in r2,
which included commits to RCS files with non-trunk default branches.

by birney on 2000-01-26 15:53 (over 8 years ago)

Interesting to find out what happened before this administrative commit,
as there were 6539 lines of code already.

**Last commit**

started to develop a mmcif parser

by Andreas.Prlic (Using name ‘andreas’) on 2008-04-28 07:27 (11 days
ago)

**BioJava group on LinkedIn**

There is a BioJava group on LinkedIn:

Developers of the BioJava open-source bioinformatics project.

Not sure how to link to it though.