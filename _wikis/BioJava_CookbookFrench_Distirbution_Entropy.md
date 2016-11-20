---
title: BioJava:CookbookFrench:Distirbution:Entropy
permalink: wikis/BioJava%3ACookbookFrench%3ADistirbution%3AEntropy
---

Comment trouver la quantité d'information ou d'entropie d'une Distribution?
---------------------------------------------------------------------------

La quantité d'information ou d'entropie d'une *Distribution* est le
reflet de la redondance de cette *Distribution*. L'information et
l'entropie de Shannon peuvent être calculés en utilisant des méthodes
statiques de la classe *DistributionTools*.

L'information de Shannon est retournée en valeur de type double et est
le reflet du contenu total en information. L'entropie est retournée en
objet de type *HashMap*, entre chacun des *Symbol* et son entropie
correspondant. Le programme suivant calcule les deux paramètres pour une
*Distribution* très biaisée.

```java import java.util.\*; import org.biojava.bio.dist.\*; import
org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class Entropy {

` public static void main(String[] args) {`  
`   `  
`   Distribution dist = null;`

`   try {`  
`     //créer une Distribution biaisée`  
`     dist =`  
`         DistributionFactory.DEFAULT.createDistribution(DNATools.getDNA());`  
`     //ajuster la valeur de à 0.97`  
`     dist.setWeight(DNATools.a(), 0.97);`  
`     //ajuster les autres valeurs à 0.01`  
`     dist.setWeight(DNATools.c(), 0.01);`  
`     dist.setWeight(DNATools.g(), 0.01);`  
`     dist.setWeight(DNATools.t(), 0.01);`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`     System.exit(-1);`  
`   }`  
`   `  
`   //calculer le contenu en information`  
`   double info = DistributionTools.bitsOfInformation(dist);`  
`   `  
`   System.out.println("information = "+info+" bits");`  
`   System.out.print("\n");`  
`   `  
`   //calculer l'entropie (utilisant le log en base 2, conventionnel)`  
`   HashMap entropy = DistributionTools.shannonEntropy(dist, 2.0);`  
`   `  
`   //imprimer l'entropie pour chacun des résidues`  
`   System.out.println("Symbol\tEntropy");`  
`   `  
`   for (Iterator i = entropy.keySet().iterator(); i.hasNext(); ) {`  
`     Symbol sym = (Symbol)i.next();`  
`     System.out.println(sym.getName()+ "\t" +entropy.get(sym));`  
`   }`  
` }`

} ```
