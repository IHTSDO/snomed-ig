## {{ site.data.fhir.igName }}
{:.no_toc}

###  Implementing Terminology Services with SNOMED CT


| Operation Name | Resource | Considerations|
" $validate-code | ValueSet | |


#### Best Practice Discussions
Paging - note that the $expand operation defines its own offset and count (count be 0 if you're interested in the total number of matches)

Limits on value set sizes - 1M configurable limit, default page size of 1K

Default language considerations - http headers, server settings (Link to Reuben's work and discussion of X-headers for LangRefsets)

Algorithms for text searching (reference implementation course eg "PNE PNE" finding Pneumococcal pneumonia)