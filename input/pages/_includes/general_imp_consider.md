## {{ site.data.fhir.igName }}
{:.no_toc}

###  General Implementation Considerations

When starting to think about a SNOMED on FHIR implementation, the following questions should be considered:
* Is the goal (a) homogenous population of resources or (b) permissive guidance to cater for greater flexibility?
* Do we restrict value sets to ensure that the same information cannot be represented in 2 different ways
* The same semantics can’t be included in 2 data elements
* The same semantics can’t be included in 2 resources
* How widely do we require/recommend SNOMED CT is used across each resource (e.g. vital signs, statuses)
* Which of these are potentially in scope?
* Restricting value sets to specific sub-hierarchies
* New value sets for elements not using SNOMED CT
* Restricting cardinalities to reduce ambiguity
* Splicing to align with SNOMED CT concept model
* Mapping FHIR value sets to SNOMED CT (e.g. status)
* Defining SNOMED CT templates to support transformations

