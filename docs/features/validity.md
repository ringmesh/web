# What about validity in RINGMesh?

The "validity" is a complex and non-unique notion that often depend on the particular requirements of the 
tools used to assess a particular problem. Considering that, RINGMesh propose a set of tools to ensure 
(1) the topological and geometrical "validity" of Geometrical and Geological entity hold by the `GeoModel`; 
(2) the "validity" of the `GeoModel` itself.

## GeoModel Geometrical Entities Validity Checks

 * Mesh entities: check if mesh entity meshes are valid (no degenerated mesh elements, number of connected 
 component is 1 based on our entity API and call mesh API validity functions which are no isolated vertices) 
 and if the mapping between GeoModelMesh indices are consistent with mesh entity mesh vertices indexation.
 * Check for non manifold edges: use our entity API outputs a .geogram filled with intersecting polygons
 * Surface polygon intersections: use our API (based on GeoModelMesh) and outputs a GEO::Mesh filled with 
 intersecting polygons
 
## GeoModel Geological Entities Validity Checks

 * Geological entities: check that the geological entities has children and the bijectivity of relationships 
 between children and parents
 
## GeoModel Validity Checks
### Topology checks
 * Finite extension test: This validity check ensure that the `GeoModel` have a finite extension. In other words, 
 we check if we can define an internal and external part in a GeoModel. This functionality is defined both in 2D 
 (using `RINGMesh::LineMesh` API) and 3D (using the `RINGMesh::SurfaceMesh` API). Every entities that define the 
 external boundary of the GeoModel are selected and we test:
	1. all these entities defined a closed boundary.
	1. all these entities constitute a unique connected component.
 
  * Test the consistency of connectivity tree:
  With this test, we ensure a consistent organization of geometrical entities hold by a GeoModel. We check:
	1. the bijective relation between boundary and incident entities. If a line "l" is the border of the surface "s", 
	we ensure that (1) "l" is in the order list of "s" and (2) "s" is in the incident list of "l". 
	1. that each entities are at least in the boundary of one another boundary (except for region).
 
### Geometry checks

 * We ensure the conformity between meshes holds by GeoModel geometrical entities (TODO : figure). The conformity is checked
	1. between Lines and their Corners boundary: we check if the vertex of corner is a vertex on the border of incident line.
	1. between Surfaces and their Lines boundary: we check if all vertices and all edges of a line are also vertices and edges on the 
	border of incident surfaces.		
	1. between Regions and their Surfaces boundary (if the volumes are meshed): we check if all vertices and all edges and all polygons 
	of a surface are also a vertices, edges and cell facet on the border of incident region.
	
	In practice, we check the consistency between the geometrical and topological information for all vertices into the GeoModel.
	Ex1: If a vertex belongs to a line but does not belong to any corner, it means that this vertex should not belong any other line of the `GeoModel`.
	EX2: If a vertex belongs to two surfaces, it means that this vertex must belong to a line that is a common boundary of these two surfaces.
	TODO explicit an exhaustive list of tested configuration.

 Note: by default, all checks are launched when you load a GeoModel. You have the possibility to disale some checks 
 with the command line option `validity:do_not_check`.

