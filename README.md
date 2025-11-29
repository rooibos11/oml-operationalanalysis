# CI/CD 

メモ

[published pages](https://utnak.github.io/oml-operationalanalysis/omlanalysis/analysis_matrix.html)

# Query Pattern

## 01 Get Capability and Mission 'operational:requires'
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX base:        <http://imce.jpl.nasa.gov/foundation/base#>
PREFIX operational:        <http://opencaesar.io/example/vocabulary/operational#>

#SELECT DISTINCT ?iri ?id ?name ?type
SELECT DISTINCT* 
WHERE {
	?iri a operational:Capability ;
		base:hasDescription ?m_name .
  	OPTIONAL{
    	?miri operational:requires ?iri.
  }
}
ORDER BY ?m_id
```

## 02 Get Capability and Mission 'operational:isRequiredBy'
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX base:        <http://imce.jpl.nasa.gov/foundation/base#>
PREFIX operational:        <http://opencaesar.io/example/vocabulary/operational#>

#SELECT DISTINCT ?iri ?id ?name ?type
SELECT DISTINCT* 
WHERE {
	?iri a operational:Capability ;
		base:hasDescription ?m_name .
  	OPTIONAL{
    	?iri operational:isRequiredBy ?miri.
  }
}
ORDER BY ?m_id
```


# Setup CI/CD

![1763816576432](image/README/1763816576432.png)




# OML Template

[![Build Status](https://github.com/opencaesar/oml-template/actions/workflows/ci.yml/badge.svg)](https://github.com/opencaesar/oml-template/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/opencaesar/oml-template?label=Release)](https://github.com/opencaesar/oml-template/releases/latest)
[![Documentation](https://img.shields.io/badge/Documentation-HTML-orange)](https://www.opencaesar.io/oml-template/) 

This repository has a template [OML](https://github.com/opencaesar/oml) project. It is meant to be forked as a starting point by pressing the 'Use this template' button above.

> this template is suitable for use with OML Rosetta and OML Luxor (but not OML Vision)

## Clone
```
  git clone https://github.com/opencaesar/oml-template.git
  cd oml-template
```

## Build

Check the consistency of the dataset

```
./gradlew build
```

## Generate Docs

Generate documentation from dataset

```
./gradlew generateDocs
```

## Start Fuseki Server

Start the Fuseki triple store

```
./gradlew startFuseki
```

Navigate to http://localhost:3030

Verify you see a dataset: `template`

## Stop Fuseki Server

Stop the Fuseki triple store

```
./gradlew stopFuseki
```

## Load Dataset to Fuseki

Load the dataset to Fuseki server

```
./gradlew load
```

Navigate to http://localhost:3030/#/dataset/template/info

Click on `count triples in all graphs` and observe the triple counts

## Run SPARQL Queries

Run the SPARQL queries

```
./gradlew query
```

Inspect the results at `build/results/template`

## Run SHACL Rules
Run the SHACL rules

```
./gradlew validate
```

Inspect the results at `build/logs/template`

## Publish to Maven Local

Publish the OML dataset as an archive in the local maven repo

```
./gradlew publishToMavenLocal
```

Inspect the OML archive

```
ls ~/.m2/repository/io/opencaesar/oml-template
```

## Customize Template

The name of this project is `oml-template`. You can change it to your own project name. The easiest way to do this is to look for the word `template` in this repo and replace it. The files that need to be changes include:

- `.project` (name)
- `.catalog.xml` (first rewriteURI)
- `README.md` (various places)
- `.oml/fuseki.ttl` (fuseki:name)
- `.oml/oml.yml` (various places)
- `src/oml/*` (namespaces of ontologies)
- `src/sparcl/*` (namespaces of ontologies)
- `src/shacl/*` (namespaces of ontologies)


