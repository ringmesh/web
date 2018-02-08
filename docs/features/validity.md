# What about validity in RINGMesh?

The "validity" is a complex and non-unique notion that often depend on the particular requirements of the 
tools used to assess a particular problem. Considering that, RINGMesh propose a set of tools to ensure 
(1) the topological and geometrical "validity" of Geometrical and Geological entity hold by the `GeoModel`; 
(2) the "validity" of the `GeoModel` itself.

Note: by default, all checks are launched when you load a GeoModel. You have the possibility to disale some checks 
 with the command line option `validity:do_not_check`.

 
## About GeoModel Topology
### Finite extension test:
This validity check ensure that the `GeoModel` have a finite extension. In other words, 
we check if we can define an internal and external part in a GeoModel. This functionality is defined both in 2D 
(using `RINGMesh::LineMesh` API) and 3D (using the `RINGMesh::SurfaceMesh` API). Every entities that define the 
external boundary of the GeoModel are selected and we test:

 1. all these entities defined a closed boundary.
 1. all these entities constitute a unique connected component.
 
### Ensure a consistent mapping of geometrical entities
We ensure a consistent organization of geometrical entities hold by a GeoModel.

 1. We check the bijective relation between boundary and incident entities. If a line "l" is the border of the surface "s", 
 we ensure that (1) "l" is in the order list of "s" and (2) "s" is in the incident list of "l". 
 1. We check that each entities are at least in the boundary of one another boundary (except for region).

### Ensure a consistent mapping of geological entities
We ensure a consistent organization of geological entities hold by a GeoModel.

 1. A geological entity must have at least one "child" geometrical entity.
 1. We check the bijective relation between a parent and its child entities.

## About GeoModel Geometry

### Global Geometry checks: 
 1. Ensure that there is no degenerated mesh elements.
 1. Ensure that a Geometrical Entity is composed by a unique connected component.
 1. Ensure that there is no isolated vertices. 
 1. Ensure that their in no non manifold edges.
 1. Ensure that their is no intersections between any surface polygons in the GeoModel.
### We ensure the conformity between meshes holds by GeoModel geometrical entities (TODO : figure). The conformity is checked
 1. between Lines and their Corners boundary: we check if the vertex of corner is a vertex on the border of incident line.
 1. between Surfaces and their Lines boundary: we check if all vertices and all edges of a line are also vertices and edges on the 
 border of incident surfaces.        
 1. between Regions and their Surfaces boundary (if the volumes are meshed): we check if all vertices and all edges and all polygons 
 of a surface are also a vertices, edges and cell facet on the border of incident region.
    
	In practice, we check the consistency between the geometrical and topological information for all vertices into the GeoModel.
    Ex1: If a vertex belongs to a line but does not belong to any corner, it means that this vertex should not belong any other line of the `GeoModel`.
    EX2: If a vertex belongs to two surfaces, it means that this vertex must belong to a line that is a common boundary of these two surfaces.
    TODO explicit an exhaustive list of tested configuration.

## About RINGMesh conventions

We ensure a consistent mapping between `GeoModelMesh` vertex indexation and vertex indexation in Geometrical Entities.

