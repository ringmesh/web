# Glossary

This page gives definitions of the words commonly used in the RINGMesh project.

## Base objects
 * Point - A position in space: (x,y) in 2D or (x,y,z) in 3D.
 * Segment - Part of a line bounded by two distinct points.
 * Polygon - Part of a plane bounded by a finite number of non-intersecting segments closing in a loop.
 * Polyhedron - Part of a space bounded by a finite number of non-intersecting polygons defining an interior and an exterior.
 
 * N-simplex - The convex-hull of N+1 points
   * Point: 0-simplex
   * Segment: 1-simplex
   * Triangle: 2-simplex
   * Tetrahedron: 3-simplex
 

## Elements of a mesh
 * Mesh cell - A polyhedron of a volumetric mesh.
 * Mesh polygon - A polygon of a surface mesh.
 * Mesh edge - A segment of a linear mesh.
 * Vertex - A corner point of a mesh cell, a mesh polygon or a mesh edge.
 
 * Facet - A (N-1) boundary of a mesh element
   * A face of a mesh cell
   * An edge of a mesh polygon
   * A vertex of a mesh edge

## Mesh: Set of elements 
 * Structured mesh - A mesh with regular connectivity meaning that each vertex is connected to the same number of vertices.
 * Unstructured mesh - A mesh with any connectivity between vertices.
 
 
## Entity

## Notion
 * Topology - Connectivity information between entities. 
