---
title: BioJava3 Design
---

**Not current**

The content on this page was used during the development of the BioJava
3. BioJava 3 has been released on December 28th 2010. The latest release
is available from <BioJava:Download>

Implementation
--------------

For information on the current status of the BioJava 3 implementation go
to [BioJava3\_project](/wikis/BioJava3_project "wikilink")

References
----------

This document was based on comments made on the following pages:

-   <http://biojava.org/wiki/BioJava3_Proposal>
-   <http://biojava.org/wiki/Talk:BioJava3_Proposal>
-   <http://biojava.org/wiki/UsageAnalysis>
-   <http://www.derkholm.net/svn/repos/bjv2/website/docs/index.html>

Basic principles
----------------

-   BioJava3 (BJ3) will freely incorporate features from Java 6.
-   Maven will be used to build the project.
-   Full unit testing for every aspect from the ground up using JUnit.
-   Modular design without any cyclic dependencies, with separate JARs
    for key components (IO, databases, genetic algorithms, sequence
    manipulation, etc.)
-   Separation of APIs from implementation code by means of packages.
-   Base package name: org.biojava3 (to prevent clashes with org.biojava
    and org.biojavax, both of which will have backwards-compatibility
    extensions to BJ3 in order to make old code reusable).
-   Use of JavaBeans concepts wherever possible, e.g. getters/setters.
    This would enhance Java EE compliance and improve integration into
    larger things. DON'T do this where immutability is key to efficiency
    though, like with Strings.
-   Fully commented code in LOTS of detail INCLUDING package-level docs
    AND wiki-docs such as the cookbook.
-   Use of annotations for things like database mappings.
-   A consistent coding style to be developed and applied.
-   No Swing code to be included, but graphics code is OK for obviously
    useful things such as protein structures or sequence traces. Swing
    code is impossible to write in a way that will integrate fully with
    each different individual's own program requirements.
-   Keep It Simple Stupid (KISS) - don't object-ify things unless
    absolutely necessary. Sequences are perfectly happy as Strings
    unless you want to do complex things like store base quality
    information, and only at that point should you want to convert them
    into more complex object models.
-   Separation of functionality - don't make sequences load features,
    and don't make features load their sequence by default. This saves
    memory and allows work to be done independently on the specific
    parts of interest.
-   Always ALWAYS correctly implement equals, compareTo, hashCode, and
    Serializable wherever possible.
-   Any general-use methods to be exposed via SPI (e.g.
    getTopBlastHit()).
-   The source code license will be the GNU Lesser General Public
    License (LGPL) "version 2.1 or any later version".
-   In general BJ3 exceptions should be RuntimeExceptions and unchecked.
    They should also be well documented and give useful messages. It
    should be up to the developer to decide what to capture and what not
    to. In the current BioJava there are way to many exceptions that
    can't really happen under any normal circumstances. We should only
    need to think about exceptions in exceptional circumstances.
-   The default Java logging API should be used extensively. This will
    allow a developer the ability to fine tune debugging. The core
    module should have a logging helper with static convenience methods
    to make it very easy to liberally use logging calls via static
    imports.

Compromises and Unfinished bits
-------------------------------

-   TestNG was suggested instead of JUnit, but knowledge of this tool is
    not so widespread and this may impact on quality of testing.
-   A tool for analysing comment coverage and coding style was
    suggested, but none have been identified. Please amend this document
    with the names of any good ones you know.

[Jalopy <http://jalopy.sourceforge.net/>] - can be used as Eclipse
plugin, or Ant task.  
[Cobertura <http://cobertura.sf.net>] - can be used to assess JUnit test
coverage.  
[FindBugs <http://findbugs.sf.net>] - does static analysis of code (also
runnable as Eclipse plugin or Ant task.

Priorities
----------

Andreas' very useful Usage Analysis page shows the most frequently
requested documentation. In the absence of any real usage statistics, we
must assume that the things people most often want to read about are the
things that people most often use. (It could also be said that the
things that people most read about are the things that work least well
in the present code... but we shall ignore that for now...).

Here are the priorities based on Andreas' work:

-   How to get an Alphabet
-   How to make a Sequence Object from a String or make a Sequence
    Object back into a String
-   How to parse a Blast output
-   How to read sequences from a Fasta file
-   How to read a GenBank, SwissProt or EMBL file
-   How to generate a global or local alignment with the
    Needleman-Wunsch- or the Smith-Waterman-algorithm
-   How to read a protein structure - PDB file
-   How to export a sequence to fasta
-   How to view a sequence in a gui
-   How to parse a Fasta database search output file

These can be broken down into the following modules:

-   Plain sequence \<-\> Enriched sequence
-   Sequence similarity -\> Sequence similarity IO (Blast, Fasta, etc.)
-   Plain sequence -\> Plain sequence IO (Genbank, FASTA, etc.)
-   Enriched sequence -\> Sequence alignments
-   Enriched sequence -\> Protein structures

Module structure
----------------

-   BioJava3 module
    -   API module contains object builder signature (builder builds
        objects from events, much like a SAX parser does).
    -   Listeners can choose to cache data in memory, on disk, keep a
        pointer to the source and read it back later, or whatever. Up to
        them. Optimisation becomes easier this way as listeners can
        choose exactly what to keep in memory and what not to.

<!-- -->

-   Sequence module
    -   API module defines entire BioJava sequence object model (similar
        to current one but allowing for non-symbol based sequences and
        separation of sequences from features).
    -   API has subclasses of object builders for sequences. Builder can
        specify it is only interested in certain events, and parsers can
        query this to optimise parsing by skipping irrelevant sections.
    -   Conversion to symbol-based sequences on demand to/from strings.
    -   Simplified alphabet concept, made easier by avoiding use of XMLs
        to configure them.
    -   WATCH OUT for localised strings when manipulating sequences.
    -   WATCH OUT for singletons and multi-processor environments.
        Consider using JNDI if they are absolutely necessary.

<!-- -->

-   Feature module
    -   API module defines entire BioJava feature object model (similar
        to current one but allowing for separation of sequences from
        features).
    -   API has subclasses of object builders for features. Builder can
        specify it is only interested in certain events, and parsers can
        query this to optimise parsing by skipping irrelevant sections.
    -   Allow feature naming using any of the standard ontologies.

<!-- -->

-   IO module
    -   API module contains basic read() and write() function
        signatures.
    -   API has concept of RecordSource which is either a file, a group
        of files (e.g. directory), a database, a web service, etc. - all
        of which implement some kind of RecordProvider interface for
        iterating over objects. Those objects can be sequences,
        features, etc.
    -   Implementation module - one per sequence format - e.g. Genbank,
        FASTA, etc.
    -   Use of event listeners to fire events at an object builder.
    -   Each implementation has default object model and builder that
        exactly matches that format, along with a converter that will
        'read' the object model and fire events as if it was being read
        again (to allow for conversion to other formats via the listener
        framework).
    -   BioSQL is an IO module. So are other dbs, e.g. Entrez, ebEye.
    -   A RecordSearch API to be implemented to search for matching
        records in any RecordSource.
    -   LazyLoading where possible.
    -   Input AND Output achieved by SAX-like event firing. Reading a
        file fires events at an object builder containing bits of data
        as they are read. Writing a file causes an object parser to
        parse an object and fire events at a file writer. Any listener
        can listen to any other source of events, so you can
        short-circuit file conversion by reading GenBank and specifying
        the reader-listener as an instance of a FASTA writer-listener.
    -   RecordSources to be versioned to cope with changing formats over
        time.
    -   Each IO module to be entirely independent and agnostic of the
        way it is used. This allows modules to optimise themselves for
        random access etc., if they see fit. By using the methods on the
        API to check what the listener is interested in receiving, they
        can also cut out the work of parsing uninteresting stuff.

<!-- -->

-   Other modules
    -   Ontology handling.
    -   Protein structure
    -   Microarray analysis
    -   Phylogenetics
    -   etc. etc. etc.

Use cases
---------

It is planned to document BioJava in parallel with development. To do
this, we want to drive development from a set of [ use
cases](/wikis/BioJava 3 Use Cases "wikilink").
