---
layout: page
title: Installation
permalink: /installation/
menu: main
order: 1
---

RINGMesh is tested under Linux (64 bits) and Windows (64 bits).
You will need CMake (version >= 3.1). There is no other dependency (everything
you need is shipped with RINGMesh). Follow the Linux, Mac OS or Windows instructions below.

To clone RINGMesh you need Git (https://git-scm.com/).
Make sure that Git binary directory is in your computer path (environment variable).
Under Windows, after installing Git you should have in your path environment variable:
C:\Program Files\Git\cmd.
Warning: TortoiseGit (https://tortoisegit.org/) does not install Git.

# Linux


## Configuring RINGMesh

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

## Compiling RINGMesh

To compile you need the following packages (on Debian-based linux):

 * build-essential
 * libx11-dev
 * libxrandr-dev
 * libxinerama-dev
 * libxcursor-dev
 * freeglut3-dev
 * libxi-dev

Note: you need gcc/g++ version higher or equal to 4.8 to compile RINGMesh.

Then, to compile RINGMesh, go to RINGMesh root directory and:

```bash
cd build/Release
make
```
To build in debug, go to build/Debug instead.

## Compiling the documentation

To be able to compile the documentation, you have to set the cmake flag `BUILD_DOCUMENTATION`
to on when configuring the project:

```bash
cd build
cmake .. -DBUILD_DOCUMENTATION:bool=on
cd build Release
make doc-devkit
```
## Troubleshooting

If you get this error during geogram gfx compilation (occured for Ubuntu 17.04):
```
No rule to make target '/usr/lib/x86_64-linux-gnu/libGL.so'
```
you can try under root:
```bash
rm /usr/lib/x86_64-linux-gnu/libGL.so
ln -s /usr/lib/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
```
## Additionnal information

### Eclipse-cdt project
[Eclipse-cdt](http://www.eclipse.org/cdt/)
project is provided (.project and .cproject). You can import RINGMesh into
Eclipse: File>Import...>General>Existing Projects into Workspace.

# Windows

## Configuring RINGMesh

Launch CMake GUI, indicate where is the source code as the path to RINGMesh root and
where to put the binaries as this_root/build/ringmesh.
Configuration options can be set in using the interface.

RINGMesh has previously been compiled with:

* Visual Studio 10 2010 Win64
* Visual Studio 11 2012 Win64
* Visual Studio 12 2013 Win64
* Visual Studio 14 2015 Win64
* Visual Studio 15 2017 Win64

## Compiling RINGMesh

Make sure that you have installed C++ package for VisualStudio through the VisualStudio installer.
You can either launch building in VisualStudio or calling cmake in command line
in the build directory created at the configuration step:

```
cmake --build . --config Release
cmake --build . --config Debug
cmake --build . --config RelWithDebInfo
```

The available compilation modes are:

* Release
* Debug
* RelWithDebInfo (mandatory to debug a Gocad plugin in Debug mode with a Gocad
  in Release, there are issues between libraries in Debug linked to a Gocad plugin)

## Compiling the documentation

* Check the BUILD_DOCUMENTATION option when using cmake
* Open the solution which is in build/ringmesh/RINGmesh.sln in VisualStudio
* Build the doc-devkit or the doc-devkit-lite project

See the documentation section for more details.

# Mac OS

## Configuring RINGMesh

## Using clang (without Xcode)
As in Linux.

## Using Xcode IDE
As in Windows but with the Xcode generator
(use "-G Xcode" if you use cmake in command lines).

## Compiling RINGMesh
You need to install the Mac OS "Command Line Developer Tools".

Note: you need gcc/g++ version higher or equal to 4.2 to compile RINGMesh.
In Mac OS, clang is used.

### Using clang (without Xcode)
As in Linux except for the packages.

### Using Xcode IDE
You need to install Xcode IDE.
Open the build/ringmesh/RINGMesh.xcodeproj with Xcode IDE,
and then compile (as in Windows with VisualStudio).
Or use these command lines:
```
cd build/ringmesh
xcodebuild -project RINGMesh.xcodeproj -alltargets -configuration Release
```
To build in Debug, replace "Release" by "Debug" after "-configuration".
