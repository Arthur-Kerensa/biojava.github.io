---
title: BioJava:CookBook:Distribution:Emission
---

What is an easy way to tell if two Distributions have equal weights?
--------------------------------------------------------------------

Testing two distributions for equal weights is a good way of telling if
a training procedure has converged or if two Sequences are likely to
come from the same organism. It is a bit tedious to loop through all the
residues, especially in a large Alphabet. Fortunately there is a static
method called areEmissionSpectraEqual() in DistributionTools that checks
for you.

Using this method is demonstrated below.

```java import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.symbol.\*; import org.biojava.bio.\*; import
org.biojava.utils.\*;

public class EqualDistributions {

` public static void main(String[] args) {`  
`   FiniteAlphabet alpha = DNATools.getDNA();`

`   //make a uniform distribution`  
`   Distribution uniform = new UniformDistribution(alpha);`

`   try {`  
`     //make another Distribution with uniform weights`  
`     Distribution dist = DistributionFactory.DEFAULT.createDistribution(alpha);`  
`     dist.setWeight(DNATools.a(), 0.25);`  
`     dist.setWeight(DNATools.c(), 0.25);`  
`     dist.setWeight(DNATools.g(), 0.25);`  
`     dist.setWeight(DNATools.t(), 0.25);`

`     //test to see if the weights are equal`  
`     boolean equal = DistributionTools.areEmissionSpectraEqual(uniform, dist);`  
`     System.out.println("Are 'uniform' and 'dist' equal? "+ equal);`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
