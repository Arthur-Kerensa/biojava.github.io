---
title: BioJava:CookBook3:ModFinder
---

How can I identify protein modifications in a structure?
--------------------------------------------------------

BioJava provide a module *biojava3-modfinder* for identification of
protein pre-, co-, and post-translational modifications from structures.
[A list of protein
modifications](/wikis/BioJava:CookBook3:SupportedProtMod "wikilink") has been
pre-loaded. It is possible to identify all pre-loaded modifications or
part of them.

Example: identify and print all preloaded modifications from a structure
------------------------------------------------------------------------

```java

Set<ModifiedCompound> identifyAllModfications(Structure struc) {

   ProteinModificationIdentifier parser = new ProteinModificationIdentifier();
   parser.identify(struc);
   Set`<ModifiedCompound> mcs = parser.getIdentifiedModifiedCompound();
   return mcs;

}
```

Example: identify phosphorylation sites in a structure
------------------------------------------------------

```java List<ResidueNumber> identifyPhosphosites(Structure struc) {

   List`<ResidueNumber> phosphosites = new ArrayList`<ResidueNumber>`();  
   ProteinModificationIdentifier parser = new ProteinModificationIdentifier();  
   parser.identify(struc, ProteinModificationRegistry.getByKeyword("phosphoprotein"));  
   Set`<ModifiedCompound> mcs = parser.getIdentifiedModifiedCompound();  
   for (ModifiedCompound mc : mcs) {`  
       Set`<StructureGroup> groups = mc.getGroups(true);  
       for (StructureGroup group : groups) {`  
           phosphosites.add(group.getPDBResidueNumber());  
       }`  
   }`  
   return phosphosites;

} ```

Demo code to run the above methods
----------------------------------

```java import org.biojava.nbio.structure.ResidueNumber; import
org.biojava.nbio.structure.Structure; import
org.biojava.nbio.structure.io.PDBFileReader; import
org.biojava.nbio.protmod.structure.ProteinModificationIdentifier;

public static void main(String[] args) {

   try {`  
       PDBFileReader reader = new PDBFileReader();  
       reader.setAutoFetch(true);

       // identify all modificaitons from PDB:1CAD and print them`  
       String pdbId = "1CAD";  
       Structure struc = reader.getStructureById(pdbId);  
       Set`<ModifiedCompound> mcs = identifyAllModfications(struc);  
       for (ModifiedCompound mc : mcs) {`  
           System.out.println(mc.toString());  
       }`

       // identify all phosphosites from PDB:3MVJ and print them`  
       pdbId = "3MVJ";  
       struc = reader.getStructureById(pdbId);  
       List`<ResidueNumber> psites = identifyPhosphosites(struc);  
       for (ResidueNumber psite : psites) {`  
           System.out.println(psite.toString());  
       }`  
   } catch(Exception e) {`  
       e.printStackTrace();  
   }`

} ```

See also
--------

<div style="-moz-column-count:3; column-count:3;">
-   [How can I get the list of supported protein
    modifications?](/wikis/BioJava:CookBook3:SupportedProtMod "wikilink")
-   [How can I define a new protein
    modification?](/wikis/BioJava:CookBook3:AddProtMod "wikilink")

</div>

