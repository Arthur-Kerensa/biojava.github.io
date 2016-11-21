---
title: BioJava:CookbookPortuguese:Sequence
permalink: wikis/BioJava%3ACookbookPortuguese%3ASequence
---

Como eu crio uma Sequence de uma String ou crio de volta uma String de um Objeto Sequence?
------------------------------------------------------------------------------------------

Há muito tempo que se utiliza uma sequencia representando-a como uma
*String* como por exemplo "atgccgtggcatcgaggcatatagc". Este é um método
bastante conveniente para vizualizar de forma simples a representação de
um polímero biológico complexo. O BioJava utiliza *SymbolLists* e
*Sequences* para representar este polímeros biológicos como Objetos. Um
objeto do tipo ''Sequence' estende *SymbolList* e provê métodos extras
para armazenar coisas, como por exemplo, o nome da sequencia ou qualquer
critério.

Dentro da *Sequence* e *SymbolList* o polímero não é armazenado como uma
String. O BioJava diferencia os resíduos do polímero como objetos do
tipo *Symbol* que vêm de *Alphabet*s diferentes. Deste modo é fácil
dizer se uma sequencia pertence a DNA ou RNA ou qualquer outra coisa, em
outras palavras o símbolo 'A' do DNA não é igual ao símbolo 'A' do RNA.
A parte fundamental está na necessidade de existir um metodo em que um
programador possa converter uma *String* facilmente legível em um Objeto
do Biojava, bem como permitir que inverso também ocorra. Desta forma, o
BioJava possui *Tokenizer*s que podem ler uma *String* de um texto e
convertê-laem um objeto *Sequence* do BioJava ou um objeto *SymbolList*.
No caso de DNA, RNA e Proteina você pode fazer isto com uma única
chamada de método. A chamada é feita para um método estático das classes
DNATools, RNATools ou ProteinTools.

### String para SymbolList

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSymbolList {

` public static void main(String[] args) {`  
`  `  
`   try {`  
`     //cria um DNA SymbolList a partir de uma String`  
`     SymbolList dna = DNATools.createDNA("atcggtcggctta");`

`     //cria um RNA SymbolList a partir de uma String`  
`     SymbolList rna = RNATools.createRNA("auugccuacauaggc");`

`     //cria uma Protein SymbolList a partir de uma String`  
`     SymbolList aa = ProteinTools.createProtein("AGFAVENDSA");`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //isto irá acontecer se utilizar um caracter não aceito pela IUB.`  
`     ex.printStackTrace();`  
`   }`  
`  `  
` }`

} ```

### String para Sequence

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSequence {

` public static void main(String[] args) {`

`   try {`  
`     //cria uma sequencia de DNA com o nome dna_1`  
`     Sequence dna = DNATools.createDNASequence("atgctg", "dna_1");`

`     //cria uma sequencia de RNA sequence com o nome rna_1`  
`     Sequence rna = RNATools.createRNASequence("augcug", "rna_1");`

`     //cria uma sequencia de Protein com o nome prot_1`  
`     Sequence prot = ProteinTools.createProteinSequence("AFHS", "prot_1");`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //uma exceção é lançada se voce utilizar um simbolo não IUB `  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```

### SymbolList para String

Você pode chamar o metodo seqString() em um *SymbolList* ou uma
*Sequence* para adquiri-la em forma de uma *String*.

```java import org.biojava.bio.symbol.\*;

public class SymbolListToString {

` public static void main(String[] args) {`  
`   SymbolList sl = null;`  
`   //insira um codigo aqui para instanciar sl`  
`  `  
`   //converte sl numa String`  
`   String s = sl.seqString();`  
` }`

} ```
