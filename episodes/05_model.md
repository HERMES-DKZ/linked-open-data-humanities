---
title: "Model with Ontologies and Vocabularies"
teaching: 10
exercises: 2
---

::: questions
-   What steps you need to take to create an RDF data model from tabular data?
-   What is the difference between a resource and a concept?
-   What is RDF Schema used for and what does it include?
-   What are vocabularies and ontologies used for?
-   How to find vocabularies and ontologies?
-   How to apply RDF Schema and vocabularies to create a RDF datamodel?
:::

::: objectives
-   Identify entities and relationships in tabular data
-   Distinguish between resources, concepts, and literals
-   Explain the purpose of RDF Schema
-   Apply classes and properties to RDF data
-   Reuse existing vocabularies and ontologies
-   Create a simple RDF data model from tabular data
:::

## Planning the Data Model

After exploring the basic concepts and syntax of Linked Open Data, we will now work with a tabular museum dataset containing information about artworks from the Metropolitan Museum of Art (the Met).

Before we can create an RDF dataset, we first need to understand the structure of the data and build a conceptual data model (decide how the underlying data model will look). Although the dataset is presented as a table, each row contains information about several different entities at once.

Our task is to identify these entities, the relationships between them as well as the attributes of the entities, and gradually transform the tabular data into a RDF data model.

| objectID | museum | department | departmentID | accessionYear | objectName | title | artistRole | artistDisplayBio | artist | objectDate | city | country | classification | linkResource | tags | tag1 |
|----|----|----|----|----|----|----------|----|----|----|----|----|----|----|----|----|----|
| 693151 | Metropolitan Museum of Art | Drawings and Prints | 3 | 1978 | Print | The Dismissed Servant | Publisher | French, Paris ca. 1686–1762 Grand Vaux | Surugue, Louis | ca. 1749 | Berlin |  | Prints | http://www.metmuseum.org/art/collection/search/693151 | Women\|Servants | woman |
| 708926 | Metropolitan Museum of Art | Arts of Africa, Oceania, and the Americas | 2 | 2015 | Photograph | Woman outdoors – Ewe kente skirt, headtie and blouse | Photographer | Togolese, Kedzi 1880–1975 Lomé | Acolatse, Alex Agbaglo | 1975 | Lomé | Togo | Photographs | http://www.metmuseum.org/art/collection/search/708926 | Portraits\|Women | Portraits |

::: instructor
The lesson repository contains both a markdown and an HTML representation of the dataset:

-   [markdown representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.md)

-   [html representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.html)

Depending on the size of the group, learners can either inspect the table individually or work in small groups.
:::

### Entities and Attibutes

:::: discussion
Look at the dataset as a group, especially pay attention to the coloum headers.

Which different kinds of entities are described in the table?
Which columns seem to describe the same entities?

::: solution
The table contains information on three main entities. If we take the coloum headers these could be: museum, artworks and artists. The museum could include `museum`, `department` and `departmentID` or department could be seen as an indepentant entity; the artists includes `artist` `artist bio` and `artistrole`; and the artworks include, for example, `objectid`, `classification`, `title` and `tags`.

However, there are also columns that cannot be clearly assigned. For example, `city` and `country` may also refer to the artist or the artwork or could be seen as independant entities, whilst `accession year` only makes sense in relation to the artwork and the museum, and `artist role` in relation to both the artwork and the artist.

As always, modelling decisions are heavily influenced by interpretation.
:::
::::

We took the first step to identify the key entities in our dataset and started with distinguishing between entities and attributes, describing these. 

TODO: Add description of attriubutes.



:::: challenge
## Create a Mind Map out of the Tabular Dataset

Work in small groups and choose one row from the dataset. Use Excalidraw (https://excalidraw.com/) or a sheet of paper to build a mind map step by step.

1.  Think about what entities we identified earlier. Draw nodes for these entities and think about which table cell could represent them.  

2. Cluster the informations in the other table cells around these.

2.  How are the central nodes interconnected with the coloumn header? The column headers help you interpret the values.
    Use them to decide what the values represent.

3.  Name the relationships between the central nodes by assigning labels to the connections. Pay attention to the direction of the arrows.

Tip: Do not try to model everything at once. Start by identifying the main entities, then gradually add more detail.
::: solution
TODO: Add image of mindmap

1.  Central nodes are the ones where the most other nodes cluster around. For example: objectID, artist, department or museum. Keep in mind – Modeling decisions are subjective.

2.  The column headings provide context for the values in the table. For example, without the column header, an ObjectID would simply be a number. The column header tells us that the number refers to an artwork like `708926` → is a `ObjectID` in the context of our artwork. You can expand this process with the other coloumns as well: Similarly, the value "Photographer" in the `artistrole` column only becomes meaningful when we know that it refers to the creator of the artwork. The `Acolatse, Alex Agbaglo` is the `Photoprapher` of the artwork.

3.  Possible relationship labels include:

-   Museum → owns → ObjectID
-   Department → manages → ObjectID
-   Artist → created → ObjectID

:::instructor
Its always possible to turn around the statement.

-   ObjectID  → was created by → Artist
-   ObjectID → is owned by → Museum
-   ObjectID → is managed by → Department

::::

Other valid relationships may be possible depending on how the data is interpreted.
:::
::::

## Resources and Classes

The mind map already contains several interconnected nodes. We can now add another layer of meaning to the model.

The ObjectID does not simply represent a number. It refers to a specific artwork. Likewise, an artist name refers to a specific person.

In RDF, we call these identifiable things resources. Resources can also belong to broader categories.

``` text
ObjectID1234 rdf:type Object
```

The artwork represented by ObjectID `693151` is an individual resource, while `Object` represents a more abstract concept the ressource belongs to called a class. 

This distinction between individual resources and classes is an important part of RDF modeling.

-   Museum → owns → Artwork
-   Department → manages → Artwork
-   Artist → created → Artwork

:::: challenge
## Challenge

::: solution
:::
::::

## RDF Schema

RDF Schema (RDFS) extends the basic RDF vocabulary. It provides terms that help describe the structure of RDF data.
You can think of RDF Schema as a vocabulary for describing data models.
The official RDF Schema specification is available at:

https://www.w3.org/TR/rdf11-schema/

Some commonly used RDFS terms include:

-   Classes
    -   rdfs:Class
    -   rdf:Property
-   Properties
    -   rdfs:domain
    -   rdfs:range
    -   rdfs:subClassOf
    -   rdfs:label
    -   rdf:type


:::: challenge
## Classify the nodes in the model

Look at the nodes in your data model.

For each node, decide whether it represents:

-   a resource,
-   a literal,
-   or a class.

Discuss your reasoning with your group.

::: solution
:::
::::

## Vocabularies and Ontologies

TODO

Different projects could invent different names for the same property.

Vocabularies provide shared meaning and terms across data models. They promote interoperability. So reuse existing vocabularies.

Frequent vocabularies, where can you find them and how can you read them.

:::: challenge
## Extend the data model by the use of vocabularies

::: solution
:::
::::

::: keypoints
-   keypoint1
:::