# Configuration and compilation

RINGMesh is tested under Linux (64 bits) and Windows (64 bits).
You will need CMake (version >= 3.1) to configure it.
There is no other dependency (everything you need is shipped with RINGMesh). 
Follow the Linux, Mac OS or Windows instructions below.

To clone RINGMesh you need Git (https://git-scm.com/).
Make sure that Git binary directory is in your computer path (environment variable).
Under Windows, after installing Git you should have in your path environment variable:
C:\Program Files\Git\cmd.
Warning: TortoiseGit (https://tortoisegit.org/) does not install Git.

You can clone RINGMesh using:

```
git clone https://github.com/ringmesh/RINGMesh/
```

## Linux


### Configuring RINGMesh

Execute cmake command in a RINGMesh/build directory.

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

### Generating the documentation

If Doxygen is installed on your computer, a target ```doc-devkit``` is built during RINGMesh configuration. 
You can generate the documentation using the following command in the `RINGMesh_root/build/config` directory:

```bash
make doc-devkit
```
Open the RINGMesh documentation with your favorite web browser at:  `RINGMesh_root/build/config/ringmesh/devkit/html/index.html`

### Troubleshooting

If you get this error during geogram gfx compilation (occured for Ubuntu 17.04):
```
No rule to make target '/usr/lib/x86_64-linux-gnu/libGL.so'
```
you can try under root:
```bash
rm /usr/lib/x86_64-linux-gnu/libGL.so
ln -s /usr/lib/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
```
### Additionnal information

#### Eclipse-cdt project
[Eclipse-cdt](http://www.eclipse.org/cdt/)
project is provided (.project and .cproject). You can import RINGMesh into
Eclipse: File>Import...>General>Existing Projects into Workspace.

## Windows

### Configuring RINGMesh

 * Launch CMake GUI interface. 
 * Indicate where is the source code as the path to RINGMesh root and where to put the binaries as 
 `RINGMesh_root/build`.
 * Set the Configuration options using the CMake GUI interface.
 * Launch the `configure`and `generate` option.

RINGMesh compiles with the following Visual Studio version:

* Visual Studio 12 2013 Win64
* Visual Studio 14 2015 Win64
* Visual Studio 15 2017 Win64

Note: RINGMesh uses C++11 features. Make sure that you have installed C++ package for Visual Studio through the 
Visual Studio installer.


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

If Doxygen is installed on your computer, a target ```doc-devkit``` is built during RINGMesh configuration. You can generate the documentation by:
* Opening the solution which is in `RINGMesh_root/build/ringmesh/RINGMesh.sln` in Visual Studio
* Building the doc-devkit

Open the RINGMesh documentation with your favorite web browser at:  `RINGMesh_root\build\ringmesh\devkit\html\index.html`

## Mac OS

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
