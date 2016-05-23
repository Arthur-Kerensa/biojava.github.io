---
title: BioJava:CookbookFrench:PDB:Seqres
---

Obtenir les informations SEQRES et ATOM contenues dans les fichiers PDB
-----------------------------------------------------------------------

Les informations SEQRES contenues dans un fichier PDB contiennent la
séquence en acides aminés ou en nucléotides de chaque chaîne de la
macromolécule décrite par le fichier. Dans le cas des informations ATOM,
elles correspondent aux coordonnées de ces résidus qui ont pu être
observé.

Afin de joindre ces deux éléments d'information, BioJava aligne les
informations SEQRES et ATOM pour chaque chaîne. Cet alignement est
optionnel mais sera fait par défaut à moins d'utiliser la méthode
PDBFileReader.setAlignSeqRes() pour spécifier le contraire. L'accès à
l'information des groupes ATOM se fait via la méthode
Chain.getAtomGroups(); l'accès à l'information des groupes SEQRES se
fait de la même manière via la méthode Chain.getSeqResGroups(). Les
groupes dérivés de groupes SEQRES seront vides (c.-à-d. sans Atomes) à
moins qu'ils ne puissent être ramené à des informations de groupes ATOM.
Dans un tel cas, il sera alors possible d'accéder à l'informations des
groupes ATOM.

```java

public static void main(String[] args){

`       String code =  "1aoi";`

`       PDBFileReader pdbreader = new PDBFileReader();`  
`   pdbreader.setPath("/Path/To/PDBFiles/");`  
`   pdbreader.setParseSecStruc(true);// lire l'information de la structure secondaire contenu dnas le fichier PDB`  
`   pdbreader.setAlignSeqRes(true);  // aligner les informations SEQRES et ATOM`  
`   pdbreader.setAutoFetch(true);    // obtenir les fichiers PDB à partir du WWW si non-disponible localement`

`   try{`  
`       Structure struc = pdbreader.getStructureById(code);`  
`       `  
`       System.out.println("The SEQRES and ATOM information is available via the chains:");`

`       int modelnr = 0 ; // aussi 0 si structure est XRAY.`

`       List`<Chain>` chains = struc.getChains(modelnr);`  
`       for (Chain cha:chains){`  
`           List`<Group>` agr = cha.getAtomGroups("amino");`  
`           List`<Group>` hgr = cha.getAtomGroups("hetatm");`  
`           List`<Group>` ngr = cha.getAtomGroups("nucleotide");`

`           System.out.print("chain: >"+cha.getName()+"<");`  
`           System.out.print(" length SEQRES: " +cha.getLengthSeqRes());`  
`           System.out.print(" length ATOM: " +cha.getAtomLength());`  
`           System.out.print(" aminos: " +agr.size());`  
`           System.out.print(" hetatms: "+hgr.size());`  
`           System.out.println(" nucleotides: "+ngr.size());  `  
`       }`

`   } catch (Exception e) {`  
`       e.printStackTrace();`  
`   }`

}

```

Ce programme produire la sortie suivante:

    The SEQRES and ATOM information is available via the chains:
    chain: >A< length SEQRES: 116 length ATOM: 98 aminos: 98 hetatms: 0 nucleotides: 0
    chain: >B< length SEQRES: 87 length ATOM: 83 aminos: 83 hetatms: 0 nucleotides: 0
    chain: >C< length SEQRES: 116 length ATOM: 115 aminos: 115 hetatms: 0 nucleotides: 0
    chain: >D< length SEQRES: 99 length ATOM: 99 aminos: 99 hetatms: 0 nucleotides: 0
    chain: >E< length SEQRES: 116 length ATOM: 116 aminos: 116 hetatms: 0 nucleotides: 0
    chain: >F< length SEQRES: 87 length ATOM: 87 aminos: 87 hetatms: 0 nucleotides: 0
    chain: >G< length SEQRES: 116 length ATOM: 108 aminos: 108 hetatms: 0 nucleotides: 0
    chain: >H< length SEQRES: 99 length ATOM: 99 aminos: 99 hetatms: 0 nucleotides: 0
    chain: >I< length SEQRES: 0 length ATOM: 146 aminos: 0 hetatms: 0 nucleotides: 146
    chain: >J< length SEQRES: 0 length ATOM: 146 aminos: 0 hetatms: 0 nucleotides: 146
    chain: > < length SEQRES: 0 length ATOM: 19 aminos: 0 hetatms: 19 nucleotides: 0
