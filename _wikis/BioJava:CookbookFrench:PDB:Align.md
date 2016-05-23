---
title: BioJava:CookbookFrench:PDB:Align
---

Comment calculer un alignement de structures?
---------------------------------------------

BioJava vous permet de faire l'alignement de deux Structures grâce à un
algorithme basé sur une variation d'un algorithme en C++ fourni par
Peter Lackner, Univ. de Salzburg (communication personnelle). Cet
algorithme est basé sur la représentation des structures de protéines
comme des corps rigides sur lesquelles on transpose une matrice de
distance. L'algorithme peut calculer les types d'alignement suivants:

-   structures complètes
-   chaînes uniques
-   des ensembles d'atomes

Il permet également des solutions alternatives qui peuvent être
rassemblées en groupes d'alignement similaire. Il utilise une série
d'étapes:

-   Il identifie de courtes portions de deux structures protéiques ayant
    des distances intra-moléculaires similaires.
-   Les paires de fragments sont comparés, et si possible, assemblés sur
    de plus longs fragments.
-   Une dernière étape de raffinement tente d'allonger l'alignement pour
    obtenir une alignement complet des deux structures.

Le code source est
[ici](http://code.open-bio.org/svnweb/index.cgi/biojava/view/biojava-live/trunk/src/org/biojava/bio/structure/align/StructurePairAligner.java).
Un programme Java Web Start est
[disponible](http://www.biojava.org/download/performance/biojava-structure-example1.jnlp)
(Le fichier téléchargé comprend aussi Jmol).

Vous pouvez ensuite envoyer cet alignement pour affichage par Jmol grâce
à cette
[recette](http://biojava.org/wiki/BioJava:CookBookFrench:PDB:Jmol).

```java

` public static void main(String[] args){`

`           // Evidemment, adapter selon vos propres`  
`           // valeurs`  
`           PDBFileReader pdbr = new PDBFileReader();          `  
`           pdbr.setPath("/chemin/vers/mes/PDBFiles/");`  
`           `  
`           `  
`           String pdb1 = "1buz";`  
`           String pdb2 = "1ali";            `  
`           String outputfile = "/ailleurs/alig_"+pdb1+"_"+pdb2+".pdb";`  
`         `

`           // AUCUN BESOIN DE MODIFIER QUOIQUE CE SOIT APRES CETTE LIGNE...`  
`           try{`  
` `  
`               StructurePairAligner sc = new StructurePairAligner();            `  
`           `  
`               // Etape 1 : lire les fichiers `  
`               System.out.println("aligning " + pdb1 + " vs. " + pdb2);`  
`           `  
`               Structure s1 = pdbr.getStructureById(pdb1);`  
`               Structure s2 = pdbr.getStructureById(pdb2);                       `  
`               // Vous n'avez pas besoin d'utiliser les structures completes.`  
`               // Vous pourriez n'utiliser que les atomes de votre choix ;-)`

`               // Etape 2 : faire les calculs`  
`               sc.align(s1,s2);`

`               // Si vous desirez plus de controle grace aux parametre d'alignement,`  
`               // utilisez un objet de la classe StrucAligParameters:`

`               //StrucAligParameters params = new StrucAligParameters();`  
`               //params.setFragmentLength(8);      `  
`               //sc.align(s1,s2,params); `

`               AlternativeAlignment[] aligs = sc.getAlignments();`  
`           `  
`               // Rassembler les resultats similaires ensembles `  
`               ClusterAltAligs.cluster(aligs);`  
`           `  
`               // Impression des resultats:`  
`               // L'objet AlternativeAlignment vous donne acces aux matrices de rotation `  
`               // et aux vecteurs de deplacement.`  
`               for(int i=0 ; i< aligs.length; i ++){`  
`                  AlternativeAlignment aa = aligs[i];`  
`                  System.out.println(aa);              `  
`               }`  
`                     `  
`               // Convertir l'objet AlternativeAlignment aa1 en fichier PDB`  
`               // afin de l'ouvrir avec le logiciel de visualisation de votre choix`  
`               // (e.g. Jmol, Rasmol)`  
`           `  
`               if( aligs.length > 0) {`  
`                 AlternativeAlignment aa1 =aligs[0];`  
`                 String pdbstr = aa1.toPDB(s1,s2);`  
`               `  
`                 System.out.println("writing alignment to " + outputfile);`  
`                 FileOutputStream out= new FileOutputStream(outputfile); `  
`                 PrintStream p =  new PrintStream( out );`  
`       `  
`                 p.println (pdbstr);`

`                 p.close();`  
`                 out.close();`  
`                }                       `  
`       } `  
`       // Collecte generique des exceptions lancees par try`  
`       catch (Exception e){`  
`           e.printStackTrace();`  
`       }`

} ```
