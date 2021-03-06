---
title: BioJava:CookBook:Blast:Echo
permalink: wiki/BioJava%3ACookBook%3ABlast%3AEcho
---

How do I parse a large file; Or, How do I make a custom SearchContentHandler?
-----------------------------------------------------------------------------

If you are parsing a blast report (or fasta) you can use the standard
set up, but you may want to know how those search objects that result
are constructed. You may also be interested in making your own
SearchContentHandler. This will be especially true if you are parsing
huge Blast files because if everything ends up in objects that will use
a lot of memory. This can be really annoying if you only want a small
part of the information in the file!

The program below shows a program that I find very useful when I want to
make a custom handler (it also demonstrates how to make one.
Essentially, the program contains a custom handler that listens for all
the parsing events and echos them to STDOUT. This allows you to see what
events are being generated and what type of event contains the
information you are looking for. You can then create a
SearchContentHandler that does your bidding by extending
SearchContentAdapter and overriding the methods that take care of the
events you are interested in.

### BlastEcho.java

```java

`1 import org.xml.sax.*; `  
`2 import java.io.*; `  
`3 import org.biojava.bio.program.sax.*; `  
`4 import org.biojava.bio.program.ssbind.*; `  
`5 import org.biojava.bio.search.*; `  
`6 `  
`7 /** `  
`8  * `

Echo"s events from a blast like sax parser

`9  */ `

10 11 public class BlastEcho { 12 public BlastEcho() { 13 } 14 15
private void echo (InputSource source) throws IOException, SAXException{
16 //make a BlastLikeSAXParser 17 BlastLikeSAXParser parser = new
BlastLikeSAXParser(); 18 //calling this means the parser doesn"t bother
checking the 19 //version of the Blast report before parsing it. 20
parser.setModeLazy(); 21 22 ContentHandler handler = new
SeqSimilarityAdapter(); 23 24 //use our custom SearchContentHandler (see
below) 25 SearchContentHandler scHandler = new EchoSCHandler(); 26
((SeqSimilarityAdapter)handler).setSearchContentHandler(scHandler); 27
28 parser.setContentHandler(handler); 29 parser.parse(source); 30 } 31
32 /\*\* 33 \* Customs Search Content Handler. Intercepts all events and
logs 34 \* them to STDOUT 35 \*/ 36 private class EchoSCHandler extends
SearchContentAdapter{ 37 public void startHit(){ 38
System.out.println("startHit()"); 39 } 40 public void endHit(){ 41
System.out.println("endHit()"); 42 } 43 public void startSubHit(){ 44
System.out.println("startSubHit()"); 45 } 46 public void endSubHit(){ 47
System.out.println("endSubHit()"); 48 } 49 public void startSearch(){ 50
System.out.println("startSearch"); 51 } 52 public void endSearch(){ 53
System.out.println("endSearch"); 54 } 55 public void
addHitProperty(Object key, Object val){ 56
System.out.println("\\tHitProp:\\t"+key+": "+val); 57 } 58 public void
addSearchProperty(Object key, Object val){ 59
System.out.println("\\tSearchProp:\\t"+key+": "+val); 60 } 61 public
void addSubHitProperty(Object key, Object val){ 62
System.out.println("\\tSubHitProp:\\t"+key+": "+val); 63 } 64 public
void setQueryID(String queryID) { 65 System.out.println("\\tQueryID:\\t
"+queryID); 66 } 67 public void setDatabaseID(String databaseID) { 68
System.out.println("\\tDatabaseID: "+databaseID); 69 } 70 } 71 72 public
static void main(String[] args) throws Exception{ 73 InputSource is =
new InputSource(new FileInputStream(args[0])); 74 BlastEcho blastEcho =
new BlastEcho(); 75 blastEcho.echo(is); 76 } 77 } ```
