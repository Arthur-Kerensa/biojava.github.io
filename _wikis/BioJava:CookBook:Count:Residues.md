---
title: BioJava:CookBook:Count:Residues
---

How Do I Count the Residues in a Sequence?
------------------------------------------

Counting the residues in a Sequence is a fairly standard bioinformatics
task. Generally you would construct an array of ints and use some
arbitrary indexing system. Better yet you could use an AlphabetIndex to
impose a standardized index. You would get one from the AlphabetManager
using one of its getAlphabetIndex() methods. Because this type of
activity is so standard BioJava conveniently wraps up all the indexing
etc into a class called IndexedCount which is an implementation of the
Count interface.

The following program reads some type of sequence file and counts the
residues, printing the results to STDOUT. Note that this program will
not cope with ambiguity symbols. If you want to count ambiguity symbols
you need add a partial count for each Symbol that makes up the ambiguity
If this is the case you would use this solution.

### Solution 1

```java import java.io.\*; import java.util.\*;

import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.seq.io.\*; import org.biojava.bio.symbol.\*;

public class CountResidues {

` /**`  
`  * Takes 3 arguments, first is a sequence filename the second is the`  
`  * sequence format (case insensitive) and the third is the sequence`  
`  * alphabet (eg DNA, also case insensitive)`  
`  */`  
` public static void main(String[] args) {`  
`   //reference to object to hold the counts`  
`   Count counts = null;`

`   try {`  
`     //open sequence file`  
`     BufferedReader br = new BufferedReader(new FileReader(args[0]));`

`     //get a SequenceIterator for the sequences in the file`  
`     SequenceIterator iter =`  
`         (SequenceIterator)SeqIOTools.fileToBiojava(args[1],args[2],br);`

`     //for each sequence`  
`     while(iter.hasNext()){`  
`       Sequence seq = iter.nextSequence();`

`       //if needed initialize counts`  
`       if(counts == null){`  
`         counts = new IndexedCount((FiniteAlphabet)seq.getAlphabet());`  
`       }`

`       //iterate through the Symbols in seq`  
`       for (Iterator i = seq.iterator(); i.hasNext(); ) {`  
`         AtomicSymbol sym = (AtomicSymbol)i.next();`  
`         counts.increaseCount(sym,1.0);`  
`       }`  
`     }`

`     //now print the results`  
`     for (Iterator i = ((FiniteAlphabet)counts.getAlphabet()).iterator();`  
`          i.hasNext(); ) {`  
`       AtomicSymbol sym = (AtomicSymbol)i.next();`  
`       System.out.println(sym.getName()+" : "+counts.getCount(sym));`  
`     }`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```

### Solution 2

```java import java.io.\*; import java.util.\*;

import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.seq.io.\*; import org.biojava.bio.symbol.\*;

public class CountResidues2 {

`   /**`  
`  * Takes 3 arguments, first is a sequence filename the second is the`  
`  * sequence format (case insensitive) and the third is the sequence`  
`  * alphabet (eg DNA, also case insensitive)`  
`  */`  
` public static void main(String[] args) {`  
`   //reference to object to hold the counts`  
`   Count counts = null;`

`   try {`  
`     //open sequence file`  
`     BufferedReader br = new BufferedReader(new FileReader(args[0]));`

`     //get a SequenceIterator for the sequences in the file`  
`     SequenceIterator iter =`  
`         (SequenceIterator)SeqIOTools.fileToBiojava(args[1],args[2],br);`

`     //for each sequence`  
`     while(iter.hasNext()){`  
`       Sequence seq = iter.nextSequence();`

`       //if needed initialize counts`  
`       if(counts == null){`  
`         counts = new IndexedCount((FiniteAlphabet)seq.getAlphabet());`  
`       }`

`       //iterate through the Symbols in seq`  
`       for (Iterator i = seq.iterator(); i.hasNext(); ) {`  
`         Symbol sym = (Symbol)i.next();`

`         /*`  
`          * The Symbol may be ambiguous so add a partial count for each Symbol`  
`          * that makes up the ambiguity Symbol. Eg the DNA ambiguity n is made`  
`          * of an Alphabet of four Symbols so add 0.25 of a count to each.`  
`          */`  
`         FiniteAlphabet subSymbols = (FiniteAlphabet)sym.getMatches();`  
`         for (Iterator i2 = subSymbols.iterator(); i2.hasNext(); ) {`  
`           AtomicSymbol sym2 = (AtomicSymbol)i2.next();`  
`           counts.increaseCount(sym2, 1.0 / (double)subSymbols.size());`  
`         }`  
`       }`  
`     }`

`     //now print the results`  
`     for (Iterator i = ((FiniteAlphabet)counts.getAlphabet()).iterator();`  
`          i.hasNext(); ) {`  
`       AtomicSymbol sym = (AtomicSymbol)i.next();`  
`       System.out.println(sym.getName()+" : "+counts.getCount(sym));`  
`     }`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
