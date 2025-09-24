# Schema of Senotype Submission

## Provenance Model

In the senotype provenance model, the senotype submission is atomic.

### Version

In general, the definition of a **senotype**  will change over time. 
A senotype will thus have multiple **versions**, or representation of the senotype at 
different stages of the senotype's evolution.

A citation for a senotype must refer to a particular version of the senotype. 
A version of a senotype is _published_ in DataCite Commons and assigned 
a unique **Digitial Object Identifier** (DOI).
Once a version of a senotype is published in DataCite, its content is fixed. Changing the
definition for a Senotype will require publishing a new version.

### Senotype Submission

A subject matter expert will use the Senotype Editor to define a senotype. 
Each version of a senotype is _submitted_ to the senlib database. 

A **senotype submission** corresponds to a version of a senotype. 

Senotype submission files will be stored in JSON format 
in the **senotype** table of the senlib database.

A senotype submission will be assigned a unique SenNet resource identifier. 

The DOI for a published version is associated with a senotype submission.
Because of the constraint introduced by DOIs, the senotype submission is 
atomic in the senotype data model.

### Provenance

Submissions for a senotype are organized temporally into a _provenance chain_.

Each submission record will include two SenNet provenance identifiers that locate
the submission in the senotype's provenance chain:
- the identifer of the submission's **predecessor**
- the identifier of the submission's **successor**

The version of a senotype admission is derived from the entire provenance chain--
i.e., from the provenance identifiers of all submissions for the senotype.


For example, consider a set of senotype submission jsons with the following provenance identifiers:
```
"id": "SNT888.TEST.020",
		"provenance": {
			"predecessor": null,
			"successor": "SNT888.TEST.021"
		}
------
"id": "SNT888.TEST.021",
		"provenance": {
			"predecessor": "SNT888.TEST.020",
			"successor": "SNT888.TEST.022"
		}
------
"id": "SNT888.TEST.022",
		"provenance": {
			"predecessor": "SNT888.TEST.021",
			"successor": null
		}	
		
```
The provenance chain for this set of submission is [SNT888.TEST.020, SNT888.TEST.021, SNT888.TEST.022].
We can use the provenance chain to assert that "Version 1" of the senotype has identifier SNT888.TEST.020
and that the latest version of the senotype ("VERSION 3") has identifier SNT888.TEST.022.


### Simple Assertions

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
- source
  The _source_ will be one of the following:
  - **valueset**: terms for the object will be obtained from the valueset in the _valuesets_ directory
  - **external**: terms for the object will be obtained via API calls to external sources
- code
  A code will be in format SAB:code, in which SAB refers to an ontology or vocabulary in the 
  HubMAP/SenNet instance of the **Unified Biomedical Knowledge Graph** (UBKG).

### Example
The following represents the assertion that the senotype 
is associated with humans.
```commandline
"assertions": [
		{
			"predicate": {
				"term": "in_taxon",
				"IRI": "http://purl.obolibrary.org/obo/RO_0002162"
			},
			"objects": [
				{
				"source": "valueset",
				"code": "NCBI:9606"
				}
			]
		},
```


### Context assertions
A **context assertion** is an assertion that allows the specification of bounds and units.
Each object of a context assertion has the following keys:
- term: term for the object
- code: code for the object in an external vocabulary
- lowerbound, upperbound: range
- unit: unit for the context object

Following is an example of an age context.

```commandline
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
					"unit": "year"
				}
			]
		},
```


