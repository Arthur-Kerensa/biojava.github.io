---
title: BioJava talk:Tutorial:Simple HMMs with BioJava
permalink: wikis/BioJava_talk%3ATutorial%3ASimple_HMMs_with_BioJava
---

Great tutorial, David. One suggestion, though, this code:

` public static MarkovModel createCasino() {`  
`   Symbol[] rolls=new Symbol[6];`

`   //set up the dice alphabet`  
`   SimpleAlphabet diceAlphabet=new SimpleAlphabet();`  
`   diceAlphabet.setName("DiceAlphabet");`

`   for(int i=1;i<7;i++) {`  
`     try {`  
`       rolls[i-1]= AlphabetManager.createSymbol((char)('0'+i),""+i,Annotation.EMPTY_ANNOTATION);`  
`       diceAlphabet.addSymbol(rolls[i-1]);`  
`     } catch (Exception e) {`  
`       throw new NestedError(`  
`         e, "Can't create symbols to represent dice rolls"`  
`       );`  
`     }`  
`   }`

Is the beginning of the method you are developing here, however, the
last brace should be omitted since the method spans multiple code
blocks. Suggest deleting final brace and adding ellipsis comments for
clarity (//...) I can do this, just didn't want to trample all over your
nice tutorial without your
consent. --[James.swetnam](User:James.swetnam "wikilink") 15:40, 6 April
2010 (UTC)
