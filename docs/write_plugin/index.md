# Write plugin

NanoFL has several interfaces to be extended by plugins.
You can write plugin on TypeScript or Haxe (or even on pure JavaScript).
Using NanoFL PluginAPI declaration files (`nanofl.d.ts` for TypeScript and `*.hx` for Haxe) making development simple.

Each plugin is just a `*.js` file in **plugins** application folder.
Also, that folder may contain a directory with plugin-related files.
By convection, this directory must be named same as a plugin.

There are several types of plugins are supported:

* [Importer](#importer) - allow import graphics/sounds/fonts/etc from third-party formats into NanoFL documents;
* [Exporter](#exporter) - allow export graphics/sounds/fonts/etc from NanoFL documents into third-party formats;
* [Filter](#filter) - a raster transformation applyed to symbol instances;
* [Language](#language) - generator of the result files (source files on specified programming language);
* [IDE](#ide) - generator of the solution/project files for specified code IDE.


<a name="importer"></a>

## Importer
Importer plugin is a class which implements `models.common.plugins.IImporterPlugin` interface.
The main method of this class, called by NanoFL IDE, is `importDocument`.
This method must store imported data to received `documentProperties` and `library` objects.
If you need to save media files - use a path from `library.libraryDir`.

Plugin file must contain registration code (executed on plugin load):
```
models.common.Plugins.registerImporter(new MyPluginClass());

```
Plugin file may not have any public variables/functions - core interacts with plugin only by reference from `registerImporter`.

For example of importer plugin written on Haxe, see [FlashXflImporterPlugin](https://bitbucket.org/nanofl/plugins/src/default/FlashXflImporterPlugin).


<a name="exporter"></a>

## Exporter
Exporter plugin is a class which implements `models.common.plugins.IExporterPlugin` interface.
The main method of this class, called by NanoFL IDE, is `exportDocument`.
This method must store data from received `documentProperties` and `library` objects to files of desired format.
If you need to get base path to media files - use `library.libraryDir`.

Plugin file must contain registration code (executed on plugin load):
```
models.common.Plugins.registerExporter(new MyPluginClass());

```
Plugin file may not have any public variables/functions -
core interacts with plugin only by reference from `registerExporter`.

There are not yet any examples of the exporter plugins, but you can look to
[FlashXflExporterPlugin](https://bitbucket.org/nanofl/plugins/src/default/FlashXflExporterPlugin).
This plugin is not ready, but it can be a good start point
(just remember to change "Custom Build" to "Application" in plugin's project properties).


<a name="filter"></a>

## Filter
Filter plugin allow you create visual effects for symbols on the scene.
NanoFL contains [StdFiltersPlugin](https://bitbucket.org/nanofl/plugins/src/default/StdFiltersPlugin) which register several filters:

* [Adjust Color](https://bitbucket.org/nanofl/plugins/src/default/StdFiltersPlugin/src/AdjustColorFilterPlugin.hx) - tune brightness/contrast;
* [Blur](https://bitbucket.org/nanofl/plugins/src/default/StdFiltersPlugin/src/BlurFilterPlugin.hx) - bluring effect;
* [Drop Shadow](https://bitbucket.org/nanofl/plugins/src/default/StdFiltersPlugin/src/DropShadowFilterPlugin.hx) - draw a shadow;
* [Glow](https://bitbucket.org/nanofl/plugins/src/default/StdFiltersPlugin/src/GlowFilterPlugin.hx) - glowing effect.

Each plugin's filter class must implement `models.client.plugins.IFilterPlugin` and have two main points:

* `properties` - array of special objects which describe plugin parameters (user will tune these parameters in NanoFL IDE);
* `getFilter` - method to get instance of EaselJS's [Filter](http://createjs.com/Docs/EaselJS/classes/Filter.html) class.

Plugin file must contain registration code (executed on plugin load):
```
models.common.Plugins.registerFilter(new MyPluginClass());

```
Plugin file may not have any public variables/functions -
core interacts with plugin only by reference from `registerFilter`.

The source code of the filter plugin concatenated to generated result file (`*.html` or `*.js`)
if at least one of the plugin's filters was used in NanoFL document.

<a name="language"></a>

## Language


<a name="ide"></a>

## IDE


[Edit this page at bitbucket](https://bitbucket.org/nanofl/site/src/default/docs/examples/index.md)