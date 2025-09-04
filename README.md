# SenLib - The Senotype Library

A **senotype**, or _senescence associated secretory phenotype_, is a cellular senescence functional definition and associated multidimensional description. 
A senotype associates a phenotype with a disease; a set of _markers_ (genes or proteins) expressed by _cell types_ in an anatomic _location_; and an _assay_.

The entities and relationships of a senotype can be encoded with values from standard biomedical vocabularies. A senotype can be modeled using a knowledge graph database
such as the Unified Biomedical Knowledge Graph ([UBKG](https://ubkg.docs.xconsortia.org/)).

Following is a high-level model of an encoded senotype:

<img width="565" height="488" alt="image" src="https://github.com/user-attachments/assets/6c7b8841-c01e-4008-8f30-94e6b816d1f3" />

## Senotype import 
It is anticipated that senotypes will be defined gradually and imported into an instance of UBKG. Senotypes will share a Source ABbreviation (SAB). 

The UBKG architecture currently does not support CRUD operations such as inserts or updates: instead, when source data changes, a UBKG context is generated anew from source. The import of senotype data into the UBKG will require that the UBKG's generation framework first consolidate data on the individually defined senotypes into UBKG edge and node files and then import using the edge and node files. 

This repository will be used to document the schema of Senotype submission files and for
development of the Senotype editor UI.


## Data storage
Senotype submissions will be maintained as JSON objects. 

CRU operations (not delete) will be managed by the [Senotype Editor](https://github.com/sennetconsortium/senotype_editor).

The [attached Excel file](https://github.com/sennetconsortium/senlib/blob/main/doc/Senotype_Library_Example_Submission.xlsx) simulates the user interface for the curation application.

# Examples and use cases
Examples of Senotype admissions are in the _senotypes_ directory of this repository.

The example use case is a submission with three versions, the latest of which has not been published.

# Schema of Senotype admission

### Provenance, DOI, and versioning
A submission will be assigned a SenNet ID via the uuid-api. Each version of a submission
will have its own SenNet ID. The provenance for a version of a submission will be 
stored in terms of the SenNet IDs of the version's predecessor (**previous**) and successor
(**next**).

The relative version can be derived via the **provenance** object.

A senotype submission will be _published_ with a DOI. A published submission with a DOI 
cannot be edited. A new version of a published submission cn be created: the new version
can be edited until it is associated with a DOI.

### Assertions

Each assertion (**subject** _predicate_ **object**) in a Senotype will be represented with a **predicate** object and an **objects**
array. 

#### subject

The Senotype is the **subject** in all of its assertions, so the JSON does not refer to
assertion subjects.

#### predicate

Assertion predicates can be represented with one of the following:
1. an _International Resource Identifier_ (**IRI**) from the [Relations Ontology](https://www.ebi.ac.uk/ols4/ontologies/ro).
2. a underscore-delimited **term**.

### objects

In general, there will be more than one assertion of a particular type--e.g., a Senotype will
have multiple _specified markers_.

The **objects** array collects all objects of an assertion.

Each element of the array will have keys:
- type
  The type will be one of the following:
  - **valueset**: terms for the object will be obtained from the valueset in the _valuesets_ directory
  - **external**: terms for the object will be obtained via API calls to external sources
- code
  A code will be in format SAB:code, in which SAB refers to an ontology or vocabulary in the 
  HubMAP/SenNet instance of the **Unified Biomedical Knowledge Graph** (UBKG).


