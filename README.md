### MeshLab in Houdini

Bringing [MeshLab](http://meshlab.sourceforge.net/) functionality into Houdini.

![alt tag](http://i.imgur.com/6GCDgxq.png)

MeshLab filters can be treated as particular SOP nodes doing remeshing, simplification, repairing, colorizing, etc. There are several dozen of them in the MeshLab. Since Houdini is a processing application itself, many of the filters are present as actual SOP nodes or can be simulated easy with Houdini instruments. Other filters are unique or doing a better job. MeshLab SOPs can be used in networks as ordinary SOP nodes like PolyReduce, Remesh or Subdivide.

#### Installation
[`meshlab.hda`](https://github.com/teared/meshlab-in-houdini/raw/master/otls/meshlab.hda), requires installed  [MeshLab](http://meshlab.sourceforge.net/)

Drop into one of the OTL scan paths, e. g. `$HOME/otls` or `$HIP/otls`.

#### Usage
Select one or more filters and setup parameters for them, building the script. Parameters are similar to MeshLab filter dialogs. Input geometry can be cached to speedup cooking, disconnect corresponding input and select a file in the Input Mesh parameter. If using colorize, vertex quality, uv output filters, corresponding -om options must be present, otherwise MeshLab won't export it. Use the arrow-menu to list all -om options. Tip: change network update mode to "Manual" to make proper script setup. Changing any parameter forces this node to begin non-interruptible cook.

##### Settings
![alt tag](http://i.imgur.com/4w7breX.png)

Path to MeshLab executable must be present. For geometry generation filters such as "Fractal Terrain" inputs are ignored and can be empty. You generally shouldn't change file formats, since default PLY is the most feature-rich. OBJ and STL also can be used to send geometry between both applications.

##### Manage filters
![alt tag](http://i.imgur.com/01DuNRo.png)

It is up to users which filters they want to use. New filters can be exported from MeshLab as .mlx scripts. To import new filters, load MeshLab, apply some filters, export them from `Filters/Show current filter script` dialog into a file, then select this file with "Install Filters" selector. All filters inside the file will be installed, existing filters can be updated or skipped during installation. Uninstall process is pretty straightforward, just select unwanted scripts with the arrow-menu. Both install and uninstall operations invoked with the `Update` button. Tip: MeshLab exports filters with parameters values was set by user. This values will be used as defaults in Houdini. To get proper defaults, reset all parameters in the MeshLab filter dialog when applying the filter.

##### Caveats
1. Processing can be buggy and the MeshLab can crash or freeze during operations. Kill the process and check the "Temp Directory" path for undeleted files. Normally, all files are deleted after processing or processing error.
2. Dumping geometry on disc and then loading it back can be slower than actual processing.

#### License
Public domain.
