# Scripts

You can control NanoFL IDE (open/save documents, draw, select objects, manage library...) with js-scripts.

## Use pure JavaScript

First of all, prepare *.js file:
```
var app = window.app; // link to NanoFL application

var editor = app.document.editor;

editor.set_zoomLevel(50);

var curve = new models.common.geom.StrokeEdge(1,1,50,1,100,100,new models.common.strokes.SolidStroke("red"));
editor.get_activeLayer().shape.get_element().combine_strokeEdge(curve);

var line = new models.common.geom.StrokeEdge(100,100,350,100,null,null,new models.common.strokes.SolidStroke("green",3));
editor.get_activeLayer().shape.get_element().combine_strokeEdge(line);

var textRun = new nanofl.TextRun("Hello World!","green","Arial","",40,"left",0,null,null);
var textField = new models.common.elements.TextElement("",0,0,false,false,[textRun],null);
textField.matrix.tx = 120;
textField.matrix.ty = 40;
editor.get_activeLayer().addElement(textField);

```

Next, run your NanoFL and specify script name as argument:
```
NanoFL.exe myScript.js
```

It's all!

## Use Haxe
