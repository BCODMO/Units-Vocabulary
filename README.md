# Units-Vocabulary

For annotations to NERC P06 vocabulary
http://vocab.nerc.ac.uk/collection/P06/current/

See: https://github.com/BCODMO/laminar-web/issues/386

## Competency Questions

1. Use US English label

```
PREFIX annotation: <http://lod.bco-dmo.org/id/annotation/>
SELECT ?id IF(STR(?annotated_name)= "", ?name, ?annotated_name) as ?label ?definition ?deprecated
WHERE {
  GRAPH <http://vocab.nerc.ac.uk/collection/P06/current/> {
    ?id skos:prefLabel ?name .
    ?id skos:definition ?definition .
    OPTIONAL { ?id owl:deprecated ?deprecated . }
    OPTIONAL { 
      ?id annotation:hasAnnotation ?annotation . 
      ?annotation annotation:hasAssertion ?name_assertion .
      ?name_assertion skos:prefLabel ?annotated_name .
      FILTER NOT EXISTS { ?name_assertion owl:deprecated "true"^^xsd:boolean }
    }
  }
}
```
