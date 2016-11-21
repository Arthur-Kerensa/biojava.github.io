---
title: BioJava:CookBookItaliano:Alphabets:Custom
permalink: wikis/BioJava%3ACookBookItaliano%3AAlphabets%3ACustom
---

Come posso creare un Alfabeto personalizzato con Simboli personalizzati?
------------------------------------------------------------------------

Questo esempio mostra la creazione di un alfabeto binario che ha 2
[Simboli](http://www.biojava.org/docs/api15/org/biojava/bio/symbol/Symbol.html)
zero e uno. La personalizzazione dei
[Simboli](http://www.biojava.org/docs/api15/org/biojava/bio/symbol/Symbol.html)
e
dell'[Alfabeto](http://www.biojava.org/docs/api15/org/biojava/bio/symbol/Alphabet.html)
può essere utilizzata per costruire nuove [Liste di
Simboli](http://www.biojava.org/docs/api15/org/biojava/bio/symbol/SymbolList.html),
[Sequenze](http://www.biojava.org/docs/api15/org/biojava/bio/seq/Sequence.html),
[Distribuzioni](http://www.biojava.org/docs/api15/org/biojava/bio/dist/Distribution.html),
etc.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.\*;
import java.util.\*;

public class Binary {

`   public static void main(String[] args) {`

`       //crea il Simbolo zero senza nessuna annotazione`  
`       Symbol zero =`  
`           AlphabetManager.createSymbol("zero", Annotation.EMPTY_ANNOTATION);`

`       //creo il Simbolo uno`  
`       Symbol one =`  
`           AlphabetManager.createSymbol("one", Annotation.EMPTY_ANNOTATION);`

`       //inserisco i 2 simboli in un Set`  
`       Set symbols = new HashSet();`  
`       symbols.add(zero); symbols.add(one);`

`       //creo l'alfabeto binary`  
`       FiniteAlphabet binary = new SimpleAlphabet(symbols, "Binary");`

`       //itero i vari elementi dell'alfabeto per verificare che tutto funzioni correttamente`  
`       for (Iterator i = binary.iterator(); i.hasNext(); ) {`  
`         Symbol sym = (Symbol)i.next();`  
`         System.out.println(sym.getName());`  
`       }`

`       //Bisogna registrare i nuovi alfabeti con l'AlphabetManager`  
`       AlphabetManager.registerAlphabet(binary.getName(), binary);`

`       /*`  
`        * Il nuovo alfabeto cosi' creato e' stato registrato con `  
`        * l'AlphabetManager con il nome "Binary". Per ottenere l'istanza di`  
`        * di quest'ultimo basta richiamarlo con il nome assegnato alla precendente istanza`  
`        */`  
`       `  
`       Alphabet alpha = AlphabetManager.alphabetForName("Binary");`

`       //verifico che siamo uguali`  
`       System.out.println(alpha == binary);`  
`     }`  
`   }````
