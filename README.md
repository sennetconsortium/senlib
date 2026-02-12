# SenLib - The Senotype Library Database

A **senotype**, or _senescence associated secretory phenotype_, is a cellular senescence functional definition and associated multidimensional description. 
A senotype associates a phenotype with a disease; a set of _markers_ (genes or proteins) expressed by _cell types_ in an anatomic _location_; and an _assay_.

The entities and relationships of a senotype can be encoded with values from standard biomedical vocabularies. A senotype can be modeled using a knowledge graph database
such as the Unified Biomedical Knowledge Graph ([UBKG](https://ubkg.docs.xconsortia.org/)).

Following is a high-level model of an encoded senotype:

<img width="565" height="488" alt="image" src="https://github.com/user-attachments/assets/6c7b8841-c01e-4008-8f30-94e6b816d1f3" />


## Senlib database
The Senlib database will support the definition of senotypes:
1. Senotype _submissions_ will be maintained as JSON objects. Refer to the [Senotype_Submission_Schema](https://github.com/sennetconsortium/senlib/blob/main/doc/Senotype_Submission_Schema.md) document.
2. Assertion reference information used by the Senotype editor will be maintained in various lookup tables. The lookup tables are defined in [this DDL script](https://github.com/sennetconsortium/senlib/blob/main/doc/senotype%20ddl.txt).

CRU operations (not delete) will be managed by the [Senotype Editor](https://github.com/sennetconsortium/senotype_editor).

The [attached Excel file](https://github.com/sennetconsortium/senlib/blob/main/doc/Senotype_Library_Example_Submission.xlsx) simulates the user interface for the curation application.
