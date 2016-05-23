---
title: BioJava:CookbookFrench:Blast:Extract
---

Comment extraire les informations voulues d'un résultat de recherche?
---------------------------------------------------------------------

Les procedures d'extraction des résultats Blast et Fasta déjà présentées
produisent, lorsque le fichier a été lu, une liste d'objets de type
*SeqSimilaritySearchResult*. Un de ces objets est crée pour chaque
requête. Chaque *SeqSimilaritySearchResult* contient une liste d'objets
de type *SeqSimilaritySearchHit* qui détaille le résultat de la séquence
'Query' à sa séquence 'Subject' correspondante (homologie). Chaque objet
*SeqSimilaritySearchHit* contient une liste d'objets
*SeqSimilaritySearchSubHit*. Ces objets sont équivalents aux HSPs
rapportés par BLAST.

Les classes associées aux résultats, les homologies et les HSPs
contiennent des méthodes pratique de type **getXYZ()** pour récupérer
l'information emmagasinée.

Le petit fragment de code ci-dessous montre une méthode privée qui
prends une liste produite par la lecture d'un fichier BLAST ou FASTA et
qui en extrait l'id de l'homologie (subject id), sa valeur et son score
e.

```java private static void formatResults(List results){

`   //itération à travers chacun des SeqSimilaritySearchResult`  
`   for (Iterator i = results.iterator(); i.hasNext(); ) {`  
`     SeqSimilaritySearchResult result = (SeqSimilaritySearchResult)i.next();`

`     //itération à travers les homologies`  
`     for (Iterator i2 = result.getHits().iterator(); i2.hasNext(); ) {`  
`       SeqSimilaritySearchHit hit = (SeqSimilaritySearchHit)i2.next();`

`       //imprimer ID pour chacune des séquences trouvées, sa valeur et son score e`  
`       System.out.println("subject:\t"+hit.getSubjectID() +`  
`                          " bits:\t"+hit.getScore()+`  
`                          " e:\t"+hit.getEValue());`  
`     }`  
`   }`

} ```
