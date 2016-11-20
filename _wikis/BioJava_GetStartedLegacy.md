---
title: BioJava:GetStartedLegacy
permalink: wikis/BioJava%3AGetStartedLegacy
---

Introduction
------------

Welcome to BioJava 1 or BioJava Legacy. BioJava Legacy is the
continuation of the old BioJava core while a new code base, BioJava 3,
is currently being developed. As of the concurrent release of BioJava
and BioJava , many functionalities are still not available in BioJava 3
and differences between their respective sequence models may make
BioJava 1 a valid option for your project.

To find out more about BioJava 1, check any of the following entry
points:

-   [Tutorial](/wikis/BioJava:Tutorial "wikilink") to learn about symbols,
    sequence, and events.
-   [Cook Book](/wikis/BioJava:CookBookLegacy "wikilink"), also famously known
    as BioJava in Anger, to find out many code snippets.
-   [BioJavax Extension](/wikis/BioJava:BioJavaXDocs "wikilink") which provides
    sophisticated event-based methods to read, write, and manipulate
    sequence files.

Installation
------------

BioJava 1 will run on any computer with a Java virtual machine complying
to the Java 2 Standard Edition (J2SE) 1.5 (or later) specifications.
Java implementations for Linux, Windows, and Solaris are available to
download from [Oracle's java
website](http://www.oracle.com/technetwork/java/). Recent versions of
MacOS X include a suitable Java implementation as standard. Java is also
available on many other platforms: if in doubt, contact your vendor.
BioJava binaries are distributed in .jar (Java ARchive) format.

You can get the latest version from the download page [BioJava (requires
Java 1.5+)](/wikis/BioJava:Download_{{current version legacy}} "wikilink").

You can also integrate BioJava with NetBeans IDE. To find out how follow
this [link](How_to_integrate_BioJava_in_NetBeans_IDE "wikilink").

None of these .jar files need to be unpacked for normal use -- simply
place them in a convenient directory. To use BioJava, add the required
JAR files to your CLASSPATH environment variable. The exact syntax
varies between platforms. The text is wrapped due to limited space. The
actual commands should be on a single line:

### UNIX Bourne-type shells (the default with most Linux distributions and MacOS 10.3)

`export CLASSPATH=/home/thomas/biojava-live.jar:/home/thomas/bytecode.jar:`  
`                        /home/thomas/commons-cli.jar:`  
`                        /home/thomas/commons-collections-2.1.jar:`  
`                        /home/thomas/commons-dbcp-1.1.jar:`  
`                        /home/thomas/commons-pool-1.1.jar:.`

### UNIX C-type shell (for example: versions of Mac OS X pre-10.3)

`setenv CLASSPATH /home/thomas/biojava-live.jar:/home/thomas/bytecode.jar:`  
`                        /home/thomas/commons-cli.jar:`  
`                        /home/thomas/commons-collections-2.1.jar:`  
`                        /home/thomas/commons-dbcp-1.1.jar:`  
`                        /home/thomas/commons-pool-1.1.jar:.`

### Windows from command line

`set CLASSPATH C:\biojava-live.jar;C:\bytecode.jar;C:\commons-cli.jar;`  
`                        C:\commons-collections-2.1.jar;C:\commons-dbcp-1.1.jar;`  
`                        C:\commons-dbcp-1.1.jar;.`

### Windows autoexec.bat files

`set CLASSPATH=C:\biojava-live.jar;C:\bytecode.jar;C:\commons-cli.jar;`  
`                        C:\commons-collections-2.1.jar;C:\commons-dbcp-1.1.jar;`  
`                        C:\commons-pool-1.1.jar;.`

In some distributions of Biojava, you need to specify biojava.jar
instead of biojava-live.jar in the above. Note: Since version 1.8,
BioJava is modular and the scripts need to be adjusted to incorporate
submodules.

It is also possible to "install" JAR files onto your system by copying
them into your Java installation's extensions directory. On most Unix
systems, this is named *${JAVA\_HOME}/jre/lib/ext*. On Mac OS X there is
a per-user extensions directory called *~/Library/Java/Extensions* (you
may have to create this directory yourself). For other platforms,
consult your Java vendor.

You can now compile and run BioJava programs using the *javac* and
*java* commands. You might like to look at the
[tutorial](/wikis/BioJava:Tutorial "wikilink"),
[<http://www.biojava.org/docs/api> API documentation] and the [Legacy
Cookbook](/wikis/BioJava:CookBookLegacy "wikilink") section. Finally, you can
learn a lot about BioJava by trying the demo programs included in the
source distribution (see below).

Building your own
-----------------

If you want to modify BioJava, you can obtain a copy of the source code
from the [Maven repository](http://biojava.org/download/maven/) of the
download area. Source releases are distributed in .tar.gz format. You
can also obtain up-to-the-minute [source code](Get source "wikilink").

Since version 1.8, BioJava Legacy 1.8 requires
[Maven](http://maven.apache.org/) for the build process. We are also
providing a BioJava specific Maven repository at
<http://biojava.org/download/maven/> .

Building the demo programs
--------------------------

The source distribution contains a number of small demo programs. Once
you have a working *biojava.jar* on your classpath, these can be
compiled directly using *javac* from the demos directory.

` (unix)`  
` cd demos`  
` javac seq/TestEmbl.java`  
` java seq.TestEmbl seq/AL121903.embl`  
` `  
` (windows)`  
` cd demos`  
` javac seq\TestEmbl.java`  
` java seq.TestEmbl seq\AL121903.embl`
