---
title: BioJava:CookbookFrench:Distribution:RandomSeqs
permalink: wikis/BioJava%3ACookbookFrench%3ADistribution%3ARandomSeqs
---

Comment créer une séquence aléatoire à partir d'une Distribution?
-----------------------------------------------------------------

Les objets *Distribution* de BioJava ont une méthode pour échantillonner
les *Symbols*. En échantillonnant suffisamment de *Symbols*, vous pouvez
contruire une séquence aléatoire. Puisque c'est une tâche courante, une
méthode statique de *DistributionTools*, **generateSequence()**, est
fournie.

Le programme suivant crée une séquence aléatoire utilisant une
*Distribution* uniforme sur l'Alphabet ADN. La séquence émise sera à
chaque fois différente mais sa composition devrait être proche de 25%
par résidu. Des distributions non-uniformes peuvent aussi être utilisées
pour créer des séquences biaisées.

```java import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.seq.io.\*; import java.io.\*;

public class RandomSequence {

` public static void main(String[] args) {`  
`   //créer une distribution uniforme sur l'Alphabet ADN`  
`   Distribution dist = new UniformDistribution(DNATools.getDNA());`

`   //créer une séquence aléatoire de 700 nuc.`  
`   Sequence seq = DistributionTools.generateSequence("random seq", dist, 700);`  
`   `  
`   try {`  
`     //imprimer sur STDOUT`  
`     SeqIOTools.writeFasta(System.out, seq);`  
`   }`  
`   catch (IOException ex) {`  
`     //erreur de i/o`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
