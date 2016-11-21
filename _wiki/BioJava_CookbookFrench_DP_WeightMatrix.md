---
title: BioJava:CookbookFrench:DP:WeightMatrix
permalink: wiki/BioJava%3ACookbookFrench%3ADP%3AWeightMatrix
---

Comment utiliser une WeightMatrix pour trouver un motif?
--------------------------------------------------------

Une *WeightMatrix* est une manière pratique de représenter un alignement
ou un motif. Elle peut aussi être utilisée comme matrice d'évaluation
(*scoring matrix*) pour détecter un motif similaire dans une autre
séquence. BioJava contient une classe *WeightMatrix* dans le package
org.biojava.bio.dp. Il y a aussi une classe *WeightMatrixAnnotator* qui
utilise un objet de type *WeightMatrix* afin d'ajouter les motifs
trouvés sous la forme de *Features*, pourvu que le motif trouvé dépasse
un seuil de détection.

Le programme suivant crée une *WeightMatrix* à partir d'un alignement et
utilise cette matrice pour annoter une *Sequence* avec un seuil minimal
de détection de 0.1.

```java import java.util.\*; import org.biojava.bio.dist.\*; import
org.biojava.bio.dp.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.symbol.\*;

public class WeightMatrixDemo { public static void main(String[] args)
throws Exception{

`   //créer un alignement de motifs.`  
`   Map map = new HashMap();`  
`   map.put("seq0", DNATools.createDNA("aggag"));`  
`   map.put("seq1", DNATools.createDNA("aggaa"));`  
`   map.put("seq2", DNATools.createDNA("aggag"));`  
`   map.put("seq3", DNATools.createDNA("aagag"));`  
`   Alignment align = new SimpleAlignment(map);`

`   //créer un tableau de Distribution[] pour ce motif`  
`   Distribution[] dists =`  
`       DistributionTools.distOverAlignment(align, false, 0.01);`

`   //créer une WeightMatrix`  
`   WeightMatrix matrix = new SimpleWeightMatrix(dists);`

`   //la séquence où ce motif est recherché`  
`   Sequence seq = DNATools.createDNASequence("aaagcctaggaagaggagctgat","seq");`

`   //annoter la séquence avec la matrice pour une valeur seuil basse (0.1)`  
`   WeightMatrixAnnotator wma = new WeightMatrixAnnotator(matrix, 0.1);`  
`   seq = wma.annotate(seq);`

`   //imprimer l'information des matches`  
`   for (Iterator it = seq.features(); it.hasNext(); ) {`  
`        Feature f = (Feature)it.next();`  
`        Location loc = f.getLocation();`  
`        System.out.println("Match at " + loc.getMin()+"-"+loc.getMax());`  
`        System.out.println("\tscore : "+f.getAnnotation().getProperty("score"));`  
`   }`  
` }`

} ```
