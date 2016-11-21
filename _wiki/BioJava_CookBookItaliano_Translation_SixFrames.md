---
title: BioJava:CookBookItaliano:Translation:SixFrames
permalink: wiki/BioJava%3ACookBookItaliano%3ATranslation%3ASixFrames
---

Come posso tradure una sequenza di nucleotidi secondo tutti i sei frame?
------------------------------------------------------------------------

Questo è probabilmente una dele più frequenti applicazioni della
bioinformatica e una delle questioni più postate all'interno della
mailing list.

La traduzione secondo tutti i sei frame è utile per individuare le più
ampie Cornici di lettura aperte (Open Reading Frames) le quali, è noto,
sono redioni codificanti o al limite sono regioni prive di introni. Per
risolvere il problema della traduzione a sei frame basta prendere una
sotto sequenza della sequenza di interesse e invertirla, traslarla o
crearne il complemento in maniera appropriata, per poi ovviamente
tradurla. L'unico ostacolo che ci si pone dinnanzi e come scegliere le
sottosequenze in maniera tale da avere regioni ugualmente divisibili per
tre, altrimenti il metodo translate solleverà una
IllegalArgumentException.

L'esempio seguente mostra un semplice programma che data una sequenza ne
fa la traduzione secondo tutti i sei frame o leggendolo da un file in
formato fasta o prendendo la sequenza da una costante, il risultato
viene poi memorizzato in un file e inviato nello STDOUT in formato
FASTA.

*Nota Bene:Segui questo
[link](/wiki/BioJava:CookBookItaliano:Sequence:SubSequence "wikilink") per
scoprire come ottenere una porzione di una Sequenza per poi tradurla*

```java import java.io.BufferedReader; import java.io.File; import
java.io.FileOutputStream; import java.io.FileReader; import
java.io.IOException; import java.io.PrintStream; import
java.util.NoSuchElementException;

import org.biojava.bio.Annotation; import org.biojava.bio.BioException;
import org.biojava.bio.seq.DNATools; import
org.biojava.bio.seq.RNATools; import org.biojava.bio.seq.Sequence;
import org.biojava.bio.seq.SequenceIterator; import
org.biojava.bio.seq.SequenceTools; import
org.biojava.bio.seq.io.SymbolTokenization; import
org.biojava.bio.symbol.AlphabetManager; import
org.biojava.bio.symbol.IllegalAlphabetException; import
org.biojava.bio.symbol.SymbolList; import
org.biojavax.bio.seq.RichSequence;

/\*\*

`* `

`* Programma per la traduzione secondo tutti i 6 frame di una sequenza di nucleotidi`  
`* utilizzo: java Hex.class `<file>` `<DNA|RNA>` o nessun argomento verranno utilizzati dei parametri standard`  
`* `

`*/`

public class Hex {

`   public static void main(String[] args) {`  
`       `  
`       String filename = "";`  
`       String type = "";`

`       try {`  
`           if (args.length != 0) {`  
`               filename = args[0];`  
`               type = args[1].toUpperCase();`  
`           }else{`  
`               filename =System.getProperty("java.io.tmpdir")+"/MYOZ1.fasta";`  
`               type="DNA";`  
`               FileOutputStream f = new FileOutputStream(new File(filename));  `  
`               PrintStream ps = new PrintStream(f);`  
`               ps.print(MYOZ1);`  
`               ps.close();`  
`               f.close();`  
`           }`

`           SymbolTokenization toke = AlphabetManager.alphabetForName(type)`  
`                   .getTokenization("token");`

`           BufferedReader br = new BufferedReader(new FileReader(filename));`

`           SequenceIterator seqi = RichSequence.IOTools.readFasta(br,`  
`                   toke, null);`  
`           `  
`           // per ogni sequenza`  
`           while (seqi.hasNext()) {`  
`               Sequence seq = seqi.nextSequence();`

`               // per ogni frame`  
`               for (int i = 0; i < 3; i++) {`  
`                   SymbolList prot;`  
`                   Sequence trans;`

`                   // prendiamo il frame di lettura`  
`                   // Ricorda che in una SymbolList il primo elemento ha indice 1`  
`                                       // Ricorda che se la lunghezza della lista non è divisibile per 3`  
`                                       // altrimento quando se ne effettua la traduzione verrà sollevata una`  
`                                       // eccezione di tipo IllegalArgumentException `  
`                   SymbolList syms = seq.subList(i + 1, seq.length()`  
`                           - (seq.length() - i) % 3);`

`                                       // se è DNA lo trascrivo in RNA`  
`                   if (syms.getAlphabet() == DNATools.getDNA()) {`  
`                       syms = DNATools.toRNA(syms);`  
`                   }`

`                   // redirigo l'output sullo STDOUT`  
`                   prot = RNATools.translate(syms);`  
`                   trans = SequenceTools.createSequence(prot, "", seq`  
`                           .getName()`  
`                           + "TranslationFrame: +" + i,`  
`                           Annotation.EMPTY_ANNOTATION);`

`                   RichSequence.IOTools.writeFasta(System.out, trans, null);`

`                   // redirigo l'output sullo STDOUT`  
`                   syms = RNATools.reverseComplement(syms);`  
`                   prot = RNATools.translate(syms);`  
`                   trans = SequenceTools.createSequence(prot, "", seq`  
`                           .getName()`  
`                           + " TranslationFrame: -" + i,`  
`                           Annotation.EMPTY_ANNOTATION);`  
`   `  
`                   RichSequence.IOTools.writeFasta(System.out, trans, null);`  
`               }`  
`           }`  
`           br.close();`  
`       } catch (IOException e) {`  
`           e.printStackTrace();`  
`       } catch (IllegalAlphabetException e) {`  
`           e.printStackTrace();`  
`       } catch (NoSuchElementException e) {`  
`           e.printStackTrace();`  
`       } catch (BioException e) {`  
`           e.printStackTrace();`  
`       }`  
`   }`

`   private static String MYOZ1 = ">gi|21359948|ref|NM_021245.2| Homo sapiens myozenin 1 (MYOZ1), mRNA "`  
`           + "\n"`  
`           + "GTTTCTCCCTAAGTGCTTCTTTGGATCTCAGGCTCTAGGTGCAATGTGAAGGGGAGTCCCTGGGCAGACTGATCCCTGGC"`  
`           + "TCAGACAGTTCAGTGGGAGAATCCCAAAGGCCTTTTCCCTCCTTCCTGAGCCTCCGGGCAAGGAGGGAGGGATCTTGGTT"`  
`           + "CCAGGGTCTCAGTACCCCCTGTGCCATTTGAGCTGCTTGCGCTCATCATCTCTATTAATAACCAACTTCCCTCCCCCACT"`  
`           + "GCCAGTGCTGCCCCCACGCCTGCCCAGCTCGTGTTCTCCGGTCACAGCAGCTCAGTCCTCCAAAGCTGCTGGACCCCAGG"`  
`           + "GAGAGCTGACCACTGCCCGAGCAGCCGGCTGAATCCACCTCCACAATGCCGCTCTCAGGAACCCCGGCCCCTAATAAGAA"`  
`           + "GAGGAAATCCAGCAAGCTGATCATGGAACTCACTGGAGGTGGACAGGAGAGCTCAGGCTTGAACCTGGGCAAAAAGATCA"`  
`           + "GTGTCCCAAGGGATGTGATGTTGGAGGAACTGTCGCTGCTTACCAACCGGGGCTCCAAGATGTTCAAACTGCGGCAGATG"`  
`           + "AGGGTGGAGAAGTTTATTTATGAGAACCACCCTGATGTTTTCTCTGACAGCTCAATGGATCACTTCCAGAAGTTCCTTCC"`  
`           + "AACAGTGGGGGGACAGCTGGGCACAGCTGGTCAGGGATTCTCATACAGCAAGAGCAACGGCAGAGGCGGCAGCCAGGCAG"`  
`           + "GGGGCAGTGGCTCTGCCGGACAGTATGGCTCTGATCAGCAGCACCATCTGGGCTCTGGGTCTGGAGCTGGGGGTACAGGT"`  
`           + "GGTCCCGCGGGCCAGGCTGGCAGAGGAGGAGCTGCTGGCACAGCAGGGGTTGGTGAGACAGGATCAGGAGACCAGGCAGG"`  
`           + "CGGAGAAGGAAAACATATCACTGTGTTCAAGACCTATATTTCCCCATGGGAGCGAGCCATGGGGGTTGACCCCCAGCAAA"`  
`           + "TGAACCCCTGGTCCTCTACAACCAAAACCTCTCCAACAGGCCTTCTTTCAATCGAACCCCTATTCCCTGGCTGAGCTCTG"`  
`           + "GGGAGCCTGTAGACTACAACGTGGATATTGGCATCCCCTTGGATGGAGAAACAGAGGAGCTGTGAGGTGTTTCCTCCTCT"`  
`           + "GATTTGCATCATTTCCCCTCTCTGGCTCCAATTTGGAGAGGGAATGCTGAGCAGATAGCCCCCATTGTTAATCCAGTATC"`  
`           + "CTTATGGGAATGGAGGGAAAAAGGAGAGATCTACCTTTCCATCCTTTACTCCAAGTCCCCACTCCACGCATCCTTCCTCA"`  
`           + "CCAACTCAGAGCTCCCCTTCTACTTGCTCCATATGGAACCTGCTCGTTTATGGAATTTGCTCTGCCACCAGTAACAGTCA"`  
`           + "ATAAACTTCAAGGAAAATGAAAAAAAA";`

} ```
