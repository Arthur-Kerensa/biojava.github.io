---
title: BioJava:Cookbook:Locations:Point
permalink: wiki/BioJava%3ACookbook%3ALocations%3APoint
---

How do I specify a PointLocation?
---------------------------------

In BioJava locations in a Sequence are specified by simple objects that
implement the interface Location.

A point location is the inclusive location of a single symbol in a
SymbolList or Sequence. PointLocations have public constructors and are
easy to instantiate. The following example demonstrates the creation of
a PointLocation and it's specification of a single Symbol in a
SymbolList.

Remember that BioJava uses the biological coordinate system thus the
first PointLocation in a Sequence will be 1 not 0.

As of BioJava 1.8, you may want to consider using
[RichLocation](http://www.biojava.org/docs/api1.8/org/biojavax/bio/seq/RichLocation.html)
from the [BioJavax](/wiki/BioJava:BioJavaXDocs "wikilink") extension.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class SpecifyPoint {

` public static void main(String[] args) {`  
`   try {`  
`     //make a PointLocation specifying the third residue`  
`     PointLocation point = new PointLocation(3);`  
`     //print the location`  
`     System.out.println("Location: "+point.toString());`

`     //make a SymbolList`  
`     SymbolList sl = RNATools.createRNA("gcagcuaggcggaaggagc");`  
`     System.out.println("SymbolList: "+sl.seqString());`

`     //get the SymbolList specified by the Location`  
`     SymbolList sym = point.symbols(sl);`  
`     //in this case the SymbolList will only have one base`  
`     System.out.println("Symbol specified by Location: "+sym.seqString());`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //illegal symbol used to make sl`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
