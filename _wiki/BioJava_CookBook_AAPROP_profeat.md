---
title: BioJava:CookBook:AAPROP:profeat
permalink: wiki/BioJava%3ACookBook%3AAAPROP%3Aprofeat
---

### How can I compute PROFEAT properties via APIs?

BioJava provides a set of APIs to generate PROFEAT properties.  
 PROFEAT generate properties of a protein sequence based on its
converted attributes.  

-   The seven different attributes are
-   Hydrophobicity (Polar, Neutral, Hydrophobicity)
-   Normalized van der Waals volume (Range 0 - 2.78, 2.95 - 4.0, 4.03 -
    8.08)
-   Polarity (Value 4.9 - 6.2, 8.0 - 9.2, 10.4 - 13.0)
-   Polarizability (Value 0 - 1.08, 0.128 - 0.186, 0.219 - 0.409)
-   Charge (Positive, Neutral, Negative)
-   Secondary structure (Helix, Strand, Coil)
-   Solvent accessibility (Buried, Exposed, Intermediate)

Please see
[PROFEAT](http://nar.oxfordjournals.org/content/34/suppl_2/W32.abstract)
for more information about these properties.  
 The class providing the core functionality for this is the
IProfeatProperties class.  

Short Example 1: Computing composition of the various grouping for all seven attributes
---------------------------------------------------------------------------------------

```java String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
Map<ATTRIBUTE, Map<GROUPING, Double>\> attribute2Grouping2Double =
ProfeatProperties.getComposition(sequence); for(ATTRIBUTE
a:attribute2Grouping2Double.keySet()){

`   System.out.println("=======" + a + "=======");`  
`   System.out.println("GROUP1 = " + attribute2Grouping2Double.get(a).get(GROUPING.GROUP1));`  
`   System.out.println("GROUP2 = " + attribute2Grouping2Double.get(a).get(GROUPING.GROUP2));`  
`   System.out.println("GROUP3 = " + attribute2Grouping2Double.get(a).get(GROUPING.GROUP3));`  
`   System.out.println();`

} ```

Short Example 2: Computing the number of transition between various grouping for all seven attribute with respect to the length of sequence
-------------------------------------------------------------------------------------------------------------------------------------------

```java String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
Map<ATTRIBUTE, Map<TRANSITION, Double>\> attribute2Transition2Double =
ProfeatProperties.getTransition(sequence); for(ATTRIBUTE
a:attribute2Transition2Double.keySet()){

`   System.out.println("=======" + a + "=======");`  
`   System.out.println("1<=>1 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_11));`  
`   System.out.println("2<=>2 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_22));`  
`   System.out.println("3<=>3 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_33));`  
`   System.out.println("1<=>2 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_12));`  
`   System.out.println("1<=>3 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_13));`  
`   System.out.println("2<=>3 = " + attribute2Transition2Double.get(a).get(TRANSITION.BETWEEN_23));`  
`   System.out.println();`

} ```

Short Example 3: Computing the position with respect to the sequence where the given distribution of the grouping can be found
------------------------------------------------------------------------------------------------------------------------------

```java String[] sequences = new String[3]; String sequence =
"QIKDLLVSSSTDLDTTLVLVNAIYFKGMWKTAFNAEDTREMPFHVTKQESKPVQMMCMNNSFNVATLPAE";
Map<ATTRIBUTE , Map<GROUPING, Map<DISTRIBUTION, Double>\>\>
attribute2Grouping2Distribution2Double =
ProfeatProperties.getDistributionPosition(sequence); for(ATTRIBUTE
a:attribute2Grouping2Distribution2Double.keySet()){

`   System.out.println("=======" + a + "=======");`  
`   System.out.println("GROUP1 = " + attribute2Grouping2Distribution2Double.get(a).get(GROUPING.GROUP1));`  
`   System.out.println("GROUP2 = " + attribute2Grouping2Distribution2Double.get(a).get(GROUPING.GROUP2));`  
`   System.out.println("GROUP3 = " + attribute2Grouping2Distribution2Double.get(a).get(GROUPING.GROUP3));`

} ```
