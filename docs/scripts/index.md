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
var document = app.document; // current NanoFL document; `app` is a global link to NanoFL API root object
var editor = document.editor; // editor allow you to modify document
var shape = editor.activeLayer.shape.originalElement; // shape to draw to

editor.zoomLevel = 50;

var curve = new nanofl.engine.geom.StrokeEdge(1, 1, 50, 1, 100, 100, new nanofl.engine.strokes.SolidStroke("red"));
shape.combine(new nanofl.engine.elements.ShapeElement([ curve ]));

var line = new nanofl.engine.geom.StrokeEdge(100, 100, 350, 100, null, null, new nanofl.engine.strokes.SolidStroke("green", 3));
shape.combine(new nanofl.engine.elements.ShapeElement([ line ]));

var textRun = new nanofl.TextRun("Hello World!");
textRun.fillColor = "green";
textRun.family = "Arial";
textRun.size = 40;

var textField = new nanofl.engine.elements.TextElement("", 0, 0, false, false, [textRun]);
textField.matrix.tx = 120;
textField.matrix.ty = 40;
editor.activeLayer.addElement(textField);

editor.update();
```

Next, run your NanoFL and specify script name as argument:
```shell
NanoFL.exe myScript.js
```

It's all!
