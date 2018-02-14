# Validate your GeoModel with RINGMesh!

"Validity" is a complex and non-unique notion that often depends on application requirements of the 
tools you used to solve a particular problem. Considering that, RINGMesh provides a set of checks to ensure:

1. the topological and geometrical "validity" of each `GeoModel` entities (both geometrical and geological); 
1. the "validity" of the `GeoModel` itself.

Note: by default, all checks are verified at `GeoModel` loading. You can always disable some or all the checks with the command line option `validity:do_not_check`.

 
## GeoModel topology validation
### Finite extension
This first check ensures the finite extension of your `GeoModel`. In other words, 
we verify if we can define the interior and the exterior of your `GeoModel`. This check is defined both in 2D and 3D. 
All the entities defining the external boundary of the `GeoModel` (i.e. `Lines` in 2D and `Surfaces` in 3D) should define:

 1. a closed boundary;
 1. a unique connected component.
 
### Geometrical entiy mapping consistency
We check if the relationships between the geometrical entities are consistent by verifying:

 1. the bijectivity of `Boundary`/`Incident Entity` relationships. If a `Line` L is a border of a `Surface` S, 
 we ensure that (1) L is in the border Entity list of S and (2) S is in the incident Entity list of L.
 1. each Entity is in the boundary of at least one another Entity (except for `Regions` in 3D and `Surfaces` in 2D).

### Geological entiy mapping consistency
We check if the relationships between the geological entities are consistent by verifying:

 1. each geological Entity must have at least one `Child` geometrical Entity;
 1. the bijectivity between `Parent`/`Child` relationships.

## GeoModel geometry validation

### Classic geometric checks
We ensure some minimal requirements on the geometry:

 1. no degenerated mesh element;
 1. a geometrical `Entity` is composed by a unique connected component;
 1. no isolated vertices;
 1. no non-manifold edges;
 1. no intersection between any `Surface` polygons in the `GeoModel`.
 
### Conformity between geometrical entity meshes (TODO: Figure)
The conformity is checked following these properties:

 1. between `Lines` and their `Corners` boundary: the vertex of corner is a vertex on the border of incident `Lines`;
 1. between `Surfaces` and their `Lines` boundary: all the vertices and all the edges of a `Line` are also vertices and edges on the border of incident `Surfaces`;
 1. between `Regions` and their `Surfaces` boundary: all the vertices and all the edges and all the polygons of a `Surface` are also vertices, edges and cell facets on the border of incident `Regions`.
    
## RINGMesh conventions

We check a consistent mapping between `GeoModelMesh` vertex indexation and vertex indexations in geometrical `Entities`.

