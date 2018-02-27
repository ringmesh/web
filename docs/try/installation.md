#Get Started with RINGMesh

## About the source code

### Download the source Code

The source code is available by:

 1. cloning the directory from GitHub
 1. downloading Source archives (Released or lining) 
 
 Please follow the instructions of the [Download](download.md) section. 
 
### Configure and compile the source Code

RingMesh is tested under:

 * Linux (64bits)
 * Windows (64 bits)
 * Mac OS (64 bits)

Please find the corresponding instruction in the [configure and compile tutorial](/try/tutorials/configure_compile_ringmesh). 

## About pre-compiled packages

Pre-compiled packages are available in the [Download](download.md) section.
After having downloaded the archive that correspond to your operating system, 
please extract the files in the folder where you want to use it.


## Develop with RINGMesh

RINGMesh is a classical library that provide an API with functions that can be used in an external project.
We provide an example of a project that set the dependency with RINGMesh and use some functions from the RINGMesh API.

Please Look at the [RINGMesh Plugin example on GitHub](https://github.com/ringmesh/RINGMeshPluginExample).

Once your project is started, you can follow some [tutorials](/try/tutorials) to learn more about the RINGMesh API.

## RINGMesh Utilities 

To access the utilities RINGMesh need to be configured and compiled with the corresponding option.
If you did not check that option during the configuration using CMake please go back to the 
[configure and compile tutorial](/try/tutorials/configure_compile_ringmesh) and select the `RINGMESH_WITH_UTILITIES` option.

## RINGMesh View 
This is the list of the current utilities available in RINGMesh