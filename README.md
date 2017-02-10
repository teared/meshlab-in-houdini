## MeshLab in Houdini

Bringing [MeshLab](http://meshlab.net/) functionality into Houdini.

![alt tag](http://i.imgur.com/6GCDgxq.png)

MeshLab filters can be treated as particular SOP nodes doing remeshing, simplification, repairing, colorizing, etc. Since Houdini is a processing application itself, many of the filters are present as actual SOP nodes or can be simulated easy with Houdini instruments. Other filters are unique or doing a better job. MeshLab SOPs can be used in networks as ordinary SOP nodes like PolyReduce, Remesh or Subdivide.

### Installation
See [Releases](https://github.com/teared/meshlab-in-houdini/releases).

### Usage
![alt tag](http://i.imgur.com/32znbzM.png)

Select one or more filters and setup parameters for them. Parameters are similar to MeshLab filter dialogs. If using filters for colorize, compute quality, generate uv, corresponding Options must be present, otherwise MeshLab won't export it. Use the arrow-menu to list all of them. Input geometry can be cached to speedup cooking. Disconnect input and instead select a file.

Latest MeshLab does not allow empty input. To generate something like fractal terrain from scratch, input dummy box, then use "Delete Current Mesh" as first filter. For another example, to output third mesh created from two inputs, use "Set Current Mesh" filter. Set *current* mesh on first input, then delete current mesh *twice* (second mesh will automatically became *current* when you delete first).

1. Changing any parameter forces this node to begin cook. Change network update mode to "Manual" to make proper script setup before.
2. Processing can be buggy and MeshLab can crash or freeze during operations. Normally, all files are deleted after processing or processing error, but you should check. By default, it dumps files in $HIP.
3. Dumping geometry on and then loading it back can be slower than actual processing.
4. To troubleshoot problems, create script in MeshLab manually and try to use meshlabserver directly. It is easier to break MeshLab than Houdini, so, if you have problems it may be useless to try to fix anything in asset.

### Settings
![alt tag](http://i.imgur.com/4w7breX.png)

Path to MeshLab executable must be present. You generally shouldn't change file formats, since default PLY is the most feature-rich. OBJ and STL also can be used to send geometry between both applications.

### Manage filters
![alt tag](http://i.imgur.com/01DuNRo.png)

It is up to users which filters they want to use. New filters can be exported from MeshLab as .mlx scripts. To import new filters, load MeshLab, apply some filters, export them from `Filters/Show current filter script` dialog into a file, then select this file with "Install Filters" selector. All filters inside the file will be installed, existing filters can be updated or skipped during installation. Uninstall process is pretty straightforward, just select unwanted scripts with the arrow-menu. Both install and uninstall operations invoked with the `Update` button. Tip: MeshLab exports filters with parameters values was set by user. This values will be used as defaults in Houdini. To get proper defaults, reset all parameters in the MeshLab filter dialog when applying the filter.

### License
Public domain.
