---
title: BioJava:CookbookFrench:Distirbution:Emission
permalink: wikis/BioJava%3ACookbookFrench%3ADistirbution%3AEmission
---

Comment savoir facilement si deux Distributions sont identiques?
----------------------------------------------------------------

Vérifier si deux *Distributions* sont identiques est une bonne façon de
dire si la procédure d'entrainement à converger ou si deux *Sequences*
sont susceptibles de provenir du même organisme. C'est assez fastidieux
de faire une boucle et de passer à travers tous les résidues, surtout
pour un grand *Alphabet*. Une méthode statique,
**areEmissionSpectraEqual()** de la classe *DistributionTools*,
simplifie la tâche en vérifiant pour vous.

L'utilisation de cette méthode se trouve ci-dessous.

```java import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.symbol.\*; import org.biojava.bio.\*; import
org.biojava.utils.\*;

public class EqualDistributions {

` public static void main(String[] args) {`  
`   `  
`   FiniteAlphabet alpha = DNATools.getDNA();`  
`   `  
`   //créer une Distribution uniforme`  
`   Distribution uniform = new UniformDistribution(alpha);`  
`   `  
`   try {`  
`     //créer une autre Distribution avec des valeurs uniformes`  
`     Distribution dist = DistributionFactory.DEFAULT.createDistribution(alpha);`  
`     dist.setWeight(DNATools.a(), 0.25);`  
`     dist.setWeight(DNATools.c(), 0.25);`  
`     dist.setWeight(DNATools.g(), 0.25);`  
`     dist.setWeight(DNATools.t(), 0.25);`  
`     `  
`     //vérifier si les valeurs sont égales`  
`     boolean equal = DistributionTools.areEmissionSpectraEqual(uniform, dist);`  
`     `  
`     System.out.println("Are "uniform" and "dist" equal? "+ equal);`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
