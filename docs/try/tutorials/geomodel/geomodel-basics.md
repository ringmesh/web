
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

```
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
```

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
This part is dedicated to GeoModel toplogical Entities [see GeoModel](/features/geomodel).
It shows how to access and manipulate geometrical and geological enties either
by their global index or their adjacency relationships.

#### GeoModelMeshEntities
This example shows how to iterates on geometrical enties that define the boundary representation of the model.

```
    // Iterates on the Surfaces of a GeoModel and looks for boundaries and incident_entities
    for( const auto& surface : geomodel.surfaces() )
    {
        // Iterates on boundary lines
        for( auto boundary_id : range( surface.nb_boundaries() )
        {
            const auto& line = surface.boundary( boundary_id );
            ...
        }
        // Iterates on incident regions (max. 2 incident regions)
        for( auto incident_id : range( surface.nb_incident_entities() )
        {
            const auto& region = surface.incident_entity( incident_id );
            ...
        }
    }
```

#### GeoModelGeologicalEntities
This example shows how to iterate on geological enties. It allows to access to geometrical entities that belong
to the same geological feature.

```
    // Iterates on the Interfaces of a GeoModel and looks for children (being GeoModelMeshEntities)
    for( const auto& cur_interface : geomodel.geol_entities( Interface::type_name_static() ) )
    {
        // Iterates on boundary lines
        for( auto child_id : range( cur_interface.nb_children() )
        {
            const auto& surface = cur_interface.child( child_id );
            ...
        }
    }

    // Iterates on the Surfaces of a GeoModel and looks for them parent of type Interface
    for( const auto& cur_surface : geomodel.surfaces() )
    {
        if( cur_surface.has_parent( Interface::type_name_static() ) )
        {
            const auto& parent = cur_surface.parent( Interface::type_name_static() );
            ...
        }
    }
```

### Manipulate GeoModelMesh

The GeoModelMesh is made of four data bases to provide a global and unique indexing of mesh component.
This ease a global iteration through the GeoModel.

```
    // Build GeoModelMesh
    GeoModelMesh gmm(geomodel);

    // Iterates on the RINGMesh::GeoModelMesh (gmm) vertices without redundancy
    for( auto v : range( gmm.vertices.nb_vertices() ) )
    {
        const auto& point = gmm.vertices.vertex( v );
    }

    // Iterates on the RINGMesh::GeoModelMesh (gmm) facets without redundancy
    for( auto surface_id : range( gmm.model().nb_surfaces() ) )
    {
        // Each surface can be stored twice if it is at the interface of two meshes
        // It is also possible to iterate only on triangles or quads
        for( auto polygon_id : range( gmm.polygons.nb_polygons( surface_id ) ) )
        {
            auto polygon_id_in_the_mesh = gmm.polygons.polygon( surface_id, polygon_id );
            std::cout << "Nb vertices in the polygon: " <<
                gmm.polygons.nb_vertices( polygon_id_in_the_mesh ) << std::endl;
        }
    }

    // Iterates on the RINGMesh::GeoModelMesh (gmm) cells and their adjacent cells
    for( auto region_id : range( gmm.model().nb_regions() ) ) {
        // It is also possible to iterate only on a specific cell type
        for( auto cell_id : range( gmm.cells.nb_cells( region_id ) ) )
        {
            auto cell_in_gmm = gmm.cells.cell( region_id, cell_id );
            for( auto facet_id : range( gmm.cells.nb_facets( cell_in_gmm ) ) )
            {
                // Global cell adjacent index
                auto global_c_adj = gmm.cells.adjacent( { cell_in_gmm, facet_id } );
                if( global_c_adj == NO_ID )
                {
                    // The cell is on the border
                    ...
                }
                else
                {
                    ...
                }
            }
        }
    }
```
