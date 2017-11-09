The key object of RINGMesh is the GeoModel that represents a geological model.

# Constitutive elements

A model is defined by its constitutive elements (RINGMesh::GeoModelEntity) that can
be derived into several classes:
* The base entities (RINGMesh::GeoModelMeshEntity). They define the geometry of the model
  * Regions 3D  
  * Surfaces 2D
  *  Lines 1D
  * Corners 0D 

* The geological entities (RINGMesh::GeoModelGeologicalEntity). They are groups of
  base entities according to their geological meaning.
  * Layers 
  * Interfaces
  * Contacts
    
* The RINGMesh::Universe that bounds the volume of interest.

\image html geomodel_elements.svg 
\image html ringmesh_uml.png

The RINGMesh::GeoModelEntity stores the basic required information to identify an element
of the RINGMesh::GeoModel: 
* The RINGMesh::GeoModel owning the element.
* The index and type of the element.
* A name.
* A geological feature (fault, horizon...).
* ...

# The Geometrical Entities: RINGMesh::GeoModelMeshEntity

A RINGMesh::GeoModelMeshEntity is an abstract class 
of the RINGMesh::GeoModelEntity. It stores a RINGMesh::Mesh to support the
Geometry of:
* RINGMesh::Region 
* RINGMesh::Surface
* RINGMesh::Line
* RINGMesh::Corner

The low level classes implement methods to operate on meshes according to their dimension.

# The Geological Entities: RINGMesh::GeoModelGeologicalEntity

A RINGMesh::GeoModelGeologicalEntity is an abstract class 
of the RINGMesh::GeoModelEntity. It stores the connectivity between RINGMesh::GeoModelMeshEntity
to provide a geological meaning to geometrical entities. It uses a kind of parent/child
implementation.
Built-in RINGMesh::GeoModelGeologicalEntity (sub-classes) in RINGMesh are:
* RINGMesh::Contact. It is the parent of several RINGMesh::Line (children).
  A RINGMesh::Contact represents
  a geological contact, i.e. the intersections between two
  RINGMesh::Interface (intersection between two
  faults or between a fault and a horizon for instance).
* RINGMesh::Interface. It is the parent of several RINGMesh::Surface (children).
  A RINGMesh::Interface represents a 2D geological objects such as a fault or a horizon.
* RINGMesh::Layer. It is the parent of several RINGMesh::Region (children). It represents
  a geological layer.

It is possible to define other kinds of RINGMesh::GeoModelGeologicalEntity
by deriving RINGMesh::GeoModelGeologicalEntity.
 
# RINGMesh::GeoModelMesh : a global mesh representation of the GeoModel
 
The GeoModelMesh is one mesh built from copying and merging the RINGMesh::GeoModelMeshEntity.
\link ringmesh_geomodel_mesh Description of the GeoModelMesh \endlink
 
 
#Building a GeoModel
 
The class RINGMesh::GeoModelBuilder implements functions to 
build and modify the elements of a RINGMesh::GeoModel.
Any new builder should derive from this class.
Three main builders are implemented:
* RINGMesh::GeoModelBuilderGM to load RINGMesh geological model format
  (boundary representation or 3D meshed models).
* RINGMesh::GeoModelBuilderGocad to load either:
  * A SKUA-GOCAD structural model saved in a .ml (RINGMesh::GeoModelBuilderML) file.
  * A volumetric model saved in a .so (RINGMesh::GeoModelBuilderTSolid) file.
* RINGMesh::GeoModelBuilderSurfaceMesh and RINGMesh::GeoModelBuilderMesh to build a
RINGMesh::GeoModel from a RINGMesh::Mesh.
