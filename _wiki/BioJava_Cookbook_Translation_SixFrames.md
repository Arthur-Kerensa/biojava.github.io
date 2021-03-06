---
title: BioJava:Cookbook:Translation:SixFrames
permalink: wiki/BioJava%3ACookbook%3ATranslation%3ASixFrames
---

How can I translate all six frames of a nucleotide Sequence?
------------------------------------------------------------

This is probably one of the more frequent tasks in bioinformatics and
one of the most frequent questions posted to the mailing list.

Six frame translations are good for identifying large ORFs which can be
indicators of coding regions, at least in species that don't have
introns. A six frame translation is a simple matter of taking
subsequences of the sequence(s) of interest and reverse
complementing/translating as appropriate. The only trick is figuring out
how to take the subsequences so you have regions that are equally
divisible by three.

*NOTE: See ['how to get a
subsequence'](BioJava%3ACookbook%3ASequence%3ASubSequence "wikilink") for a
description of how to get a portion of a Sequence for translation.*

The following example shows a simple program that will six frame
translate all sequences in a file and print the results to STDOUT in
fasta format.

<java> import java.io.BufferedReader; import java.io.File; import
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

`* Program to six-frame translate a nucleotide sequence usage: java Hex `<file>  
`* `<dna|rna>  
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
`           // for each sequence`  
`           while (seqi.hasNext()) {`  
`               Sequence seq = seqi.nextSequence();`

`               // for each frame`  
`               for (int i = 0; i < 3; i++) {`  
`                   SymbolList prot;`  
`                   Sequence trans;`

`                   // take the reading frame`  
`                   // remember that in a SymbolList the first element has`  
`                   // index= 1`  
`                   // remember that if the length of the list evenly divisible`  
`                   // by three an IllegalArgumentException will be thrown`  
`                   SymbolList syms = seq.subList(i + 1, seq.length()`  
`                           - (seq.length() - i) % 3);`

`                   // if it is DNA transcribe it to RNA`  
`                   if (syms.getAlphabet() == DNATools.getDNA()) {`  
`                       syms = DNATools.toRNA(syms);`  
`                   }`

`                   // output forward translation to STDOUT`  
`                   prot = RNATools.translate(syms);`  
`                   trans = SequenceTools.createSequence(prot, "", seq`  
`                           .getName()`  
`                           + "TranslationFrame: +" + i,`  
`                           Annotation.EMPTY_ANNOTATION);`  
`                   /*`  
`                    * This method is deprecated since BioJava 1.5`  
`                    * SeqIOTools.writeFasta(System.out, trans);`  
`                    */`  
`                   RichSequence.IOTools.writeFasta(System.out, trans, null);`

`                   // output reverse frame translation to STDOUT`  
`                   syms = RNATools.reverseComplement(syms);`  
`                   prot = RNATools.translate(syms);`  
`                   trans = SequenceTools.createSequence(prot, "", seq`  
`                           .getName()`  
`                           + " TranslationFrame: -" + i,`  
`                           Annotation.EMPTY_ANNOTATION);`  
`                   /*`  
`                    * This method is deprecated since BioJava 1.5`  
`                    * SeqIOTools.writeFasta(System.out, trans);`  
`                    */`  
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

} </java>
