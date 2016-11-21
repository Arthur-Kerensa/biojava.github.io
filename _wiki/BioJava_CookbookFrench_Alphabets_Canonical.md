---
title: BioJava:CookbookFrench:Alphabets:Canonical
permalink: wiki/BioJava%3ACookbookFrench%3AAlphabets%3ACanonical
---

Comment savoir si deux Symbols ou Alphabets sont identiques?
------------------------------------------------------------

Dans Biojava, les mêmes *Alphabets* et les mêmes *Symbols* sont
identiques quelque soit la manière dont ils on été construits ou de leur
origine . Ceci veut dire que si deux alphabets d'ADN (ou des *Symbols*
provenant de ces alphabets) sont instanciés à des moments différents,
ils sont identiques à la fois par la méthode **equals()** et l'opérateur
==. De plus , les *Symbols* des alphabets PROTEIN et PROTEIN-TERM sont
identiques tout comme les *Symbols* provenant de *IntegerAlphabet* et de
*SubIntegerAlphabets*.

C'est vrai même pour des *Alphabets* et des *Symbols* qui se trouvent
sur différentes machines virtuels (grâce à un peu de magie par
Serialization) ce qui veut dire que BioJava fonctionne à travers RMI.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class Canonical {

` public static void main(String[] args) {`

`   // obtenir l'alphabet d'ADN des deux manières`  
`   Alphabet a1 = DNATools.getDNA();`  
`   Alphabet a2 = AlphabetManager.alphabetForName("DNA");`

`   // sont-ils identiques?`  
`   System.out.println("equal: "+ a1.equals(a2));`

`   // sont-ils identiques?`  
`   System.out.println("canonical: "+ (a1 == a2));`  
` }`

} ```
