---
title: BioJava:CookBookItaliano:Sequence:ChangeName
permalink: wikis/BioJava%3ACookBookItaliano%3ASequence%3AChangeName
---

Come posso cambiare il nome di una sequenza visto che è immutabile?
-------------------------------------------------------------------

La maggior parte degli oggetti BioJava Sequence sono immutabili. Questa
caratteristica da una grande sicurezza nel prevenire cambiamenti o
anomalie che possono causare la corruzione dei dati. Una conseguenza di
ciò è che non esiste alcun metodo del tipo setName() all'interno della
classe Sequence. Una maniera per poter cambiare la "vista" di una
Sequence è quella di creare una ViewSequence utilizzando la Sequence
originale come argomento del costruttore. In sostanza invece di
utilizzare una sequenza con nome 'foo', creiamo una ViewSequence con
nome 'bar' passandogli nel costruttore la sequenza di nome 'foo'.
Durante l'esecuzione del programma useremo la ViewSequence 'bar' (al
posto della sequenza 'foo') che agirà come wrapper redirigendo tutte le
chiamate verso la sequenza originale. Con un unico vantaggio: la
ViewSequence può essere chiamata come vogliamo.

Il codice sequente mostra quanto detto sopra:

```java import java.io.\*;

import org.biojava.bio.seq.\*; import org.biojava.bio.seq.io.\*; import
org.biojava.bio.symbol.\*;

public class NameChange {

` public static void main(String[] args) {`  
`   try {`  
`     Sequence seq =`  
`         DNATools.createDNASequence("atgcgctaggctag","gi|12356|ABC123");`

`     //creo un vista della sequenze assegnando un nome alla view`  
`     Sequence view = SequenceTools.view(seq, "ABC123");`

`     //print to FASTA to prove the name has changed`  
`     SeqIOTools.writeFasta(System.out, view);`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //tried to make seq with non DNA symbol`  
`     ex.printStackTrace();`  
`   }catch (IOException ex) {`  
`     //couldn't print view to System out??`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
