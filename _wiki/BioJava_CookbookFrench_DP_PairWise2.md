---
title: BioJava:CookbookFrench:DP:PairWise2
permalink: wiki/BioJava%3ACookbookFrench%3ADP%3APairWise2
---

Comment faire pour créer un alignement global (algorithme de Needleman-Wunsh) ou local (algorithme de Smith-Waterman)
---------------------------------------------------------------------------------------------------------------------

Les alignements de deux séquences ont traditionnellement été obtenues
par des approches de programmation dynamique déterministique. Deux
algorithmes de cette nature sont utilisés: l'algorithme de
Needleman-Wunsch est utilisé pour des alignements globaux alors que
l'algorithme de Smith-Waterman a été développé pour les alignements
locaux. L'exemple ci-dessous vous montre comment faire l'un ou l'autre
grâce aux implémentations de chacun de ces algorithmes retrouvées dans
le package `org.biojava.bio.alignment`. Ces classes ne sont disponibles
qu'á partir de la version 1.5.

L'idée derrière ces approches est de maintenir un représentation
matricielle d'un graphe d'édition, avec des fonctions d'insertion, de
délétion, de substitution et d'extension de gap; en pratique,
l'insertion et la délétion sont des opérations d'ouverture de gaps au
sein de la séquence connue de l'un, de la séquence inconnue de l'autre.
Par programmation dynamique, les éléments contenus dans la matrice, qui
sont des valeurs représentant la valeur de l'opération à effectuer, sont
calculés. Le parcours permettant d'obtenir le meilleur score produit le
meilleur alignement.

Les implémentations de ces algorithmes doivent être initialisées avec
des pénalités pour chaque opération d'édition. Cependant, les matrices
de substitution utilisent des scores (points) qui sont tout l'opposé des
pénalités. Ceci signifie qu'on peut obtenir les pénalités en multipliant
les scores par la valeur -1. L'utilisation de pénalités plutôt que des
points permet de calculer une distance d'édition pour les alignements
globaux. Une telle distance n'est pas utile dans le cas des alignements
locaux car dans les cas extrêmes, l'alignement local entre deux
séquences pourrait n'avoir qu'un seul symbole de chaque séquence et par
conséquent avoir une valeur de distance de zéro. Voilà pourquoi les
alignements locaux utilisent les points plutôt que les pénalités.
Néanmoins, le constructeur de `SmithWaterman` demande des pénalités et
pas des points.

Les alignements utilisant des valeurs différentes pour la pénalité d'une
ouverture et son élongation consomment une plus grande quantité de
mémoire et de temps de traitement par rapport à des valeurs identiques
pour les deux. C'est parce qu'il faut maintenir trois matrices pour
préserver l'information nécessaire afin de retrouver le meilleur chemin
sur le graphe. Il est nécessaire de maintenir deux matrices pour les
identités et les substitutions dans la séquence connue et la séquence
inconnue respectivement et une troisieme mattrice pour préserver les
valeurs optimales de ces deux premières ainsi que des opérations de
match/remplacement; toutes ces matrices ont une dimensions de
`query.length()` par `target.length()`.

Il est possible d'utiliser une des nombreuses matrices de substitution
existantes ainf de faire la calcul des alignements; elles permettent de
calculer la valeur de transition d'un acide aminé à un autre. Elles
peuvent être téléchargées à partir du
[NCBI](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/) et sont nécessaires
pour cet exemple. Si cela vous est nécessaire, il est possible de créer
vos propres matrices grâce à la classe `SubstitutionMatrix`. Cette
dernière vous donne accès à un constructeur permettant de créer votre
propre matrice avec des valeurs **égales** pour chaque identité et
chaque substitution.

La superclasse *SequenceAlignment* de chaque algorithme possède une
méthode pour formatter la sortie de l'alignement. Par conséquent, si
vous désirez écrire votre propre algorithme d'alignment ou si vous
voulez utiliser [l'algorithme basé sur les modèles de
Markov](BioJava%3ACookbookFrench%3ADP%3APairWise "wikilink"), vous pouvez
dériver votre classe à partir de la super-classe et appliquer la
méthode.

Une démo des classes d'alignement global et local
-------------------------------------------------

```java import java.io.File;

import org.biojava.bio.alignment.NeedlemanWunsch; import
org.biojava.bio.alignment.SequenceAlignment; import
org.biojava.bio.alignment.SmithWaterman; import
org.biojava.bio.alignment.SubstitutionMatrix; import
org.biojava.bio.seq.DNATools; import org.biojava.bio.seq.Sequence;
import org.biojava.bio.symbol.AlphabetManager; import
org.biojava.bio.symbol.FiniteAlphabet;

/\*

`* Created on Mar 28, 2006`  
`*/`

/\*\* Demo effectuant l'alignement global et local, successivement,

` * de deux sequences avec affichage des resultats a l'ecran. `  
` * L'usage d'une matrice de substitution est necessaire, facilement obtenues via`  
` * `[`ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/`](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/)  
` * Cette demo ne fonctionne qu'avec des sequences d'ADN. Cependant, les algorithmes fonctionnent `  
` * avec n'importe quel Alphabet pourvu qu'une matrice valable existe `  
` * Dans cet exemple, la matrice NUC.4.4 est adequate.`  
` *`  
` * @author Andreas Dräger`  
` */`

public class DeterministicAlignmentDemo {

` /** Cette classe permet l'alignement de deux sequences `  
`   * pour affichage a l'ecran.`  
`   * @param args: une sequence inconnue et une sequence connue, `  
`   *   un fichier avec les valeurs de la matrice de subsitution a utiliser.`  
`   * @link `[`ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/`](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/)  
`   */`  
` public static void main (String args[]) {`  
`   if (args.length < 3)`  
`     throw new Error("Usage: DeterministicAlignmentDemo " +`  
`                     "querySeq targetSeq substitutionMatrixFile");`  
`   try {`  
`     /* Specification de l'Alphabet des sequences, DNA dans cet exemple.`  
`     *  Pour des sequences proteiques, simplement utiliser`  
`     *  AlphabetManager.alphabetForName("Protein");`  
`     */      `  
`     FiniteAlphabet alphabet = (FiniteAlphabet) AlphabetManager.alphabetForName("DNA");`  
`     `  
`     // Lecture du fichier de la matrice de substitution. `  
`     // Pour cet exemple, la matrice NUC.4.4 est correcte.`  
`     SubstitutionMatrix matrix = new SubstitutionMatrix(alphabet, new File(args[2]));`  
`     `  
`     // Definition les valeurs des couts par defaut pour l'alignement global.`  
`     SequenceAlignment aligner = new NeedlemanWunsch( `  
`       (short)0,   // match`  
`       (short)3,   // remplacement`  
`       (short)2,      // insertion`  
`       (short)2,   // deletion`  
`       (short)1,      // gapExtend`  
`       matrix  // Matrice de substitution`  
`     );`

`     Sequence query  = DNATools.createDNASequence(args[0], "query");`  
`     Sequence target = DNATools.createDNASequence(args[1], "target");`

`     // Faire l'alignement et perserver les resultats.`  
`     aligner.pairwiseAlignment(`  
`       query,  // sources`  
`       target  // sequenceDB`  
`     );`

`     // Imprimer l'alignement obtenu a l'ecran`  
`     System.out.println("Global alignment with Needleman-Wunsch:\n"+`  
`       aligner.getAlignmentString());    `  
`     `  
`     // Effectuer l'alignement local. `  
`     // Primo, definir la valeur du cout de chaque operation.`  
`     aligner = new SmithWaterman(`  
`       (short)-1,      // match`  
`       (short)3,       // remplacement `  
`       (short)2,       // insertion`  
`       (short)2,       // deletion`  
`       (short)1,       // gapExtend`  
`       matrix   // Matrice de substitution`  
`     );`  
`     // Faire l'alignement et perserver les resultats.`  
`     aligner.pairwiseAlignment(query, target);`

`     // Imprimer l'alignement obtenu a l'ecran`  
`     System.out.println("\nLocal alignment with Smith-Waterman:\n"+`  
`       aligner.getAlignmentString());`  
`   } catch (Exception exc) {`  
`     exc.printStackTrace();`  
`   }`  
` }`

} </java>
