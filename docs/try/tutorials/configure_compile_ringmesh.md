# Configure and compile RINGMesh source code

## RINGMesh Configuration options
RINGMesh comes with a CMake configuration file. Several options can be selected in order to build the project that fits your needs:

 * `BUILD_GEOGRAM_WITHOUT_EXE`: RINGMesh build the GEOGRAM project. This option allow to build the GEOGRAM libraries used in RINGMesh
 without building executable from GEOGRAM.
 * `BUILD_RINGMESH_VIEW`: Build the viewer to visualize the GeoModel data structure.
 * `RINGMESH_WITH_GRAPHICS`: Build graphical libraries of RINGMesh and GEOGRAM.
 * `RINGMESH_WITH_TESTS`: Build the RINGMesh test environment.
 * `RINGMESH_WITH_TETGEN`: Build the [TetGen](http://wias-berlin.de/software/index.jsp?id=TetGen&lang=1) wrapper library. 
 This option provides functionalities to mesh and re-mesh volume and surfaces with TetGen. Please make sure that you respect the 
 [AGPLv3 license](http://www.gnu.org/licenses/agpl-3.0.en.html) before checking that option.
 * `RINGMESH_WITH_TUTORIALS`: Build the tutorial environment.
 * `RINGMESH_WITH_UTILITIES`: Build all executable corresponding to RINGMesh utilities.
 
## Linux configuration and compilation

### Toolbox

#### Mandatory tools
 * CMake (version >= 3.1)
 * gcc/g++ (version >= 4.8; C++11 support)

#### Other dependencies
To compile the graphical libraries of RINGMesh (more precisely of Geogram),
you need to install the development package of:

 * [X11](https://www.x.org)
 * [XRandR](https://www.x.org/wiki/Projects/XRandR/)
 * [Xinerama](https://sourceforge.net/projects/xinerama/files/)
 * [Xcursor](https://www.x.org)
 * [FreeGlut](http://freeglut.sourceforge.net/)
 * [X Input Extension](https://www.x.org)

The command line under Debian-based OS to install all the necessary packages to
compile RINGMesh is:
```
    sudo apt-get install build-essential libx11-dev libxrandr-dev libxinerama-dev
	libxcursor-dev freeglut3-dev libxi-dev
```

#### Optional tools
 * [Eclipse-cdt](http://www.eclipse.org/cdt/)
project is provided (.project and .cproject). You can import RINGMesh into
Eclipse: File>Import...>General>Existing Projects into Workspace.
 * Doxygen (version >= 1.8.2; C++11 support). This is required if you want to build the documentation.
 
There is no other dependency (everything you need is shipped with RINGMesh).

### Configuring RINGMesh

Execute cmake command in a `RINGMesh/build` directory.

```bash
mkdir build
cd build
```
To configure using default options:
```bash
cmake ..
```
To define the options, use the cmake interface

```bash
cmake-gui .. or ccmake ..
```

### Compiling RINGMesh

To compile RINGMesh, go to RINGMesh root directory and:

```bash
cd build/Release
make
```
To build in debug, go to build/Debug instead.

Note: RINGMesh uses C++ 11 features. You need gcc/g++ version higher or equal to 4.8 to compile it.

#### Troubleshooting

If you get this error during geogram gfx compilation (occured for Ubuntu 17.04):
```
No rule to make target '/usr/lib/x86_64-linux-gnu/libGL.so'
```
you can try under root:
```bash
rm /usr/lib/x86_64-linux-gnu/libGL.so
ln -s /usr/lib/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
```

### Generating the documentation

If Doxygen is installed on your computer, a target ```doc-devkit``` is built during RINGMesh configuration. 
You can generate the documentation using the following command in the `RINGMesh_root/build/config` directory:

```bash
make doc-devkit
```
Open the RINGMesh documentation with your favorite web browser at:  `RINGMesh_root/build/config/ringmesh/devkit/html/index.html`

## Windows configure and compile

### Toolbox
#### Mandatory tools
 * CMake (version >= 3.1)
 * gcc/g++ (version >= 4.8; C++11 support)
 

#### Optional tools

 * RINGMesh is tested using Visual Studio. Make sure that you have installed C++ package for Visual Studio through the 
Visual Studio installer. It compiles with the following version:
	* Visual Studio 12 2013 Win64
	* Visual Studio 14 2015 Win64
	* Visual Studio 15 2017 Win64
 * Doxygen (version >= 1.8.2; C++11 support). This is required if you want to build the documentation.

There is no other dependency (everything you need is shipped with RINGMesh).

### Configuring RINGMesh

 * Launch CMake GUI interface (version >= 3.1). 
 * Indicate where is the source code as the path to RINGMesh root and where to put the binaries as 
 `RINGMesh_root/build`.
 * Set the Configuration options using the CMake GUI interface.
 * Launch the `configure`and `generate` option.

### Compiling RINGMesh

RINGMesh need several third parties that are automatically compiled and installed by compiling 
the project `SUPERBUILD.sln`.

 * Open the project `SUPERBUILD.sln` with the visual studio version that you choose during the configuration step.
 * Build the solution.
 
All the RINGMesh third parties have now been compiled, installed and the `RINGMesh.sln` project have been created in the repository: `RINGMesh_root/build/ringmesh`.

 * Open the project `RINGMesh.sln`.
 * Build the solution. 

The available compilation modes are:

* Release
* Debug
* RelWithDebInfo 

Note: Visual Studio has on pile per configuration mode. You must link consistently with the expected configuration mode.

### Compiling the documentation

If Doxygen (version >= 1.8.2) is installed on your computer, a target ```doc-devkit``` is built during RINGMesh configuration. You can generate the documentation by:
* Opening the solution which is in `RINGMesh_root/build/ringmesh/RINGMesh.sln` in Visual Studio
* Building the doc-devkit

Open the RINGMesh documentation with your favorite web browser at:  `RINGMesh_root\build\ringmesh\devkit\html\index.html`

## Mac OS configure and compile

### Toolbox

#### Mandatory tools
 * CMake (version >= 3.1)
 * gcc/g++ (version >= 4.8; C++11 support)

#### Optional tools
 * Doxygen (version >= 1.8.2; C++11 support). This is required if you want to build the documentation.

There is no other dependency (everything you need is shipped with RINGMesh).

### Configuring RINGMesh

#### Using clang (without Xcode)
As in Linux.

#### Using Xcode IDE
As in Windows but with the Xcode generator
(use "-G Xcode" if you use cmake in command lines).

### Compiling RINGMesh
You need to install the Mac OS "Command Line Developer Tools".

Note: you need gcc/g++ version higher or equal to 4.2 to compile RINGMesh.
In Mac OS, clang is used.

#### Using clang (without Xcode)
As in Linux except for the packages.

#### Using Xcode IDE
You need to install Xcode IDE.
Open the build/ringmesh/RINGMesh.xcodeproj with Xcode IDE,
and then compile (as in Windows with VisualStudio).
Or use these command lines:
```
cd build/ringmesh
xcodebuild -project RINGMesh.xcodeproj -alltargets -configuration Release
```
To build in Debug, replace "Release" by "Debug" after "-configuration".
