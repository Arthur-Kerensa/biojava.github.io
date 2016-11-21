---
title: BioJava:CookBookItaliano:Proteomics:AAindex
permalink: wikis/BioJava%3ACookBookItaliano%3AProteomics%3AAAindex
---

Come posso analizzare le proprietà dei vari simboli di una sequenza peptidica utilizzano Amino Acid Index DataBase?
-------------------------------------------------------------------------------------------------------------------

Per poter analizzare le proprietà dei vari residui che compongono la
sequenza amminoacidica, come ad esempio l'idrofobicità media, è
possibile utilizzare l'interfaccia
`[http://www.biojava.org/docs/api14/org/biojava/bio/symbol/SymbolPropertyTable.html SymbolPropertyTable]`.
Vediamo come funziona: sappiamo che il database [Amino Acid
Index](http://www.genome.ad.jp/dbget/aaindex.html) contiene oltre 500
tipi differenti tavole di proprietà di amminoacidi e di coppie di
amminoacidi. Queste tavole sono reperibili a questo indirizzo ftp
*[aaindex1](ftp://ftp.genome.ad.jp/pub/db/genomenet/aaindex/aaindex1)* o
http [AAindex1](http://www.genome.jp/dbget-bin/show_man?aaindex) in
formato testo e possono essere caricate tramite la classe
`AAindexStreamReader`. Utilizzando il metodo
`[http://www.biojava.org/docs/api14/org/biojava/bio/symbol/SymbolPropertyTable.html#getDoubleValue(org.biojava.bio.symbol.Symbol) getDoubleValue]`
della
`[http://www.biojava.org/docs/api14/org/biojava/bio/symbol/SymbolPropertyTable.html SymbolPropertyTable]`
che restituisce un valore numerico per un dato amminoacido, possiamo
recuperare il valore della proprietà corrispondente. Le tavole delle
proprietà possono essere gestite una dopo l'altra tramite il metodo
`nextTable`, che restituisce per ogni tavola un oggetto di tipo
`AAindex` che implementa l'interfaccia `SymbolPropertyTable`. Per poter
effettuare un accesso di tipo casuale a dette tavole basta utilizzare
`SimpleSymbolPropertyTableDB` inizializzandolo con un oggetto di tipo
`AAindexStreamReader`.

L'esempio seguente mostra un metodo che calcola l'idrofobicità media di
un gruppo di residui di una data sequenza peptidica (in questo esempio
la sequenza contiene solamente 20 residui) sulla base della tavola
*CIDH920105* preso dall'indice *aaindex1*:

```java public class Test {

`   public static void main(String[] args) {`  
`             AAindexStreamReader aai = AAindexStreamReader(new FileReader("aaindex1"));`  
`             SimpleSymbolPropertyTableDB db = new SimpleSymbolPropertyTableDB(aai);`  
`             AAindex hydrophobicity = (AAindex) db.table("CIDH920105");`  
`             SymbolList symbols = ProteinTools.createProtein("ARNDCEQGHILKMFPSTWYV");`  
`             double hp = 0.0;`  
`             for (int i = 1; i <= symbols.length(); i++) {`  
`                      hp += hydrophobicity.getDoubleValue(symbols.symbolAt(i));`  
`             }`  
`             System.out.println("Average hydrophobicity: " + Double.toString(hp / symbols.length()));`  
`       }`

} ```
