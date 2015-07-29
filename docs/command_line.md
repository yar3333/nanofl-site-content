# NanoFL command-line


## Normal mode
In normal mode IDE starts as usual and support interactions with user after command-line arguments processing.
Don't use this in batch processing due to some limits (not support relative file paths, process can exit without waiting real IDE closing, exit code may be wrong).
```
NanoFL.exe [ <options> ] [ <file_to_load_or_import> | <script_file_to_execute.js> ] ...
```

Options sequence is important: NanoFL process options consecutive from first to last. Next options are supported:

* `-export <output file path>` - Export or save current document depends on output file extension.
* `-resize-fit <width>x<height>` - Resize document to fit specified size. `<width>` or `<height>` can be ommited.
* `-generator <name>/<mode>` - Set document's generator and it's mode. If mode ommited, then the first mode will be used. For example: "CreateJS/HTML" or just "CreateJS".
* `-fps` - Show frames per second HUD.
* `-jsconsole` - Show debug console.

Examples:
```
# import Flash document and save as NanoFL document
NanoFL.exe c:\myflash\myflash.xfl -export c:\mynanofl\mynanofl.nfl

# load NanoFL document and export as PNG image
NanoFL.exe c:\mynanofl\mynanofl.nfl -export c:\myimage.png
```


## Batch mode
Use next command to run NanoFL in batch mode (advantages: waiting for exit, correct exit code and relative paths support):
```
nanoflc.exe <any_nanofl_options>
```
		
Examples:
```
# load NanoFL document, export as PNG image and exit
nanoflc.exe mynanofl\mynanofl.nfl -export myimage.png
```
