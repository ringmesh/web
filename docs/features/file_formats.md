# Input and Output file formats

For saving and loading a GeoModel, RINGMesh proposes an home-made file format with the extension `.gm` for GeoModel.
Moreover, RINGMesh offers the possibility to import and export GeoModels from other kinds of file formats.

You will find below the list of input and output file format RINGMesh can read/write for GeoModel in 2D and 3D.

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

For converting a geological model from one file format to another one, 
you can make use of the utility executable shipped with RINGMesh: `ringmesh-convert`.

Here is the command syntax:

    ringmesh-convert in:geomodel=/path/to/your/file.ext1 out:geomodel=/where/you/want/to/save/file.ext2

Note: to generate and compile this executable, you should select the option `RINGMESH_WITH_UTILIES` in the cmake configuration options.
