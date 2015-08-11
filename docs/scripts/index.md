# Scripts

You can control NanoFL IDE (open/save documents, draw, select objects, manage library...) with js-scripts.

## Run JavaScript from command-line

Just use `-script` command-line option. For example:
```shell
nanoflc.exe mydoc.nfl -script "app.document.properties.width = 1000; app.document.properties.height = 500;" -export mydoc.nfl
```

## Run JavaScript from external file

First of all, prepare `*.js` file:
```js
var app = window.app; // link to NanoFL application

var document = app.document; // current NanoFL document
var editor = document.editor; // editor allow you to modify document

editor.set_zoomLevel(50);

var curve = new nanofl.engine.geom.StrokeEdge(1,1,50,1,100,100,new models.common.strokes.SolidStroke("red"));
editor.get_activeLayer().shape.get_element().combine_strokeEdge(curve);

var line = new nanofl.engine.geom.StrokeEdge(100,100,350,100,null,null,new models.common.strokes.SolidStroke("green",3));
editor.get_activeLayer().shape.get_element().combine_strokeEdge(line);

var textRun = new nanofl.TextRun("Hello World!","green","Arial","",40,"left",0,null,null);
var textField = new nanofl.engine.elements.TextElement("",0,0,false,false,[textRun],null);
textField.matrix.tx = 120;
textField.matrix.ty = 40;
editor.get_activeLayer().addElement(textField);
```

Next, run your NanoFL and specify script name as argument:
```shell
NanoFL.exe myScript.js
```

It's all!
