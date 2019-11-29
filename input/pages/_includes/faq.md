# {{ page.title }}

**Top Tip**

1. Watch out for a URL for the Expand operation that contains an additional question mark (e.g. implicit Value Set syntax); these SHOULD be %-encoded
`https://snowstorm-fhir.snomedtools.org/fhir/ValueSet/$expand?url=http://snomed.info/sct?fhir_vs=refset&_format=json`


**How can I get a list of CodeSystems installed on a Terminology Server?**

This is done with FHIR's Search operation - `[base]/CodeSystem` or `[base]/CodeSystem/_search`.
For example, [https://r4.ontoserver.csiro.au/fhir/CodeSystem](https://r4.ontoserver.csiro.au/fhir/CodeSystem)

For details on the extent of support for various CodeSystems (e.g., can it be used in a `[base]/ValueSet/$expand`), you need to consult the Server's TerminologyCapabilities statement which is available at `[base]/metadata?mode=terminology`

(further discussion needed on distinction as to a) whether the code system is present on the server and b) whether it is possible to be used a the substrate for an expansion operation)

**What FHIR Servers can I try connecting to?**

This page by [CSIRO](https://csiro.au) lists a number of servers and sends them requests for valueset expansions:
[https://ontoserver.csiro.au/vstool/](https://ontoserver.csiro.au/vstool/)

**How do I list all the Editions and Versions of SNOMED Installed on a server?**

Note: work needed on the Terminology Capabilities resource to properly answer this question.

**Which version of ECL should be implemented?**

The latest version of the ECL specification is here [https://snomed.org/ecl].
As an implementer it is ideal if you implement the latest version.

As a client you can look at the [TerminologyCapabilities](https://hl7.org/fhir/terminologycapabilities.html) statement to dertermine whether the `constraint` filter is supported for SNOMED CT.
However, there is currently no standard computable mechanism for a server to indicate which version of ECL it supports, nor if it supports ECL-based implicit ValueSets.
Furthermore, there is no computable mechanism in FHIR, nor the ECL specification itself, for indicating whether a subset of the full ECL specification is implemented.

[All ECL versions](https://confluence.ihtsdotools.org/x/DxH-AQ)

**How should historical associations best be accessed?**

Concept Map for "SameAs", accessed via translate operation.

`http://snomed.info/sct[/edition[/version]]?fhir_cm=900000000000527005`

Example of AU Map to 11000168105 |Australian Register of Therapeutic Goods identifier reference set (foundation metadata concept)| ([other available AU maps](https://confluence.ihtsdotools.org/x/1YeJAw)).

`[base]/ConceptMap/$translate?code=60732011000036106&system=http://snomed.info/sct&target=https://www.tga.gov.au/australian-register-therapeutic-goods&url=http://snomed.info/sct?fhir_cm=11000168105`

Example to find "SameAs" for an inactive concept in the International Edition:

`[base]/ConceptMap/$translate?code=134811001&system=http://snomed.info/sct&source=http://snomed.info/sct?fhir_vs&target=http://snomed.info/sct?fhir_vs&url=http://snomed.info/sct?fhir_cm=900000000000527005`

Expected SAME AS association 88189002 |Anesthesiologist (occupation)|

For other types of historic association see [3.2.6.3.2. Representing Historical Associations](https://confluence.ihtsdotools.org/x/8hglAg)


**How to do lookup and expand operations?**

`$lookup`: [https://hl7.org/fhir/codesystem-operation-lookup.html#examples](https://hl7.org/fhir/codesystem-operation-lookup.html#examples)

`$expand`: [https://hl7.org/fhir/valueset-operation-expand.html#examples](https://hl7.org/fhir/valueset-operation-expand.html#examples)

**Why is my CURL not working?**

Watch that running this statement on any unix or mac command line will result in the dollar sign being interpreted as a variable (which probably doesn't exist!) and the URL will break at that point.   Change the " to ' to avoid this.

```
curl --location --request GET "https://ontoserver.csiro.au/stu3-latest/ValueSet/$expand?url=http%253A%252F%252Fsnomed.info%252Fsct%252F32506021000036107%252Fversion%252F20160630%253Ffhir_vs%253Drefset%252F929360061000036106&_format=xml"
```

**How can I find out which value sets contain a given concept?**

See Section 4.9.8.6 of the FHIR Specification - [Searching for codes in Value Sets](http://hl7.org/fhir/valueset.html#search).
In the case of SNOMED CT, this would normally not include any implicit FHIR Value Set that contains an edition and version of the Code System in its entirety.

**How can I find out which reference sets contain a given concept?**

There is currently no simple and direct means to determine this with the FHIR API.

It is possible to expand the implicit ValueSet of all Reference Sets (`http://snomed.info/sct?fhir_vs=refset`) and then to iterate over the resulting codes withe a `$validate-code` call for the code in question and each implicit ValueSet of the form `http://snomed.info/sct?fhir_vs=refset/[sctid]`

It has been suggested that reference set membership could be exposed as a property of the code, but this behaviour is not standardised.


**In ConceptMap translate what is the difference between system and source/target?**

`source` and `target` are ValueSet URIs and `system` is the CodeSystem URI of the code being looked up.

**Do I need a CodeSystem resource in order to implement a SNOMED CT ValueSet?**

This question came up in relation to an implementer using the Global Patient Set (GPS) in a non-member country.   The Code System Resource is required to ensure interoperability between licensed and non-licensed sites. In the later case, using the GPS, the Code System Content Mode should be set to fragment, to indicate that only a subset of the contents of the full Code System are included. However, the Code System URL of that fragment should still be http://snomed.info/sct.

