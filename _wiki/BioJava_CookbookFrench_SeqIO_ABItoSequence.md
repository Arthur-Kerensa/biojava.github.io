---
title: BioJava:CookbookFrench:SeqIO:ABItoSequence
permalink: wikis/BioJava%3ACookbookFrench%3ASeqIO%3AABItoSequence
---

Comment transformer un fichier de tracé ABI en Sequence BioJava?
----------------------------------------------------------------

Une grande partie de la bio-informatique consiste en lectures d'un (ou
de plusieurs) morceau d'ADN obtenu à l'aide d'un séquenceur automatique.
Un fichier de sortie typique est un tracé ABI. BioJava contient une
classe appelée *ABITrace* qui lira soit un fichier ABITrace, un URL ou
un tableau byte[] pour stocker les valeurs pour ensuite les récupérer
pour les traitements à venir.

Le programme suivant est une version modifiée d'un programme
gracieusement offert par Matthew Pocock. Il montre comment créer une
*Sequence* BioJava à partir d'un fichier de tracé ABI.

```java import java.io.\*; import org.biojava.bio.\*; import
org.biojava.bio.program.abi.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.seq.impl.\*; import org.biojava.bio.seq.io.\*; import
org.biojava.bio.symbol.\*;

public class Trace2Seq {

`   public static void main(String[] args) throws Exception {`  
`   File traceFile = new File(args[0]);`  
`   `  
`   //le nom de la séquence`  
`   String name = traceFile.getName();`

`   //lire le tracé`  
`   ABITrace trace = new ABITrace(traceFile);`

`   //extraire les Symbols`  
`   SymbolList symbols = trace.getSequence();`

`   //créer une séquence en bonne et due forme    `  
`   Sequence seq = new SimpleSequence(symbols, name, name, Annotation.EMPTY_ANNOTATION);`

`   //écrire la séquence sur STDOUT`  
`   SeqIOTools.writeFasta(System.out, seq);`  
` }`

} ```
