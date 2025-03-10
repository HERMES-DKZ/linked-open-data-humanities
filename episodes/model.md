---
title: "Model Linked Data"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are IRIs, literals and a blanknodes and when to use them?
- How to write down RDF?
- What is Turtle?
- What is a vocabulary and a namespace?
- What is RDF Schema and what is it used for?



::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Differentiate between the concepts of IRIs, literals and blanknodes?
- Know when to use IRIs, literals and blanknodes.
- Write down RDF in turtle format?
- Understand what a vocabulary is used for in linked open data.
- Remember where to look for the concepts of the RDF schema vocabulary and their definitions.

::::::::::::::::::::::::::::::::::::::::::::::::

## Different concepts in RDF

* IRI
* Literal
* Blanknode


## Serialization formats

A serialisation format is the answer to the question of how to write things down in RDF so that the machine understands them. In short
Turtle is an example for such a format.

Turtle example
```

##namespaces
##statements
```
Other common serialization formats:

* RDF/XML
* JSON-LD



You do not have to know all the serialization Formats, there are plenty of converter tools on the web, for example the [EASYRDF Converter](https://www.easyrdf.org/converter) or the [RDF Converter by Zazuko](https://converter.zazuko.com/).


::::::::::::::::::::::::::::::::::::: challenge

## Write down the information in turtle

List some statements and ask the learners to transform them to valid turtle.

:::::::::::::::: solution


```
TODO
Valid turtle.
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Vocabularies & namespaces


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

## Apply RDF Schmea to our artwork example

Fill in the cloze or the gaps in the picture.

:::::::::::::::: solution



:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


:::::: keypoints
 - keypoint 1
 - keypoint 2
::::::