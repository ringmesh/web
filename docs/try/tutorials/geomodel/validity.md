# What can we check in RINGMesh?

## Checks on `GeoModel` topology

 * Finite extension test: based on our Mesh API (LineMesh for GeoModel2D and SurfaceMesh for GeoModel3D) -> computes universe and checks number of connected component / use repair fonction from GEOGRAM
 * Connectivity of the geomodel entities: for each mesh entities check both boundary validity and incident validity (bijectivity of relation) and check that entities are at least in the boundary of another boundary (except for region)

## Checks on `GeoModel` geometry

 * Conformity of the meshes between:
  * Surfaces and their Lines boundary
  * Regions and their boundary Surfaces (if the volumes are meshed)
  -> based on our API for GeoModelMesh. Check that points on surfaces are also a point on the border of incident regions. Checks also the validity of all points on into the model (Ex: a point is on a line but does not correspond to a corner, so the point should belong to a single line, and so on.)
 * Mesh entities: check if mesh entity meshes are valid (no degenerated mesh elements, number of connected component is 1 based on our entity API and call mesh API validity functions which are no isolated vertices) and if the mapping between GeoModelMesh indices are consistent with mesh entity mesh vertices indexation.
 * Check for non manifold edges : use our entity API outputs a .geogram filled with intersecting polygons
 * Surface polygon intersections : use our API (based on GeoModelMesh) and outputs a GEO::Mesh filled with intersecting polygons

## Checks about geology

 * Geological entities: check that the geological entities has children and the bijectivity of relationships between children and parents
 
 
 
 Note: by default, all checks are launched when you load a GeoModel. You have the possiblity to disale some checks with the command line option `validity:do_not_check`.

