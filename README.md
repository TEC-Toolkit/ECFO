# ECFO-Emission-conversion-Factor-Ontology

With the Net Zero agenda gaining significant traction across the world, organisations are often required to report carbon emissions associated with their operation. However, calculating emissions is not a trivial task and reported scores can differ depending on the choices made by those performing the calculations or the software used to assist with this task.

The aim of this ontology is to formalise emission conversion factors, in order to make the process of emissions calculations more transparent.

## Availability
This ontology is available at [https://w3id.org/ecfo#](https://w3id.org/ecfo#) with content negotiation in RDF/XML, TTL, JSON-LD and N-Triples.

To download the ontology in different serializations, you can use a curl command like:
```
curl -sH "Accept:text/turtle" -L https://w3id.org/ecfo#
```

To see the documentation of the ontology, just open its URI on a browser.


## Versioning
ECFO uses semantic versioning. All ontology releases have their own URI. For example, version 0.0.1 is available at [https://w3id/ecfo/0.0.1](https://w3id.org/ecfo/0.0.1):

[https://w3id/ecfo#](https://w3id.org/ecfo#) redirects to the last available version.

## Relevant repositories:
- [The provenance of emission calculation ontology](https://github.com/EATS-UoA/peco): Repository of an ontology extending the PROV standard with the traces of emission calculations.
- [The conversion factors knowledge graph](https://github.com/EATS-UoA/cfkg): Repository with the mappings, cleaning steps and sources used to generate a knowledge graph of conversion factors.
- [Conversion factor SPARQL endpoint](https://cf.linkeddata.es/sparql): SPARQL endpoint with the current conversion factors loaded.