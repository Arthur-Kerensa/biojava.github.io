---
title: BioJava:CookbookFrench
permalink: wiki/BioJava%3ACookbookFrench
---

BioJava quand il y a le feu - Un tutoriel et un manuel pour les gens pressés
----------------------------------------------------------------------------

La librairie BioJava est imposante et il faut le dire, peut être
intimidante. Pour ceux parmi nous qui sommes pressés, il y a vraiment
assez de matériel pour faire tourner la tête. Ce document est conçu pour
vous aider à développer des applications utilisant BioJava, applications
capables d'accomplir 99% des tâches les plus courantes, sans avoir à
comprendre 99% de l'API de BioJava.

Ce site est inspiré de tous ces livres de recettes en programmation et
suit la même approche du "Comment faire pour...". Chacune de ces
recettes contient également des codes de démonstration qui font ce que
vous voulez et parfois plus. En bref, si vous trouvez le code que vous
recherchez et faites un simple copier-coller dans votre programme, vous
devriez être en mesure de réussir rapidement. J'ai tenté (enfin, Mark
tente et je traduit!) de sur-documenter le code pour rendre plus évident
ce qui est tenté, ce qui explique pourquoi le code à l'air un peu obèse.

'BioJava in Anger' est maintenu par Mark Schreiber. Si vous avez des
suggestions, questions ou commentaire, contacter la [liste de
courriel](mailto://biojava-l@biojava.org) de BioJava. Pour s'y abonner,
cliquer [ici](http://www.biojava.org/mailman/listinfo/biojava-l).

Traduction française: [Sylvain
Foisy](mailto://sylvain.foisyCHEZdiploide.net). Donc toute erreur est
mienne; contactez-moi pour correction. Encore mieux: participer au
concept Wiki et faites-les vous-mêmes!!

Présentation
------------

Une présentation en format Powerpoint de Mark décrivant Biojava se
trouve [ici](http://www.biojava.org/docs/bj_in_anger/BioJavaAPI.ppt).

Publications utilisant BioJava
------------------------------

Pour obtenir la liste des articles contenus dans Google Scholar et
citant BioJava, cliquer
[ici](http://scholar.google.com/scholar?q=biojava&ie=UTF-8&oe=UTF-8&hl=en).

Comment faire pour ...?
-----------------------

### Installation

-   [Comment obtenir Java?](http://java.sun.com/downloads) N.B.: Cette
    page est exclusivement en anglais.
-   [Comment obtenir et installer
    BioJava?](http://biojava.open-bio.org/wiki/BioJava:GetStarted) N.B.:
    cette page est exclusivement en anglais.

### Alphabets et Symbols

-   [Comment obtenir un Alphabet d'ADN, d'ARN ou de
    protéine?](/wiki/BioJava:CookbookFrench:Alphabets "wikilink")
-   [Comment faire un Alphabet sur mesure à partir de Symbols sur
    mesure?](/wiki/BioJava:CookbookFrench:Alphabets:CustomAlphabets "wikilink")
-   [Comment faire un CrossProductAlphabet, par exemple, un Alphabet de
    codons?](/wiki/BioJava:CookbookFrench:Alphabets:CrossProduct "wikilink")
-   [Comment décomposer les Symbols d'Alphabets CrossProductAlphabet en
    leurs Symbols
    constituants?](/wiki/BioJava:CookbookFrench:Alphabets:Component "wikilink")
-   [Comment dire si deux Alphabets ou Symbols sont
    identiques?](/wiki/BioJava:CookbookFrench:Alphabets:Canonical "wikilink")
-   [Comment faire pour créer un Symbol ambigüe comme Y ou
    R?](/wiki/BioJava:CookbookFrench:Alphabets:Ambiguity "wikilink")

### Manipulation simples des séquences

-   [Comment créer une Sequence à partir d'une chaîne de caractères ou
    transformer un objet Sequence en chaîne de
    caractères?](/wiki/BioJava:CookbookFrench:Sequence "wikilink")
-   [Comment obtenir une portion d'une
    Sequence?](/wiki/BioJava:CookbookFrench:Sequence:SubSequence "wikilink")
-   [Comment transcrire une Sequence d'ADN en Sequence
    d'ARN?](/wiki/BioJava:CookbookFrench:Sequence:Transcribe "wikilink")
-   [Comment obtenir la séquence complémentaire à une Sequence d'ADN ou
    d'ARN?](/wiki/BioJava:CookbookFrench:Sequence:Reverse "wikilink")
-   [Les Sequences sont immuables alors comment faire pour en changer le
    nom?](/wiki/BioJava:CookbookFrench:Sequence:ChangeName "wikilink")
-   [Comment éditer une Sequence ou un
    SymbolList?](/wiki/BioJava:CookbookFrench:Sequence:Edit "wikilink")
-   [Comment utiliser une sequence comme expression régulière pour
    chercher des
    motifs?](/wiki/BioJava:CookbookFrench:Sequence:Regex "wikilink")

### Traduction

-   [Comment traduire une Sequence ou une SymbolList d'ADN ou d'ARN en
    proteine?](/wiki/BioJava:CookbookFrench:Translation "wikilink")
-   [Comment traduire une seul codon en son acide aminé
    correspondant?](/wiki/BioJava:CookbookFrench:Translation:Single "wikilink")
-   [Comment utiliser un code génétique
    non-standard?](/wiki/BioJava:CookbookFrench:Translation:NonStandard "wikilink")
-   [Comment traduire une Sequence dans ses 6 cadres de
    lectures?](/wiki/BioJava:CookbookFrench:Translation:SixFrame "wikilink")
-   [Comment obtenir les acides aminés codés par un codon ambigu dans le
    code à une
    lettre?](/wiki/BioJava:CookbookFrench:Translation:OneLetterAmbi "wikilink")

### Protéomique

-   [Comment calculer la masse et le pI d'un
    peptide?](/wiki/BioJava:CookbookFrench:Proteomics "wikilink")
-   [Comment analyser les propriétés d'une séquence protéique en
    utilisant la base de données *Amino Acid
    Index*?](/wiki/BioJava:CookbookFrench:Proteomics:AAindex "wikilink")

### Entrée/Sortie des fichiers de séquence

-   [Comment écrire des Sequences en format Fasta (ou tout autre
    format)?](/wiki/BioJava:CookbookFrench:SeqIO:WriteInFasta "wikilink")
-   [Comment lire un fichier en format
    Fasta?](/wiki/BioJava:CookbookFrench:SeqIO:ReadFasta "wikilink")
-   [Comment lire un fichier en format
    GenBank/EMBL/SwissProt?](/wiki/BioJava:CookbookFrench:SeqIO:ReadGES "wikilink")
-   [Comment lire un fichier en format GenBank/EMBL/SwissProt avec
    Biojavax?](/wiki/BioJava:CookbookFrench:SeqIO:ReadGESBiojavax "wikilink")
-   [Comment extraire les séquence en format GenBank/EMBL/Swissprot et
    les écrire en format
    Fasta?](/wiki/BioJava:CookbookFrench:SeqIO:GBToFasta "wikilink")
-   [Comment transformer un fichier ABI en Sequence
    BioJava?](/wiki/BioJava:CookbookFrench:SeqIO:ABItoSequence "wikilink")
-   [Comment fonctionne les entrées / sorties de fichiers de séquence
    avec Biojava?](/wiki/BioJava:CookbookFrench:SeqIO:Echo "wikilink")

### Annotations

-   [Comment faire la liste des Annotations d'une
    Sequence?](/wiki/BioJava:CookbookFrench:Annotations:List "wikilink")
-   [Comment filtrer une Sequence en se basant sur l'espèce (ou tout
    autre propriété d'une
    Annotation)?](/wiki/BioJava:CookbookFrench:Annotations:Filter "wikilink")

### Positions et caractéristiques (*Features*)

-   [Comment faire pour spécifier une position ponctuelle
    (*PointLocation*)?](/wiki/BioJava:CookbookFrench:Locations:Point "wikilink")
-   [Comment faire pour spécifier une position par intervalle
    (*RangeLocation*)?](/wiki/BioJava:CookbookFrench:Locations:Range "wikilink")
-   [Comment fonctionne les
    CircularLocations?](/wiki/BioJava:CookbookFrench:Locations:Circular "wikilink")
-   [Comment créer une caractéristique
    (*Feature*)?](/wiki/BioJava:CookbookFrench:Locations:Feature "wikilink")
-   [Comment filtrer les *Features* par
    type?](/wiki/BioJava:CookbookFrench:Locations:Filter "wikilink")
-   [Comment supprimer un
    *Feature*?](/wiki/BioJava:CookbookFrench:Locations:Remove "wikilink")

### BLAST et FASTA

-   [Comment lire un fichier de résultats
    BLAST?](/wiki/BioJava:CookbookFrench:Blast:Parser "wikilink")
-   [Comment lire un fichier de résultats
    FASTA?](/wiki/BioJava:CookbookFrench:Fasta:Parser "wikilink")
-   [Comment extraire les informations à partir des résultats
    lus?](/wiki/BioJava:CookbookFrench:Blast:Extract "wikilink")
-   [Comment extraire les infos d'un gros fichier ou comment créer son
    propre
    SearchContentHandler?](/wiki/BioJava:CookbookFrench:Blast:Echo "wikilink")
-   [Vous voulez plus d'info sur l'infrastructure de lecture SAX2 de
    Biojava?](/wiki/BioJava:Tutorial:Blast-like_Parsing_Cook_Book "wikilink")
    Note: section du tutoriel anglais

### Comptes et Distributions

-   [Comment compter les résidus d'une
    Sequence?](/wiki/BioJava:CookbookFrench:Count:Residues "wikilink")
-   [Comment faire pour calculer la fréquence d'un Symbol dans une
    Sequence?](/wiki/BioJava:CookbookFrench:Count:Frequency "wikilink")
-   [Comment transformer un Count en
    Distribution?](/wiki/BioJava:CookbookFrench:Count:ToDistrib "wikilink")
-   [Comment générer une séquence aléatoire à partir d'une
    Distribution?](/wiki/BioJava:CookbookFrench:Distribution:RandomSeqs "wikilink")
-   [Comment trouver la quantité d'information ou d'entropie d'une
    Distribution?](/wiki/BioJava:CookbookFrench:Distirbution:Entropy "wikilink")
-   [Comment savoir facilement si deux Distributions sont
    identiques?](/wiki/BioJava:CookbookFrench:Distirbution:Emission "wikilink")
-   [Comment créer une OrderNDistribution avec un Alphabet sur
    mesure?](/wiki/BioJava:CookbookFrench:Distirbution:Custom "wikilink")
-   [Comment écrire une Distribution en format
    XML?](/wiki/BioJava:CookbookFrench:Distribution:XML "wikilink")
-   [Comment construire un échantilloneur de Gibbs à l'aide de
    Distributions?](/wiki/BioJava:CookbookFrench:Distribution:Gibbs "wikilink")
-   [Comment utiliser les Distributions afin d'obtebir un classificateur
    bayésien
    simple?](/wiki/BioJava:CookbookFrench:Distribution:Bayes "wikilink")
-   [Comment calculer la composition d'une ou plusieurs
    séquences?](/wiki/BioJava:CookbookFrench:Distribution:Composition "wikilink")

### Matrices et Programmation Dynamique

-   [Comment utiliser une WeightMatrix pour trouver un
    motif?](/wiki/BioJava:CookbookFrench:DP:WeightMatrix "wikilink")
-   [Comment créer un HMM semblable à un profile
    HMMER?](/wiki/BioJava:CookbookFrench:DP:HMM "wikilink")
-   [Comment créer un HMM sur
    mesure?](/wiki/BioJava:Tutorial:Dynamic_programming_examples "wikilink")
    Note: section du tutoriel anglais
-   [Comment faire un alignement de deux séquences en utilisant un
    modèle de Markov?](/wiki/BioJava:CookbookFrench:DP:PairWise "wikilink")
-   [Comment faire un alignement de deux séquences en utilisant
    l'algorithme de Smith-Waterman ou de
    Needleman-Wunsh?](/wiki/BioJava:CookbookFrench:DP:PairWise2 "wikilink")

### Interfaces Usagers Graphiques

-   [Comment visualiser Annotations et Features sous la forme d'un
    arbre?](/wiki/BioJava:CookbookFrench:Interfaces:ViewAsTree "wikilink")
-   [Comment afficher une Sequence dans un interface
    graphique?](/wiki/BioJava:CookbookFrench:Interfaces:ViewInGUI "wikilink")
-   [Comment afficher les coordonnées d'une
    séquence?](/wiki/BioJava:CookbookFrench:Interfaces:Coordinates "wikilink")
-   [Comment afficher les caractéristiques d'une
    séquence?](/wiki/BioJava:CookbookFrench:Interfaces:Features "wikilink")
-   [Comment afficher les caractéristiques d'une protéine avec les
    fragments d'une digestion tryptique (ou
    autre)?](/wiki/BioJava:CookbookFrench:Interfaces:ProteinPeptideFeatures "wikilink")

### Intégration avec des bases de données externes: OBDC / JDBC / BioSQL

-   [Comment créer une base de données avec BioSQL et
    PostgreSQL?](/wiki/BioJava:CookBook:BioSQL:SetupPostGre "wikilink") Note:
    en anglais seulement
-   [Comment créer une base de données avec BioSQL et
    Oracle?](/wiki/BioJava:CookBook:BioSQL:SetupOracle "wikilink") Note: en
    anglais seulement
-   [Comment ajouter, voir et éliminer des objets Séquences d'une base
    de données BioSQL?](/wiki/BioJava:CookbookFrench:BioSQL:Manage "wikilink")
-   [Comment récupérer des séquences directement du
    NCBI?](/wiki/BioJava:CookbookFrench:ExternalSources:NCBIFetch "wikilink")

### Utilisation de services externes

-   [Comment faire pour aligner une séquence en utilisant le service
    QBlast?](/wiki/BioJava:CookbookFrench:Services:Qblast "wikilink")

### Algorithmes génétiques

-   [Comment écrire un algorithme génétique avec
    BioJava?](/wiki/BioJava:CookbookFrench:GA "wikilink")

### Analyse structurale des protéines

-   [Comment faire pour lire un fichier en format
    PDB?](/wiki/BioJava:CookbookFrench:PDB:Read "wikilink")
-   [Comment faire pour lire un fichier en format
    MMCIF?](/wiki/BioJava:CookbookFrench:PDB:Mmcif "wikilink")
-   [Comment obtenir les informations sur les atomes présent dans un
    fichier PDB?](/wiki/BioJava:CookbookFrench:PDB:Atom "wikilink")
-   [Comment faire des calculs sur des Atomes présent dans un fichier
    PDB?](/wiki/BioJava:CookbookFrench:PDB:AtomCalc "wikilink")
-   [Comment travailler avec des objets de type Group
    (AminiAcid,Nucleotide,Hetatom)?](/wiki/BioJava:CookbookFrench:PDB:Group "wikilink")
-   [Comment accéder aux informations contenues dans l'en-tete d'un
    fichier PDB?](/wiki/BioJava:CookbookFrench:PDB:Header "wikilink")
-   [Comment utiliser les information des groupes SEQRES et ATOM avec
    BioJava?](/wiki/BioJava:CookbookFrench:PDB:Seqres "wikilink")
-   [Comment puis-je modifié un
    résidu?](/wiki/BioJava:CookbookFrench:PDB:Mutate "wikilink")
-   [Comment faire pour calculer la superposition de deux
    Structures?](/wiki/BioJava:CookbookFrench:PDB:Align "wikilink")
-   [Comment faire une interface graphique simple pour calculer la
    superposition de deux Structures? (À
    venir...)](/wiki/BioJava:CookbookFrench:PDB:AlignGui "wikilink")
-   [Comment faire interagir une Structure avec
    Jmol?](/wiki/BioJava:CookbookFrench:PDB:Jmol "wikilink")
-   [Comment faire pour obtenir les informations des éléments PDB
    contenues dans une base de données locale? (À
    venir)](/wiki/BioJava:CookbookFrench:PDB:Hibernate "wikilink")

### Utilisation des ontologies avec BioJava

-   [Comment faire pour lire une ontologie en format
    OBO?](/wiki/BioJava:CookbookFrench:Ontology:OBO "wikilink")

Désaveu de responsabilité
-------------------------

Ces codes sont généreusement offerts par des gens qui ont probablement
mieux à faire. Lorsque c'est possible, nous les avons testés mais des
erreurs ont pu s'y glisser. Par conséquent, les codes et conseils
retrouvés ici ne contiennent aucune garantie de quelque nature que ce
soit. Vous n'avez rien payé et si vous les utilisez, nous ne sommes pas
responsables si quelque chose tourne mal. Soyez un bon programmeur et
testez vous-même vos codes avant de les insérer dans votre banque de
données.

Copyright
---------

La documentation retrouvée sur ce site demeure la propriété des
personnes qui y ont contribué. Si vous désirez l'utiliser dans une
publication, prière d'en faire la demande via la [liste de
distribution](mailto://biojava-l@biojava.org) de BioJava. Les codes
contenus dans ce site sont [à licence
libre](http://fr.wikipedia.org/wiki/Open_Source) (open source). Une
bonne définition de la licence libre se trouve
[ici](http://www.opensource.org/docs/definition_plain.php). Si vous
acceptez ces conditions, vous pouvez utiliser les codes de ce site.

--[Foisys](User:Foisys "wikilink") 12:06, 6 February 2006 (EST)
