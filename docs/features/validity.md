# What about validity in RINGMesh?

The "validity" is a complex and non-unique notion that often depends on the particular requirements of the 
tools used to assess a particular problem. Considering that, RINGMesh proposes a set of tools to ensure 
(1) the topological and geometrical "validity" of geometrical and geological entities hold by the `GeoModel`; 
(2) the "validity" of the `GeoModel` itself.

Note: by default, all checks are launched when you load a `GeoModel`. You have the possibility to disable some checks with the command line option `validity:do_not_check`.

 
## About GeoModel Topology
### Finite extension test
This validity check ensures that the `GeoModel` has a finite extension. In other words, 
we check if we can define an interior and an exterior in a `GeoModel`. This functionality is defined both in 2D 
(using `RINGMesh::LineMesh` API) and 3D (using the `RINGMesh::SurfaceMesh` API). All the Entities (i.e. `Lines` in 2D and `Surfaces` in 3D) defining the external boundary of the `GeoModel` are selected and we test that:

 1. all these `Entities` defined a closed boundary.
 1. all these `Entities` constitute a unique connected component.
 
### Checking the consistency of geometrical entiy mapping
We check if the organization between the geometrical entities hold by a `GeoModel` is consistent.

 1. We check the bijectivity of `Boundary`/`Incident Entity` relationships. If a `Line` L is a border of a `Surface` S, 
 we ensure that (1) L is in the border Entity list of S and (2) S is in the incident Entity list of L. 
 1. We check that each Entity is in the boundary of at least one another Entity (except for `Regions` in 3D and `Surfaces` in 2D).

### Checking the consistency of geological entiy mapping
We check if the organization between the geological entities hold by a `GeoModel` is consistent.

 1. A geological Entity must have at least one `Child` geometrical Entity.
 1. We check the bijectivity between `Parent`/`Child` relationships.

## About GeoModel Geometry

### Global Geometry checks
 1. We check that there is no degenerated mesh elements.
 1. We check that a geometrical `Entity` is composed by a unique connected component.
 1. We check that there is no isolated vertices. 
 1. We check that there is non-manifold edges.
 1. We check that there is no intersection between any `Surface` polygons in the `GeoModel`.
 
### Check the conformity between meshes holds by GeoModel geometrical entities (TODO: Figure). 
The conformity is checked
 1. between `Lines` and their `Corners` boundary: we check that the vertex of corner is a vertex on the border of incident `Line`.
 1. between `Surfaces` and their `Lines` boundary: we check that all the vertices and all the edges of a `Line` are also vertices and edges on the border of incident `Surfaces`.        
 1. between `Regions` and their `Surfaces` boundary (if the volumes are meshed): we check that all the vertices and all the edges and all the polygons 
 of a `Surface` are also vertices, edges and cell facets on the border of incident `Region`.
    
	In practice, we check the consistency between the geometrical and topological information for all vertices into the GeoModel.
    Ex1: If a vertex belongs to a line but does not belong to any corner, it means that this vertex should not belong any other line of the `GeoModel`.
    EX2: If a vertex belongs to two surfaces, it means that this vertex must belong to a line that is a common boundary of these two surfaces.
    TODO explicit an exhaustive list of tested configuration.

## About RINGMesh conventions

We check a consistent mapping between `GeoModelMesh` vertex indexation and vertex indexations in geometrical `Entities`.

