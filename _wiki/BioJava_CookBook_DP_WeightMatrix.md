---
title: BioJava:CookBook:DP:WeightMatrix
permalink: wiki/BioJava%3ACookBook%3ADP%3AWeightMatrix
---

How do I use a WeightMatrix to find a motif?
--------------------------------------------

A Weight Matrix is a useful way of representing an alignment or a motif.
It can also be used as a scoring matrix to detect a similar motif in a
sequence. BioJava contains a class call WeightMatrix in the
org.biojava.bio.dp package. There is also a WeightMatrixAnnotator which
uses the WeightMatrix to add Features to any portion of the sequence
being searched which exceed the scoring threshold.

The following program generates a WeightMatrix from an aligment and uses
that matrix to annotate a Sequence with a threshold of 0.1

```java import java.util.\*;

import org.biojava.bio.dist.\*; import org.biojava.bio.dp.\*; import
org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class WeightMatrixDemo {

` public static void main(String[] args) throws Exception{`  
`   //make an Alignment of a motif.`  
`   Map map = new HashMap();`  
`   map.put("seq0", DNATools.createDNA("aggag"));`  
`   map.put("seq1", DNATools.createDNA("aggaa"));`  
`   map.put("seq2", DNATools.createDNA("aggag"));`  
`   map.put("seq3", DNATools.createDNA("aagag"));`  
`   Alignment align = new SimpleAlignment(map);`

`   //make a Distribution[] of the motif`  
`   Distribution[] dists =`  
`       DistributionTools.distOverAlignment(align, false, 0.01);`

`   //make a Weight Matrix`  
`   WeightMatrix matrix = new SimpleWeightMatrix(dists);`

`   //the sequence to score against`  
`   Sequence seq = DNATools.createDNASequence("aaagcctaggaagaggagctgat","seq");`

`   //annotate the sequence with the weight matrix using a low threshold (0.1)`  
`   WeightMatrixAnnotator wma = new WeightMatrixAnnotator(matrix, 0.1);`  
`   seq = wma.annotate(seq);`

`   //output match information`  
`   for (Iterator it = seq.features(); it.hasNext(); ) {`  
`     Feature f = (Feature)it.next();`  
`     Location loc = f.getLocation();`  
`     System.out.println("Match at " + loc.getMin()+"-"+loc.getMax());`  
`     System.out.println("\tscore : "+f.getAnnotation().getProperty("score"));`  
`   }`  
` }`

} ```
