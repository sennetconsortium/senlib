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

This repository will be used to manage individually defined senotypes. Each _submission_ of a senotype definition will be archived in the repository.

Senotype submissions will be stored as files in JSON format.

It is anticipated that a Web-based curation application will allow users to define senotypes and submit definitions for import into the UBKG context.
The [attached Excel file](https://github.com/sennetconsortium/senlib/blob/main/doc/Senotype_Library_Example_Submission.xlsx) simulates the user interface for the curation application.


Senotype submissions will be stored in the repository as JSON files. The schema of the JSON file is straightforward.
A senotype definition is essentially a set of assertions with the senotype as subject. It is assumed that there will be multiple assertions of the same type--e.g., between the senotype and each of its markers. Thus,
1. Assertions are organized into an array.
2. Each assertion object consists of a predicate object and an array of "object" objects.


The following JSON represents the senotype definition in the attached Excel file.

```
{
	"senotype":	{
		"code": "SENOTYPE_C0001",
		"term": "human lung fibroblast copd sasp",
		"definition": "This senescence associated secretory phenotype has been demonstrated in human lung fibroblasts in chronic obstructive pulmonary disease patients using spatial transcriptomics."
	},
	"submitter": {
		"name":	{
			"first": "Jonathan",
			"last": "Silverstein",
			"email": "j.c.s@pitt.edu"
		}
	},
	"assertions": [
		{
			"predicate": {
				"term": "in_taxon",
				"IRI": "http://purl.obolibrary.org/obo/RO_0002162"
			},
			"objects": [
				{
				"term": "human",
				"code": "NCBI:9606"
				}
			]
		},
		{
			"predicate": {
				"term": "located_in",
				"IRI": "http://purl.obolibrary.org/obo/RO_0001025"
			},
			"objects": [
				{
					"term": "lung",
					"code": "UBERON:0002048"
				}
			]
		},
		{
			"predicate": {
				"term": "has_cell_type"
			},
			"objects": [
				{
					"term": "fibroblast of lung",
					"code": "CL:0002553"
				}
			]
		},
		{
			"predicate": {
				"term": "has_hallmark"
			},
			"objects": [
				{
					"term": "senescence associated secretory phenotype",
					"code": "SENOTYPE_VS:C00201"
				}
			]
		},
		{
			"predicate": {
				"term": "has_molecular_observable"
			},
			"objects": [
				{
					"term": "secretome",
					"code": "SENOTYPE_VS:C00111"
				}
			]
		},
		{
			"predicate": {
				"term": "has_origin"
			},
			"objects": [
				{
					"term": "RRID:111111",
					"code" : "https://scicrunch.org/resolver/RRID:AB_90755"
				}
			]
		},
		{
			"predicate": {
				"term": "has_inducer"
			},
			"objects": [
				{
					"term": "radiation",
					"code": "SENOTYPE_VS:C00401"
				}
			]
		},
		{
			"predicate": {
				"term": "has_context"
			},
			"objects": [
				{
					"term": "age",
					"code": "SNOMEDCT_US:397669002",
					"lowerbound": 18,
					"upperbound": 85,
					"unit": {
						"term": "year"
					}
				}
			]
		},
		{
			"predicate": {
				"term": "has_assay"
			},
			"objects": [
				{
					"term": "tandem mass spectrometry analysis",
					"code": "OBI:0003647"
				}
			]
		},
		{
			"predicate": {
				"term": "has_citation"
			},
			"objects": [
				{
					"term": "PMID:31945054",
					"code":"https://pubmed.ncbi.nlm.nih.gov/31945054/"
				}
			]
		},
		{
			"predicate": {
				"term": "has_dataset"
			},
			"objects": [
				{
					"term": "SNT499.ZXRV.452",
					"code": "https://data.sennetconsortium.org/dataset?uuid=83679ee4b5e77f2186eff41e872fee9e/"
				}
			]
		},
		{
			"predicate": {
				"term": "has_characterizing_marker_set",
				"IRI": "http://purl.obolibrary.org/obo/RO_0015004"
			},
			"objects": [
				{
					"symbol": "O76094",
					"code": "UNIPROTKB:O76094"
				},
				{
					"symbol": "ABL1",
					"code": "HGNC:76"
				}
				]
		},
		{
			"predicate": {
				"term": "up_regulates"
			},
			"objects": [

				{
					"symbol": "P22087",
					"code": "UNIPROTKB:P22087"
				},
				{
					"symbol": "Q99988",
					"code": "UNIPROTKB:Q99988"
				},
				{
					"symbol": "P09429",
					"code": "UNIPROTKB:P09429"
				}
			]
		},
		{
			"predicate": {
				"term": "inconclusively_regulates"
			},
			"objects": [
				{
					"symbol": "Q7Z460",
					"code": "UNIPROTKB:Q7Z460"
				}
			]
		},
		{
			"predicate": {
				"term": "down_regulates"
			},
			"objects": [
				{
					"symbol": "P52294",
					"code": "UNIPROTKB:P52294"
				}				
			]
		}
	]
}
```

