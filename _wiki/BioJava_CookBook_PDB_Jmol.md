---
title: BioJava:CookBook:PDB:Jmol
permalink: wiki/BioJava%3ACookBook%3APDB%3AJmol
---

How to interact with Jmol
-------------------------

[Jmol](http://jmol.sourceforge.net) is a popular open source 3D viewer
written in Java. This example demonstrates how you can send a BioJava
structure object to Jmol. This can be used e.g. to visualize a protein
structure alignment as calculated with <BioJava:CookBook:PDB:alignGUI>.

The BiojavaJmol class provides a simple display of a Structure object,
if Jmol is on the classpath.

```java public static void main(String[] args){

`       try {`

`           PDBFileReader pdbr = new PDBFileReader();   `  
`           `  
`           pdbr.setPath("/Path/To/PDBFiles/");`

`           String pdbCode = "5pti";`

`           Structure struc = pdbr.getStructureById(pdbCode);`

`           BiojavaJmol jmolPanel = new BiojavaJmol();`  
`           `  
`           jmolPanel.setStructure(struc);`  
`           `  
`           // send some RASMOL style commands to Jmol`  
`           jmolPanel.evalString("select * ; color chain;");`  
`           jmolPanel.evalString("select *; spacefill off; wireframe off; backbone 0.4;  ");`

`       } catch (Exception e){`  
`           e.printStackTrace();`  
`       }`  
`   }`

```

Longer Example
==============

This example shows how you can Integrate Jmol into your appication
together with BioJava

```java /\*

Jmol.jar needs to be in your classpath for this example to work. You can
get it from <http://jmol.sourceforge.net>

-   /

package org.biojava.jmoltest;

import java.awt.Container; import java.awt.Dimension; import
java.awt.Graphics; import java.awt.Rectangle; import
java.awt.event.WindowAdapter; import java.awt.event.WindowEvent; import
javax.swing.JFrame; import javax.swing.JPanel; import
org.biojava.nbio.structure.Structure; import
org.biojava.nbio.structure.io.PDBFileReader; import
org.jmol.adapter.smarter.SmarterJmolAdapter; import
org.jmol.api.JmolAdapter; import org.jmol.api.JmolSimpleViewer;

public class SimpleJmolExample {

`   JmolSimpleViewer viewer;`  
`   Structure structure; `

`   JmolPanel jmolPanel;`  
`   JFrame frame ;`

`   public static void main(String[] args){`  
`       try {`

`           PDBFileReader pdbr = new PDBFileReader();          `  
`           pdbr.setPath("/Path/To/PDBFiles/");`

`           String pdbCode = "5pti";`

`           Structure struc = pdbr.getStructureById(pdbCode);`

`           SimpleJmolExample ex = new SimpleJmolExample();`  
`           ex.setStructure(struc);`  
`          `  
`           `  
`       } catch (Exception e){`  
`           e.printStackTrace();`  
`       }`  
`   }`

`   public SimpleJmolExample() {`  
`       frame = new JFrame();`  
`       frame.addWindowListener(new ApplicationCloser());`  
`       Container contentPane = frame.getContentPane();`  
`       jmolPanel = new JmolPanel();`  
`  `  
`       jmolPanel.setPreferredSize(new Dimension(200,200));`  
`       contentPane.add(jmolPanel);`

`       frame.pack();`  
`       frame.setVisible(true); `

`   }`  
`   public void setStructure(Structure s) {`  
`       `  
`       frame.setName(s.getPDBCode());`

`       // actually this is very simple`  
`       // just convert the structure to a PDB file`  
` `  
`       String pdb = s.toPDB();`  
`      `  
`       structure = s;`  
`       JmolSimpleViewer viewer = jmolPanel.getViewer();`

`       // Jmol could also read the file directly from your file system`  
`       //viewer.openFile("/Path/To/PDB/1tim.pdb");`  
` `  
`       // send the PDB file to Jmol.`  
`       // there are also other ways to interact with Jmol, but they require more`  
`       // code. See the link to SPICE above...`  
`       viewer.openStringInline(pdb);`  
`       viewer.evalString("select *; spacefill off; wireframe off; backbone 0.4;  ");`  
`       viewer.evalString("color chain;  ");`  
`       this.viewer = viewer;`

`   }`

`   public void setTitle(String label){`  
`       frame.setTitle(label);`  
`   }`

`   public JmolSimpleViewer getViewer(){`

`       return jmolPanel.getViewer();`  
`   }`

`   static class ApplicationCloser extends WindowAdapter {`  
`       public void windowClosing(WindowEvent e) {`  
`           System.exit(0);`  
`       }`  
`   }`

`   static class JmolPanel extends JPanel {`  
`       /**`  
`        * `  
`        */`  
`       private static final long serialVersionUID = -3661941083797644242L;`  
`       JmolSimpleViewer viewer;`  
`       JmolAdapter adapter;`  
`       JmolPanel() {`  
`           adapter = new SmarterJmolAdapter();`  
`           viewer = JmolSimpleViewer.allocateSimpleViewer(this, adapter);`  
`           `  
`       }`

`       public JmolSimpleViewer getViewer() {`  
`           return viewer;`  
`       }`

`       public void executeCmd(String rasmolScript){`  
`           viewer.evalString(rasmolScript);`  
`       }`

`       final Dimension currentSize = new Dimension();`  
`       final Rectangle rectClip = new Rectangle();`

`       public void paint(Graphics g) {`  
`           getSize(currentSize);`  
`           g.getClipBounds(rectClip);`  
`           viewer.renderScreenImage(g, currentSize, rectClip);`  
`       }`  
`   }`

}

```

For a more complex example that includes a number of classes that
interact with Jmol on a deeper level see [the SVN repository of
SPICE](http://www.derkholm.net/svn/repos/spice/trunk/src/org/biojava/spice/jmol/)
