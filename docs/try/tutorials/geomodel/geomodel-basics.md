
## Basic functionalities on GeoModel
The most efficient way to build a GeoModel is to import its geometry and topology from a
geomodeler. This tutorial presents a simple code to load manipulate and export `GeoModel`.

### GeoModel I/O

GeoModel stores the geometry and the topology of a geological model. It can be imported from boundary 
representation or volumetric representation file.
RINGMesh uses an extensible design to handle various file formats.
The file extention is the key for selecting the suitable loader/saver. 
The Input/Output file formats currently supported by RINGMesh are listed [here](/features/file_formats).

A GeoModel can be loaded and saved as follow:

	 // GeoModel instantiation in 3D
	 GeoModel3D geomodel ;
	
	 // LOADING
	 // path to the file to load
	 // the file extention is the factory key.
	 std::string input_file_name = "path/to/your_input_model.key";
	 // function to load a geomodel from input_file_name
	 geomodel_load( geomodel, input_file_name ) ;
	 
	 // SAVING
	 // path to the file to write
	 // the file extention is the factory key.
	 std::string output_file_name = "path/to/your_output_model.key"; 
	 geomodel_save(geomodel, output_file_name);

When a GeoModel is loaded, its validity is automatically checked and resulting information 
are displayed.

####Try:

 * Load the `ModelA1.ml` (a 3D model boundary representation from gocad).
 * Save it to the GINGMesh file format (.gm)`ModelA1.gm`.
 * Open and look at the .gm file [see description](/features/file_formats).

### Basic Usage
Several functions can be called to study/manipulate/repair the GeoModel:

	print_geomodel_mesh_stats( geomodel ) ; //print the geomodel statistics in the command terminal
	is_geomodel_valid( geomodel ) ; //investigate the validity of the geomodel
	translate(geomodel, {0,0,100}) ; //translate geomodel along vertical axis
	
If RINGMesh is compiled with a meshing sofware:
 
	tetgen_tetrahedralize_geomodel_regions( geomodel ) ; //build volumetric mesh in geomodel regions using TetGen [Si,2015] 
	
This is not an exaustive list of functionalities. Please look at the doxygen documentation.

Try:

 * Load the `ModelA1.ml` (a 3D model boundary representation from gocad).
 * Print statistics on the imported geomodel.
 * Mesh it with TetGen.
 * Print statistics on the imported geomodel.
 * Save it to the GINGMesh file format (.gm) `ModelA1.gm`.
 * Open and analyse the .gm file [see description](/features/file_formats).
 
### Manipulate GeoModelEntities

### Manipulate GeoModelMesh

The GeoModelMesh is made of four data bases to provide a global and unique indexing of mesh component.
This ease a global iteration through the GeoModel.

	// Build GeoModelMesh
	GeoModelMesh gmm(geomodel);
	
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
	