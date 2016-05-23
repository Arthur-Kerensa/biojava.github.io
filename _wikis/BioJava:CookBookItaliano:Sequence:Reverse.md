---
title: BioJava:CookBookItaliano:Sequence:Reverse
---

Come posso fare il complemento inverso di una sequenza o di una SymbolList?
---------------------------------------------------------------------------

Per ottenere il complemento inverso di una DNA SymbolList o si una DNA
Sequence basta utilizzare il metodo statico
DNATools.reverseComplement(SymbolList sl). Un metodo equivalente è
presente all'interno della classe RNATools per effettuare la stessa
operazione sulle Sequences e le SymbolList basate sull'RNA.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class ReverseComplement {

` public static void main(String[] args) {`  
`  `  
`   try {`  
`     //make a DNA SymbolList`  
`     SymbolList symL = DNATools.createDNA("atgcacgggaactaa");`

`     //reverse complement it`  
`     symL = DNATools.reverseComplement(symL);`  
`    `  
`     //prove that it worked`  
`     System.out.println(symL.seqString());`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //viene sollevata una eccezione se non vengono utilizzati i Simboli previsti dallo IUB`  
`     ex.printStackTrace();`  
`   }catch (IllegalAlphabetException ex) {`  
`     //questa eccezione viene sollevata se si cerca di effettuare il complemento inverso di`  
`     //una non DNA (non RNA) Sequence utilizzando DNATools (RNATools)`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
