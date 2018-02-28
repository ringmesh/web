# Input and Output file formats

The GeoModel is the Data Model powered by RINGMesh (see the full description of the GeoModel [here](/features/geomodel).
RINGMesh proposes an home-made file format with the `.gm` extension to read and write GeoModels.

Beyond that, RINGMesh is able to deal with various file format. We present here an exhaustive list of input and output file format
supported by RINGMesh. These file format are different if you are dealing with 2D or 3D GeoModels.

## Input 

### GeoModel2D 

| Extension          |     Software    | 
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .model             | Stradivarius    |
| .svg               | Inkscape        |
| .msh (in progress) | GMSH            |

### GeoModel3D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .ml                | SKUA-GOCAD      |
| .so                | SKUA-GOCAD      |
| .msh (in progress) | GMSH            |


## Output

### GeoModel2D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .mfem              | MFEM            |
| .msh (in progress) | GMSH            |


### GeoModel3D

| Extension          |     Software    |
| -------------      | -------------   |
| .gm                | RINGMesh        |
| .ml                | SKUA-GOCAD      |
| .so                | SKUA-GOCAD      |
| .msh               | GMSH            |
| .tetgen            | TetGen          |
| .csmp              | CSMP++          |
| .vtk               | ParView         |
| .mfem              | MFEM            |
| .inp               | Abaqus          |
| .adeli             | Adeli           |
| .fem               | Feflow          |
| .smesh             | Smesh           |
| .stl               |                 |


## Conversion

For converting a geological model from one file format to another, 
you can make use of the utility executable shipped with RINGMesh: `ringmesh-convert`.

Here is the command syntax:

    ringmesh-convert in:geomodel=/path/to/your/file.ext1 out:geomodel=/where/you/want/to/save/file.ext2

Note: to generate and compile this executable, you should select the option `RINGMESH_WITH_UTILITIES` in the cmake configuration options.
