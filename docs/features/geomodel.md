# GeoModel: Mutable object composition to represent Geological Model

The key feature of RINGMesh is the `RINGMesh::GeoModel`. It aims at representing a geological model 
with a level of complexity adapted to the problem to solve. Geological objects are complex and 
multiscale.
 
 * The first way to represent and discretize a high level of detail is to use a mesh composition 
of Entities called `RINGMesh::GeoModelEntities`. In this case, the `RINGMesh::GeoModel` defines the
boundary representation of major geological objects holding the discretization and connectivity 
between Entities.
 * The second way to deal with the geological model is to consider the global geometry through a 
single mesh. The `RINGMesh::GeoModel` have that ability to build a `RINGMesh::GeoModelMesh` on the fly.
In this object, every node, edge, polygon and cell can be assessed through 
a global index. It also enables a duplication of nodes along surfaces. This is useful
to feed some physical simulators and export several data structure formats.

## GeoModel Constitutive Elements: GeoModelEntity

A model is defined by its constitutive elements `RINGMesh::GeoModelEntity`. 
There are two main kinds of entities (Figure @fig:geomodel_entities):

 * Geometrical entities that define the geometry of the model through several dimensions:
     * Regions 
     * Surfaces
     * Lines
     * Corners
 * Geological entities that group several geometrical entities according to their geological meaning:
    * Layers 
    * Interfaces
    * Contacts

![Geomodel entities divided into the geometrical entities and the geological entities.
Figure from Pellerin et al. (2017).](images/geomodel_elements.svg){#fig:geomodel_entities}

We know that this is not a complete list. A lot of entities would be valuable to complete the model. 
We strongly encourage people to contribute and complete these lists :)	

### GeoModel Geometrical Entities: GeoModelMeshEntity

A set of `RINGMesh::GeoModelMeshEntity` holds the discretization and the boundary representation of the 
geological model. Each mesh entity knows all connected higher and lower dimension mesh entities. Even if
the topology between Entities is known, each `RINGMesh::GeoModelMeshEntity` stores its own mesh data 
structure independently of each other and you cannot get any global information. Geometrical 
information is contained by an abstract mesh class implemented in RINGMesh. This abstraction level is 
a strength of RINGMesh because it can be adapted to any data structure and eases the coupling between 
softwares ([more details about meshes](./../../features/mesh)).

 * A `RINGMesh::Region` is a volume defined by a set of `RingMesh::Surface` creating a closed "box". 
Every surface that bounds a region can be accessed by its index. A region can be meshed with cells.
 * A `RINGMesh::Surface` is defined by a set of `RINGMesh::Line` creating a closed curve. It defines 
one border of a `RINGMesh::Region`. Neighboring lines and surfaces can be accessed by their indices.
 * A `RINGMesh::Line` is defined by two `RINGMesh::Corner`. Connected corners and surfaces can be 
accessed by their indices.
 * A `RINGMesh::Corner` is a single node that bounds a `RingMesh::Line`. Connected lines can be 
accessed by their indices.

### GeoModel Geological Entities: GeoModelGeologicalEntity

A `RINGMesh::GeoModelGeologicalEntity` stores a geological-based topological structure. It uses a kind
of parent/child implementation where `RINGMesh::GeoModelGeologicalEntity` is the parent of its children
`RINGMesh::GeoModelMeshEntity`. The main idea is to cluster several geometrical entities that compose a 
geological object.

 * `RINGMesh::Layer` is composed by several RINGMesh::Region. A layer is the parent of several children 
 regions. It represents a geological layer.
 * `RINGMesh::Interface` is composed by several RINGMesh::Surface. An interface is the parent of several
 children surfaces. It represents a geological object such as a fault or a horizon.
 * A `RINGMesh::Contact` (parent) is composed by several RINGMesh::Line (children). It corresponds to the
 intersection between two `RINGMesh::Interface`.
 
## GeoModel Global Representation: GeoModelMesh
 
The GeoModelMesh is one mesh built by copying and merging all `RINGMesh::GeoModelMeshEntity` of the GeoModel 
in a global and unique mesh. It allows to access to (1) a more general information than the one stored inside 
the mesh of `RINGMesh::GeoModelEntity`, and (2) a single mesh representing the entire geological model.

To ease the global access to vertices, edges, facets and cells without redundancy at GeoModel geometrical
entity borders; four databases are available. These databases are empty by default and are automatically 
filled as soon as they are used.

 * The `RINGMesh::GeoModelMeshVertices` gives a global and unique access to any vertex of the GeoModel. 
 * The `RINGMesh::GeoModelMeshEdges` gives a global and unique access to any edge and adjacent edges 
 of each GeoModel contacts.
 * The `RINGMesh::GeoModelMeshPolygons` gives a global and unique access to any polygon and adjacent polygons 
 of each GeoModel interfaces.
 * The `RINGMesh::GeoModelMeshCells` gives a global access to any cell and its adjacent cells. At the mesh
interfaces cells can be either connected or disconnected. Several disconnection modes are available according
to the geologic features.
    * No Duplication
	* Duplication along faults only
	* Duplication along horizons only
	* Duplication along faults and horizons
 * The `RINGMesh::GeoModelMeshWells` is a particular database to ease the iteration on well geometry. It provides
 a global and unique access to any edge and adjacent edges of wells. 
