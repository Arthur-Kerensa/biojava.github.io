---
title: BioJava:Cookbook:SeqIO:ReadGESBiojavax
permalink: wiki/BioJava%3ACookbook%3ASeqIO%3AReadGESBiojavax
---

How do I read a sequence file (in whatever format) with the new Biojavax extension?
-----------------------------------------------------------------------------------

Since its inception, Biojava has been able to read files in the most
popular file formats used in bio-informatics. Since Biojava 1.5 and the
addition of the Biojavax extension, the way of reading files has changed
somewhat. Although you can still read sequence files using the
**SeqIOTools** class, it has been marked deprecated and is now replaced
by the **RichSequence.IOTools** class. This class keeps the mapping of
the information found in a given file format, allowing better
correspondance to BioSQL databases. It also enforce the use of
namespaces. The Biojavax extension also allows for easy parser creation
if you need to read a new file format. But for most users, this is a
rather remote thing. So, how is it different? Actually, it is not that
different ;-) **RichSequence.IOTools** allows you to read files (DNA,
RNA or protein) in the following format:

-   EMBL (native or XML)
-   FASTA
-   GenBank
-   INSDseq
-   UniProt (native or XML)

This class also has a method, *readFile*, that can read a file while
guessing its format.

```java import java.io.BufferedReader; import java.io.FileReader;

import org.biojavax.SimpleNamespace; import
org.biojavax.bio.seq.RichSequence; import
org.biojavax.bio.seq.RichSequenceIterator;

public class ReadGES\_BJ1\_6{

`   /* `  
`    * ReadGES_BJ1_6.java - A pretty simple demo program to read a sequence file`  
`    * with a known format using Biojavax extension found in BJ1.6. `  
`    * `  
`    * You only need to provide a file as args[0]`  
`    */`  
`   public static void main(String[] args) {`  
`       BufferedReader br = null;`  
`       SimpleNamespace ns = null;`  
`       `  
`       try{`  
`           br = new BufferedReader(new FileReader(args[0]));`  
`           ns = new SimpleNamespace("biojava");`  
`           `  
`           // You can use any of the convenience methods found in the BioJava 1.6 API`  
`           RichSequenceIterator rsi = RichSequence.IOTools.readFastaDNA(br,ns);`  
`   `  
`           // Since a single file can contain more than a sequence, you need to iterate over`  
`           // rsi to get the information.`  
`           while(rsi.hasNext()){`  
`               RichSequence rs = rsi.nextRichSequence();`  
`               System.out.println(rs.getName());`  
`           }`  
`       }`  
`       catch(Exception be){`  
`           be.printStackTrace();`  
`           System.exit(-1);`  
`       }`  
`   }`

} ```
