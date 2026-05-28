---
title: "Model with Ontologies and Vocabularies"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are Ontologies, Vocabularies and RDF Schema?
- How to create an Entity in RDF with an Ontology?
- How can I describe RDF resources?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what a vocabulary is used for in linked open data.
- Create a Person Entity in RDF from our example Dataset

::::::::::::::::::::::::::::::::::::::::::::::::


## Planning the Data Model

Before we can create a whole RDF dataset, we need to decide what our data should look like. A flat table is not flat data, it contains information about several different things at once. Each row in our dataset describes not just one object, but also other entities.

:::::::::::::::::::::::::::::::::::::: discussion

### Discussion: What entities or classes can you identify in the dataset that we could model in RDF?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Ontologies

## Vocabularies

## RDF Schema

RDF Schema is an extension of the basic RDF vocabulary, you already know from before.
You can always go to the published (RDF Schema Vocabulary file)[https://www.w3.org/TR/rdf11-schema/] and look up the the terms (concepts), meanings and rules.

* Classes
    * rdfs:Resource
    * rdfs:Class
    * rdfs:Literal
* Properties
    * rdfs:domain
    * rdfs:range
    * rdfs:subClassOf
    * rdfs:subClassOf
    * rdfs:label

::::::::::::::::::::::::::::::::::::: challenge

## Create a person entity

Create a ttl file for one person from our example data. Use classes

:::::::::::::::: solution



:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


:::::: keypoints
 - keypoint 1
 - keypoint 2
::::::