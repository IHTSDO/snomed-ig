# SNOMED CT FHIR Implementation Guide

For information about building an implementation guide (both in terms of structure and tooling) see documentation here:  https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation

The built/online version of this guide can be seen here: http://build.fhir.org/ig/IHTSDO/snomed-ig/

This IG uses [FSH](https://build.fhir.org/ig/HL7/fhir-shorthand/).

To install (tested with version 0.14.0):
```
npm install -g fsh-sushi
```

To build using HL7 IG Publisher and Ontoserver:
```
cd snomed-ig
java -Xmx4G -jar publisher.jar -ig . -tx https://r4.ontoserver.csiro.au/fhir
```
 
