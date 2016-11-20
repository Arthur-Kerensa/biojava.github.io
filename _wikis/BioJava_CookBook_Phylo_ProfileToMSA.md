---
title: BioJava:CookBook:Phylo:ProfileToMSA
permalink: wikis/BioJava%3ACookBook%3APhylo%3AProfileToMSA
---

`       MultipleSequenceAlignment`<ProteinSequence, AminoAcidCompound>` multipleSequenceAlignment= new MultipleSequenceAlignment `<ProteinSequence, AminoAcidCompound>`();`  
`       List`<AlignedSequence<ProteinSequence,AminoAcidCompound>`> alSeq=profile.getAlignedSequences();`  
`       Sequence`<AminoAcidCompound>` seq;`  
`       ProteinSequence pSeq;`  
`       for (int i=0; i<alSeq.size(); i++){`  
`     `  
`           seq=alSeq.get(i);`  
`           pSeq=new ProteinSequence(seq.getSequenceAsString(),seq.getCompoundSet());`  
`           pSeq.setAccession(seq.getAccession());`  
`           multipleSequenceAlignment.addAlignedSequence(pSeq);`  
`              `  
`       }`
