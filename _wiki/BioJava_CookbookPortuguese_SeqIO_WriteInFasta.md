---
title: BioJava:CookbookPortuguese:SeqIO:WriteInFasta
permalink: wikis/BioJava%3ACookbookPortuguese%3ASeqIO%3AWriteInFasta
---

Como eu imprimo uma sequencia no formato Fasta?
-----------------------------------------------

O FASTA é um formato de saída padrão para dados de bioinformatica,
conveniente e fácil de ler. O BioJava possui uma classe de ferramentas
chamada *SeqIOTools* que provê métodos estáticos para executar várias
tarefas comums de entrada e saida (IO) em bioinformatica. Os trechos de
código abaixo demonstram como imprimir uma *Sequence* ou até mesmo um
''SequenceDB' completo em formato FASTA utilizando um *OutputStream* em
conjunto com o *System*.**out**.

Todos os métodos do tipo *Write*XX do *SeqIOTools* possui um
*OutputStream* como argumento. Deste modo você pode enviar os dados
recém formatados para um arquivo ou outro método ou STDOUT, STDERR etc.

A classe *SeqIOTools* pode ser encontrada na package
org.biojava.bio.seq.io.

### Imprimindo uma SequenceDB

```java

`     //cria uma instancia de SequenceDB interface`  
`     SequenceDB db = new HashSequenceDB();`

`     //adiciona as sequencias para o DB`  
`     db.addSequence(seq1);`  
`     db.addSequence(seq2);`

`     /*`  
`      * agora imprime para um output stream no formato FASTA usando um método estatico`  
`      * da classe de utilitário SeqIOTools. Neste caso nosso output stream é`  
`      * STDOUT`  
`      */`  
`     SeqIOTools.writeFasta(System.out, db);`

```

### Imprimindo de uma SequenceIterator

Muitos métodos do tipo *read*XXX() da classe *SeqIOTools* retornam um
objeto do tipo *SequenceIterator* que itera sobre todas as *Sequences*
de um arquivo. A maioria dos métodos *write*XXX() da *SeqIOTools* tem
uma versão dos métodos que recebem um *SequenceIterator* como argumento.
ex:

```java

`     SequenceIterator iter =`  
`         (SequenceIterator)SeqIOTools.fileToBiojava(fileType, br);`

`     // e agora escreve tudo para FASTA, (você pode escrever em `  
`     // qualquer OutputStream, não apenas System.out)`

`     SeqIOTools.writeFasta(System.out, iter);`

```

### Imprimindo uma única Sequence

```java

`     /*`  
`      * SeqIOTools também possui um método que recebe uma única sequencia `  
`      * assim você não tem que fazer um SequenceDB`  
`      */`  
`     SeqIOTools.writeFasta(System.out, seq1);`

```
