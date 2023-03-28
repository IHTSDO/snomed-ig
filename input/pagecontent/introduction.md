### Welcome
FHIR welcomes all users into the house with open arms, offering an information model which often makes recommendations, but rarely specifies exactly which terminology should be used to populate its resources.  When an organization has selected SNOMED CT as its terminology of choice, there are a number of features of FHIR which can be used to their full potential and also a number of potential issues which should be carefully considered and steps taken to avoid.   This guide will attempt to guide Developers, Analysts and System Architects in the best practices for using FHIR specifically with SNOMED CT in order to maximise both the rich expressivity of SNOMED and the semantic operability when exchanging FHIR Resources between systems. 

A summary of using SNOMED CT with FHIR can be found here: [https://hl7.org/implement/standards/fhir/snomedct.html](https://hl7.org/implement/standards/fhir/snomedct.html)

### Benefits of Using SNOMED CT

SNOMED CT supports the development of comprehensive high-quality clinical content in health records. It provides a standardized way to represent clinical phrases captured by the clinician and enables automatic interpretation of these. SNOMED CT is a clinically validated, semantically rich, controlled vocabulary that facilitates evolutionary growth in expressivity to meet emerging requirements.  [Read more here.](https://confluence.ihtsdotools.org/display/DOCSTART/2.+SNOMED+CT+Benefits)

### Interoperability

SNOMED CT could be considered to be like a dictionary.  It tells you exactly what medical concepts mean.  And unlike a dictionary, there is only one definition for each term.   SNOMED also shows how terms relate to each other through a polyhierarchy of "IS A" relationships and concept attributes.   It does not, however, tell you how to write a letter.  It does not tell you how to put those concepts down in a page (or a medical record) in a way that could be transmitted to another system and understood.  For this, it requires a information model, a standard for how records and messages should be laid out and populated.  Which is where HL7 FHIR comes in.   By combining these two world leading standards of both Terminology and Information Model, systems using SNOMED CT and FHIR together will be able to communicate clear and unambiguous meaning in a standard way that can be automatically understood worldwide.

### Distinction between Terminology Services and Binding

This implementation guide will often make a distinction between Terminology Services - that is, the software server that supplies terminology and the operations it performs - with Terminology Binding which is the specification of exactly which coded values (in this case, SNOMED CT concepts) can be put into what parts of the information model, specified by the FHIR Standard.

### Introduction for specific stakeholders
Developers
System Architects
Business Analysts / Specifiers / Profile Designers

### This Guide

FHIR is 
This implementation guide contains:
* mappings from FHIR defined concepts (e.g. codes in code systems, and value sets) to SNOMED CT concepts
* mappings from FHIR resources to the SNOMED CT concept model
* Conformance rules for a FHIR terminology service that provides services for SNOMED CT implementations.

Note, though, that HL7 and SNOMED International may decide to additionally publish some or all of these things elsewhere.

