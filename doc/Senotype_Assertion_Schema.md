# Senotype Assertion Schema

```commandline
# The Senotype library table.
# Each row corresponds to a senotype submission.
CREATE TABLE senotype (
    senotypeid VARCHAR(15) PRIMARY KEY, 
    senotypejson JSON
);

# Senotype assertion valuesets.
# Each row corresponds to a member of an assertion valueset--i.e., the categorical values associated with an assertion.
# Fields:
# - predicate_IRI: IRI from the Relations Ontology for the assertion predicate, if the assertion is defined in Relations Ontology
# - predicate_term: the term used for the assertion predicate
# - valueset_code: the valueset member's code in a vocabulary or ontology
# - valueset_term: the valueset member's term as used in Senotype
# Example: the 'human' element of the 'taxon' valueset:
# - predicate_IRI = http://purl.obolibrary.org/obo/RO_0002162'
# - predicate_term = 'in_taxon'
# - valueset_code = 'NCBI:9606'
# - valueset_term = 'human'
# 'http://purl.obolibrary.org/obo/RO_0002162','in_taxon','NCBI:9606','human'
CREATE TABLE senotype_editor_valuesets (
    predicate_IRI VARCHAR(255),
    predicate_term VARCHAR(100),
    valueset_code VARCHAR(100),
    valueset_term VARCHAR(255),
);

INSERT INTO senotype_editor_valuesets (predicate_IRI, predicate_term, valueset_code, valueset_term) VALUES
('http://purl.obolibrary.org/obo/RO_0002162','in_taxon','NCBI:9606','human'),
('http://purl.obolibrary.org/obo/RO_0002162','in_taxon','NCBI:10088','mouse'),
('http://purl.obolibrary.org/obo/RO_0001025','located_in','UBERON:0002048','lung'),
('','has_cell_type','CL:0002553','fibroblast of lung'),
('','has_hallmark','SENOTYPE_VS:C00201','senescence associated secretory phenotype'),
('','has_molecular_observable','SENOTYPE_VS:C00111','secretome'),
('','has_origin','',''),
('','has_inducer','SENOTYPE_VS:C00401','radiation'),
('','has_context','SNOMEDCT_US:397669002','age'),
('','has_assay','OBI:0003647','tandem mass spectrometry analysis'),
('','has_citation','',''),
('','has_dataset','',''),
('http://purl.obolibrary.org/obo/RO_0015004','has_characterizing_marker_set','',''),
('','up_regulates','',''),
('','inconclusively_regulates','',''),
('','down_regulates','','');



# Map of assertion predicates to:
# 1. type of object (valueset or external) 
# 2. name of the field in the Senotype Editor application 
# Fields:
# - predicate_term: the term used for the assertion predicate
# - object_source: 
#   - valueset: the object is a member of a Senotype valueset
#   - external: the object is from an external source - i.e., PubMed, SciCrunch, or SenNet
# - object_form_field: the identifier used for the field in the Edit form of the Senotype Editor
# Example: in_taxon
# - predicate_term: in_taxon
# - object_source: valueset
# - object_form_field: taxon
CREATE TABLE assertion_predicate_object (
	predicate_term VARCHAR(100) PRIMARY KEY,
	object_source VARCHAR(255),
	object_form_field VARCHAR(255)

);

INSERT INTO assertion_predicate_object (predicate_term, object_source, object_form_field) VALUES
('in_taxon','valueset','taxon'),
('located_in','valueset','location'),
('has_cell_type','valueset','celltype'),
('has_hallmark','valueset','hallmark'),
('has_molecular_observable','valueset','observable'),
('has_inducer','valueset','inducer'),
('has_assay','valueset','assay'),
('has_citation','external','citation'),
('has_origin','external','origin'),
('has_dataset','external','dataset');


# Table that maps context assertions to codes.
# Fields: 
# context_name: name of the Senotype context 
# code: code in a vocabulary or ontology
# Example: age
# - context_name: age
# - code: SNOMEDCT_US:397669002 
CREATE TABLE context_assertion_code (
	context_name VARCHAR(100) PRIMARY KEY,
	code VARCHAR(100)
);



INSERT INTO context_assertion_code (context_name, code) VALUES
('age','SNOMEDCT_US:397669002');

```