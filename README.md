# MeshLab in Houdini

Processes geometry through [MeshLab](http://meshlab.sourceforge.net/) command line interface bringing the MeshLab functionality into Houdini interface.

![alt tag](http://i.imgur.com/GgRZ6Fo.png)

MeshLab filters can be treated as particular SOP nodes doing remeshing, simplification, repairing, colorizing, etc. There are several dozen of them in the MeshLab. Since Houdini is a processing application itself, many of the filters are present as actual SOP nodes or can be simulated easy with Houdini instruments. Other filters are unique or doing a better job.

## Installation
[`meshlab.hda`](https://github.com/teared/meshlab-in-houdini/raw/master/otls/meshlab.hda), requires installed  [MeshLab](http://meshlab.sourceforge.net/)

Drop into one of the OTL scan paths, e. g. `$HOME/otls` or `$HIP/otls`.

## Usage
MeshLab SOPs can be used in networks as ordinary SOP nodes like PolyReduce, Remesh or Subdivide. Select one or more filters and setup parameters for them, building the script. Processing will begin when node cook. Parameters are similar to MeshLab dialogs which popups when filters are used.

Tip: change the network update mode to "Manual" or set the visibility flag on other node to make a proper script setup. Changing any parameter forces this node to begin non-interruptible (at this moment) cook.

#### Input and output
![alt tag](http://i.imgur.com/uD7Cs1b.png)

Path to MeshLab executable must be present. If using colorize, vertex quality, uv output filters, corresponding -om options must be present, otherwise MeshLab won't export it. Use the arrow-menu to list all -om options.

For geometry generation filters such as "Fractal Terrain" inputs are ignored and can be empty. If the filter expects an input mesh (or meshes), the connected input (or inputs) will be used. Any number of inputs can be connected and processed via MeshLab - edit the operator type definition to get more connections or even multi-input.

#### Manage filters
![alt tag](http://i.imgur.com/01DuNRo.png)

It is up to users which filter they want to use. New filters can be exported from MeshLab as an .mlx scripts. Load the MeshLab, apply some filters and then export them from `Filters/Show current filter script` dialog into a file, then select it in "Install Filters" parameter. All filters inside the script will be installed, existing filters can be updated or skipped during installation. Uninstall process is pretty straightforward - select unwanted scripts with arrow-menu. Both install and uninstall operations invoked with the `Update` button.

Tip: MeshLab exports filters with parameters values was set by user. This values will be used as defaults in Houdini. To get proper defaults, reset all parameters in the MeshLab filter dialog when applying the filter.

#### Caveats
1. Processing can be buggy and the MeshLab can crash or freeze during operations. Kill the process and check the "Temp Directory" path for undeleted files. Normally, all files are deleted after processing or processing error.
2. Dumping geometry on disc and then loading it back can be slower than actual processing.
3. Due to difference in .ply standards Houdini and MeshLab are using, the .obj format is used for input meshes. It is impossible to import any color into MeshLab from Houdini because .obj doesn't store it.

## License
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <http://unlicense.org/>
