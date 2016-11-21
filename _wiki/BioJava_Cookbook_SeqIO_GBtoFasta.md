---
title: BioJava:Cookbook:SeqIO:GBtoFasta
permalink: wiki/BioJava%3ACookbook%3ASeqIO%3AGBtoFasta
---

How do I extract Sequences from GenBank/EMBL/UniProt/FASTA/INSDseq and write them as Fasta?
-------------------------------------------------------------------------------------------

To perform this task we are going to extend the general reader from the
previous demo and include in it the ability to write sequence data in
fasta format.One example are provided here:

Following this
[link](http://www.ncbi.nlm.nih.gov/nuccore/146274?report=genbank) you
can download some example files.

```java import java.io.BufferedReader; import java.io.File; import
java.io.FileOutputStream; import java.io.FileReader;

import org.biojavax.Namespace; import org.biojavax.RichObjectFactory;
import org.biojavax.bio.seq.RichSequence; import
org.biojavax.bio.seq.RichSequenceIterator;

public class ReadWriteGES\_BJ1\_6{

`   public static void main(String[] args) {`  
`       BufferedReader br = null;`  
`       Namespace ns = null;`  
`               //this path is used for destination file too`  
`       String filePath= "/whereYourFileIs/sequences";`  
`       String insdExt=".gbc";`  
`       String fastaExt=".FASTA";`  
  
  
`       try{`  
`           br = new BufferedReader(new FileReader(filePath+insdExt));`  
`           ns = RichObjectFactory.getDefaultNamespace();`  
  
  
`               // You can use any of the convenience methods found in the BioJava 1.6 API`  
`                       RichSequenceIterator rsi = RichSequence.IOTools.readINSDseqDNA(br, ns);`  
  
`           // Since a single file can contain more than a sequence, you need to iterate over`  
`           // rsi to get the information.`  
`                       while (rsi.hasNext()) {`  
`                           RichSequence seq = rsi.nextRichSequence();`  
`                           RichSequence.IOTools.writeFasta(new `  
`                                        FileOutputStream(new File(filePath+fastaExt)), seq, ns);`  
`                           System.out.println(`  
`                                   seq.toString() +`  
`                                   " has " + seq.countFeatures() + `  
`                                   " features");`  
`                       }`  
  
`       }`  
`       catch(Exception be){`  
`           be.printStackTrace();`  
`           System.exit(-1);`  
`       }`  
`   }`

} ```
