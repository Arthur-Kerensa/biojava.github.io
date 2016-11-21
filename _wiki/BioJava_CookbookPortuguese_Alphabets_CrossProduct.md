---
title: BioJava:CookbookPortuguese:Alphabets:CrossProduct
permalink: wiki/BioJava%3ACookbookPortuguese%3AAlphabets%3ACrossProduct
---

Como crio um CrossProductAlphabet, por exemplo, um alfabeto de codons?
----------------------------------------------------------------------

Um *CrossProductAlphabet* resulta da multiplicação de alguns
*Alphabet*s. Eles são usados para transformar 2 ou mais *Symbol*s em um
único *Symbol* "cross product".

Por exemplo:

Utilizando 3 nucleotideos do alfabeto de [DNA](wp:DNA "wikilink") você
pode obter um [codon](wp:codon "wikilink") representado por um único
*Symbol*. A partir dai é possível obter uma contabilização dos
[codons](wp:codon "wikilink") em um objeto *Count* ou ainda utilizá-los
em um objeto *Distribution*.

*CrossProductAlphabets* podem ser criados pelo nome (se o componente
*Alphabet* está registrado no *AlphabetManager*) ou criando uma lista
com o auxilio da Classe *Collections*. Ambas as possibilidades são
mostradas no exemplo abaixo:

```java import java.util.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.symbol.\*;

public class CrossProduct {

` public static void main(String[] args) {`

`   //cria um CrossProductAlphabet a partir de uma Lista`  
`   List l = Collections.nCopies(3, DNATools.getDNA());`  
`   Alphabet codon = AlphabetManager.getCrossProductAlphabet(l);`

`   //retorna o Alfabeto de codons`  
`   Alphabet codon2 =`  
`       AlphabetManager.generateCrossProductAlphaFromName("(DNA x DNA x DNA)");`

`   //exibe se os dois alfabetos são canonical`  
`   System.out.println(codon == codon2);`  
` }`

} ```
