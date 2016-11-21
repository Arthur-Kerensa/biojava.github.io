---
title: BioJava:CookbookFrench:Locations:Range
permalink: wiki/BioJava%3ACookbookFrench%3ALocations%3ARange
---

Comment faire pour spécifier une position par intervalle (*RangeLocation*)?
---------------------------------------------------------------------------

Dans BioJava, une *RangeLocation* est un objet qui contient les
positions de départ (minimum) et de fin (maximum) d'une région sur une
*SymbolList* ou une *Sequence*. Les minimum et maximum sont inclusifs.

L'exemple suivant montre l'utilisation d'une RangeLocation.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class SpecifyRange {

` public static void main(String[] args) {`  
`   try {`  
`     //créer une RangeLocation contenant les résidus 3 a 8`  
`     Location loc = LocationTools.makeLocation(3,8);`  
`     //imprimer la position désirée`  
`     System.out.println("Location: "+loc.toString());`

`     //créer une SymbolList`  
`     SymbolList sl = RNATools.createRNA("gcagcuaggcggaaggagc");`  
`     System.out.println("SymbolList: "+sl.seqString());`

`     //obtenir la SymbolList specifiée par loc`  
`     SymbolList sym = loc.symbols(sl);`  
`     System.out.println("Symbols specified by Location: "+sym.seqString());`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //symbole illégal utilisé pour créer sl`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
