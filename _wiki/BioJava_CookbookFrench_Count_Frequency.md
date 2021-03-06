---
title: BioJava:CookbookFrench:Count:Frequency
permalink: wiki/BioJava%3ACookbookFrench%3ACount%3AFrequency
---

Comment calculer la fréquence d'un Symbol dans une Sequence?
------------------------------------------------------------

Une des classes les plus utiles de BioJava est la classe *Distribution*.
Une *Distribution* est une carte associant un *Symbol* à sa fréquence
dans une *SymbolList*. Les *Distributions* sont entrainées avec les
*Symbols* observés en utilisant un *DistributionTrainerContext*. Un
*DistributionTrainerContext* peut entrainé plusieurs *Distributions*
enregistrées et peut traité n'importe quel *Symbol* provenant de
n'importe quel *Alphabet*. Les *Symbols* ambiguës sont divisés parmi les
*AtomicSymbols* qui constitue le *BasisSymbol* ambiguë.

Le programme suivant montre l'entrainement de trois *Distributions* avec
des *Sequences* faites à partir de trois *Alphabets* différents.

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;
import org.biojava.bio.dist.\*; import org.biojava.utils.\*; import
java.util.\*;

public class Frequency {

` public static void main(String[] args) {`  
`   try {`  
`     //créer une SymbolList d'ADN`  
`     SymbolList dna = DNATools.createDNA("atcgctagcgtyagcntatsggca");`  
`     //créer une SymbolList d'ARN`  
`     SymbolList rna = RNATools.createRNA("aucgcuaucccaggga");`  
`     //créer une SymbolList de protéines`  
`     SymbolList protein = ProteinTools.createProtein("asrvgchvhilmkapqrt");`  
`     SymbolList[] sla = {dna, rna, protein};`  
`     `  
`     //obtenir un DistributionTrainerContext`  
`     DistributionTrainerContext dtc = new SimpleDistributionTrainerContext();`  
`     `  
`     //créer trois Distributions`  
`     Distribution dnaDist =`  
`         DistributionFactory.DEFAULT.createDistribution(dna.getAlphabet());`  
`     Distribution rnaDist =`  
`         DistributionFactory.DEFAULT.createDistribution(rna.getAlphabet());`  
`     Distribution proteinDist =`  
`         DistributionFactory.DEFAULT.createDistribution(protein.getAlphabet());`  
`     Distribution[] da = {dnaDist, rnaDist, proteinDist};`  
`     `  
`     //enregistrer les Distributions auprès du trainer`  
`     dtc.registerDistribution(dnaDist);`  
`     dtc.registerDistribution(rnaDist);`  
`     dtc.registerDistribution(proteinDist);`  
`     `  
`     //pour chaque Sequence`  
`     for (int i = 0; i < sla.length; i++) {`  
`       //compter chaque Symbol dans la Distribution appropriŽe`  
`       for(int j = 1; j <= sla[i].length(); j++){`  
`         dtc.addCount(da[i], sla[i].symbolAt(j), 1.0);`  
`       }`  
`     }`  
`     `  
`     //former les Distributions`  
`     dtc.train();`  
`     `  
`     //imprimer la valeur de chaque Distribution`  
`     for (int i = 0; i < da.length; i++) {`  
`       for (Iterator iter = ((FiniteAlphabet)da[i].getAlphabet()).iterator();`  
`            iter.hasNext(); ) {`  
`         Symbol sym = (Symbol)iter.next();`  
`         System.out.println(sym.getName()+" : "+da[i].getWeight(sym));`  
`       }`  
`       System.out.println("\n");`  
`     }`  
`   }`  
`   catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
