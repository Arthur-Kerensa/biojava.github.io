---
title: BioJava:Performance:AlignSW
---

This is the source code for the [Smith Waterman performance
example](/wikis/BioJava:Performance "wikilink").

```java /\*

`* Jun 25, 2008 Copyright (c) ZBiT, University of Tübingen, Germany`  
`* Compiler: JDK 1.6.0`  
`*/`

/\*\*

`* @author Andreas Dräger (draeger) `<andreas.draeger@uni-tuebingen.de>  
`* @date Jun 25, 2008`  
`*/`

public class AlignmentTest {

`      /**`  
`       * This method computes a pairwise local alignment between two given sequences`  
`       * and prints the result on the standard output stream. The sequences must be`  
`       * genbank files and the substitution matrix must be defined for the same`  
`       * alphabet than both sequences.`  
`       *`  
`       * @param args`  
`       *          query sequence file (genbank), subject sequence file (genbank),`  
`       *          substitution matrix file`

`       */`  
`      public static void main(String[] args) {`  
`              try {`  
`                      RichSequenceIterator rsiQuery = org.biojavax.bio.seq.RichSequence.IOTools`  
`                          .readGenbankDNA(new BufferedReader(new FileReader(args[0])),`  
`                              RichObjectFactory.getDefaultNamespace());`  
`                      RichSequenceIterator rsiSubject = org.biojavax.bio.seq.RichSequence.IOTools`  
`                          .readGenbankDNA(new BufferedReader(new FileReader(args[1])),`  
`                              RichObjectFactory.getDefaultNamespace());`  
`                      if (rsiQuery.hasNext() && rsiSubject.hasNext()) {`  
`                              RichSequence query = rsiQuery.nextRichSequence();`  
`                              RichSequence subject = rsiSubject.nextRichSequence();`  
`                              SequenceAlignment sa = new SmithWaterman(0, 5, 2, 2, 1,`  
`                                  new SubstitutionMatrix((FiniteAlphabet) query.getAlphabet(),`  
`                                      new File(args[2])));`  
`                              sa.pairwiseAlignment(query, subject);`  
`                              System.out.println(sa.getAlignmentString());`  
`                      }`  
`              } catch (FileNotFoundException e) {`  
`                      e.printStackTrace();`  
`              } catch (NoSuchElementException e) {`  
`                      e.printStackTrace();`  
`              } catch (BioException e) {`  
`                      e.printStackTrace();`  
`              } catch (IOException e) {`  
`                      e.printStackTrace();`  
`              } catch (Exception e) {`  
`                      e.printStackTrace();`  
`              }`  
`      }`

} ```
