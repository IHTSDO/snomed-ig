## {{ site.data.fhir.igName }}
{:.no_toc}

###  Terminology Binding

#### Conflicts & Specialisation within a Resource
Many resources specify a "*code*" element which is the obvious location for a SNOMED CT code and this should be used where feasible.  However, other fields may exist (often with multiple cardinality) that could potentially conflict or extend the meaning given by the code field.   For example, in the Procedure Resource as well as the code, a message can supply (potentially multiple) bodysite codeable concepts.

So where a body site is NOT a child of the body site specified in code, what behaviour is expected?

Comment - issues with lack of relationship grouping (eg device with bodysite where multiple exist) and inability to specify whether the site is being accessed in a direct or indirect manner.    We could, potentially, suggest enhancements to FHIR to bring its model into line with that of SNOMED to allow it to accurately state meaning using SNOMED CT concepts in an atomic manner, but what benefit would this give (plus ongoing maintenance overhead) when compared to using SNOMED CT in the first place?

#### Options for Handling Semantic Overlap
The following options could be considered to handle the semantic overlap between, say, Condition code and bodySite:

1. Restrict bodySite to [0..0] and require finding site in code
2. BodySite can only be populated if code has no finding site
3. BodySite (if exists) must be a specialization of finding site
4. BodySite must always be a specialization or self of finding site (or absent, since redundant)
5. Only allow conditions with no finding sites and include bodySite
6. Any condition and any bodySite

The SNOMED on FHIR group have a discussion page for these 6 options here:  Binding patterns

We should list the implications of each of these choices.  Also the use each solution in terms of the other.  For example, option 1 is the simple case of version 4.   

If we were to say that all of the semantic meaning exists in the code, then that increases the burden on the maintenance of SNOMED.

Any solution that allows for population of multiple fields must deal with potential conflict - or worse, where a value has been deliberately populate to indicate some other meaning eg second body site affected, and this is mistaken for a conflict.


