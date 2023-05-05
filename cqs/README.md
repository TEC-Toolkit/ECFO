# Competency Questions

The list of ECFO competency questions.

## SPARQL queries used for implementing the CQs

Using the KG available at:

> https://sparql.cf.linkeddata.es

Queries can be performed urlencoding the query under the following URL:

```
https://sparql.cf.linkeddata.es/dataset.html#query={query}
```

where `{query}` is the SPARQL query URL encoded.

All queries assume a single conversion factor:

> `Kilowatt-hours of Butane` into `Kilograms of CO2e`

### CQ1: What is the source of the emission factor <https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_1>?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?source
WHERE {
    ecfo_instance:CF_1 ecfo:hasEmissionSource/rdfs:label ?source
}
```

#### Answer

| source |
|-|
| Gaseous_fuels_Butane |

### CQ2: What are the units in which the emission source is measured?

(e.g., tonnes of butane, where the unit is tonne)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?unit
WHERE {
    ecfo_instance:CF_1 ecfo:hasSourceUnit/rdfs:label ?unit
}
```

#### Answer

| unit |
|-|
| kilowatt hour |

### CQ3: What is the target chemical compound of a conversion factor?

(e.g., CO2e)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?target
WHERE {
    ecfo_instance:CF_1 ecfo:hasEmissionTarget/rdfs:label ?target
}
```

#### Answer

| target |
|-|
| carbon dioxide equivalent |

### CQ4: What are the units of the chemical compound produced by the emission source?

(e.g., kg of CO2e, where the unit is Kg)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?unit
WHERE {
    ecfo_instance:CF_1 ecfo:hasTargetUnit/rdfs:label ?unit
}
```

#### Answer

| unit |
|-|
| Kilogram |


### CQ5: What is the applicable region of this conversion factor?

(i.e., the region that applies to this CF, like burning tonnes of butane in UK)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?location
WHERE {
    ecfo_instance:CF_1 ecfo:hasApplicableLocation ?location
}
```

#### Answer

| location |
|-|
| https://www.wikidata.org/wiki/Q145 (United Kingdom) |

### CQ6: What is the applicable period for this conversion factor?

(e.g., in the UK they are released in a year basis)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX time: <http://www.w3.org/2006/time#>

SELECT ?start ?end
WHERE {
    ecfo_instance:CF_1 ecfo:hasApplicablePeriod ?t.
    ?t time:hasBeginning/time:inXSDDate ?start.
    ?t time:hasEnd/time:inXSDDate ?end
}

```
Answer:

| start | end |
|-|-|
| 2021-01-01T00:00:00 | 2021-12-31T23:59:59 |

### CQ7: How has a conversion factor varied through the years for a given region?

For this SPARQL query we switch to CNG, because Butane is not available in many years.
We also focus only on the "Net CV" value (there are other conversion factors for "Gross CV").

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2020/>
PREFIX time: <http://www.w3.org/2006/time#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?cf ?value ?start ?end ?context
WHERE {
    ecfo_instance:CF_1 ecfo:hasEmissionSource ?e;
        ecfo:hasEmissionTarget ?t.
    ?cf ecfo:hasEmissionSource ?e;
        ecfo:hasEmissionTarget ?t;
        ecfo:hasAdditionalContext ?context;
        ecfo:hasApplicableLocation ?region;
        rdf:value ?value;
        ecfo:hasScope ecfo:Scope1 ;
        ecfo:hasApplicablePeriod ?period.
    ?period time:hasBeginning/time:inXSDDate ?start;
        time:hasEnd/time:inXSDDate ?end
  filter(regex(?context,"Net cv","i"))
}
```

#### Answer

| cf  | value  | start  | end  | context  | scope  |
|---|---|---|---|---|---|
| https://w3id.org/ecfkg/i/UK/BEIS/2022/CF_2393  | 0.04282 | 2022-01-01T00:00:00 | 2022-12-31T23:59:59 | Net CV  | https://w3id.org/ecfo#Scope3  |
| https://w3id.org/ecfkg/i/UK/BEIS/2022/CF_25  | 0.20227 | 2022-01-01T00:00:00 | 2022-12-31T23:59:59 | Net CV  | https://w3id.org/ecfo#Scope1  |
| https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_21  | 0.20297 | 2021-01-01T00:00:00 | 2021-12-31T23:59:59 | Energy - Net CV  | https://w3id.org/ecfo#Scope1  |
| https://w3id.org/ecfkg/i/UK/BEIS/2020/CF_5  | 0.20374 | 2020-01-01T00:00:00 | 2020-12-31T23:59:59 | Energy - Net CV  | https://w3id.org/ecfo#Scope1  |
| https://w3id.org/ecfkg/i/UK/BEIS/2019/CF_5  | 0.20428 | 2019-01-01T00:00:00 | 2019-12-31T23:59:59 | Energy - Net CV  | https://w3id.org/ecfo#Scope1  |

We can see the evolution of the conversion factor for five years. For one of the years there are two conversion factors for the same materials,

### CQ8: Who is the publisher of the conversion factor?

```sparql
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>

SELECT ?publisher
WHERE {
    ecfo_instance:CF_1 dc:publisher ?publisher.
}
```

#### Answer

| publisher |
|-|
| https://w3id.org/ecfkg/i/Organization/BEIS |

### CQ9: Does this conversion factor need additional context?

(for example, butane is measured as net, not gross value)

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?context
WHERE {
    ecfo_instance:CF_1 ecfo:hasAdditionalContext ?context.
}
```

#### Answer

| context |
|-|
| Energy - Gross CV |

### CQ10: Do any other conversion factors convert from the emission source to the target emission?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?cf ?context
WHERE {
    ecfo_instance:CF_1 ecfo:hasEmissionSource ?e;
        ecfo:hasEmissionTarget ?t.
    ?cf ecfo:hasEmissionSource ?e;
        ecfo:hasEmissionTarget ?t;
        ecfo:hasAdditionalContext ?context.
}
```

Answer:
| cf | context |
|-|-|
| https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_1 | Energy - Gross CV |
| https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_13 | Tonnes |
| https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_5 | Energy - Net CV |
| https://w3id.org/ecfkg/i/UK/BEIS/2021/CF_9 | Volume |


### CQ11: Are there any descriptive tags associated with the source material of a conversion factor?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?tag
WHERE {
    ecfo_instance:CF_1 ecfo:hasTag/rdfs:label ?tag
}
```

#### Answer

| tag |
|-|
| Butane |
| Fuels |
| Gaseous fuels |

### CQ12: Are there any usage notes or disclaimers associated with a conversion factor?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>

SELECT ?notes
WHERE {
    ecfo_instance:CF_1 ecfo:hasUsageNotes ?notes
}
```

#### Answer

| notes |
|-|
| empty (no disclaimers) |

### CQ13: What is the value of a conversion factor?

```sparql
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?value
WHERE {
    ecfo_instance:CF_1 rdf:value ?value
}
```

#### Answer

| value |
|-|
| "0.2224"^^xsd:float |

### CQ14: What is the molecular formula associated with the target emission?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX schema: <https://schema.org/>

SELECT ?formula
WHERE {
    ecfo_instance:CF_1 ecfo:hasEmissionTarget/schema:molecularFormula ?formula
}
```

#### Answer

| formula |
|-|
| CO2e |

### CQ15: What is the symbol used in the source and target units?

```sparql
PREFIX ecfo: <https://w3id.org/ecfo#>
PREFIX ecfo_instance: <https://w3id.org/ecfkg/i/UK/BEIS/2021/>
PREFIX qudt: <http://qudt.org/schema/qudt/>

SELECT ?source ?target
WHERE {
    ecfo_instance:CF_1 ecfo:hasSourceUnit/qudt:abbreviation ?source;
        ecfo:hasTargetUnit/qudt:abbreviation ?target
}
```

#### Answer

| source | target |
|-|-|
| kW.h | kg |
