---
title: BioJava:CookbookFrench:Count:Residues
permalink: wiki/BioJava%3ACookbookFrench%3ACount%3AResidues
---

Comment compter les résidues d'une Sequence?
--------------------------------------------

Faire le décompte des résidues d'une *Sequence* est une tâche standard
de la bio-informatique. En général, vous construiriez un tableau
d'entiers et établiriez une forme d'indexation arbitraire. Mieux encore,
vous pourriez utiliser un *AlphabetIndex* pour imposer un index
standardisé. Vous pouvez en obtenir un à partir du *AlphabetManager* en
utilisant les méthodes **getAlphabetIndex()**. Parce que ce type de
traitement est si souvent utilisé, BioJava enveloppe toutes les
indexations de ce type dans une classe appellée *IndexedCount*, une
implementation de l'interface *Count*.

Le programme suivant lit un fichier de séquence d'un type quelquonque et
en compte les résidues, imprimant les résultats sur STDOUT. Noter que ce
programme ne peut accepter des Symbols ambigüs. Si vous voulez faire le
décompte des Symbols ambigüs, vous devez ajouter un décompte partiel
pour chaque Symbol qui fait partie de l'ambiguité. Si c'est le cas, vous
utiliseriez la solution 2.

### Solution 1

```java import java.io.\*; import java.util.\*;

import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.seq.io.\*; import org.biojava.bio.symbol.\*;

public class CountResidues {

` /**`  
`  * Prends 2 arguments: le 1er est un nom de fichier de séquence,le 2ème est un entier `  
`  * qui est égal à un des formats supportés par SeqIOTools. Les formats de fichiers`  
`  * appropriés sont:`  
`  * FASTADNA = 1;`  
`  * FASTAPROTEIN = 2;`  
`  * EMBL = 3;`  
`  * GENBANK = 4;`  
`  * SWISSPROT = 5;`  
`  * GENPEPT = 6;`  
`  */`  
` public static void main(String[] args) {`  
`   //créer une réference à un objet pour contenir les décomptes`  
`   Count counts = null;`

`   try {`  
`     //lire le fichier de séquence`  
`     BufferedReader br = new BufferedReader(new FileReader(args[0]));`

`     //obtenir un SequenceIterator pour les séquences contenues dans ce fichier`  
`     SequenceIterator iter = (SequenceIterator)SeqIOTools.fileToBiojava(`  
`         Integer.parseInt(args[1]), br);`

`     //pour chaque séquence`  
`     while(iter.hasNext()){`  
`       Sequence seq = iter.nextSequence();`

`       //au besoin, initialiser counts`  
`       if(counts == null){`  
`         counts = new IndexedCount((FiniteAlphabet)seq.getAlphabet());`  
`       }`

`       //iteration à travers les Symbols contenus dans seq`  
`       for (Iterator i = seq.iterator(); i.hasNext(); ) {`  
`         AtomicSymbol sym = (AtomicSymbol)i.next();`  
`         counts.increaseCount(sym,1.0);`  
`       }`  
`     }`

`     //imprimer les résultats`  
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

` /**`  
`  * Prends 2 arguments: le 1er est un nom de fichier de séquence,le 2ème est un entier`  
`  * qui est égal à un des formats supportés par SeqIOTools. Les formats de fichiers`  
`  * appropriés sont:`  
`  * FASTADNA = 1;`  
`  * FASTAPROTEIN = 2;`  
`  * EMBL = 3;`  
`  * GENBANK = 4;`  
`  * SWISSPROT = 5;`  
`  * GENPEPT = 6;`  
`  */`  
` public static void main(String[] args) {`  
`   //créer une réference à un objet pour contenir les décomptes`  
`   Count counts = null;`

`   try {`  
`     //lire le fichier de séquence`  
`     BufferedReader br = new BufferedReader(new FileReader(args[0]));`

`     //obtenir un SequenceIterator pour les séquences de ce fichier`  
`     SequenceIterator iter = (SequenceIterator)SeqIOTools.fileToBiojava(`  
`         Integer.parseInt(args[1]), br);`

`     //pour chaque séquence`  
`     while(iter.hasNext()){`  
`       Sequence seq = iter.nextSequence();`

`       //au besoin, initialiser counts`  
`       if(counts == null){`  
`         counts = new IndexedCount((FiniteAlphabet)seq.getAlphabet());`  
`       }`

`       //faire un iteration à travers les  Symbols de seq`  
`       for (Iterator i = seq.iterator(); i.hasNext(); ) {`  
`         Symbol sym = (Symbol)i.next();`

`         /*`  
`          * Ce Symbol peut etre ambigu: ajouter un décompte partiel  pour chaque Symbol`  
`          * qui constitue ce  Symbol ambigu. Ex.: le Symbol ADN ambigu est crée à partir`  
`          * d'un Alphabet de 4 Symbols, alors ajouter 0.25 au décompte de chacun des nucl.`  
`          */`  
`         FiniteAlphabet subSymbols = (FiniteAlphabet)sym.getMatches();`  
`         for (Iterator i2 = subSymbols.iterator(); i2.hasNext(); ) {`  
`           AtomicSymbol sym2 = (AtomicSymbol)i2.next();`  
`           counts.increaseCount(sym2, 1.0 / (double)subSymbols.size());`  
`         }`  
`       }`  
`     }`

`     //imprimer les résultats `  
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
