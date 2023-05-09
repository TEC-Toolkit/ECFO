# ECFO - Emission Conversion Factors Ontology <img src="Logo ECFO.svg" width=30/>
[![DOI](https://zenodo.org/badge/566369718.svg)](https://zenodo.org/badge/latestdoi/566369718)

With the Net Zero agenda gaining significant traction across the world, organisations are often required to report carbon emissions associated with their operation.
However, calculating emissions is not a trivial task and reported scores can differ depending on the choices made by those performing the calculations or the software used to assist with this task.

The aim of this ontology is to formalise emission conversion factors, in order to make the process of emissions calculations more transparent.

## Getting Started

This ontology is available at [https://w3id.org/ecfo#](https://w3id.org/ecfo#) with content negotiation in RDF/XML, TTL, JSON-LD and N-Triples.

To download the ontology in different serializations, you can use a curl command like:

```
curl -sH "Accept:text/turtle" -L https://w3id.org/ecfo#
```

To see the documentation of the ontology, just open its URI on a browser.

<!-- ## Deployment

Add additional notes about how to deploy this on a live system

## Built With

 -->

## Versioning

ECFO uses [Semantic Versioning](http://semver.org).
All ontology releases have their own URI.
For example, version 0.0.1 is available at [https://w3id/ecfo/0.0.1](https://w3id.org/ecfo/0.0.1):

[https://w3id.org/ecfo#](https://w3id.org/ecfo#) redirects to the last available version.

## Authors

* Milan Markovic (Interdisciplinary Centre for Data and AI, [University of Aberdeen](https://www.abdn.ac.uk))
* Daniel Garijo (Ontology Engineering Group, [Universidad Politécnica de Madrid](https://www.upm.es))
* Stefano Germano (Department of Computer Science, [University of Oxford](https://www.cs.ox.ac.uk))
* Iman Naja (Knowledge Media Institute, [The Open University](https://www.open.ac.uk))

## License

This project is licensed under the Creative Commons Attribution 4.0 International License - see the [LICENSE.md](LICENSE.md) file for details.

<!-- ## Acknowledgments -->

## Additional resources

* [Provenance of Emission Calculation Ontology](https://github.com/EATS-UoA/peco)  
  Repository of an ontology extending the PROV standard with the traces of emission calculations.
* [Conversion Factors Knowledge Graph](https://github.com/EATS-UoA/cfkg)  
  Repository with the mappings, cleaning steps and sources used to generate a knowledge graph of conversion factors.
* [Conversion factor SPARQL endpoint](https://sparql.cf.linkeddata.es/)  
  SPARQL endpoint with the current conversion factors loaded.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on the process for submitting pull requests to us. Remember that the last version of the ontology can be found in the `development` folder


This ontology is part of the [TEC-Toolkit](https://github.com/TEC-Toolkit). <img src="Logo TEC.svg" width=40/>


