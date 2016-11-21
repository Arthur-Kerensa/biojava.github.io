---
title: RCSB Viewers:Viewer Framework:General Rendering
permalink: wiki/RCSB_Viewers%3AViewer_Framework%3AGeneral_Rendering
---

Notes
-----

-   `     Much of this is GL specific, and the namespace reflects that.  Expect these names to change to`  
    `     more generic terms.  For example:`  
    `     `
    -   JoglSceneNode -\> Scene (node has connotations in scenegraph
        structures, so would rather either
        `           ignore the term, or tie to a proper corollary)`

    -   DisplayListGeometry -\> ScenePrimitive
    -   DisplayListRenderable -\> SubScene
    -   DisplayLists -\> flat collection of all display lists objects.
-   `     A further goal would be to factor out the GL specific parts of the code and allow the system to be`  
    `     switched to a different rendering engine.`  
    `   `

Relevent Classes
----------------

-   GlGeometryViewer
-   JoglSceneNode
-   DisplayListGeometry\*
-   Renderable
-   DisplayListRenderable
-   DisplayLists

Explanation
-----------

Rendering is a fairly complex topic, so we can only give the broad
brush-strokes, here.

Essentially, all rendering is triggered/controlled by the
*GlGeometryViewer* class and it's derivations. When called upon to
render, it runs through a set of 'display list' structures, which
contain geometry definitions on a component type by component type
basis.

Actual geometry generation is delegated to the
*\<componentType\>Geometry* classes. If rendering the first time, the
class generates the geometry and hands back the created display list. On
subsequent renders, just the display list is returned, saving
regeneration of geometry.

Analysis
--------

Essentially, this is a good mechanism, however the granularity is too
fine. Display lists are only for spheres, cylinders, and the residue
pieces created for secondary structures. Again, while the latter is
good, the former is too fine-grained. It would be better if higher level
display lists were defined on a chain basis, that would in turn invoke
the sphere and cylinder display lists.

This adds to the complication in case of editing/modification, of
course, because in doing so, the higher level display lists need to be
discarded and regenerated. This is probably the biggest argument for
going with a scene-graph implementation - a scene-graph facility will
automatically handle all of this.
