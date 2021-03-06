---
title: BioJava:CookbookKorean
permalink: wiki/BioJava%3ACookbookKorean
---

BioJava In Anger - 바쁜 사람을 위한 튜토리얼과 레시피북
-------------------------------------------------------

BioJava는 거대하고 다가서기 힘든 면이 있습니다. 따라서 BioJava를 빨리
사용하고 싶은 사용자들은 해야 할 것들이 많이 존재합니다. 본 문서는 그런
사용자들을 위해서 BioJava API에 대해서 모두 이해하지 않고서도 99%의
일반적인 BioJava 프로그램을 개발 할 수 있도록 돕기 위해 만들어졌습니다.

본 페이지들은 프로그래밍의 여러가지 쿡 북 형식을 참고로 하고 있으며
"어떻게 하면 되나요?" 의 형식을 취하고 있습니다. 각각의 "어떻게 하면
되나요?"의 형식은 당신이 하고 싶은것과 그에 대한 코딩 예제에 링크되어
있습니다. 기본적으로 코딩 예제를 찾아내면 당신을 그 프로그램을
복사&붙여넣기 하여 재빨리 프로그래밍 할 수 있습니다. 프로그래밍에 이해를
돕기 위해 코드에 주석을 넣는 것에 힘을 썼기 때문에 조금 커진 코딩 예제도
있습니다.

건의사항이나 질문 또는 코멘트 등이 있으면 [biojava 바이오자바 메일링
리스트](mailto:biojava-l@biojava.org)로 접근하시면 됩니다. 메일링
리스트를 구독하고 싶은 분은
[여기에서](http://biojava.org/mailman/listinfo/biojava-l) 구독하시면
됩니다.

쿡북의 코드를 사용하기 원하시면 다음을 인용해 주세요:

Announcing
----------

You can now read BioJava in Anger in
[French](/wiki/BioJava:CookbookFrench "wikilink") (Translated by Sylvain
Foisy; mise à jour / updated : 28 août 2008).

You can also read Biojava in Anger in
[Portuguese](/wiki/BioJava:CookbookPortuguese "wikilink") (Translated by
Dickson Guedes)

You can also read BioJava in Anger in
[Japanese](http://www.geocities.jp/bio_portal/bj_in_anger_ja/)
(Translated by Takeshi Sasayama and Kentaro Sugino, updated 14 Aug
2004).

How about simplified
[Chinese](http://www.cbi.pku.edu.cn/chinese/documents/PUMA/biojava/index-cn.html)?
(Translated by Wu Xin).

뭘 해야하나요?
--------------

### 셋업

-   [Java는 어디에서 가져와야 하나요](http://java.sun.com/downloads/)?
-   [BioJava는 어디서 다운로드해서 설치할 수
    있나요](/wiki/BioJavaKorean:GetStarted "wikilink")?

### 알파벳과 심볼

-   [어떻게 DNA, RNA 또는 단백질 알파벳을 얻을 수
    있나요](/wiki/BioJavaKorean:Cookbook:Alphabets "wikilink")?
-   [어떻게 커스텀 심볼로 부터 커스텀 알파벳을 만들 수
    있나요](/wiki/BioJavaKorean:Cookbook:Alphabets:Custom "wikilink")?
-   [어떻게 코돈 알파벳과 같은 CrossProductAlphabet을 만들 수
    있나요](/wiki/BioJava:Cookbook:Alphabets:CrossProduct "wikilink")?
-   [어떻게 컴포넌트 심볼의 CrossProduct 알파벳으로부터 분해 할 수
    있나요](/wiki/BioJava:Cookbook:Alphabets:Component "wikilink")?
-   [어떻게 두 알파벳 또는 심볼이 같다고 말할 수
    있나요](/wiki/BioJava:Cookbook:Alphabets:Cononical "wikilink")?
-   [어떻게 Y나 R과 같이 애매한 심볼을 만들 수
    있나요](/wiki/BioJava:Cookbook:Alphabets:Ambiguous "wikilink")?

### 기본적인 서열 조작하기

-   [어떻게 하면 문자로 부터 서열 객체를 작성하거나 서열 객체를 문자로
    되돌릴 수 있나요](/wiki/BioJava:Cookbook:Sequence "wikilink")?
-   [어떻게 서열 객체의 일부분을 가져올 수
    있나요](/wiki/BioJava:Cookbook:Sequence:SubSequence "wikilink")?
-   [어떻게 DNA 서열을 RNA 서열로 전사할 수
    있나요](/wiki/BioJava:Cookbook:Sequence:Transcribe "wikilink")?
-   [어떻게 DNA나 RNA 서열의 reverse complement를 만들 수
    있나요](/wiki/BioJava:Cookbook:Sequence:Reverse "wikilink")?
-   [Sequences are immutable so how can I change it's
    name](/wiki/BioJava:Cookbook:Sequence:ChangeName "wikilink")?
-   [어떻게 Sequence나 SymbolList를 편집할 수
    있나요](/wiki/BioJava:Cookbook:Sequence:Edit "wikilink")?
-   [How can I make a sequence motif into a regular
    expression](/wiki/BioJava:Cookbook:Sequence:Regex "wikilink")?
-   [How can I extract all regions beeing marked (or not) with a special
    feature (e.g. 'gene' or
    'CDS')](/wiki/BioJava:Cookbook:Sequence:ExtractGeneRegions "wikilink")?

### 번역

-   [어떻게 DNA, RNA, SymbolList를 단백질로 번역할 수
    있나요](/wiki/BioJava:Cookbook:Translation "wikilink")?
-   [어떻게 싱글 코돈을 싱글 아미노산으로 번역할 수
    있나요](/wiki/BioJava:Cookbook:Translation:Single "wikilink")?
-   [어떻게 비 표준의 번역 테이블을 사용할 수
    있나요](/wiki/BioJava:Cookbook:Translation:NonStandart "wikilink")?
-   [How do I translate a nucleotide sequence in all six
    frames](/wiki/BioJava:Cookbook:Translation:SixFrames "wikilink")?
-   [How do I retrieve the 1-Letter code of a translated sequence
    containing
    ambiguities](/wiki/BioJava:Cookbook:Translation:OneLetterAmbi "wikilink")?

### 프로테오믹스

-   [How do I calculate the mass and pI of a
    peptide](/wiki/BioJava:Cookbook:Proteomics "wikilink")?
-   [How do I analyze the symbol properties of an amino acid sequence
    using the Amino Acid Index
    database](/wiki/BioJava:Cookbook:Proteomics:AAindex "wikilink")?

### 서열 입출력

-   [어떻게 서열을 Fasta 형식으로 만들 수
    있나요](/wiki/BioJava:Cookbook:SeqIO:WriteInFasta "wikilink")?
-   [어떻게 Fasta 파일을 읽을 수
    있나요](/wiki/BioJava:Cookbook:SeqIO:ReadFasta "wikilink")?
-   [어떻게 GenBank/EMBL/SwissProt 파일을 읽을 수
    있나요](/wiki/BioJava:Cookbook:SeqIO:ReadGES "wikilink")?
-   [어떻게 Biojavax 확장을 가지고 서열 파일을 읽을 수
    있나요](/wiki/BioJava:Cookbook:SeqIO:ReadGESBiojavax "wikilink")?
-   [How do I extract GenBank/EMBL/Swissprot sequences and write them as
    Fasta](/wiki/BioJava:Cookbook:SeqIO:GBtoFasta "wikilink")?
-   [How do I turn an ABI sequence trace into a BioJava
    Sequence](/wiki/BioJava:Cookbook:SeqIO:ABItoSequence "wikilink")?
-   [How does sequence I/O work in
    BioJava](/wiki/BioJava:Cookbook:SeqIO:Echo "wikilink")?

### 주석

-   [How do I list the Annotations in a
    Sequence](/wiki/BioJava:Cookbook:Annotations:List "wikilink")?
-   [How do I filter a Sequences based on their species (or another
    Annotation
    property)](/wiki/BioJava:Cookbook:Annotations:Filter "wikilink")?

### 위치 정보와 특징

-   [How do I specify a
    PointLocation](/wiki/BioJava:Cookbook:Locations:Point "wikilink")?
-   [How do I specify a
    RangeLocation](/wiki/BioJava:Cookbook:Locations:Range "wikilink")?
-   [How do CircularLocations
    work](/wiki/BioJava:Cookbook:Locations:Circular "wikilink")?
-   [How can I make a
    Feature](/wiki/BioJava:Cookbook:Locations:Feature "wikilink")?
-   [How can I filter Features by
    type](/wiki/BioJava:Cookbook:Locations:Filter "wikilink")?
-   [How can I remove
    features](/wiki/BioJava:Cookbook:Locations:Remove "wikilink")?

### BLAST와 FASTA

-   [어떻게 BLAST 파서를 설정
    하나요](/wiki/BioJava:CookBook:Blast:Parser "wikilink")?
-   [어떻게 FASTA 파서를 설정
    하나요](/wiki/BioJava:CookBook:Fasta:Parser "wikilink")?
-   [어떻게 파싱된 결과로 부터 정보를 추출
    하나요](/wiki/BioJava:CookBook:Blast:Extract "wikilink")?
-   [어떻게 큰 파일을 파싱할 수 있나요;또는 어떻게 맞춤
    SearchContentHandler를 만들 수
    있나요](/wiki/BioJava:CookBook:Blast:Echo "wikilink")?
-   [어떻게 XML 형태의 BLAST 결과를 HTML 페이지로 만들 수
    있나요](/wiki/BioJava:CookBook:Blast:XML "wikilink")?

### 카운트와 배포

-   [How do I count the residues in a
    Sequence](/wiki/BioJava:CookBook:Count:Residues "wikilink")?
-   [How do I calculate the frequency of a Symbol in a
    Sequence](/wiki/BioJava:CookBook:Count:Frequency "wikilink")?
-   [How can I turn a Count into a
    Distribution](/wiki/BioJava:CookBook:Count:ToDistrib "wikilink")?
-   [How can I generate a random sequence from a
    Distribution](/wiki/BioJava:CookBook:Distribution:RandomSeqs "wikilink")?
-   [How can I find the amount of information or entropy in a
    Distribution](/wiki/BioJava:CookBook:Distribution:Entropy "wikilink")?
-   [What is an easy way to tell if two Distributions have equal
    weights](/wiki/BioJava:CookBook:Distribution:Emission "wikilink")?
-   [How can I make an OrderNDistribution over a custom
    Alphabet](/wiki/BioJava:CookBook:Distribution:Custom "wikilink")?
-   [How can I write a Distribution as
    XML](/wiki/BioJava:CookBook:Distribution:XML "wikilink")?
-   [Using Distributions to make a Gibbs
    sampler](/wiki/BioJava:CookBook:Distribution:Gibbs "wikilink")
-   [Using Distributions to make a naive Bayes
    classifier](/wiki/BioJava:CookBook:Distribution:Bayes "wikilink")
-   [How do I calculate the composition of a Sequence or collection of
    Sequences?](/wiki/BioJava:CookBook:Distribution:Composition "wikilink")
    This example uses JDK 1.5 and BioJavaX

### 중요 행렬과 동적 프로그래밍

-   [How do I use a WeightMatrix to find a
    motif](/wiki/BioJava:CookBook:DP:WeightMatrix "wikilink")?
-   [How do I make a HMMER like profile
    HMM](/wiki/BioJava:CookBook:DP:HMM "wikilink")?
-   |How do I set up a custom HMM? (Link to
    Tutorial?? --[Guedes](User:Guedes "wikilink") 11:43, 8 February 2006
    (EST) )
-   [How do I generate a pair-wise alignment with a Hidden Markov
    Model](/wiki/BioJava:CookBook:DP:PairWise "wikilink")?
-   [How do I generate a global or local alignment with the
    Needleman-Wunsch- or the
    Smith-Waterman-algorithm](/wiki/BioJava:CookBook:DP:PairWise2 "wikilink")?

### 유저 인터페이스

-   [How can I visualize Annotations and Features as a
    tree](/wiki/BioJava:CookBook:Interfaces:ViewAsTree "wikilink")?
-   [How can I display a Sequence in a
    GUI](/wiki/BioJava:CookBook:Interfaces:ViewInGUI "wikilink")?
-   [How do I display Sequence
    coordinates](/wiki/BioJava:CookBook:Interfaces:Coordinates "wikilink")?
-   [How can I display
    features](/wiki/BioJava:CookBook:Interfaces:Features "wikilink")?
-   [How can I display Protein Features / a Peptide
    Digest](/wiki/BioJava:CookBook:Interfaces:ProteinPeptideFeatures "wikilink")?

### BioSQL과 서열 데이터베이스

-   [어떻게 PostgreSQL을 가지고 BioSQL을
    설정하나요](/wiki/BioJava:CookBook:BioSQL:SetupPostGre "wikilink")?
    ([[User:David|David Huen]로 부터])
-   [어떻게 오라클을 가지고 BioSQL을
    설정하나요](/wiki/BioJava:CookBook:BioSQL:SetupOracle "wikilink")?
    ([[User:Richard|Richard Holland]로 부터])
-   [How do I add, view and remove Sequence Objects from a BioSQL
    DB?](/wiki/BioJava:CookBook:BioSQL:Manage "wikilink")
-   [How can I get a sequence straight from
    NCBI?](/wiki/BioJava:CookBook:ExternalSources:NCBIFetch "wikilink")

### 유전자 알고리즘

-   [어떻게 BioJava를 가지고 유전자 알고리즘을 만들 수
    있나요](/wiki/BioJava:CookBook:GA "wikilink")?

### 단백질 구조

-   [어떻게 PDB 파일을 읽을 수
    있나요](/wiki/BioJava:CookBook:PDB:read "wikilink")?
-   [어떻게 .mmcif 파일을 읽을 수
    있나요](/wiki/BioJava:CookBook:PDB:mmcif "wikilink")?
-   [어떻게 구조 파일의 원자에 접근할 수
    있나요](/wiki/BioJava:CookBook:PDB:atoms "wikilink")?
-   [어떻게 원자를 계산할 수
    있나요](/wiki/BioJava:CookBook:PDB:atomsCalc "wikilink")?
-   [어떻게 PDB 파일의 헤더 정보에 접근할 수
    있나요](/wiki/BioJava:CookBook:PDB:header "wikilink")?
-   [How does BioJava deal with SEQRES and ATOM
    groups?](/wiki/BioJava:CookBook:PDB:seqres "wikilink")
-   [How can I mutate a
    residue?](/wiki/BioJava:CookBook:PDB:mutate "wikilink")
-   [How can I calculate a structure
    superimposition?](/wiki/BioJava:CookBook:PDB:align "wikilink")
-   [How can I use a simple GUI to calculate a
    superimposition?](/wiki/BioJava:CookBook:PDB:alignGUI "wikilink")
-   [어떻게 Jmol과 사용할 수
    있나요](/wiki/BioJava:CookBook:PDB:Jmol "wikilink")?
-   [어떻게 데이터베이스로 부터 직렬화 할 수
    있나요](/wiki/BioJava:CookBook:PDB:hibernate "wikilink")?

### 온톨로지

-   [어떻게 OBO 파일을 파싱할 수
    있나요](/wiki/BioJava:CookBook:OBO:parse "wikilink")?

Disclaimer
----------

This code is generously donated by people who probably have better
things to do. Where possible we test it but errors may have crept in. As
such, all code and advice here in has no warranty or guarantee of any
sort. You didn't pay for it and if you use it we are not responsible for
anything that goes wrong. Be a good programmer and test it yourself
before unleashing it on your corporate database.

Copyright
---------

The documentation on this site is the property of the people who
contributed it. If you wish to use it in a publication please make a
request through the [biojava mailing
list](mailto:biojava-l@biojava.org).

The code is [open-source](wp:Open source "wikilink"). A good definition
of open-source can be found
[here](http://www.opensource.org/docs/definition_plain.php). If you
agree with that definition then you can use it.
