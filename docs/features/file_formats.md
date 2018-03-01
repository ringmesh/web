# Input and Output file formats

The GeoModel is the Data Model powered by RINGMesh (see the full description of the GeoModel [here](/features/geomodel).
RINGMesh proposes an home-made file format with the `.gm` extension to read and write GeoModels.

Beyond that, RINGMesh provides an extensible design to ease your possibility to add new file formats. We present here an exhaustive list 
of input and output file formats currently supported by RINGMesh. These file formats are different if you are dealing with GeoModels in 3D 
or if you are dealing with a cross section of a GeoModels in 2D.

## Input/Output GeoModels in 3D

### Inputs GeoModel3D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .ml                | SKUA-GOCAD      |
| .so                | SKUA-GOCAD      |
| .msh (in progress) | GMSH            |


### Outputs GeoModel3D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .ml                | SKUA-GOCAD      |
| .so                | SKUA-GOCAD      |
| .msh               | GMSH            |
| .tetgen            | TetGen          |
| .csmp              | CSMP++          |
| .vtk               | ParaView        |
| .mfem              | MFEM            |
| .inp               | Abaqus          |
| .adeli             | Adeli           |
| .fem               | Feflow          |
| .smesh             | Smesh           |
| .stl               |                 |

## Input/Output GeoModels cross section in 2D 

### Inputs GeoModel2D

| Extension          |     Software    | 
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .model             | Stradivarius    |
| .svg               | Inkscape        |
| .msh (in progress) | GMSH            |

### Outputs GeoModel2D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .mfem              | MFEM            |
| .msh (in progress) | GMSH            |

## Conversion

For converting a geological model from one file format to another, 
you can make use of the utility executable shipped with RINGMesh: `ringmesh-convert`.

Here is the command syntax:

    ringmesh-convert in:geomodel=/path/to/your/file.ext1 out:geomodel=/where/you/want/to/save/file.ext2

Note: to generate and compile this executable, you should select the option `RINGMESH_WITH_UTILITIES` in the cmake configuration options.
