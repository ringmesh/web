
## How to build and use GeoModel
### GeoModelBuilder
 
The `RINGMesh::GeoModelBuilder` implements functions to build and modify the elements of a `RINGMesh::GeoModel`.
Any new builder should derive from this class.
Three main builders are implemented:

 * RINGMesh::GeoModelBuilderGM to load RINGMesh geological model format
  (boundary representation or 3D meshed models).
 * RINGMesh::GeoModelBuilderGocad to load either:
    * A SKUA-GOCAD structural model saved in a .ml (RINGMesh::GeoModelBuilderML) file.
    * A volumetric model saved in a .so (RINGMesh::GeoModelBuilderTSolid) file.
 * RINGMesh::GeoModelBuilderSurfaceMesh and RINGMesh::GeoModelBuilderMesh to build a
RINGMesh::GeoModel from a RINGMesh::Mesh.

###GeoModelMesh: How to use the global iteration?

    // Iterates on the RINGMesh::GeoModelMesh (gmm) vertices without redundancy
    for( index_t v = 0; v < gmm.vertices.nb_vertices(); v++ ) {
        const vec3& point = gmm.vertices.vertex( v ) ;
    }
	
    // Iterates on the RINGMesh::GeoModelMesh (gmm) facets without redundancy
    for( index_t s = 0; s < gmm.model().nb_surfaces(); s++ ) {
        // Each surface can be stored twice if it is at the interface of two meshes
        for( index_t f = 0; f < gmm.facets.nb_facets( s ); f++ ) { // It is also possible to iterate only on triangle or quad
            index_t facet_id_in_the_mesh = gmm.facets.facet( s, f ) ;
            std::cout << "Nb vertices in the facets: " << gmm.facets.nb_vertices( facet_id_in_the_mesh ) << std::endl ;
        }
    }

    // Iterates on the RINGMesh::GeoModelMesh (gmm) cells and its adjacent cells
    for( index_t m = 0; m < gmm.model().nb_regions(); m++ ) {
        for( index_t c = 0; c < gmm.cells.nb_cells( m ); c++ ) { // It is also possible to iterate only on one element type
            index_t cell_in_gmm = gmm.cells.cell( m, c ) ;
            for( index_t f = 0; f < gmm.cells.nb_facets( cell_in_gmm ); f++ ) {
                index_t global_c_adj = gmm.cells.adjacent( cell_in_gmm, f ) ; // Global cell adjacent index
                if( global_c_adj == GEO::NO_CELL ) {
                    // The cell is on the border
                    ...
                } else {
                    ...
                }
            } 
        }
    }