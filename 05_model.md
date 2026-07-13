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

After exploring the basic concepts and syntax of Linked Open Data, we will now work with a tabular museum dataset containing information about artworks from the Metropolitan Museum of Art.

Before we can create an RDF dataset, we first need to understand the structure of the data. Although the dataset is presented as a table, each row contains information about several different entities at once.

Our task is to identify these entities and the relationships between them, and gradually transform the tabular data into an RDF data model.


:::instructor

The lesson repository contains both a markdown and an HTML representation of the dataset:

- [markdown representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.md)

- [html representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.html) 

Depending on the size of the group, learners can either inspect the table individually or work in small groups.

:::::


::::::::::::::::::::::::::::::::::::: discussion

Look at the dataset as a group.

What kinds of things are represented in the table?

Which columns appear to describe the same entity, and which columns describe different entities?


:::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Create a Mind Map out of the Tabular Dataset

Form groups and look at the column headings and pick a row of data in the table. 

1. Try to convert the information of one data row into a mind-map (with nodes and connections) using the (Excalidraw)[https://excalidraw.com/] tool.

2. Think about what central nodes can be identified in the mind map.

3. How are the nodes interconnected with the table header?

4. Name the relationships between the central nodes by assigning labels to the connections. Pay attention to the direction of the arrows.


:::::::::::::::: solution

TODO: Add image of mindmap 
1. TODO: Image of possible mind map.

2. Central nodes are the ones where the most other nodes cluster around: objectIDs, artist, department or museum. Keep in mind: Modeling decisions are subjective.

3. The column headings provide context for the values in the table. For example, without the column heading, an ObjectID would simply be a number. The column heading tells us that the number refers to an artwork. Similarly, the value in the Photographer column only becomes meaningful when we know that it refers to the creator of the artwork.

4. Possible relationship labels include:

- Museum → owns → Artwork
- Department → manages → Artwork
- Artist → created → Artwork

Other valid relationships may be possible depending on how the data is interpreted.
:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Resources and Concepts

The mind map already contains several interconnected nodes. We can now add another layer of meaning to the model.

The ObjectID does not simply represent a number. It refers to a specific artwork. Likewise, an artist name refers to a specific person.

In RDF, we call these identifiable things resources.

Resources can also belong to broader categories. For example:

```text
ObjectID1234 rdf:type Object
````
The artwork represented by ObjectID1234 is an individual resource, while Object represents a more abstract concept or class.

This distinction between individual resources and abstract concepts is an important part of RDF modeling.

::::::::::::::::::::::::::::::::::::: challenge
## Challenge

:::::::::::::::: solution


:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## RDF Schema

RDF Schema (RDFS) extends the basic RDF vocabulary. It provides terms that help describe the structure of RDF data.

You can think of RDF Schema as a vocabulary for describing data models.

The official RDF Schema specification is available at:

https://www.w3.org/TR/rdf11-schema/

Some commonly used RDFS terms include:

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

## Classify the nodes in the model

Look at the nodes in your data model.

For each node, decide whether it represents:

- a resource,
- a literal,
- or a class.

Discuss your reasoning with your group.

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