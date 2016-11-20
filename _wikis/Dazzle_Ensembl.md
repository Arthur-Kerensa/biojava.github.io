---
title: Dazzle:Ensembl
permalink: wikis/Dazzle%3AEnsembl
---

Deploying an ensembl-das reference server
=========================================

This document describes the steps required to install a DAS reference
server serving human genome data from an Ensembl-format SQL database.
Ensembl-DAS is implemented as a plugin for the Dazzle server framework.
If you are not familiar with Dazzle, it is recommended that you read the
[Dazzle deployment](Dazzle:deployment "wikilink") guide first.

Prerequisites
-------------

To run an Ensembl-DAS server, you will need to have the full Ensembl
core database installed. There are some instructions for doing this
here. Note that unless you actually want a local copy of the Ensembl
website (or to use the Perl APIs directly) you don't need to install any
of the Perl code. Ensembl-DAS uses pure Java APIs for accessing the
database. You only need the core databases for the species you are
interested in -- currently, no other databases are used.

### You will also need the following:

`   * A Java 2 runtime environment, version 1.4 or later`  
`   * A Java servlet container. We recommend Tomcat 5.0.`  
`   * A recent snapshot of BioJava.`  
`   * Dazzle 1.00 or later`  
`   * The biojava-ensembl bridge code`  
`   * A Java database driver for MySQL, available from MySQL AB`

The easiest way to get a server up and running is to download the latest
ensembl-das webapp skeleton. This is based on the standard Dazzle
skeleton, except that it contains biojava-ensembl code, including the
ensembl-das plugins. You therefore just need to configure and deploy the
application.

If you choose to build everything from source, note that the order of
compilation is important: you must first compile dazzle, the ensure that
dazzle.jar is available in your working directory (or on your CLASSPATH)
when you compile biojava-ensembl, otherwise the ensembl-das plugins will
not be compiled. When the biojava-ensembl build script starts up, it
displays a message to tell you whether or not Dazzle has been detected.

Basic configuration
-------------------

Like all Dazzle plugins, ensembl-das is configured by editing the
dazzlecfg.xml file. A typical minimal configuration might look like:

    <dazzle xmlns="http://www.biojava.org/2000/dazzle">
      <resource id="hsa2134" jclass="org.ensembl.das.DatabaseHolder">
        <string name="dbURL" value="jdbc:mysql://noranti.derkholm.net/homo_sapiens_core_23_34e" />
        <string name="dbUser" value="ensembl" />
        <string name="dbPass" value="xxx" />
      </resource>


      <datasource id="hsa2134" jclass="org.ensembl.das.EnsemblCoreReference">
        <string name="name" value="Human" />
        <string name="description" value="The human genome assembly from Ensembl" />
        <string name="version" value="23.34" />

        <string name="coreHolder" value="connection_hsa_core_23_34" />
        <int name="schemaVersion" value="23" />

        <string name="ensemblWebURL" value="http://www.ensembl.org/Homo_sapiens/" />
      </datasource>
    </dazzle>

Note that the database connection is not configured in the main
datasource element, but in a separate resource element. This is to allow
a single database connection to be shared between multiple DAS
datasources.

The org.ensembl.das.DatabaseHolder resource type reflects a database
connection. The dbURL property specifies the following information:

`   * The type of database driver (MySQL)`  
`   * The host name of the database server machine (e.g. noranti.derkholm.net)`  
`   * The name of the Ensembl database (e.g. homo_sapiens_core_23_34e)`

Having defined a database resource, configuring an EnsemblCoreReference
datasource is fairly standard. Note the coreHolder property, which
should be used to point to the appropriate database connection.

Once you are happy with your configuration, you should package
everything as a .WAR file and deploy it as normal for your servlet
container. If in doubt, consult the Dazzle deployment guide. As a first
test, use a web browser to view the Dazzle status page, which will
typically be:

`   `[`http://your-server:8080/das/`](http://your-server:8080/das/)` `

You could then try viewing the data source in a DAS client.

Annotation servers
------------------

Protein DAS
-----------

SNPs
----

The Generic SeqFeature plugin
-----------------------------

The GenericSeqFeatureSource plugin is a general-purpose Dazzle plugin
which allows features to be served up from an SQL database. The current
version does not depend directly on any Ensembl code or databases, but
it is distributed alongside the ensembl-das plugins described above, and
has historically been popular with Ensembl users

To serve a new dataset, create a MySQL database and add one or more
tables matching the following schema:

    CREATE TABLE my_feature ( 
      contig_id    varchar(40) NOT NULL default '', 
      start        int(10) NOT NULL default '0',
      end          int(10) NOT NULL default '0', 
      strand       int(2) NOT NULL default '0', 
      id           varchar(40) NOT NULL default '', 
      score        double(16,4) NOT NULL default '0.0000', 
      gff_feature  varchar(40) default NULL, 
      gff_source   varchar(40) default NULL,
      name         varchar(40) default NULL, 
      hstart       int(11) NOT NULL default '0',
      hend         int(11) NOT NULL default '0',
      hid          varchar(40) NOT NULL default'',
      evalue       varchar(40) default NULL,
      perc_id      int(10) default NULL, 
      phase        int(11) NOT NULL default '0', 
      end_phase    int(11) NOT NULL default '0',
      
      KEY id_contig(contig_id), 
      KEY id_pos(id,start,end) 
    ); 

A single database can contain many datasets, each in its own table. Each
dataset is served by a separate instance of the GenericSeqFeatureSource
plugin, but they can share a single pool of database connections,
therefore reducing the load on your database server if you want to serve
up a large number of datasets.

The most important columns are:

    contig_id    The name of the sequence to which a feature is attached (may actually be a contig, clone, or chromosome name).
    start    The minimum sequence position covered by the feature
    end    The maximum position covered by the feature
    strand    The strand of the feature (should be -1, 0, or 1).
    id    A unique ID for each feature
    gff_feature    The "type" of the feature
    gff_source    The "source" of the feature (e.g. the name of the program which performed the analysis)

For many purposes, the remaining fields can be left with their default
values.

A typical configuration looks like:

    <dazzle xmlns="http://www.biojava.org/2000/dazzle">
      <resource id="generic_db" jclass="org.ensembl.das.DatabaseHolder">
        <string name="dbURL" value="jdbc:mysql://noranti.derkholm.net/generic_features" />
        <string name="dbUser" value="ensembl" />
        <string name="dbPass" value="xxx" />
      </resource>


      <datasource id="somefeatures" jclass="org.ensembl.das.GenericSeqFeatureSource">
        <string name="name" value="Some features" />
        <string name="description" value="Some features which I think are really interesting" />
        <string name="version" value="1" />
        
        <string name="mapMaster" value="http://noranti.derkholm.net/das/hsa2334/">

        <string name="dbHolder" value="generic_db" />
        <string name="tableName" value="my_feature" />
      </datasource>
    </dazzle>

If the features in your database have unique IDs, it is easy to add
links to other web pages. For example:

      <datasource id="somefeatures" jclass="org.ensembl.das.GenericSeqFeatureSource">
        <string name="name" value="Some features" />
        <string name="description" value="Some features which I think are really interesting" />
        <string name="version" value="1" />
        
        <string name="mapMaster" value="http://noranti.derkholm.net/das/hsa2334/">

        <string name="dbHolder" value="generic_db" />
        <string name="tableName" value="my_feature" />
        
        <map name="uriPatterns">
          <string name="test_link" value="http://www.example.org/exciting_features.jsp?id=####;format=table">
        </map>
      </datasource>

It is possible to provide several links for each feature, so long as you
give them unique names. For each feature, the \#\#\#\# string in the
pattern is replaced by the feature ID from the database.
