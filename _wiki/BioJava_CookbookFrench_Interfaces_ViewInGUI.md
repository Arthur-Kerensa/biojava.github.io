---
title: BioJava:CookbookFrench:Interfaces:ViewInGUI
permalink: wiki/BioJava%3ACookbookFrench%3AInterfaces%3AViewInGUI
---

Comment afficher une séquence dans une interface graphique?
-----------------------------------------------------------

Lorsque vous construisez des interfaces graphiques pour des applications
de bioinformatique, vous voulez probablement afficher les séquences des
résidues d'une Sequence que vous voulez montrer. BioJava contient
certaines composantes GUI pour vous permettre d'afficher divers aspects
d'une *Sequence*.

L'unité de base de toute interface graphique basée sur un objet
*Sequence* est le *SequenceRenderContext* qui contient la *Sequence* et
envoit des instructions à un *SequenceRenderer*, responsable pour la
création du dessin de la *Sequence*. Il y a plusieurs implémentations de
*SequenceRenderer* dans BioJava. Celui qui est responsable d'afficher
les résidues dans l'ordre est le *SymbolSequenceRenderer*.

Le programme suivant montre l'utilisation d'un *SequenceRenderContext*
et d'un *SequenceRenderer* pour afficher les symboles d'une *Sequence*.

```java import java.awt.\*; import java.awt.event.\*; import
javax.swing.\*;

import org.biojava.bio.gui.sequence.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.symbol.\*;

public class SeqView extends JFrame {

` private Sequence seq;`  
` private JPanel jPanel = new JPanel();`  
` private SequencePanel seqPanel = new SequencePanel();`  
` private SequenceRenderer symSeqRenderer = new SymbolSequenceRenderer();`  
` public SeqView() {`  
`   try {`  
`     //créer la séquence à afficher`  
`     seq = RNATools.createRNASequence("accggcgcgagauuugcagcgcgcgcgcaucgcg"+`  
`                                      "gggcgcauuaccagacuucauucgacgacucagc"`  
`                                      ,"rna1");`  
`     init();`  
`   }`  
`   catch(Exception e) {`  
`     e.printStackTrace();`  
`   }`  
` }`  
` public static void main(String[] args) {`  
`   SeqView seqView = new SeqView();`  
`   seqView.pack();`  
`   seqView.show();`  
` }`

` /**`  
`  * Installer les composantes pour afficher les graphiques`  
`  */`  
` private void init() throws Exception {`  
`   this.getContentPane().setLayout(new BorderLayout());`  
`   this.getContentPane().add(jPanel, BorderLayout.CENTER);`  
`   this.setTitle("SeqView");`  
`   jPanel.add(seqPanel, BorderLayout.CENTER);`  
`   //déterminer la séquence à afficher`  
`   seqPanel.setSequence(seq);`  
`   //initialiser l'objet responsable pour peindre la sequence`  
`   seqPanel.setRenderer(symSeqRenderer);`  
`   //déterminer quelle portion de la séquence à afficher`  
`   seqPanel.setRange(new RangeLocation(1,seq.length()));`  
` }`  
` `  
` /**`  
`  * Redefinir pour terminer le programme lorsque la fenêtre est fermée.`  
`  */`  
` protected void processWindowEvent(WindowEvent we){`  
`   if (we.getID() == WindowEvent.WINDOW_CLOSING) {`  
`     System.exit(0);`  
`   }`  
`   else {`  
`     super.processWindowEvent(we);`  
`   }`  
` }`

} ```

Le code précédent donne l'image suivante:

[frame|center|Affichage simple d'une séquence dans une fenêtre
graphique](image:Seqview.jpg "wikilink")
