---
title: BioJava:Cookbook:Alphabets:CrossProduct
permalink: wiki/BioJava%3ACookbook%3AAlphabets%3ACrossProduct
---

How do I make a CrossProductAlphabet such as a codon Alphabet
-------------------------------------------------------------

CrossProductAlphabets result from the multiplication of other
[Alphabets](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Alphabet.html).
CrossProductAlphabets are used to wrap up 2 or more
[Symbols](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Symbol.html)into
a single "cross product"
[Symbol](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Symbol.html).
For example using a 3 way cross of the [DNA](wp:DNA "wikilink") alphabet
you could wrap a [codon](wp:codon "wikilink") as a
[Symbol](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Symbol.html).
You could then count those [codon](wp:codon "wikilink")
[Symbols](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Symbol.html)
in a
[Count](http://www.biojava.org/docs/api1.8/org/biojava/bio/dist/Count.html)
or you could used them in a
[Distribution](http://www.biojava.org/docs/api1.8/org/biojava/bio/dist/Distribution.html).

CrossProductAlphabets can be created by name (if the component
[Alphabets](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Alphabet.html)
are registered in the
[AlphabetManager](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/AlphabetManager.html))
or by making a list of the desired
[Alphabets](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Alphabet.html)
and creating the
[Alphabet](http://www.biojava.org/docs/api1.8/org/biojava/bio/symbol/Alphabet.html)
from the
[List](http://java.sun.com/j2se/1.4.2/docs/api/java/util/List.html).
Both approaches are shown in the example below.

```java package biojava\_in\_anger;

import java.util.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.symbol.\*;

public class CrossProduct {

` public static void main(String[] args) {`

`   //make a CrossProductAlphabet from a List`  
`   List l = Collections.nCopies(3, DNATools.getDNA());`  
`   Alphabet codon = AlphabetManager.getCrossProductAlphabet(l);`

`   //get the same Alphabet by name`  
`   Alphabet codon2 =`  
`       AlphabetManager.generateCrossProductAlphaFromName("(DNA x DNA x DNA)");`

`   //show that the two Alphabets are canonical`  
`   System.out.println(codon == codon2);`  
` }`

} ```
