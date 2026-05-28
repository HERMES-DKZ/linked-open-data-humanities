---
title: "Model with Ontologies and Vocabularies"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 
- What steps you need to take to create an RDF data model from tabular data?
- What is the difference between a resource and a concept?
- What is RDF Schema used for and what does it include?
- What are vocabularies and ontologies used for?
- How to find vocabularies and ontologies?
- How to apply RDF Schema and vocabularies to create a RDF datamodel?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Identify entities and relationships in tabular data
- Distinguish between resources, concepts, and literals
- Explain the purpose of RDF Schema
- Apply classes and properties to RDF data
- Reuse existing vocabularies and ontologies
- Create a simple RDF data model from tabular data

::::::::::::::::::::::::::::::::::::::::::::::::


## Planning the Data Model

Before we can create a whole RDF dataset, we need to decide what our data should look like. A flat table is not flat data, it contains information about several different things at once. Each row in our dataset describes not just one object, but also other entities.

::::::::::::::::::::::::::::::::::::: challenge

## Create a Mind Map out of the Dataset

Form groups and look at the column headings and pick a row of data in the table. 
1. Try to convert the information of one data row into a mind-map (with nodes and connections) using the (Excalidraw)[https://excalidraw.com/] tool.
2. Identify central nodes.
3. How are the nodes interconnected with the table header?
4. Name the relationships between the nodes by assigning labels to them.


:::::::::::::::: solution

TODO: Add image of mindmap 

Central nodes are the ones with the objectIDs, artist, department and museum. Modeling decisions are subjective.

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Resources and Concepts

Difference between individual things and abstract concepts.
(rdf:type)

::::::::::::::::::::::::::::::::::::: challenge
## Challenge

:::::::::::::::: solution


:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## RDF Schema

RDF Schema is an extension of the basic RDF vocabulary, you already know from before. It provides a way to describe / define the structure of the RDF data, a **vocabulary on data-modelling**. 
You can always go to the published (RDF Schema Vocabulary file)[https://www.w3.org/TR/rdf11-schema/] and look up the the terms, meanings and rules.


* Classes
    * rdfs:Resource
    * rdfs:Class
    * rdfs:Literal
* Properties
    * rdfs:domain
    * rdfs:range
    * rdfs:subClassOf
    * rdfs:label

::::::::::::::::::::::::::::::::::::: challenge

## Challenge



:::::::::::::::: solution



:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


## Vocabularies and Ontologies

Vocabularies provide shared meaning and terms across data models. They promote interoperability. 

Frequent vocabularies, where to find them and how to read them.

::::::::::::::::::::::::::::::::::::: challenge

## Extend the data model by the use of vacabularies



:::::::::::::::: solution



:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


:::::: keypoints
- keypoint1
::::::