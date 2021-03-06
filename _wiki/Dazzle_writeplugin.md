---
title: Dazzle:writeplugin
permalink: wiki/Dazzle%3Awriteplugin
---

How to write your own Dazzle plugin
===================================

Each plugin for [Dazzle](Dazzle "wikilink") has to implement certain
interfaces. Here we will show how to implement a Dazzle plugin that
supports the DAS - features command, using the GFFFeatureSource
interface. There are also other plugin mechanisms in Dazzle, but for the
moment let's only consider this one.

Required knowledge
------------------

For this turorial you should already know how to [deploy
Dazzle](Dazzle:deployment "wikilink")

The GFFFeatureSource interface
------------------------------

The Interface that needs to be implemented is the
[GFFFeatureSource](http://www.derkholm.net/svn/repos/dazzle/trunk/src/org/biojava/servlets/dazzle/datasource/GFFFeatureSource.java)
interface.

What this means is that the DAS source provides a method called

`GFFFeature getFeatures(String reference);`

This method accepts a String as an argument, that represents either the
chromosomal region or the accession code that is requested. It returns
an array of
[GFFFeature](http://www.derkholm.net/svn/repos/dazzle/trunk/src/org/biojava/servlets/dazzle/datasource/GFFFeature.java)
objects that contain the data that should be transported.

When Dazzle gets a DAS - Features request for your DAS source, it will
call this getFeatures method in order to obtain the data and then return
it as DAS-XML.

The AbstractGFFFeatureSource class
----------------------------------

For full DAS-specification support a couple of more methods are
required, but they do not need to worry us right now, since there is a
utility class available that contains most of the required code already.
Your plugin simply needs to extend
[AbstractGFFFeatureSource](http://www.derkholm.net/svn/repos/dazzle/trunk/src/org/biojava/servlets/dazzle/datasource/AbstractGFFFeatureSource.java).

A minimal plugin
----------------

A minimal plugin for Dazzle looks like this: let's call the file below
MyPlugin.java <java> package org.dazzle;

import org.biojava.servlets.dazzle.datasource.AbstractGFFFeatureSource;
import org.biojava.servlets.dazzle.datasource.DataSourceException;
import org.biojava.servlets.dazzle.datasource.GFFFeature;

public class MyPlugin extends AbstractGFFFeatureSource {

`   public GFFFeature[] getFeatures(String reference) `  
`   throws DataSourceException{`  
`       System.out.println("got a features request for " + reference);`  
`       return new GFFFeature[0];`  
`   }`

} </java>

and to enable this in Dazzle we add the following lines to
**dazzlecfg.xml** :

     <datasource id="myplugin" jclass="org.dazzle.MyPlugin">
        <string name="name" value="My 1st Plugin" />
        <string name="description" value="a demo for how to write a Dazzle plugin" />
        <string name="version" value="1.0" />
      </datasource>

### DAS - DSN request

Start your Dazzle instance. If you don't know how you should do that,
please see <Dazzle:deployment>. Once Dazzle is running you can do the
DAS - dsn (data source names) command, which lists all available
datasources.

[`http://localhost:8080/dazzleDemo/dsn`](http://localhost:8080/dazzleDemo/dsn)

note: Dazzle provides XSL stylesheets for a nice display of the XML
response in your browser. To view the raw XML source code in the Firefox
browser, add view-source: in front of the URL.

[`view-source:http://localhost:8080/dazzleDemo/dsn`](view-source:http://localhost:8080/dazzleDemo/dsn)

You should get this response if you called your servlet dazzleDemo and
your [basic Dazzle installation](Dazzle:deployment "wikilink") is
correct:

<xml>

<?xml version='1.0' standalone='no' ?>
<?xml-stylesheet type="text/xsl" href="das.xsl"?>
<!DOCTYPE DASDSN SYSTEM 'dasdsn.dtd' >
<DASDSN>

` `<DSN>  
`   `

    My 1st Plugin

`   `<MAPMASTER>[`http://localhost:8080/dazzleDemo/myplugin/`](http://localhost:8080/dazzleDemo/myplugin/)</MAPMASTER>  
`   `<DESCRIPTION>`a demo for how to write a Dazzle plugin`</DESCRIPTION>  
` `</DSN>

` `<DSN>  
`   `

    Test seqs

`   `<MAPMASTER>[`http://localhost:8080/dazzleDemo/test/`](http://localhost:8080/dazzleDemo/test/)</MAPMASTER>  
`   `<DESCRIPTION>`Test set for promoter-finding software`</DESCRIPTION>  
` `</DSN>

` `<DSN>  
`   `

    TSS

`   `<MAPMASTER>[`http://localhost:8080/das/test/`](http://localhost:8080/das/test/)</MAPMASTER>  
`   `<DESCRIPTION>`Transcription start sites`</DESCRIPTION>  
` `</DSN>

` `<DSN>  
`   `

    uniprot_snps

`   `<MAPMASTER>[`http://localhost:8080/dazzleDemo/uniprot_snps/`](http://localhost:8080/dazzleDemo/uniprot_snps/)</MAPMASTER>  
`   `<DESCRIPTION>`some snps on a uniprot sequence`</DESCRIPTION>  
` `</DSN>

</DASDSN> </xml>

### The DAS features command

Now you can also do a first DAS - features command:

[`http://localhost:8080/dazzleDemo/myplugin/features?segment=123`](http://localhost:8080/dazzleDemo/myplugin/features?segment=123)

should give you now a very simple response, which will not contain
features. (we did not return any, did we?)

Check your server logs it should say something like

`got a features request for 123`

If you see that, you mastered the first step!

Adding Features
---------------

So fare our response does not contain features. Let's add one:

<java> package org.dazzle;

import java.util.ArrayList; import java.util.List; import
org.biojava.servlets.dazzle.datasource.AbstractGFFFeatureSource; import
org.biojava.servlets.dazzle.datasource.DataSourceException; import
org.biojava.servlets.dazzle.datasource.GFFFeature;

public class MyPlugin extends AbstractGFFFeatureSource {

`   public GFFFeature[] getFeatures(String reference) `  
`   throws DataSourceException{`  
`       System.out.println("got a features request for " + reference);`  
`       `  
`       List`<GFFFeature>` features = new ArrayList`<GFFFeature>`();`  
`       `  
`       // This is up to YOU:`  
`       // get your data from somewhere, e.g. a database, parse a flat file`  
`       // whatever you like.`  
`       // then with your data we fill the GFFFeature objects`  
`       `  
`       // GFFFeature is a simple Java-bean`  
`       GFFFeature gff = new GFFFeature();`  
`       `  
`       gff.setType("annotation type");`  
`       gff.setLabel("the annotation label");`  
`       // start and end are strings to support e.g. PDB -file residue `  
`       // numbering, which can contain insertion codes`  
`       gff.setStart("123"); `  
`       gff.setEnd("234");`  
`       `  
`       gff.setName("the name of my feature");`  
`       gff.setMethod("the dazzle plugin tutorial");`  
`       gff.setLink("`[`http://www.biojava.org/wiki/Dazzle:writeplugin`](http://www.biojava.org/wiki/Dazzle:writeplugin)`");`  
`       gff.setNote("the note field contains the actual annotation!");`  
`       `  
`       // see the documentation for GFFFeature for all possible fields`  
`               `  
`       features.add(gff);`  
`           `  
`       // and we return our features `  
`       return (GFFFeature[]) features.toArray(new GFFFeature[features.size()]);`  
`   }`

} </java>

Now will give this response:

<xml>

<?xml version='1.0' standalone='no' ?>
<?xml-stylesheet type="text/xsl" href="das.xsl"?>
<!DOCTYPE DASGFF SYSTEM 'dasgff.dtd' >
<DASGFF>

` `<GFF version="1.0" href="http://localhost:8088/dazzleDemo/myplugin/features?segment=123">  
`   `<SEGMENT id="123" version="" start="1" stop="-1">  
`     `<FEATURE id="__dazzle__annotation type_the name of my feature_123_234" label="the annotation label">  
`       `<TYPE id="annotation type">`annotation type`</TYPE>  
`       `<METHOD id="the dazzle plugin tutorial">`the dazzle plugin tutorial`</METHOD>  
`       `<START>`123`</START>  
`       `<END>`234`</END>  
`       `<SCORE>`-`</SCORE>  
`       `

<NOTE>
the note field contains the actual annotation!

</NOTE>
`       `<LINK href="http://www.biojava.org/wiki/Dazzle:writeplugin">[`http://www.biojava.org/wiki/Dazzle:writeplugin`](http://www.biojava.org/wiki/Dazzle:writeplugin)</LINK>  
`     `</FEATURE>  
`   `</SEGMENT>  
` `</GFF>

</DASGFF> </xml>

Adding more DAS commands
------------------------

No we can already expose our annotations via the DAS - features command.
Our next step is to make this DAS source a reference source for sequence
annotations. For this we need to implement the interface
[DazzleReferenceSource](http://www.derkholm.net/svn/repos/dazzle/trunk/src/org/biojava/servlets/dazzle/datasource/DazzleReferenceSource.java),
which adds support for 2 new DAS commands - entry\_points and sequence.

<java> package org.dazzle;

import java.util.ArrayList; import java.util.List; import
java.util.NoSuchElementException; import java.util.Set; import
java.util.TreeSet; import org.biojava.bio.seq.ProteinTools; import
org.biojava.bio.seq.Sequence; import
org.biojava.bio.symbol.IllegalSymbolException; import
org.biojava.servlets.dazzle.datasource.AbstractGFFFeatureSource; import
org.biojava.servlets.dazzle.datasource.DataSourceException; import
org.biojava.servlets.dazzle.datasource.DazzleReferenceSource; import
org.biojava.servlets.dazzle.datasource.GFFFeature;

public class MyPlugin extends AbstractGFFFeatureSource implements
DazzleReferenceSource{

`   public GFFFeature[] getFeatures(String reference) `  
`   throws DataSourceException{`  
`       System.out.println("got a features request for " + reference);`  
`       `  
`       List`<GFFFeature>` features = new ArrayList`<GFFFeature>`();`  
`       `  
`       // This is up to YOU:`  
`       // get your data from somewhere, e.g. a database, parse a flat file`  
`       // whatever you like.`  
`       // then with your data we fill the GFFFeature objects`  
`       `  
`       // GFFFeature is a simple Java-bean`  
`       GFFFeature gff = new GFFFeature();`  
`       `  
`       gff.setType("annotation type");`  
`       gff.setLabel("the annotation label");`  
`       // start and end are strings to support e.g. PDB -file residue `  
`       // numbering, which can contain insertion codes`  
`       gff.setStart("123"); `  
`       gff.setEnd("234");`  
`       `  
`       gff.setName("the name of my feature");`  
`       gff.setMethod("the dazzle plugin tutorial");`  
`       gff.setLink("`[`http://www.biojava.org/wiki/Dazzle:writeplugin`](http://www.biojava.org/wiki/Dazzle:writeplugin)`");`  
`       gff.setNote("the note field contains the actual annotation!");`  
`       `  
`       // see the documentation for GFFFeature for all possible fields`  
`               `  
`       features.add(gff);`  
`           `  
`       // and we return our features `  
`       return (GFFFeature[]) features.toArray(new GFFFeature[features.size()]);`  
`   }`

`   /** This method deals with the DAS -entry points command.`  
`    * @return a set containing the references to the entry points`  
`    */ `  
`   public Set getEntryPoints() {`  
`       Set`<String>` s = new TreeSet`<String>` ();`  
`       // this example has only one feature.`  
`       // for your real data you might want to add a SQL query here.`  
`       s.add("123");`  
`       return s;`  
`   }`

`   /** This method deals with the DAS - sequence command.`  
`    * `  
`    * @return a biojava Sequence object`  
`    * `  
`    */`  
`   public Sequence getSequence(String ref) throws NoSuchElementException, DataSourceException {`  
`       String seq =  "ECNEUQESECNEUQESECNEUQESECNEUQESECNEUQES";`  
`       `  
`       try {`  
`           Sequence prot = ProteinTools.createProteinSequence(seq, ref);`  
`           return prot;`  
`       } catch ( IllegalSymbolException e){`  
`           throw new DataSourceException(e.getMessage());`  
`       }       `  
`   }`

} </java>

### The DAS entry\_points command

If we forgot which reference points we annotated, we can do a DAS -
entry\_points request:

[`http://localhost:8080/dazzleDemo/myplugin/entry_points`](http://localhost:8080/dazzleDemo/myplugin/entry_points)

now returns: <xml>

<?xml version='1.0' standalone='no' ?>
<?xml-stylesheet type="text/xsl" href="das.xsl"?>
<!DOCTYPE DASEP SYSTEM 'dasep.dtd' >
<DASEP>

` `<ENTRY_POINTS href="http://localhost:8088/dazzleDemo/myplugin/entry_points" version="1.0">  
`   `<SEGMENT id="123" size="-1" subparts="no" />  
` `</ENTRY_POINTS>

</DASEP> </xml>

### The DAS SEQUENCE command

The entry points command showed us that we could use "123" as a
reference (a chromosomal region, or a database accession code) for a
request.

[`http://localhost:8080/dazzleDemo/myplugin/sequence?segment=123`](http://localhost:8080/dazzleDemo/myplugin/sequence?segment=123)

gives the response: <xml>

<?xml version='1.0' standalone='no' ?>
<?xml-stylesheet type="text/xsl" href="das.xsl"?>
<!DOCTYPE DASSEQUENCE SYSTEM 'dassequence.dtd' >
<DASSEQUENCE>

` `<SEQUENCE id="123" version="" start="1" stop="40" moltype="Protein">

ECNEUQESECNEUQESECNEUQESECNEUQESECNEUQES

` `</SEQUENCE>

</DASSEQUENCE> </xml>

Congratulations! at this point you have set up our first DAS - reference
server!
