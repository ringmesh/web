# Get Started with RINGMesh

## About the source code

### Download the source Code

The source code is available by:

 1. cloning the directory from [GitHub](https://github.com/ringmesh/RINGMesh)
 1. downloading an archive of the sources ([Releases(https://github.com/ringmesh/RINGMesh/releases) 
 or [latest developments](https://github.com/ringmesh/RINGMesh/archive/master.zip)) 
 
 For more information, please follow the instructions of the [Download](/download) section. 
 
### Configure and compile the source Code

RINGMesh is tested under:

 * Linux (64bits)
 * Windows (64 bits)
 * Mac OS (64 bits)

Please find the corresponding instruction in the [configure and compile tutorial](/try/tutorials/configure_compile_ringmesh). 

## About pre-compiled packages

Pre-compiled packages are available in the [Download](/download) section.
After having downloaded the archive that correspond to your operating system, 
please extract the files in the folder where you want to use it.

## Develop with RINGMesh

RINGMesh is a library that provide a development API with functions that can be used in an external project.
We provide an example of a project that set the dependency with RINGMesh and use some functions from the RINGMesh API.

Please Look at the [RINGMesh Plugin example on GitHub](https://github.com/ringmesh/RINGMeshPluginExample).

Once your project is started, you can follow some [tutorials](/try/tutorials) to learn more about the RINGMesh API.

## RINGMesh Utilities 

To access the utilities RINGMesh needs to be configured and compiled with the corresponding option.
If you did not check that option during the configuration using CMake please go back to the 
[configure and compile tutorial](/try/tutorials/configure_compile_ringmesh) and select the `RINGMESH_WITH_UTILITIES` option.
Pre-compiled packages have been built with the `RINGMESH_WITH_UTILITIES` option. 

After building RINGMesh with utilities a set of executable is generated and can be executed from the RINGMesh install directory:

 * Window: `RINGMesh\build\ringmesh\bin\CONFIG\**.exe`
 * Linux: `RINGMesh\build\ringmesh\CONFIG\bin\**.exe`
  
Here is the list of the RINGMesh utilities:

 * `ringmesh-convert`: Load a GeoModel, check its validity and export GeoModel. 
 Supported input and output file formats are listed [here](/features/file_formats). 
 Performed validity checks performed are explained [here](/features/validity).
 * `ringmesh-edit-infos`: Edit information of a GeoModel (such as its name) and save this change in the same file (overwrite) or another one.
 * `ringmesh-mesh-quality`: Load a GeoModel and compute its cell quality. 
 Several metrics are available and the results are stored as an Attribute on each cell.
 Warning: this is only applicable on GeoModel with Regions meshed with tetrahedra.
 * `ringmesh-repair`: Load a Geomodel and repair some basic issues such as geometrical issues on meshes (duplicated vertices, degenerated mesh elements).
 * `ringmesh-rotate`: Load and rotate a GeoModel using a reference frame and an angle.
 * `ringmesh-stats`: Load and print statistics on number of entities, and mesh elements in the GeoModel.
 * `ringmesh-surface-convert`: Load a set of TSurfs (Gocad file format) and output a set on triangulated surfaces 
 into a file format supported by GEOGRAM.
 * `ringmesh-tetrahedralize`: Load a boundary representation (B-Rep) and fill its Regions with tetrahedra using TetGen or another mesher.
 * `ringmesh-translate`: Load and translate a GeoModel using a 3D vector.
 
A description of both functionalities and input parameters is displayed while launching the executable.

## RINGMesh View 
